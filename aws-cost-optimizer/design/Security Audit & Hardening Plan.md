# Security Audit & Hardening Plan

> **Date:** 2026-04-07
> **Method:** Multi-agent adversarial audit — 5 specialized security agents independently reviewed the codebase and debated findings.
> **Agents:** SQL Injection, IDOR/BOLA, Path Traversal/File Upload, Auth/Secrets, XSS/CSRF/General

---

## Executive Summary

**Overall Security Posture: GOOD for a localhost desktop app. NOT ready for network exposure.**

The app has strong fundamentals — parameterized queries, OS keychain credential storage, safe-by-default destructive operations, Pydantic input validation. However, **zero authentication/authorization** means any network exposure is catastrophic. Multiple hardening opportunities exist.

---

## Agent Consensus & Debates

### Where All 5 Agents Agreed

| Finding | Verdict |
|---------|---------|
| SQL queries are properly parameterized | SAFE — no SQL injection possible |
| AWS credentials handled securely (OS keychain) | SAFE — never logged or returned in responses |
| Destructive actions default to blocked | SAFE — requires explicit env var opt-in |
| No file upload endpoints exist | SAFE — no unrestricted upload risk |
| No authentication layer exists | CRITICAL — must fix before any network exposure |
| CORS `allow_methods=["*"]` too permissive | HIGH — restrict to GET/POST/OPTIONS |
| No rate limiting on any endpoint | HIGH — DoS risk if network-exposed |
| No security headers (X-Frame-Options, etc.) | HIGH — add middleware |

### Where Agents Disagreed

#### Debate 1: Is "no auth" acceptable for a desktop app?

**Agent 4 (Auth/Secrets):** "No auth needed. App inherits OS-level security. Localhost-only. Single user by design. Adding auth adds complexity without real benefit."

**Agent 2 (IDOR/BOLA):** "Hard disagree. The API has 8 CRITICAL BOLA vulnerabilities. Any malware, compromised browser extension, or misconfigured deployment exposes everything. A simple API key header takes 15 minutes to implement."

**Agent 5 (XSS/CSRF):** "Siding with Agent 2. Localhost binding is NOT a security boundary. SSRF from other local services, DNS rebinding attacks, and browser-based CSRF can all reach 127.0.0.1:8000."

**Resolution:** Add lightweight auth (API key or session token generated at startup). Low effort, high impact.

#### Debate 2: Database path traversal — real risk or theoretical?

**Agent 3 (Path Traversal):** "CRITICAL. `RUNS_DB_PATH` env var flows directly into `Path()` with `mkdir(parents=True)`. An attacker controlling env vars can write DB files anywhere."

**Agent 1 (SQL Injection):** "Disagree on severity. If an attacker controls your environment variables, you have much bigger problems. This is defense-in-depth, not a realistic attack vector for a desktop app."

**Agent 5 (General):** "Agree it's defense-in-depth, but the fix is trivial — resolve the path and check it's within an allowed directory. Do it."

**Resolution:** Fix it. 5-line change. No reason not to.

#### Debate 3: How urgent is rate limiting?

**Agent 5 (General):** "HIGH priority. `/scan` can trigger 100,000 S3 API calls. No throttling."

**Agent 4 (Auth/Secrets):** "LOW priority. Localhost only. The user would be DoS-ing themselves. AWS SDK already has built-in retry/backoff."

**Resolution:** Medium priority. Add it before any network exposure. Not urgent for current desktop-only deployment.

---

## Vulnerability Catalog

### CRITICAL

#### C1: No Authentication or Authorization
- **Files:** `server/app/api/routes/optimizer.py` (all endpoints)
- **Impact:** Any process on localhost can scan, execute, rollback S3 operations
- **Attack:** Malware, browser extension, DNS rebinding, SSRF from other local services
- **Fix:** Generate a random API key at app startup (Tauri side), pass to backend as env var, require `X-API-Key` header on all requests

```python
# server/app/middleware/auth.py
import os
from fastapi import HTTPException, Header

API_KEY = os.getenv("APP_API_KEY", "")

async def verify_api_key(x_api_key: str = Header(...)):
    if not API_KEY or x_api_key != API_KEY:
        raise HTTPException(status_code=401, detail="Unauthorized")
```

#### C2: IDOR/BOLA on All Resource Endpoints
- **Files:** `server/app/api/routes/optimizer.py` lines 43-220
- **Endpoints affected:** `/score`, `/execute`, `/rollback`, `/runs`, `/runs/{run_id}`, `/runs/{run_id}/audit`
- **Impact:** Any caller can access/modify/rollback any run by guessing UUID
- **Attack:** `GET /runs` leaks all run IDs → attacker uses them on `/execute` or `/rollback`
- **Fix:** If multi-user is ever added, add `user_id` column to `runs` table and filter all queries. For now, auth (C1) mitigates this.

### HIGH

#### H1: CORS Wildcard Methods & Headers
- **File:** `server/app/main.py` lines 21-22
- **Current:** `allow_methods=["*"], allow_headers=["*"]`
- **Fix:**
```python
allow_methods=["GET", "POST", "OPTIONS"],
allow_headers=["Content-Type", "X-API-Key"],
```

#### H2: Missing Security Headers
- **File:** `server/app/main.py`
- **Fix:** Add middleware:
```python
class SecurityHeadersMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        response = await call_next(request)
        response.headers["X-Frame-Options"] = "DENY"
        response.headers["X-Content-Type-Options"] = "nosniff"
        response.headers["X-XSS-Protection"] = "1; mode=block"
        response.headers["Referrer-Policy"] = "strict-origin-when-cross-origin"
        return response
```

#### H3: No Rate Limiting
- **Files:** All API routes
- **Fix:** Add `slowapi` to `requirements.txt`, apply limits:
  - `/scan`: 10/hour
  - `/execute`: 5/hour
  - `/rollback`: 5/hour
  - `/runs`: 60/minute

#### H4: No Input Validation on List Fields
- **File:** `server/app/models/contracts.py` lines 129-130
- **Issue:** `include_buckets` and `exclude_buckets` have no max length or format validation
- **Fix:**
```python
include_buckets: list[str] = Field(default_factory=list, max_length=100)
exclude_buckets: list[str] = Field(default_factory=list, max_length=100)

@field_validator("include_buckets", "exclude_buckets")
@classmethod
def validate_bucket_names(cls, v):
    for name in v:
        if not (3 <= len(name) <= 63):
            raise ValueError(f"Invalid bucket name length: {name}")
    return v
```

#### H5: Health Endpoint Leaks Environment
- **File:** `server/app/api/routes/health.py` line 25
- **Issue:** Returns `environment=settings.environment` (reveals dev vs prod)
- **Fix:** Remove `environment` field from `HealthResponse`

### MEDIUM

#### M1: Database Path Traversal
- **File:** `server/app/state/store.py` lines 41-44
- **Issue:** `RUNS_DB_PATH` env var used directly without path validation
- **Fix:**
```python
def __init__(self, db_path: str = "data/runs.db") -> None:
    resolved = Path(db_path).resolve()
    # Ensure path is within project data directory
    allowed_base = Path(__file__).resolve().parent.parent.parent / "data"
    if not str(resolved).startswith(str(allowed_base.resolve())):
        raise ValueError(f"DB path must be within {allowed_base}")
    self._db_path = resolved
```

#### M2: No audit_ids List Size Limit
- **File:** `server/app/state/store.py` lines 234-237
- **Issue:** Unbounded `audit_ids` list creates unbounded SQL IN clause
- **Fix:** Cap at 1000 items, validate UUID format

#### M3: CORS Origins Not Validated
- **File:** `server/app/core/settings.py` lines 12-20
- **Issue:** `CORS_ORIGINS` env var parsed without URL validation; could inject `*` or malicious origins
- **Fix:** Validate each origin is a proper URL, reject wildcards

#### M4: No Security Event Logging
- **Files:** All API routes
- **Issue:** No logging of execution attempts, permission checks, or failed operations
- **Fix:** Add structured security audit logger for all mutation endpoints

#### M5: SQLite Concurrency
- **File:** `server/app/state/store.py`
- **Issue:** `Lock()` is per-instance. Multiple workers = multiple locks = race conditions
- **Fix:** Enable WAL mode: `conn.execute("PRAGMA journal_mode=WAL")`

#### M6: Unencrypted Local Database
- **File:** `server/app/state/store.py` line 43
- **Issue:** `runs.db` stores S3 bucket names, object keys, execution history in plaintext
- **Fix:** Use `sqlcipher3` for encryption at rest, or document that OS-level disk encryption is required

### LOW

#### L1: `style-src 'unsafe-inline'` in Tauri CSP
- **File:** `client/src-tauri/tauri.conf.json` line 27
- **Impact:** Minimal in desktop context

#### L2: Sensitive Data in Audit Trail UI
- **File:** `client/src/pages/AuditTrail.tsx` lines 189, 196
- **Issue:** `pre_change_state` displayed raw, could contain S3 object tags with secrets

#### L3: Error Messages Reveal Run IDs
- **File:** `server/app/api/routes/optimizer.py`
- **Issue:** 404 messages confirm whether a run_id exists (enumeration)

---

## What's NOT Vulnerable (Confirmed Safe)

| Area | Status | Details |
|------|--------|---------|
| SQL Injection | SAFE | All 9 DB methods use parameterized queries with `?` placeholders |
| Password Reset in Response | N/A | No auth system exists — no passwords or reset tokens |
| File Upload | N/A | No file upload endpoints exist |
| XSS | SAFE | React auto-escapes; no `dangerouslySetInnerHTML` found |
| Hardcoded Secrets | SAFE | No secrets in source code; `.env` properly gitignored |
| AWS Credential Exposure | SAFE | Stored in OS keychain, passed as env vars, never logged |
| CSRF | LOW RISK | Localhost-only + CORS + Tauri CSP mitigate; no CSRF tokens needed for desktop |

---

## Allow List Implementation Plan

Currently the app uses Pydantic enums as implicit allow lists. Formalize this:

| Input | Current Validation | Recommended Allow List |
|-------|-------------------|----------------------|
| `target_storage_class` | `StorageClass` enum | Already an allow list |
| `recommendation_type` | `RecommendationType` enum | Already an allow list |
| `mode` | `ExecutionMode` enum | Already an allow list |
| `include_buckets` | None | Add regex: `^[a-z0-9][a-z0-9.-]{1,61}[a-z0-9]$` |
| `exclude_buckets` | None | Same regex |
| `audit_ids` | None | Add UUID format validation + max 1000 |
| `run_id` | None (path param) | Add UUID format validation |
| `execution_id` | None | Add UUID format validation |
| `CORS_ORIGINS` | String split | Validate URL format, reject wildcards |
| `EXECUTOR_GRANTED_PERMISSIONS` | String comparison | Validate against known S3 permission set |

---

## Remediation Roadmap

### Phase 1: Critical (Do Before Any Network Exposure)
1. Add API key auth middleware
2. Restrict CORS methods/headers
3. Add security headers middleware
4. Add bucket name validation

### Phase 2: High Priority (Next Sprint)
5. Add rate limiting (`slowapi`)
6. Remove environment from health endpoint
7. Add audit_ids size limit + UUID validation
8. Validate CORS origins format

### Phase 3: Hardening (Backlog)
9. Database path validation
10. Security event logging
11. SQLite WAL mode
12. Database encryption or document disk encryption requirement

### Phase 4: Future-Proofing (If Multi-User)
13. Full IDOR/BOLA fix with user_id scoping
14. RBAC (role-based access control)
15. JWT authentication
16. CSRF tokens

---

## Testing Recommendations

### Security Tests to Add

```python
# test_security.py

def test_sql_injection_in_audit_ids(store):
    """Verify SQL injection payloads treated as literals."""
    malicious = ["'; DROP TABLE runs; --", "' OR '1'='1"]
    result = store.list_execution_audit("fake-run", audit_ids=malicious)
    assert result == []  # No crash, no data leak

def test_bucket_name_validation_rejects_traversal(client):
    """Verify path traversal in bucket names is rejected."""
    resp = client.post("/api/v1/optimizer/scan", json={
        "include_buckets": ["../../../etc/passwd"]
    })
    assert resp.status_code == 422

def test_cors_rejects_unauthorized_origin(client):
    """Verify CORS blocks non-whitelisted origins."""
    resp = client.options("/api/v1/optimizer/scan", headers={
        "Origin": "https://evil.com",
        "Access-Control-Request-Method": "POST"
    })
    assert "Access-Control-Allow-Origin" not in resp.headers

def test_rate_limiting(client):
    """Verify scan endpoint is rate-limited."""
    for _ in range(15):
        resp = client.post("/api/v1/optimizer/scan", json={})
    assert resp.status_code == 429
```

### CI/CD Security Scanning

```bash
# Add to CI pipeline
pip install bandit safety
bandit -r server/app -ll           # Static analysis
safety check -r requirements.txt   # Dependency CVEs
npm audit --prefix client          # JS dependency CVEs
```

---

## OWASP Top 10 Coverage

| OWASP Category | Status | Findings |
|----------------|--------|----------|
| A01: Broken Access Control | RED | No auth, IDOR/BOLA on all endpoints |
| A02: Cryptographic Failures | YELLOW | Unencrypted local DB |
| A03: Injection | GREEN | Parameterized queries throughout |
| A04: Insecure Design | YELLOW | No auth by design (acceptable for desktop) |
| A05: Security Misconfiguration | YELLOW | CORS wildcards, missing headers |
| A06: Vulnerable Components | GREEN | Dependencies current, no known CVEs |
| A07: Auth Failures | RED | No auth system |
| A08: Data Integrity Failures | GREEN | Audit trail with pre/post state |
| A09: Logging Failures | YELLOW | No security event logging |
| A10: SSRF | GREEN | No user-controlled URL fetching |
