# Trivy Security Scan Results

## Trivy Filesystem Scan

The filesystem scan was performed against the application source code and Maven dependency tree.

### Initial Scan Results (Before Remediation)

| Severity | Count |
| -------- | ----- |
| CRITICAL | 10    |
| HIGH     | 18    |
| MEDIUM   | 27    |
| LOW      | 12    |

### Key Findings

| Package                | Vulnerability Type | Severity |
| ---------------------- | ------------------ | -------- |
| tomcat-embed-core      | Multiple CVEs      | CRITICAL |
| tomcat-embed-websocket | Multiple CVEs      | CRITICAL |
| tomcat-embed-el        | Multiple CVEs      | CRITICAL |


## Investigation Process

To identify the vulnerable dependency chain, Maven dependency analysis was performed.

```bash
./mvnw dependency:tree
```

The analysis identified Apache Tomcat 11.0.21 as the source of several CRITICAL vulnerabilities.

---

## Remediation Actions

### Spring Boot Upgrade

```text
Previous Version: 4.0.3
Updated Version: 4.0.6
```

### Tomcat Override

```xml
<tomcat.version>11.0.22</tomcat.version>
```

### Validation

After updating dependencies, Trivy scans were executed again to verify remediation.

---

# Trivy Filesystem Scan Results After Remediation

| Severity | Count |
| -------- | ----- |
| CRITICAL | 0     |
| HIGH     | 5     |
| MEDIUM   | 18    |
| LOW      | 12    |

### Outcome

✅ All CRITICAL vulnerabilities eliminated

✅ Significant reduction in HIGH severity findings

✅ Security gate requirements satisfied

---

# Trivy Container Image Scan

The final Docker runtime image was scanned to identify operating system and application dependency vulnerabilities.

## Initial Image Scan Results

| Severity | Count |
| -------- | ----- |
| CRITICAL | 10    |
| HIGH     | 15    |
| MEDIUM   | 20    |
| LOW      | 8     |

---

## Final Image Scan Results

| Severity | Count |
| -------- | ----- |
| CRITICAL | 0     |
| HIGH     | 4     |
| MEDIUM   | 14    |
| LOW      | 8     |

---

# Security Improvement Summary

| Metric                   | Before | After  |
| ------------------------ | ------ | ------ |
| CRITICAL Vulnerabilities | 10     | 0      |
| HIGH Vulnerabilities     | 18     | 5      |
| Security Gate Status     | Failed | Passed |

---

# Key Takeaway

This project demonstrated a complete vulnerability remediation workflow:

1. Identify vulnerabilities using Trivy.
2. Analyze dependency relationships using Maven dependency tree.
3. Investigate root causes.
4. Upgrade vulnerable dependencies.
5. Override affected component versions when necessary.
6. Re-scan the application and container image.
7. Validate compliance with security gate requirements.

The remediation effort successfully reduced CRITICAL vulnerabilities from 10 to 0 while maintaining application functionality and deployment readiness.
