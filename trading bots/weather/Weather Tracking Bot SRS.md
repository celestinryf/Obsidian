# Software Requirements Specification: Kalshi Weather Trading Bot

## 1. Introduction

### 1.1 Purpose
This document specifies the software requirements for the Kalshi Weather Trading Bot, a system that aggregates weather forecasts from 4 JSON sources (MVP) with 3 GRIB2 sources added later, generates trading recommendations for Kalshi temperature markets, and tracks performance via automated paper trading.

### 1.2 Scope
The system covers: weather data ingestion, temperature prediction, Kalshi market analysis, recommendation generation with risk scoring, automated paper trading, email notifications, and a web dashboard. The system does NOT place real trades -- it is recommendation-only.

### 1.3 Definitions

- **Kalshi** -- CFTC-regulated prediction market platform offering binary event contracts
- **Bracket** -- A temperature range (e.g., 71-72F) that a Kalshi contract covers. Each market has ~6 brackets.
- **BUY YES** -- Bet that the temperature WILL fall in the bracket
- **BUY NO** -- Bet that the temperature will NOT fall in the bracket
- **Gap** -- Difference between our model's probability and Kalshi's market-implied probability
- **EV** -- Expected value of a trade after accounting for probability, payout, and fees
- **Paper trade** -- Simulated trade using real market prices but no real money
- **GRIB2** -- Binary format used by weather agencies for gridded forecast data
- **EMOS** -- Ensemble Model Output Statistics, a calibration method for probabilistic forecasts
- **Brier score** -- Metric for evaluating calibration quality of probability estimates (lower = better)
- **NWS CLI** -- National Weather Service Daily Climate Report, the official source for Kalshi settlement

---

## 2. System Overview

### 2.1 System Context
The bot operates as a pipeline: ingest weather data and Kalshi market data, predict temperatures, generate recommendations, execute paper trades, and notify users via email and web dashboard.

### 2.2 Users

- **Admin** (MVP): Single user who manages the system, views recommendations, logs real trades
- **Users** (future): Multiple registered users with individual trade tracking and email preferences

---

## 3. Functional Requirements

### 3.1 Weather Data Ingestion (FR-WDI)

**FR-WDI-01:** The system SHALL ingest temperature forecasts from 4 JSON sources at MVP:

- NWS (api.weather.gov, JSON, free, no key -- official Kalshi settlement source)
- Visual Crossing (JSON, $35/mo -- includes 50+ year historical archive)
- PirateWeather (JSON, $2/mo -- Dark Sky-compatible, wraps GFS/HRRR/NBM)
- OpenWeatherMap (JSON, free 1M calls/mo -- adds non-NOAA model diversity)

**FR-WDI-01b:** The system SHALL support adding 3 GRIB2 sources in a later sprint:

- ECMWF (official open data portal, GRIB2, free -- world's best NWP model)
- GEM (ECCC Datamart, GRIB2, free -- Canadian model, strong for North America)
- ENS/ECMWF Ensemble (official open data portal, GRIB2, free -- 51-member probabilistic ensemble)

**FR-WDI-01c:** AccuWeather SHALL NOT be used. Their ToS prohibits AI/ML training, commingling with other weather data, and caching beyond 2 weeks.

**FR-WDI-02:** The system SHALL extract daily high and daily low temperature forecasts for each city from each source.

**FR-WDI-03:** For GRIB2 sources (later sprint), the system SHALL parse GRIB2 format files using Herbie + cfgrib/xarray/eccodes and extract point forecasts by lat/lon for each tracked city.

**FR-WDI-04:** The system SHALL run ingestion on a cron schedule:

- NWS, PirateWeather: every 2 hours
- Visual Crossing, OpenWeatherMap: every 6 hours

**FR-WDI-05:** The system SHALL store raw API responses (JSONB) alongside parsed values for debugging and reprocessing.

**FR-WDI-06:** The system SHALL retry failed API calls with exponential backoff.

**FR-WDI-07:** The system SHALL continue ingesting from other sources if one source fails.

**FR-WDI-08:** The system SHALL validate temperature values are within -50F to 150F range.

**FR-WDI-09:** The system SHALL alert (log + optional email) if a source is down for >2 consecutive ingestion cycles.

### 3.2 Kalshi Market Data (FR-KMD)

**FR-KMD-01:** The system SHALL use the `pykalshi` library (v0.4.0+, PyPI: pykalshi, GitHub: ArshKA/kalshi-client) for API interactions. The official `kalshi_python_sync` SDK SHALL NOT be used as it lacks WebSocket support, rate limiting, and retry logic.

**FR-KMD-02:** The system SHALL discover all weather markets by querying `GET /series` with category filter, then `GET /events` with `with_nested_markets=true`.

**FR-KMD-03:** The system SHALL track all active HIGH and LOW temperature markets across all Kalshi cities (~44+).

**FR-KMD-04:** The system SHALL receive real-time market prices via WebSocket `ticker` channel (yes_bid, yes_ask, no_bid, no_ask, volume, open_interest).

**FR-KMD-05:** The system SHALL receive real-time settlement notifications via WebSocket `market_lifecycle_v2` channel.

**FR-KMD-06:** The system SHALL backfill historical weather market prices using candlestick endpoints (`GET /series/{series}/markets/{ticker}/candlesticks` and `GET /historical/markets/{ticker}/candlesticks`).

**FR-KMD-07:** The system SHALL map each Kalshi city ticker to its corresponding NWS station ID.

**FR-KMD-08:** The system SHALL fall back to REST polling when WebSocket connection is interrupted.

### 3.3 Prediction Engine (FR-PE)

**FR-PE-01:** The system SHALL implement three model tiers, built incrementally:

- Tier 1: Equal-weight average of all sources
- Tier 2: Performance-weighted average using rolling 30-60 day RMSE (after 30+ days of data)
- Tier 3: EMOS nonhomogeneous Gaussian regression (after 60+ days of data)

**FR-PE-02:** The system SHALL output a Gaussian probability distribution (mean, standard deviation) for each city, date, and market type (HIGH/LOW).

**FR-PE-03:** The system SHALL convert the probability distribution to bracket probabilities using Gaussian CDF integration.

**FR-PE-04:** The system SHALL verify bracket probabilities sum to approximately 100% (99-101% tolerance).

**FR-PE-05:** The system SHALL track and correct systematic biases per city and per season using Platt scaling or isotonic regression.

**FR-PE-06:** The system SHALL track model performance metrics: MAE, RMSE, bracket accuracy, Brier score, CRPS.

### 3.4 Recommendation Engine (FR-RE)

**FR-RE-01:** The system SHALL generate a recommendation when the gap between model probability and Kalshi probability exceeds a configurable threshold (default: 15%).

**FR-RE-02:** The system SHALL support both BUY YES (model_prob >> kalshi_prob) and BUY NO (model_prob << kalshi_prob) recommendations.

**FR-RE-03:** The system SHALL calculate expected value: EV = (probability * $1.00) - cost - fees.

**FR-RE-04:** The system SHALL only recommend trades with EV above a configurable minimum threshold (default: $0.05).

**FR-RE-05:** The system SHALL calculate Kalshi fees using the formula: `round_up(0.07 * contracts * price * (1 - price))`.

**FR-RE-06:** The system SHALL lock the entry price (yes_ask or no_ask) at the exact moment the recommendation is generated.

### 3.5 Risk Scoring (FR-RS)

**FR-RS-01:** The system SHALL assign each recommendation a risk score from 1-10 based on 6 weighted factors:

- Forecast spread across sources (25%)
- Source agreement on direction (20%)
- City-specific historical accuracy (15%)
- Market liquidity/volume (10%)
- Bracket edge proximity (15%)
- Forecast lead time (15%)

**FR-RS-02:** The system SHALL categorize risk scores:

- 1-3: HIGH CONFIDENCE
- 4-6: MODERATE
- 7-10: HIGH RISK (flagged with warning)

**FR-RS-03:** The system SHALL flag HIGH SPREAD when source temperature spread exceeds 5F.

**FR-RS-04:** Risk thresholds SHALL be configurable by the user.

### 3.6 Paper Trading (FR-PT)

**FR-PT-01:** The system SHALL automatically create a paper trade for every recommendation generated.

**FR-PT-02:** The system SHALL support two paper trading modes:

- Fixed-size: 1 contract per recommendation (measures pure win rate)
- Virtual portfolio: configurable starting balance (default $10,000) with position sizing strategies (fixed percentage, confidence-scaled, Kelly criterion)

**FR-PT-03:** The system SHALL settle paper trades using Kalshi's API settlement outcomes as the primary source.

**FR-PT-04:** The system SHALL also pull NWS Daily Climate Report values as secondary verification.

**FR-PT-05:** The system SHALL track per-trade: entry price, contracts, settlement outcome (WIN/LOSS), P&L.

**FR-PT-06:** The system SHALL track aggregate metrics: accuracy %, cumulative P&L, ROI, max drawdown, Sharpe ratio.

**FR-PT-07:** The system SHALL provide breakdowns: by city, by risk level, by direction (YES/NO), by market type (HIGH/LOW).

### 3.7 Email Notifications (FR-EN)

**FR-EN-01:** The system SHALL send a daily email digest containing all recommendations for the next day.

**FR-EN-02:** Each recommendation in the email SHALL include: city, market type, bracket, Kalshi price, model probability, direction, gap, risk score, individual source forecasts, and spread.

**FR-EN-03:** The email SHALL include a paper trading performance summary (last 7 days accuracy, portfolio value).

**FR-EN-04:** Email send time SHALL be configurable (default: 11:55 PM local time).

**FR-EN-05:** The system SHALL support filtering recommendations in emails by minimum gap, maximum risk score, and specific cities.

**FR-EN-06:** The system SHALL use SendGrid for email delivery.

### 3.8 Web Application (FR-WA)

**FR-WA-01:** The system SHALL provide a React web application with 6 pages: Dashboard, Markets Browser, Paper Trading, My Trades, Analytics, Settings.

**FR-WA-02:** Dashboard SHALL display today's recommendations sorted by EV, paper trade accuracy (7d/30d/all), and data freshness per source.

**FR-WA-03:** Markets Browser SHALL display all Kalshi weather markets in a filterable table with model vs. market probabilities.

**FR-WA-04:** Paper Trading page SHALL display trade history with performance charts (accuracy over time, cumulative P&L, drawdown).

**FR-WA-05:** My Trades page SHALL allow users to log real trades manually and compare personal performance vs. bot recommendations.

**FR-WA-06:** Analytics page SHALL display model performance metrics: reliability diagrams, Brier scores, RMSE trends, city-level accuracy heatmap.

**FR-WA-07:** Settings page SHALL allow configuration of email preferences, risk thresholds, city watchlist, and paper portfolio settings.

**FR-WA-08:** The web API SHALL be served by Spring Boot (read-only from PostgreSQL, no business logic).

**FR-WA-09:** Authentication SHALL use JWT (HS256) with a single admin account for MVP. Access tokens SHALL expire in 15 minutes and be stored in httpOnly, Secure, SameSite=Strict cookies. Refresh tokens SHALL expire in 14 days, be stored hashed in a `refresh_tokens` database table, and rotate on each use.

**FR-WA-10:** The web API SHALL validate all request inputs using Jakarta Bean Validation annotations. User-provided text fields SHALL be sanitized before storage. JPA parameterized queries SHALL be used for all database operations.

**FR-WA-11:** The web API SHALL enforce per-user rate limiting via Bucket4j (60 req/min per authenticated user). Nginx SHALL enforce per-IP rate limiting (3 req/min on login, 10 req/sec on general API).

**FR-WA-12:** The web API SHALL return structured JSON error responses containing an error_code, user-friendly message, and correlation_id. Stack traces SHALL NOT be included in API responses.

**FR-WA-13:** The React SPA and Spring Boot API SHALL be served from the same origin via Nginx path routing (`/` for SPA, `/api/` for API), eliminating the need for CORS configuration.

---

## 4. Non-Functional Requirements

### 4.1 Performance (NFR-P)

**NFR-P-01:** Weather data ingestion for all 44+ cities across all 4 MVP sources (7 after GRIB2 sprint) SHALL complete within the scheduled interval (2 or 6 hours depending on source).

**NFR-P-02:** Recommendation generation SHALL complete within 5 minutes of a new prediction being generated.

**NFR-P-03:** WebSocket connection to Kalshi SHALL maintain >99% uptime with automatic reconnection.

**NFR-P-04:** Web API response time SHALL be <500ms for all endpoints under normal load.

### 4.2 Reliability (NFR-R)

**NFR-R-01:** The system SHALL continue operating if any single weather source is unavailable.

**NFR-R-02:** The system SHALL automatically reconnect WebSocket connections with exponential backoff.

**NFR-R-03:** PostgreSQL data SHALL be backed up daily via pg_dump, GPG-encrypted (AES-256), to external storage.

**NFR-R-04:** Docker containers SHALL have restart policies configured for automatic recovery.

### 4.3 Accuracy (NFR-A)

**NFR-A-01:** The system SHALL target 70%+ accuracy on recommended trades as measured by paper trading over a 30-day rolling window.

**NFR-A-02:** The system SHALL track accuracy separately for: all recommendations, low-risk only, and high-EV only.

**NFR-A-03:** Probability calibration SHALL be monitored via Brier score and reliability diagrams.

### 4.4 Security (NFR-S)

**Secrets Management:**

**NFR-S-01:** All API keys (weather APIs, SendGrid, JWT secret) SHALL be stored in `.env` files with 600 permissions, never in source code. `.env` SHALL be in `.gitignore`.

**NFR-S-02:** The Kalshi RSA private key (.pem file) SHALL be volume-mounted into containers as read-only (`./secrets/kalshi_private.pem:/app/secrets/kalshi_private.pem:ro`) with file permissions 600 on the host.

**NFR-S-03:** The SendGrid API key SHALL be scoped to "Mail Send" permission only.

**NFR-S-04:** A secrets rotation runbook (`docs/secrets-rotation.md`) SHALL document steps to rotate each secret (Kalshi RSA key, weather API keys, SendGrid key, JWT secret, DB password) without downtime.

**Network & Transport:**

**NFR-S-05:** The web application SHALL be served over HTTPS via Nginx + Let's Encrypt.

**NFR-S-06:** The VPS firewall (UFW) SHALL only expose ports 80 and 443.

**NFR-S-07:** PostgreSQL SHALL NOT publish its port to the host. Database access SHALL be restricted to containers on the internal Docker `backend` network (`internal: true`).

**NFR-S-08:** PostgreSQL connections SHALL use SSL (`sslmode=require`) for defense-in-depth, even within the Docker network.

**NFR-S-09:** VPS SSH access SHALL require key-based authentication. Password authentication SHALL be disabled in sshd_config.

**Authentication & Authorization:**

**NFR-S-10:** User passwords SHALL be stored as bcrypt hashes.

**NFR-S-11:** JWT access tokens SHALL be signed with HS256, expire in 15 minutes, and be stored in httpOnly + Secure + SameSite=Strict cookies.

**NFR-S-12:** JWT refresh tokens SHALL expire in 14 days, be stored hashed in a `refresh_tokens` database table, and rotate on each use. Server-side revocation SHALL be supported by deleting refresh tokens from the database.

**NFR-S-13:** CSRF protection SHALL be provided by SameSite=Strict cookies combined with a custom `X-Requested-With` header check on state-changing requests.

**Input & Output Security:**

**NFR-S-14:** All web API request inputs SHALL be validated using Jakarta Bean Validation. User-provided text (e.g., trade notes) SHALL be sanitized with Jsoup before storage.

**NFR-S-15:** All database queries SHALL use JPA parameterized queries. Raw SQL string concatenation SHALL NOT be used.

**NFR-S-16:** Nginx SHALL set Content-Security-Policy headers: `default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; connect-src 'self'; frame-ancestors 'none';`

**Rate Limiting:**

**NFR-S-17:** Nginx SHALL enforce per-IP rate limiting: 3 req/min on `/api/auth/login`, 10 req/sec on `/api/*`.

**NFR-S-18:** Spring Boot SHALL enforce per-user rate limiting via Bucket4j: 60 req/min per authenticated user.

**Container & CI Security:**

**NFR-S-19:** All Dockerfiles SHALL create a non-root `app` user and run the application as `USER app`.

**NFR-S-20:** Docker base images SHALL use slim variants (`python:3.12-slim`) to minimize attack surface.

**NFR-S-21:** CI/CD pipeline SHALL run dependency vulnerability scans: Dependabot for automated PRs, `pip-audit --strict` for Python, `npm audit --audit-level=high` for Node.

**NFR-S-22:** CI/CD pipeline SHALL scan built Docker images with Trivy and fail the build on HIGH or CRITICAL vulnerabilities.

**Logging & Data Protection:**

**NFR-S-23:** All services SHALL use structured JSON logging with an automatic redaction filter that replaces values of fields matching `api_key`, `password`, `token`, `authorization`, `private_key`, `secret`, `credential` with `[REDACTED]`.

**NFR-S-24:** Application logs SHALL NOT contain full HTTP request/response bodies from external APIs, as they may include credentials in headers.

**NFR-S-25:** Database backups SHALL be encrypted with GPG (AES-256, symmetric) before upload to external storage. The GPG passphrase SHALL be stored separately from the backups at `/root/.backup_passphrase` with 600 permissions.

### 4.5 Error Handling & Traceability (NFR-E)

**NFR-E-01:** Each pipeline run (ingestion → prediction → recommendation → paper trade) SHALL generate a unique correlation ID that flows through every function call and is included in all log entries.

**NFR-E-02:** All errors SHALL be classified into structured categories: `WEATHER_API_ERROR`, `KALSHI_API_ERROR`, `PREDICTION_ERROR`, `RECOMMENDATION_ERROR`, `PAPER_TRADE_ERROR`, `DB_ERROR`, `NOTIFICATION_ERROR`, `VALIDATION_ERROR`.

**NFR-E-03:** All error logs SHALL include: `correlation_id`, `timestamp`, `service`, `error_category`, `source` (which API/city/market), `operation` (which step), `error_message`, and `stack_trace`.

**NFR-E-04:** API error responses SHALL include `error_code`, user-friendly `message`, and `correlation_id`. Stack traces SHALL NOT be included in API responses.

**NFR-E-05:** Python services SHALL use a custom exception hierarchy rooted at `WeatherBotError` with subclasses per error domain (`WeatherApiError`, `KalshiApiError`, `PredictionError`, `PaperTradeError`). Each exception SHALL carry `category`, `correlation_id`, `city`, `source`, and arbitrary context fields.

**NFR-E-06:** Spring Boot SHALL implement a global `@ControllerAdvice` error handler that catches all exceptions and returns structured JSON error responses with consistent formatting.

### 4.6 Scalability (NFR-SC)

**NFR-SC-01:** The system SHALL run on a single VPS (4GB RAM, 2 vCPU) for MVP.

**NFR-SC-02:** The architecture SHALL support future migration to Kubernetes without code changes (Dockerized services with health endpoints).

**NFR-SC-03:** The system SHALL support adding new weather sources without modifying existing ingestion code (plugin architecture).

### 4.7 Monitoring (NFR-M)

**NFR-M-01:** All services SHALL expose Prometheus metrics.

**NFR-M-02:** Grafana dashboards SHALL track: system health, data pipeline freshness, model accuracy trends, paper trade P&L.

**NFR-M-03:** Alerts SHALL fire for: data source down >4 hours, accuracy drop below 60%, service crash.

---

## 5. Data Requirements

### 5.1 Data Sources

See FR-WDI-01 for the complete list of 8 weather data sources and FR-KMD for Kalshi market data.

### 5.2 Data Storage

- PostgreSQL database with tables for: cities, weather_forecasts, kalshi_markets, kalshi_market_snapshots, predictions, recommendations, paper_trades_fixed, paper_trades_portfolio, paper_portfolios, users, user_trades, email_logs, refresh_tokens
- Full schema defined in the Production Plan document

### 5.3 Data Retention

- Weather forecasts: indefinite (required for backtesting)
- Kalshi market snapshots: indefinite (required for backtesting)
- Paper trades: indefinite (performance history)
- Email logs: 90 days

---

## 6. System Interfaces

### 6.1 External APIs (MVP)

- Kalshi REST API v2 + WebSocket (via pykalshi, RSA-PSS auth)
- NWS api.weather.gov (JSON, no auth, User-Agent header required)
- Visual Crossing API (JSON, API key, $35/mo)
- PirateWeather API (JSON, API key, $2/mo)
- OpenWeatherMap API (JSON, API key, free 1M calls/mo)
- SendGrid Email API (API key, free 100 emails/day)

### 6.1b External APIs (Later Sprint - GRIB2)

- ECMWF Open Data Portal (GRIB2, no auth, via Herbie)
- ECCC Datamart (GRIB2, no auth)
- ECMWF ENS Open Data (GRIB2, no auth, via Herbie)

### 6.2 Internal Interfaces

- All services communicate via PostgreSQL (shared database)
- No inter-service HTTP or message queue for MVP
- Future: Kafka for event streaming when scale justifies it

---

## 7. Constraints

- Open-Meteo free API cannot be used (non-commercial license conflicts with trading use case)
- AccuWeather cannot be used (ToS prohibits AI/ML training, data commingling, caching >2 weeks)
- ECMWF/GEM/ENS data requires GRIB2 parsing (Herbie + cfgrib + xarray + eccodes) -- deferred to later sprint
- eccodes on Windows is "untested" per ECMWF; pip install works since v2.43.0 but no official support
- Kalshi API basic tier rate limit: 20 reads/sec, 10 writes/sec (pykalshi handles backoff automatically)
- System is recommendation-only; no automated real trading
- Visual Crossing requires paid tier ($35/mo) for 44+ city coverage
- PirateWeather free tier: 10,000 calls/month (sufficient for 44 cities at 2hr intervals, but tight)

---

## 8. Acceptance Criteria

1. All 4 MVP weather sources return valid forecasts for all tracked cities with no gaps >6 hours
2. Bracket probabilities sum to 99-101% for every market
3. Recommendations match hand-calculated gap, EV, and fee values
4. Paper trades settle correctly against Kalshi API settlement outcomes
5. Email format matches the example provided in the project description
6. Web dashboard displays consistent data across all 6 pages
7. Full daily pipeline (ingest -> predict -> recommend -> paper trade -> email) runs without errors for 7 consecutive days
8. 30-day paper trading period achieves 70%+ accuracy on recommended trades
