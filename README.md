# Spring Petclinic Containerization & DevSecOps Pipeline

## Overview

This project demonstrates the containerization and secure CI/CD implementation of the Spring Petclinic application using GitHub Actions, Docker, SonarCloud, Trivy, and AWS ECR.

A key focus of this project was implementing DevSecOps best practices through automated security scanning, branch-based security gates, and secretless AWS authentication using GitHub OpenID Connect (OIDC).

---

## Technologies

* Java 21 (Eclipse Temurin)
* Spring Boot
* Maven Wrapper
* Docker
* GitHub Actions
* SonarCloud
* Trivy
* AWS ECR
* AWS IAM
* GitHub OIDC

---

## Key Features

### CI/CD Automation

* Automated Maven build and testing
* GitHub Actions workflow orchestration
* Branch-aware deployment controls

### Containerization

* Multi-stage Docker build
* Optimized runtime image
* Reduced attack surface

### Code Quality

* SonarCloud static code analysis
* Automated quality checks

### Security

* Trivy filesystem scanning
* Trivy container image scanning
* Security artifact retention
* Branch-based security gates

### AWS Integration

* Secure image publishing to Amazon ECR
* OIDC-based authentication
* No long-lived AWS access keys

---

## Architecture

Developer → GitHub Repository → GitHub Actions Workflow

GitHub Actions Pipeline:

1. Checkout Source
2. Maven Build
3. Unit Tests
4. SonarCloud Analysis
5. Trivy Filesystem Scan
6. Docker Build
7. Trivy Image Scan
8. OIDC Authentication to AWS
9. Push Container Image to ECR

---

## AWS Authentication using OIDC

Traditional CI/CD pipelines commonly store AWS access keys as GitHub Secrets.

This project uses GitHub OpenID Connect (OIDC) to eliminate long-lived AWS credentials and improve security.

### Authentication Flow

GitHub Actions
↓
GitHub OIDC Provider
↓
AWS Security Token Service (STS)
↓
AssumeRoleWithWebIdentity
↓
IAM Role
↓
Amazon ECR

### Benefits

* No AWS access keys stored in GitHub
* Temporary credentials generated on demand
* Reduced credential management overhead
* Improved security posture
* AWS security best practice

### GitHub Permissions

```yaml
permissions:
  id-token: write
  contents: read
```

### AWS Login

GitHub Actions assumes an IAM role using OIDC and receives temporary credentials from AWS STS before pushing images to ECR.

---

## Branch-Based Security Gates

### develop Branch

Purpose:

* Feature development
* Security visibility

Behavior:

* Vulnerabilities reported
* Pipeline continues
* Image pushed to ECR

### main Branch

Purpose:

* Production-ready releases

Behavior:

* Vulnerabilities scanned
* CRITICAL findings fail pipeline
* Prevents vulnerable images from reaching production

---

## Security Remediation Success

### Initial Findings

* 10 CRITICAL vulnerabilities
* Multiple HIGH vulnerabilities

### Investigation

* Trivy report analysis
* Maven dependency tree review
* Root cause identification

### Remediation

* Spring Boot upgraded from 4.0.3 to 4.0.6
* Tomcat version overridden to 11.0.22

### Final Results

* CRITICAL vulnerabilities reduced from 10 → 0
* Production security gate passing
* Secure image successfully published to AWS ECR

---

## Outcomes

* Containerized Spring Boot application
* Automated CI/CD workflow
* Integrated DevSecOps controls
* OIDC-based AWS authentication
* Secure image publishing to ECR
* Vulnerability remediation from 10 CRITICAL findings to 0

---

## Future Enhancements

* SBOM Generation
* Cosign Image Signing
* EKS Deployment Stage
* GitOps using ArgoCD
* Kubernetes Security Scanning
* Prometheus and Grafana Monitoring
