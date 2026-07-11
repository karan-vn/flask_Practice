# Student Registration System – CI/CD Pipeline

## Project Overview

This project demonstrates the implementation of Continuous Integration and Continuous Deployment (CI/CD) for a Flask-based Student Registration System using:

- Jenkins Pipeline
- GitHub Actions
- MongoDB Atlas
- GitHub
- Python 3.13
- Flask

The application allows users to perform CRUD (Create, Read, Update, Delete) operations on student records stored in MongoDB Atlas.

---

# Technologies Used

- Python 3.13
- Flask
- Flask-PyMongo
- MongoDB Atlas
- MongoDB Compass
- Jenkins
- GitHub Actions
- Pytest
- Pylint
- Bandit
- Git & GitHub

---

# Project Structure

```
.
├── .github/
│   └── workflows/
│       └── flask-ci-cd.yml
├── templates/
├── app.py
├── test_app.py
├── requirements.txt
├── Jenkinsfile
├── README.md
└── LICENSE
```

---

# Application Features

- Add Student
- Update Student
- Delete Student
- View Student List
- MongoDB Atlas Integration
- Automated Testing
- Automated Security Scan
- Automated Linting
- CI/CD Pipeline

---

# Phase 1 – Jenkins CI/CD Pipeline

## Jenkins Pipeline Stages

1. Install Dependencies
2. Lint Code (Pylint)
3. Security Scan (Bandit)
4. Run Unit Tests (Pytest)
5. Deploy Flask Application
6. Email Notification
7. Workspace Cleanup

---

## Jenkins Pipeline Execution

```
Checkout Source Code
        ↓
Install Dependencies
        ↓
Run Pylint
        ↓
Run Bandit
        ↓
Run Pytest
        ↓
Deploy Flask Application
        ↓
Email Notification
```

---

# Phase 2 – GitHub Actions CI/CD

The GitHub Actions workflow automatically executes whenever code is pushed.

## Workflow Trigger

### Push to Main Branch

- Install Dependencies
- Run Lint
- Run Security Scan
- Execute Tests
- Build Application

### Push to Staging Branch

- Install Dependencies
- Run Tests
- Build Application
- Deploy to Staging

### Release Creation

- Install Dependencies
- Run Tests
- Build Application
- Deploy to Production

---

# GitHub Actions Workflow

The workflow consists of four jobs:

## Test Application

- Checkout Repository
- Setup Python
- Install Dependencies
- Configure Environment Variables
- Run Pylint
- Run Bandit
- Run Pytest

---

## Build Application

Creates a build artifact containing the application source code.

---

## Deploy to Staging

Runs automatically when changes are pushed to the **staging** branch.

(Currently simulated using deployment messages.)

---

## Deploy to Production

Runs automatically whenever a GitHub Release is published.

(Currently simulated using deployment messages.)

---

# Environment Secrets

The following GitHub Secrets are required.

Navigate to:

```
Repository
    ↓
Settings
    ↓
Secrets and Variables
    ↓
Actions
```

Add:

| Secret Name | Description |
|-------------|-------------|
| MONGO_URI | MongoDB Atlas Connection String |
| SECRET_KEY | Flask Secret Key |

Example:

```
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/studentsdb?retryWrites=true&w=majority

SECRET_KEY=your_secret_key
```

---

# Installing the Project

Clone the repository.

```bash
git clone https://github.com/<your-username>/<repository-name>.git

cd <repository-name>
```

Create a virtual environment.

```bash
python -m venv venv
```

Activate the virtual environment.

### Windows

```bash
venv\Scripts\activate
```

Install dependencies.

```bash
pip install -r requirements.txt
```

Create a `.env` file.

```
MONGO_URI=<your_mongodb_connection_string>

SECRET_KEY=<your_secret_key>
```

Run the application.

```bash
python app.py
```

Application URL

```
http://127.0.0.1:5000
```

---

# Running Tests

```bash
pytest test_app.py -v
```

---

# Running Pylint

```bash
pylint app.py --exit-zero
```

---

# Running Bandit

```bash
bandit -r .
```

---

# MongoDB Atlas

The application uses MongoDB Atlas for storing student records.

Database:

```
studentsdb
```

Collection:

```
students
```

---

# CI/CD Workflow

```
Developer Push
        │
        ▼
GitHub Repository
        │
        ▼
GitHub Actions
        │
        ▼
Install Dependencies
        │
        ▼
Pylint
        │
        ▼
Bandit
        │
        ▼
Pytest
        │
        ▼
Build Application
        │
        ├──────────────► Staging Deployment
        │
        └──────────────► Production Deployment
```

---

# Assignment Deliverables

✅ Jenkins Pipeline

✅ GitHub Actions Workflow

✅ Automated Testing

✅ Automated Linting

✅ Security Scanning

✅ Build Artifact

✅ Staging Deployment

✅ Production Deployment

✅ MongoDB Atlas Integration

---

## Required Screenshots

<img width="959" height="403" alt="Screenshot 2026-07-11 081612" src="https://github.com/user-attachments/assets/a96596cb-f2a1-4fb9-81ba-b8a790ba3648" />


<img width="959" height="560" alt="Screenshot 2026-07-11 081317" src="https://github.com/user-attachments/assets/ee04b079-021a-4165-b3e6-e59555cb6f11" />

<img width="727" height="314" alt="image" src="https://github.com/user-attachments/assets/af4c26d7-16e9-476f-8374-f925fd61aef3" />

<img width="725" height="367" alt="Screenshot 2026-07-09 210129" src="https://github.com/user-attachments/assets/58e6f4d8-9b7d-4571-be99-0f0721adaf0d" />
