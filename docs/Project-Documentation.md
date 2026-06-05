Project 2 – Spring Petclinic Containerization & DevSecOps Pipeline

Executive Summary

The Spring Petclinic Containerization & DevSecOps Pipeline project demonstrates the implementation of a modern CI/CD workflow using GitHub Actions, Docker, SonarCloud, Trivy, and AWS ECR.

The objective was to containerize the Spring Petclinic application, automate build and testing processes, enforce code quality standards, integrate security scanning into the software delivery lifecycle, and securely publish container images to Amazon Elastic Container Registry (ECR).

A key outcome of this project was the identification and remediation of multiple critical vulnerabilities through dependency analysis and version management, reducing CRITICAL findings from 10 to 0 while maintaining application functionality.

Developer
    │
    ▼
GitHub Repository
(main / develop)
    │
    ▼
GitHub Actions Workflow
    │
    ├── Maven Build & Unit Tests
    │
    ├── SonarCloud Analysis
    │
    ├── Trivy Filesystem Scan
    │
    ├── Docker Multi-Stage Build
    │
    ├── Trivy Image Scan
    │
    └── Security Gate Logic
    │
    ├── develop → Report Only
    │
    └── main → Fail on CRITICAL Findings
    │
    ▼
AWS ECR
(Container Registry)
    │
    ▼
Versioned Docker Images


Project Objectives
Primary Goals
Containerize a production-grade Spring Boot application.
Build a secure CI/CD pipeline using GitHub Actions.
Integrate automated security scanning.
Enforce code quality checks.
Store images in AWS ECR.
Implement branch-specific security policies.
Practice vulnerability remediation workflows.

CI/CD Workflow Explanation
