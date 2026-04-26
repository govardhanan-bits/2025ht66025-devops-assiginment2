# ACEest Fitness & Gym - CI/CD Pipeline

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-aceest--fitness-blue?logo=docker)](https://hub.docker.com/r/govardhanankanniyapansriram824/aceest-fitness)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-Jenkins-red?logo=jenkins)](https://www.jenkins.io/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Minikube-blue?logo=kubernetes)](https://kubernetes.io/)

A complete DevOps implementation of a fitness and gym management web application with CI/CD pipeline, containerization, and multiple Kubernetes deployment strategies.

**Course:** Introduction to DevOps (CSIZG514/SEZG514) | **Assignment:** 2  
**Repository:** [github.com/govardhanan-bits/2025ht66025-devops-assiginment2](https://github.com/govardhanan-bits/2025ht66025-devops-assiginment2)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [CI/CD Pipeline](#cicd-pipeline)
- [Deployment Strategies](#deployment-strategies)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Docker Images](#docker-images)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Testing](#testing)
- [Documentation](#documentation)

---

## 🎯 Overview

ACEest Fitness & Gym is a Flask-based web application converted from a desktop tkinter app, featuring a complete DevOps pipeline with automated testing, containerization, and orchestration. The project demonstrates industry-standard CI/CD practices with Jenkins, Docker, Kubernetes, and SonarQube integration.

### Application Features

- 🔐 **User Authentication** - Role-based login system
- 👥 **Client Management** - CRUD operations for fitness clients
- 📊 **Progress Tracking** - Weekly adherence and workout logging
- 💪 **Program Assignment** - Fat Loss, Muscle Gain, Beginner programs
- 📈 **Analytics** - BMI calculation, calorie estimation, progress charts
- 🔌 **REST API** - Health checks, client data, and progress endpoints

---

## 🛠️ Technology Stack

| Category | Tools |
|----------|-------|
| **Application** | Python 3.11, Flask, SQLite |
| **Testing** | Pytest (25+ test cases) |
| **Quality** | SonarQube, Code Coverage |
| **Containerization** | Docker, Docker Hub |
| **Orchestration** | Kubernetes (Minikube) |
| **CI/CD** | Jenkins, GitHub Webhooks |
| **Version Control** | Git, GitHub |

---

## 🔄 CI/CD Pipeline

### Pipeline Flow

```
GitHub Push → Jenkins Webhook → Checkout → Install Dependencies
    ↓
Run Pytest Tests → SonarQube Analysis → Quality Gate Check
    ↓
Build Docker Image → Push to Docker Hub → Deploy to Kubernetes
```

### Jenkins Stages

1. **Checkout** - Pull latest code from GitHub
2. **Install Dependencies** - Set up Python virtual environment
3. **Unit Testing** - Execute 25+ Pytest test cases
4. **SonarQube Analysis** - Static code analysis and quality checks
5. **Quality Gate** - Enforce code quality standards
6. **Build Docker Image** - Create containerized application
7. **Push to Docker Hub** - Upload image to registry
8. **Deploy to Kubernetes** - Rolling deployment to cluster

---

## 🚀 Deployment Strategies

This project implements **5 advanced Kubernetes deployment strategies**:

### 1. Rolling Update
- **Zero-downtime** deployments
- Pods replaced one at a time
- Configuration: `maxSurge: 1`, `maxUnavailable: 0`
- Rollback: `kubectl rollout undo deployment/aceest-fitness-rolling`

### 2. Blue-Green Deployment
- Two identical environments (Blue v3.1.2, Green v3.2.4)
- Instant traffic switching via service selector
- Quick rollback by changing selector
- Perfect for major releases

### 3. Canary Release
- Gradual rollout: 75% stable + 25% canary
- Monitor new version with real traffic
- Scale up canary if stable, rollback if issues
- Risk mitigation strategy

### 4. A/B Testing
- Header-based traffic routing
- Users with `X-Version: B` header see new version
- Compare feature performance
- Data-driven release decisions

### 5. Shadow Deployment
- Traffic mirroring using Istio
- New version processes real requests (responses discarded)
- Zero user impact
- Production-load testing

---

## 🚀 Getting Started

### Prerequisites

```bash
# Required tools
- Docker
- Kubernetes (Minikube or similar)
- Jenkins
- Python 3.11+
- Git
```

### Local Development

```bash
# Clone the repository
git clone https://github.com/govardhanan-bits/2025ht66025-devops-assiginment2.git
cd 2025ht66025-devops-assiginment2

# Install dependencies
pip install -r requirements.txt

# Run the application
python app.py

# Access at http://localhost:5000
```

### Run Tests

```bash
# Execute all tests
pytest test_app.py -v

# With coverage
pytest test_app.py --cov=app --cov-report=html
```

### Docker Deployment

```bash
# Build the image
docker build -t aceest-fitness:v3.2.4 .

# Run container
docker run -p 5000:5000 aceest-fitness:v3.2.4

# Or pull from Docker Hub
docker pull govardhanankanniyapansriram824/aceest-fitness:latest
docker run -p 5000:5000 govardhanankanniyapansriram824/aceest-fitness:latest
```

### Kubernetes Deployment

```bash
# Start Minikube
minikube start

# Deploy the application
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml

# Check deployment
kubectl get pods -n aceest
kubectl get svc -n aceest

# Access the application
minikube service aceest-fitness-service -n aceest
```

### Try Different Deployment Strategies

```bash
# Rolling Update
kubectl apply -f k8s/rolling-update.yaml

# Blue-Green Deployment
kubectl apply -f k8s/blue-green-deployment.yaml

# Canary Release
kubectl apply -f k8s/canary-deployment.yaml

# A/B Testing
kubectl apply -f k8s/ab-testing.yaml

# Shadow Deployment (requires Istio)
kubectl apply -f k8s/shadow-deployment.yaml
```

---

## 📁 Project Structure

```
.
├── app.py                          # Flask web application
├── test_app.py                     # Pytest unit tests (25+ cases)
├── requirements.txt                # Python dependencies
├── Dockerfile                      # Container build instructions
├── Jenkinsfile                     # CI/CD pipeline definition
├── sonar-project.properties        # SonarQube configuration
├── README.md                       # This file
├── REPORT.md                       # Detailed assignment report
│
├── templates/                      # Flask HTML templates
│   ├── base.html
│   ├── login.html
│   ├── dashboard.html
│   ├── add_client.html
│   ├── client.html
│   └── programs.html
│
├── k8s/                            # Kubernetes manifests
│   ├── namespace.yaml              # Namespace definition
│   ├── secret.yaml                 # Secrets configuration
│   ├── deployment.yaml             # Standard deployment
│   ├── service.yaml                # Service definition
│   ├── rolling-update.yaml         # Rolling update strategy
│   ├── blue-green-deployment.yaml  # Blue-green strategy
│   ├── canary-deployment.yaml      # Canary release strategy
│   ├── ab-testing.yaml             # A/B testing strategy
│   └── shadow-deployment.yaml      # Shadow deployment strategy
│
└── The code versions for DevOps Assignment/
    └── Aceestver-*.py              # Version history (v1.0 to v3.2.4)
```

---

## 🐳 Docker Images

Docker images are available on Docker Hub:

- **Repository:** [govardhanankanniyapansriram824/aceest-fitness](https://hub.docker.com/r/govardhanankanniyapansriram824/aceest-fitness)
- **Latest Version:** `v3.2.4`

```bash
# Pull specific version
docker pull govardhanankanniyapansriram824/aceest-fitness:v3.2.4

# Pull latest
docker pull govardhanankanniyapansriram824/aceest-fitness:latest
```

### Image Details

- **Base Image:** `python:3.11-slim`
- **Size:** ~150MB (optimized with .dockerignore)
- **Exposed Port:** 5000
- **Health Check:** `/api/health`

---

## ☸️ Kubernetes Deployment

### Namespace

All resources are deployed in the `aceest` namespace:

```bash
kubectl get all -n aceest
```

### Service

- **Type:** NodePort
- **Port:** 5000
- **Target Port:** 5000

```bash
# Get service URL (Minikube)
minikube service aceest-fitness-service -n aceest --url
```

### Resource Limits

```yaml
resources:
  requests:
    memory: "128Mi"
    cpu: "100m"
  limits:
    memory: "256Mi"
    cpu: "250m"
```

### Health Checks

- **Liveness Probe:** `GET /api/health` every 15s
- **Readiness Probe:** `GET /api/health` every 10s

---

## 🧪 Testing

### Test Coverage

The project includes **25+ comprehensive test cases** covering:

- ✅ User authentication (login, logout, sessions)
- ✅ Client management (create, read, update, delete)
- ✅ Progress tracking (add, retrieve, validate)
- ✅ API endpoints (health, clients, progress)
- ✅ Data validation and edge cases
- ✅ Database operations

### Running Tests

```bash
# Run all tests with verbose output
pytest test_app.py -v

# Run with coverage report
pytest test_app.py --cov=app --cov-report=html

# Run specific test
pytest test_app.py::test_login_success -v
```

### Test Results

```
test_app.py::test_health_endpoint PASSED
test_app.py::test_login_success PASSED
test_app.py::test_login_invalid PASSED
test_app.py::test_add_client PASSED
test_app.py::test_get_clients PASSED
... [25+ tests] ...
======================== 25 passed in 2.34s ========================
```

---

## 📚 Documentation

- **[REPORT.md](REPORT.md)** - Detailed assignment report with architecture, challenges, and outcomes
- **[Jenkinsfile](Jenkinsfile)** - Complete CI/CD pipeline configuration
- **[Dockerfile](Dockerfile)** - Container build instructions with comments

### API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/health` | GET | Health check endpoint |
| `/api/clients` | GET | Retrieve all clients |
| `/api/progress/<client_id>` | GET | Get client progress data |
| `/login` | POST | User authentication |
| `/logout` | GET | User logout |
| `/dashboard` | GET | Main dashboard |
| `/add_client` | POST | Add new client |
| `/client/<client_id>` | GET | Client details |

### Default Credentials

```
Username: admin
Password: admin123
```

---

## 🏆 Assignment Highlights

- ✅ **Complete CI/CD Pipeline** - Automated from code push to deployment
- ✅ **25+ Unit Tests** - Comprehensive test coverage with Pytest
- ✅ **Code Quality Gates** - SonarQube integration with quality enforcement
- ✅ **Containerization** - Optimized Docker images on Docker Hub
- ✅ **5 Deployment Strategies** - Rolling, Blue-Green, Canary, A/B, Shadow
- ✅ **Zero Downtime** - Production-ready deployment configurations
- ✅ **Health Monitoring** - Kubernetes liveness and readiness probes
- ✅ **Resource Management** - CPU and memory limits configured

---

## 📝 License

This project is created for educational purposes as part of the DevOps course at BITS Pilani.

---

## 👤 Author

**Govardhanan K S**  
BITS Pilani - 2025ht66025  
Course: CSIZG514/SEZG514 - Introduction to DevOps

---

## 🔗 Links

- **GitHub Repository:** https://github.com/govardhanan-bits/2025ht66025-devops-assiginment2
- **Docker Hub:** https://hub.docker.com/r/govardhanankanniyapansriram824/aceest-fitness
- **Report:** [REPORT.md](REPORT.md)

---

**⭐ If you find this project useful, please star the repository!**
