## 🚀 CI/CD Pipeline Implementation & Debugging (GitHub Actions)
## 👩‍💻 About This Project

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
## 🧱 Project Structure
```text
.
├── .github/workflows/ci-workflow.yml   # CI pipeline definition
├── templates/index.html               # Frontend UI
├── app.py                             # Flask application
├── run.py                             # App runner
├── requirements.txt                   # Dependencies
├── test_app.py                        # Test cases (pytest)
└── README.md
```

## ⚙️ CI Pipeline Overview

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

## 🧠 Key Engineering Learnings
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

## 🔧 Future Enhancements
- Dockerizing the application
- Adding linting (flake8) for code quality
- Implementing multi-stage CI/CD pipeline
- Deployment to AWS (ECS / EC2)

## 💡 Why This Project Matters

This project goes beyond “setting up CI/CD” and focuses on how pipelines behave in real scenarios, including failures and debugging — a critical skill expected from DevOps engineers.

**📣 Author**<br>
Pallavi Agarwal
Aspiring DevOps Engineer | Learning in Public