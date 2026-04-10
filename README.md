
![CI](https://img.shields.io/badge/CI-Passing-brightgreen)
![Docker](https://img.shields.io/badge/Docker-Enabled-blue)
![Deployment](https://img.shields.io/badge/Deployed-AWS-orange)

## 🚀 CI/CD Pipeline Implementation & Debugging (GitHub Actions)
## 👩‍💻 About This Project

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


## 🧱 Project Structure
```text
.
├── .github/workflows/
│   ├── lint-and-matrix-strategy.yml   # CI: Linting + Python matrix
│   ├── docker-push-and-build.yml      # Docker build & push
│   └── deploy-app.yml                # Deployment workflow (self-hosted)
├── templates/index.html             # Frontend UI
├── app.py                           # Flask application
├── run.py                           # App runner
├── test_app.py                      # Test cases (pytest)
├── Dockerfile                       # Container definition
├── docker-compose.yml               # Deployment configuration
├── requirements.txt                # Dependencies
├── .dockerignore
├── screenshots
│   ├── cicd-docker-deploy          #snaps of full pipeline
└── README.md
```

## ⚙️ CI Pipeline Overview

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

## 🚨 Real Issues Faced (Debugging Scenarios)
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


## 🧠 Key Engineering Learnings

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

## ☁️ Deployment

- Hosted on AWS EC2
- Deployed using Docker Compose
- Automated via GitHub Actions (self-hosted runner)

## 🔧 Future Enhancements

- Add integration tests in CI pipeline
- Implement rollback strategy in deployment
- Add monitoring & logging (Prometheus/Grafana)
- Move deployment to Kubernetes

## 💡 Why This Project Matters

This is not just a Flask app.

It demonstrates how a real-world CI/CD pipeline behaves under failure conditions, and how to debug and fix issues across multiple environments — a key skill for DevOps engineers.

**📣 Author**<br>
Pallavi Agarwal<br>
Aspiring DevOps Engineer | Learning in Public
