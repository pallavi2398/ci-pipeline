![Security](https://img.shields.io/badge/Security-Scanned-success)
![CI](https://img.shields.io/badge/CI-Passing-brightgreen)
![Docker](https://img.shields.io/badge/Docker-Enabled-blue)
![Deployment](https://img.shields.io/badge/Deployed-AWS-orange)


## 🔐 DevSecOps Pipeline Implementation (CI/CD + Security + Deployment on AWS)
## What's Inside

This repo contains a **Flask web app** with a full **CI/CD + DevSecOps pipeline** built entirely using GitHub Actions.

```
app.py                  → Flask app (source code)
Dockerfile              → Container image definition
docker-compose.yml      → Production deployment config
templates/index.html    → App frontend
index.html              → Portfolio static site
requirements.txt        → Python dependencies (flask,flake8,bandit,gunicorn,pytest,Werkzeug)
run.py                  → Entrypoint of Flask app
test_app.py             → Route tests (pytest)
screenshots             → Images
```
## Project Evolution: From CI/CD to DevSecOps

This project was built in 3 progressive stages, starting from a basic pipeline and evolving into a complete DevSecOps implementation.


## Part 1: 🚀 CI Pipeline Implementation & Debugging
### 👩‍💻 About This Project


This project demonstrates the implementation of a CI (Continuous Integration) pipeline for a Flask-based application using GitHub Actions — with a strong focus on debugging real pipeline failures rather than just setting up workflows.


**Instead of stopping at a successful pipeline setup, this project explores:**


- Why pipelines fail
- How to debug failures using logs
- How to fix issues systematically
**🎯 What This Project Demonstrates**
- Writing and structuring GitHub Actions workflows
- Understanding CI pipeline lifecycle (trigger → job → steps)
- Debugging pipeline failures using logs
- Integrating automated testing using pytest
- Fixing real-world CI issues (not just configuration setup)

### ⚙️ CI Pipeline Overview


**The pipeline is triggered on every push and performs:**


- Code checkout
- Python environment setup
- Dependency installation
- Test execution using pytest


**🚨 Real Issue Faced (Debugging Scenario)**


During implementation, the pipeline failed despite correct configuration.
```bash
Error:
collected 0 items
Root Cause:


The CI system executed successfully, but no tests were available to run.
```


**Resolution:**
- Identified issue through pipeline logs
- Added a test case (test_app.py)
- Re-ran pipeline successfully


### 🧠 Key Engineering Learnings
- CI failures are often logic or validation issues, not tool issues
- A “successful workflow” does not guarantee a meaningful pipeline
- Logs are the primary source of truth while debugging
- CI pipelines validate code — not just automate steps


**▶️ Run Locally**
```bash
pip install -r requirements.txt
python run.py
```


**Access the app at:**
```bash
http://localhost:80
```


### 🔧 Future Enhancements
- Dockerizing the application
- Adding linting (flake8) for code quality
- Implementing multi-stage CI/CD pipeline
- Deployment to AWS (ECS / EC2)

---

## Part 2: 🚀 CI/CD with Docker & Deployment
### 👩‍💻 About This Project

This project demonstrates a complete **CI/CD pipeline for a Flask-based application**, going beyond basic CI to include **Dockerization, image registry, and automated deployment on AWS using a self-hosted runner**.

**Instead of just building a working pipeline, this project focuses on:**


- Real-world pipeline failures
- Debugging across environments (local vs CI vs production)
- Understanding how systems behave in real deployments


**🎯 What This Project Demonstrates**

- Writing and structuring multiple GitHub Actions workflows
- CI with Python matrix strategy (3.13, 3.14)
- Code linting using flake8
- Containerization using Docker
- Building & pushing images to Docker Hub
- Deployment using Docker Compose
- Self-hosted runner setup on AWS EC2
- Debugging real-world CI/CD failures


### ⚙️ CI Pipeline Overview

**🔹 1. CI Pipeline (Lint + Matrix Strategy)**

- Runs on every push to main
- Tests across multiple Python versions (3.13, 3.14)
- Runs flake8 for code quality

**🔹 2. Docker Build & Push**

- Builds Docker image from Dockerfile
- Pushes image to Docker Hub
- Uses GitHub Secrets & Variables for authentication

**🔹 3. Deployment Pipeline**

- Triggered manually (workflow_dispatch)
- Runs on self-hosted runner (AWS EC2)
- Pulls latest image
- Deploys using Docker Compose

### 🚨 Real Issues Faced (Debugging Scenarios)
This project focuses heavily on real debugging:

**❌ Issue 1: Docker Compose File Not Found**
```bash
Error: no configuration file provided: not found
```
*Root Cause:*
- File name mismatch (Docker-compose.yml vs docker-compose.yml)
*Fix:*
- Renamed file correctly (case-sensitive in Linux)


**❌ Issue 2: Works Locally, Fails in CI**
Code worked on Mac but failed in GitHub Actions<br>
*Root Cause:*
- Path and environment differences


**❌ Issue 3: Deployment Failures on Self-hosted Runner**
Multiple failed deploy jobs before success<br>
*Fix:*
- Debugged logs on runner
- Fixed workflow + environment issues


### 🧠 Key Engineering Learnings

- CI success ≠ Deployment success
- Linux environments are case-sensitive (unlike Mac)
- Docker ensures consistency across environments
- Debugging pipelines is a critical DevOps skill
- Self-hosted runners give more control but require setup & maintenance

**▶️ Run Locally**
```bash
pip install -r requirements.txt
python run.py
```

**Access the app at:**
```bash
http://localhost:80
```

**🐳 Run with Docker**
```bash
docker build -t flask-app .
docker run -d -p 80:80 flask-app
```

### ☁️ Deployment

- Hosted on AWS EC2
- Deployed using Docker Compose
- Automated via GitHub Actions (self-hosted runner)

### 🔧 Future Enhancements

- Add Security in each part of CI like code scanning, secrets scanning, Docker image scanning etc.

---

## Part 3: 🚀DevSecOps Pipeline

### 👩‍💻 About This Project

This project demonstrates a complete **DevSecOps pipeline for a Flask-based application**, integrating **security at every stage of the CI/CD lifecycle**.


### 🔐 DevSecOps Features (Security Integrated Pipeline)

This project integrates multiple layers of security:

- 🔍 **SAST (Static Application Security Testing)** using Bandit
- 🔑 **Secrets Scanning** using Gitleaks
- 📦 **Dependency Vulnerability Scanning** using pip-audit
- 🛡️ **Dockerfile Scanning** using Hadolint
- 🐳 **Container Image Scanning** using Trivy


All scans are automated in GitHub Actions before deployment.

### ⚙️ DevSecOps Pipeline Overview

#### 🔹 1. Code Quality & SAST

- flake8 → Code linting
- Bandit → Security vulnerability detection in Python code

---

#### 🔹 2. Secrets Scanning

- Gitleaks scans repository for exposed secrets, tokens, credentials

---

#### 🔹 3. Dependency Security

- pip-audit checks for known vulnerabilities in Python packages

---

#### 🔹 4. Docker Security

- Validates Dockerfile best practices using Hadolint
- Builds Docker image
- Pushes to Docker Hub

---

#### 🔹 5. Container Image Scanning

- Trivy scans Docker image for vulnerabilities (OS + dependencies)

---

#### 🔹 6. Deployment

- Runs on AWS EC2
- Pulls latest secure image
- Deploys using Docker Compose


### 🛡️ Security Scan Results

- ✅ No secrets detected (Gitleaks)
- ✅ No dependency vulnerabilities (pip-audit)
- ✅ No code vulnerabilities (Bandit)
- ✅ No Dockerfiler vulnerabilities (Hadolint)
- ✅ No container vulnerabilities (Trivy)

All security checks must pass before deployment.

### 🧠 Key Engineering Learnings

- Security must be integrated early (Shift Left approach)
- CI success ≠ Secure application
- Deployment success ≠ Secure deployment
- Automated security scanning reduces risk in production
- Container security is critical in modern deployments
- DevSecOps ensures continuous security validation

### 🔧 Future Enhancements
- Implement rollback strategy in deployment
- Add monitoring & logging (Prometheus/Grafana)
- Move deployment to Kubernetes

## Repo Structure

```
.
├── .github/workflows/
│   │
│   │  # Part 1 — Fundamentals
│   ├── ci-workflow.yml           # Basic workflow, jobs
│   │
│   │  # Part 2- CI/CD 
│   ├── lint-and-matrix-strategy  # Matrix — parallel linting
│   ├── docker-build-push.yml     # Docker CI — build, tag, push (reusable)
│   ├── deploy-app.yml            # Docker CD — workflow_run, self-hosted
│   │
│   │  # Part 3 — DevSecOps Pipeline
│   ├── devsecops-pipeline.yml    # Orchestrator — chains all scans → build → deploy
│   ├── code-quality.yml          # flake8 + bandit (lint + SAST)
│   ├── secrets-scan.yml          # gitleaks (secrets in code)
│   ├── dependency-scan.yml       # pip-audit (package CVEs)
│   ├── docker-lint.yml           # hadolint (Dockerfile checks)
│   ├── image-scan.yml            # Trivy (container image CVEs)
│   └──  deploy-to-server.yml     # SSH + SCP deploy to EC2
│
├── app.py                        # Flask application
├── templates/index.html          # Flask template
├── Dockerfile                    # Container definition
├── docker-compose.yml            # Compose config
├── requirements.txt              # Python dependencies
├── run.py                        # Entrypoint for flask app
├── test_app.py                   # pytest route tests
└── screenshots                   # screenshots of all three parts
    ├── ci-pipeline               # Part 1
    ├── cicd-docker-deploy        # Part 2
    └── DevSecOps                 # Part 3
```


### 📣 Author<br>
Pallavi Agarwal<br>
Aspiring DevOps Engineer | Learning in Public
