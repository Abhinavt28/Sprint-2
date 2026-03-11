# Python CI Security Checks – DAST Doc 

---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 07-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is DAST](#2-what-is-dast)
3. [Why DAST is Required](#3-why-dast-is-required)
4. [DAST Workflow Diagram](#4-dast-workflow-diagram)
5. [DAST Tools](#5-dast-tools)
6. [Tools Comparison](#6-tools-comparison)
7. [Advantages of DAST](#7-advantages-of-dast)
8. [Best Practices](#8-best-practices)
9. [Recommendation and Conclusion](#9-recommendation-and-conclusion)
10. [Contact Information](#10-contact-information)
11. [References](#11-references)

---

# 1. Introduction

This document provides a comprehensive overview of Dynamic Application Security Testing (DAST) implemented as part of Continuous Integration (CI) security checks for Python-based attendance and notification services. It explains the purpose, workflow, tools, comparison, advantages, best practices, and recommendations for implementing DAST in the CI pipeline.

Attendance and notification services are critical backend systems that handle sensitive operational and user-related data. Ensuring these services are secure is essential to prevent vulnerabilities such as unauthorized access, injection attacks, and API exploitation.

DAST enables automated runtime security testing of the application by scanning the running service and identifying vulnerabilities before deployment. Integrating DAST into the CI pipeline ensures secure application deployment, improves system reliability, and strengthens overall application security.

---

# 2. What is DAST?

Dynamic Application Security Testing (DAST) is a security testing method that analyzes a running application to identify vulnerabilities by simulating real-world attack scenarios.

Unlike static testing, DAST tests the application externally without accessing the source code.

### Key Characteristics

| Feature                 | Description                            |
| ----------------------- | -------------------------------------- |
| Runtime Testing         | Tests running application              |
| Black-box Testing       | No source code access required         |
| Vulnerability Detection | Identifies runtime vulnerabilities     |
| Automated Testing       | Can be integrated into CI/CD pipelines |

DAST helps identify vulnerabilities in deployed Python applications such as attendance and notification services.

---

# 3. Why DAST is Required?

| Purpose                          | Description                                | Outcome                         |
| -------------------------------- | ------------------------------------------ | ------------------------------- |
| Identify Runtime Vulnerabilities | Detect vulnerabilities in running services | Improves application security   |
| Secure API Endpoints             | Protect attendance and notification APIs   | Prevent unauthorized access     |
| Prevent Security Risks           | Detect vulnerabilities before deployment   | Ensures secure deployment       |
| Improve CI/CD Security           | Integrate automated security testing       | Enhances pipeline security      |
| Compliance and Governance        | Meet security standards                    | Ensures secure system operation |

DAST ensures Python applications are secure before production deployment.

---

# 4. DAST Workflow Diagram

<img width="704" height="523" alt="image" src="https://github.com/user-attachments/assets/3ebe8ba2-f7ca-4257-b0c4-284968f23a45" />

This workflow ensures automated security validation of Python applications.

---

# 5. DAST Tools

| Tool       | Description                        | Advantages                           | Limitations                |
| ---------- | ---------------------------------- | ------------------------------------ | -------------------------- |
| OWASP ZAP  | Open-source DAST tool              | Free, widely used, CI/CD integration | Requires configuration     |
| Burp Suite | Professional security testing tool | Advanced vulnerability detection     | Paid license required      |
| Nikto      | Web server vulnerability scanner   | Easy to use                          | Limited advanced detection |
| StackHawk  | Modern DAST tool for CI/CD         | Easy CI integration                  | Paid tool                  |

These tools help identify vulnerabilities in Python applications.

---

# 6. Tools Comparison

| Tool       | Open Source | CI/CD Integration | Enterprise Ready | Ease of Use |
| ---------- | ----------- | ----------------- | ---------------- | ----------- |
| OWASP ZAP  | Yes         | Yes               | Yes              | Medium      |
| Burp Suite | No          | Yes               | Yes              | Easy        |
| Nikto      | Yes         | Limited           | Limited          | Easy        |
| StackHawk  | No          | Yes               | Yes              | Easy        |

---

# 7. Advantages of DAST

| Advantage                       | Description                                  |
| ------------------------------- | -------------------------------------------- |
| Detects Runtime Vulnerabilities | Identifies real-world security issues        |
| Improves Application Security   | Prevents exploitation                        |
| No Source Code Required         | Easy implementation                          |
| CI/CD Integration               | Enables automated testing                    |
| Protects APIs                   | Secures attendance and notification services |

DAST strengthens application security.

---

# 8. Best Practices

| Practice                        | Reason                                 |
| ------------------------------- | -------------------------------------- |
| Run DAST in CI pipeline         | Ensures continuous security validation |
| Scan staging environment        | Prevent production vulnerabilities     |
| Fix vulnerabilities immediately | Improves security posture              |
| Use reliable DAST tools         | Ensures accurate results               |
| Integrate with CI/CD            | Enables automation                     |

Following best practices ensures effective DAST implementation.

---

# 9. Recommendation and Conclusion

## Recommended Tool: OWASP ZAP

OWASP ZAP is recommended for implementing DAST for attendance and notification Python services.

### Reasons for Choosing OWASP ZAP

| Reason                           | Explanation                            |
| -------------------------------- | -------------------------------------- |
| Open Source                      | No licensing cost                      |
| CI/CD Integration                | Easy integration with CI pipelines     |
| Enterprise Ready                 | Widely used in enterprise environments |
| Reliable Vulnerability Detection | Detects common web vulnerabilities     |
| Active Community Support         | Regular updates and support            |

### Why Other Tools Not Selected

| Tool       | Limitation                                   |
| ---------- | -------------------------------------------- |
| Burp Suite | Paid tool, licensing required                |
| Nikto      | Limited vulnerability detection capabilities |
| StackHawk  | Paid tool, requires subscription             |

---

## Final Conclusion

Dynamic Application Security Testing (DAST) is essential for ensuring the security of Python attendance and notification services. It enables automated detection of vulnerabilities in running applications and ensures secure deployment through CI pipeline integration.

OWASP ZAP is the recommended tool due to its open-source availability, CI/CD compatibility, enterprise reliability, and effective vulnerability detection capabilities. Implementing OWASP ZAP in the CI pipeline ensures secure, reliable, and compliant application deployment.

---

# 10. Contact Information

| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

# 11. References

| Reference               | Description                                |
| ----------------------- | ------------------------------------------ |
| OWASP ZAP Documentation | [Official OWASP ZAP documentation](https://www.zaproxy.org/docs/)           |
| OWASP Security Guide    | [Web application security guide](https://www.hackerone.com/knowledge-center/owasp-zap-6-key-capabilities-and-quick-tutorial)|

---
