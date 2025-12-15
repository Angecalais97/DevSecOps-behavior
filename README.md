# DevSecOps-behavior
# DevSecOps From Zero to Production – Classroom Project

> **Audience**: DevOps / Cloud / Security students
>
> **Goal**: Learn how to design a real DevSecOps pipeline starting from a very simple codebase, containerize it, secure it, and deploy it using **GitHub Pages** and **AWS ECS**.

---

## 1️⃣ Project Context

This repository contains a **very small static web application**:

* `index.html`
* `style.css`

There is:

* ❌ No backend
* ❌ No database
* ❌ No framework

This is **intentional**.

The objective is to prove that **DevSecOps practices apply even to simple projects**.

---

## 2️⃣ First Step – Analyze the Code (Before Any Tool)

Before writing Dockerfiles or CI pipelines, always **understand what you are deploying**.

### What type of application is this?

* Static website
* Served by a web server (NGINX)
* No runtime dependencies

### Consequences for DevSecOps

| Decision                | Reason                             |
| ----------------------- | ---------------------------------- |
| Use NGINX               | Industry standard for static sites |
| No unit backend tests   | No backend logic exists            |
| Focus on security scans | Code & container security          |

---

## 3️⃣ Containerization – Build the Dockerfile

### Why containerize a static site?

* Consistent runtime
* Portable deployment
* Required for ECS

### Dockerfile responsibilities

* Use a minimal base image
* Serve static files securely
* Do nothing more than required

> Students must write a Dockerfile using `nginx:alpine`.

---

## 4️⃣ CI Design – Think Before YAML

Before writing GitHub Actions, define **what must be verified**.

### CI Objectives

1. Detect secrets
2. Scan source code for risks
3. Scan container images
4. Block deployment if security fails

---

## 5️⃣ Security & Quality Tools Used (and Why)

### 🔐 Gitleaks – Secret Detection

**Why**:

* Prevent API keys and passwords from entering Git history

**When**:

* First step in CI

**Official documentation**:

* [https://github.com/gitleaks/gitleaks](https://github.com/gitleaks/gitleaks)
* [https://gitleaks.io/](https://gitleaks.io/)

---

### 📊 SonarQube – Code Quality & Static Analysis

**Why SonarQube is included even for a simple project**:

* DevSecOps is not only about vulnerabilities
* Code quality issues become security issues over time
* SonarQube enforces **discipline and standards**

**What SonarQube analyzes here**:

* HTML structure issues
* Maintainability problems
* Duplicated code
* Basic security smells (e.g. unsafe patterns)

**Important teaching point**:

> Even simple codebases deserve quality gates.

**When it runs**:

* After checkout
* Before Docker build

**Pipeline rule**:

* Deployment is blocked if the Quality Gate fails

**Official documentation**:

* [https://docs.sonarsource.com/sonarqube/](https://docs.sonarsource.com/sonarqube/)
* [https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/)

---

---

### 🔎 Trivy – Vulnerability Scanning

**Filesystem scan**:

* Detects vulnerable files and misconfigurations

**Image scan**:

* Detects OS and package vulnerabilities inside the container

**Rule**:

* Fail pipeline on HIGH or CRITICAL issues

---

## 6️⃣ Image Versioning Strategy

Images are tagged using the GitHub build number:

```
IMAGE_TAG = github.run_number
```

### Why this matters

* Traceability
* Easy rollback
* Production-grade practice

---

## 7️⃣ Deployment Targets

### 📄 GitHub Actions

**Why GitHub Actions**:

* Native CI/CD for GitHub repositories
* Fine-grained permissions
* Easy integration with security tools

**Official documentation**:

* [https://docs.github.com/en/actions](https://docs.github.com/en/actions)

### 🌐 GitHub Pages (Learning & Demo)

* Fast feedback
* Visual validation
* Simple deployment

Used to demonstrate **CI → Deploy flow**.

---

### ☁️ AWS ECS (Production-style)

* Container runs in AWS
* Image pulled from Amazon ECR
* Real-world deployment model

---

## 8️⃣ Amazon ECR Lifecycle Policy

### What is it?

An automated rule that **removes old container images**.

### Why it is required

* Prevents storage explosion
* Reduces security risk
* Enforces hygiene

### Example strategy

* Keep last N tagged images
* Delete untagged images after X days

---

## 9️⃣ DevSecOps Principles Applied

* Least privilege permissions
* Security before deployment
* Fail fast, fail safe
* Simple tools used correctly

---

## 🔟 What Students Learn From This Project

* How to analyze an application
* How to design a Dockerfile
* How to build a secure CI pipeline
* How to scan containers
* How to deploy safely
* How real DevSecOps decisions are made

---

## Final Message

> DevSecOps is not about complexity.
>
> It is about **thinking clearly**, **securing early**, and **deploying responsibly**.

This project is intentionally simple to highlight **professional DevSecOps behavior**.

