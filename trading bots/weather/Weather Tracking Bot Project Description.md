
General Description:

This will be a bot that tracks the top 6 weather reporting channels/data sources to accurately predict the weather across the United States.

Predictions are made off of possible trades on Kalshi, and there should be a risk scoring system that seeks to make sure the predictions are not just accurate but safe as well. Risky predictions should not be recommended by the bot, or if they are it should be made clear the potential risk.

Testing for this bot should be made by:
- making mock trades by saving all trades each day that the bot would have made given the predictions and recommendations, and collecting the percentage of the recommended trades that are successful.
- Using past data against our recommendations to see if our predictions would have held up given the forecasts for those days

Concepts to get familiar with and document for this project:
- Kalshi
- Kalshi Weather Predictions
- Paper trading for testing
- Weather reporting
- Recommendation systems, risk systems

Key Features:
- recommendation system based off of 6 largest datasets/weather reporting institutions
- Email forwarding for weather reporting recommendations
- Web app that shows all of the recommendations, previous paper trades by the recommendation system, previous paper trades by a user, and previous trades by a user

Goals:
- 70%+ accuracy in predictions

For tech stack: I want you to mostly resemble the tech stack of this recommendation system listed underneath:


Description of another recommendation system for example of what we can do:

# Full Recommendation System[](https://nickjordan.streamlit.app/~/+/projects#full-recommendation-system)

Technologies:

TensorFlow Python Pandas NumPy Flask Spring Boot React PostgreSQL Kafka Docker Kubernetes Airflow MLflow GitOps Prometheus Grafana

### A Multi-Stage Recommendation System for Large-Scale Travel and Accommodation Platforms.[](https://nickjordan.streamlit.app/~/+/projects#a-multi-stage-recommendation-system-for-large-scale-travel-and-accommodation-platforms)

A full-stack recommendation platform built using Java Spring Boot, React, PostgreSQL, and Python to create personalized travel recommendations. The system utilizes a multi-stage pipeline with Two-Tower neural networks for candidate generation, Gradient Boosted Decision Trees (GBDT) for fine ranking, and Learn-to-Rank models for re-ranking. The system supports real-time recommendations via Kafka streaming and a feature store for high-throughput, low-latency access. End-to-end infrastructure includes ETL pipelines, online serving, containerized deployment, and automated GitOps/DevOps workflows.

- Developed ETL pipelines using Apache Spark and Airflow to clean, transform, and engineer features from 1M+ transactional and behavioral user records.
- Built Two-Tower neural network model for candidate generation achieving high recall, trained with real-world datasets including RecSys Challenge 2021, Expedia Hotel Recommendations, and Airbnb New User Bookings.
- Implemented GBDT fine-ranking stage to optimize user relevance and incorporate business rules such as blocked users, previously recommended items, and inventory constraints.
- Added Learn-to-Rank stage to further improve personalized recommendation ranking based on historical interactions and real-time feedback.
- Real-time serving infrastructure with FastAPI, Kafka streaming, and PostgreSQL to handle live user requests and update recommendations on-the-fly.
- Containerized entire system using Docker and deployed with Kubernetes for scalability, reliability, and easy orchestration.
- Implemented GitOps-based CI/CD workflow to automate testing, deployment, and rollback processes for all services.
- Monitored system performance using Prometheus and Grafana, tracking metrics such as latency, throughput, model drift, and system health.
- Built frontend React interface to visualize recommended items, user interactions, and model performance dashboards.
- Achieved production-grade throughput and latency targets while simulating Expedia-scale workloads with multi-stage pipelines and real-time streaming data.




Example of email responses each day for trades:

Kalshi Bot · Mar 09 · 11:55 PM  
6 markets shown  
  
——— TOMORROW Mar 10 ———  
  
![📍](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f4cd/32.png) MIAMI — LOW 71–72°F  
Kalshi: 54%  
Model: 12% → BUY NO (gap: -42%)  
Models: NWS 72° | VC 71° | PW 73° | ECMWF 72° | GEM 68° | ENS 75° | Spread: 7°  ![⚠️](https://fonts.gstatic.com/s/e/notoemoji/17.0/26a0_fe0f/32.png) HIGH SPREAD  
————————————————  
![📍](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f4cd/32.png) LAS VEGAS — HIGH 79–80°F  
Kalshi: 50%  
Model: 11% → BUY NO (gap: -39%)  
Models: NWS 79° | VC 79° | PW 79° | ECMWF 78° | GEM 79° | ENS 72° | Spread: 7°  ![⚠️](https://fonts.gstatic.com/s/e/notoemoji/17.0/26a0_fe0f/32.png) HIGH SPREAD  
————————————————  
![📍](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f4cd/32.png) LAS VEGAS — HIGH 77–78°F  
Kalshi: 45%  
Model: 6% → BUY NO (gap: -39%)  
Models: NWS 79° | VC 79° | PW 79° | ECMWF 78° | GEM 79° | ENS 72° | Spread: 7°  ![⚠️](https://fonts.gstatic.com/s/e/notoemoji/17.0/26a0_fe0f/32.png) HIGH SPREAD  
————————————————  
![📍](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f4cd/32.png) PHOENIX — HIGH 77–78°F  
Kalshi: 46%  
Model: 8% → BUY NO (gap: -38%)  
Models: NWS 78° | VC 77° | PW 76° | ECMWF 77° | GEM 75° | ENS 76° | Spread: 3°  
————————————————  
![📍](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f4cd/32.png) SEATTLE — HIGH 44–45°F  
Kalshi: 40%  
Model: 8% → BUY NO (gap: -32%)  
Models: NWS 45° | VC 45° | PW 43° | ECMWF 43° | GEM 44° | ENS 44° | Spread: 2°  
————————————————  
![📍](https://fonts.gstatic.com/s/e/notoemoji/17.0/1f4cd/32.png) SAN FRANCISCO — HIGH 63–64°F  
Kalshi: 39%  
Model: 8% → BUY NO (gap: -31%)  
Models: NWS 62° | VC 61° | PW 60° | ECMWF 63° | GEM 58° | ENS 63° | Spread: 5°  ![⚠️](https://fonts.gstatic.com/s/e/notoemoji/17.0/26a0_fe0f/32.png) HIGH SPREAD  
————————————————  
──────────────────────  
Not financial advice.