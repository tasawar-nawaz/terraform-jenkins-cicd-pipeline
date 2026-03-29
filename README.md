# CI/CD Pipeline for Java Application (Jenkins · Docker · Kubernetes · AWS EKS · GitOps)

## Overview

This project implements a production-grade CI/CD pipeline for a Java-based application using modern DevOps practices. It demonstrates automated build, test, security validation, containerization, and GitOps-driven deployment on AWS-managed Kubernetes (EKS).

The pipeline is designed for scalability, reliability, and deployment consistency, aligning with real-world cloud-native engineering workflows.

---

## Key Objectives

- Automate software delivery lifecycle (CI + CD)
- Enforce code quality and security gates
- Enable containerized deployments at scale
- Implement GitOps-based release management
- Ensure zero-downtime deployment strategy

---

## System Architecture

Developer → GitHub → Jenkins → SonarQube → Docker Build → Docker Hub → Trivy Scan → Kubernetes Manifest Repo → ArgoCD → AWS EKS → Slack Notifications

<img width="634" height="356" alt="Screenshot 2026-03-28 214438" src="https://github.com/user-attachments/assets/349af7b9-9e32-4081-81cd-dc035e1042bc" />

---

## Tech Stack

**Application**
- Java (Spring Boot / Core Java)
- Maven

**CI/CD**
- Jenkins (Pipeline as Code)
- GitHub Webhooks

**Code Quality & Security**
- SonarQube (Static Code Analysis)
- Trivy (Container Vulnerability Scanning)

**Containerization**
- Docker
- Docker Hub

**Deployment**
- Kubernetes (AWS EKS)
- ArgoCD (GitOps)

**Notifications**
- Slack Webhooks

---

## CI/CD Pipeline Stages

### 1. Source Control (GitHub)
Code is maintained in GitHub using a structured branching strategy. Every push triggers Jenkins via webhook automation.

### 2. Build & Test (Maven)
- Compiles Java source code
- Resolves dependencies
- Executes unit tests
- Generates deployable `.jar` artifact

### 3. Static Code Analysis (SonarQube)
- Detects code smells
- Identifies bugs and vulnerabilities
- Enforces quality gate before proceeding

### 4. Containerization (Docker)
Application is packaged into a Docker image with versioning based on build number or commit SHA.

### 5. Image Registry (Docker Hub)
Docker images are pushed to Docker Hub for centralized versioned storage.

### 6. Security Scanning (Trivy)
Container images are scanned for vulnerabilities. Critical issues can fail the pipeline based on policy.

### 7. GitOps Deployment Update
Kubernetes manifest repository is updated with the new image tag, enabling declarative deployment tracking.

### 8. Continuous Deployment (ArgoCD → AWS EKS)
ArgoCD continuously monitors the manifest repository and automatically syncs changes to the EKS cluster, ensuring desired state reconciliation.

### 9. Notifications (Slack)
Pipeline status (success/failure/deployment updates) is sent to Slack for real-time visibility.

---
<img width="933" height="439" alt="Screenshot 2026-03-28 190230" src="https://github.com/user-attachments/assets/22e265da-2dcf-4a25-bf19-ab468cb552e4" />


## Repository Structure

```bash
├── app/                          # Java application source code
├── Dockerfile                    # Docker build configuration
├── Jenkinsfile                   # CI/CD pipeline definition
├── k8s-manifests/                # Kubernetes deployment files
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
├── sonar-project.properties      # SonarQube configuration
└── README.md

