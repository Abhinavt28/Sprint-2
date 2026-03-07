# Python CI Checks - Dependency Scanning
---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 07-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents
- [Introduction](#introduction)
- [What is Dependency Scanning](#what-is-dependency-scanning)
- [Why Dependency Scanning](#why-dependency-scanning)
- [Workflow Diagram](#workflow-diagram)
- [Different Tools](#different-tools)
- [Comparison of Tools](#comparison-of-tools)
- [Advantages](#advantages)
- [POC](#poc)
- [Best Practices](#best-practices)
- [Recommendation & Conclusion](#recommendation--conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Introduction

In modern software development, applications rely heavily on third-party libraries and packages. These dependencies can contain known security vulnerabilities that can be exploited by attackers. **Dependency Scanning** is the process of automatically identifying and reporting such vulnerabilities in project dependencies before they reach production.

For Python-based microservices like the **Attendance API** and **Notification Worker**, dependency scanning ensures that all third-party packages are free from known vulnerabilities. This document covers dependency scanning tools available for Python, with a focus on `pip-audit` as the primary tool.

---

## What is Dependency Scanning

Dependency Scanning is the process of **analyzing third-party packages and libraries** used in a project to identify known security vulnerabilities. It checks dependencies against public vulnerability databases such as **PyPI Advisory Database** and **OSV (Open Source Vulnerabilities)**.

### What it covers:

| Category | Description |
|----------|-------------|
| **CVE Detection** | Finds Common Vulnerabilities and Exposures in packages |
| **Version Analysis** | Checks if installed version has known vulnerabilities |
| **Fix Versions** | Suggests versions that fix the vulnerability |
| **Transitive Dependencies** | Checks indirect dependencies too |

### Types of Vulnerabilities Found:

| Type | Description | Example |
|------|-------------|---------|
| **CVE** | Common Vulnerability and Exposure | CVE-2023-0286 in cryptography |
| **PYSEC** | Python-specific security advisory | PYSEC-2022-202 in pyjwt |
| **GHSA** | GitHub Security Advisory | GHSA-5cpq-8wj7-hf2v in cryptography |

---

## Why Dependency Scanning

| Reason | Description |
|--------|-------------|
| **Security** | Identify vulnerable packages before production deployment |
| **Early Detection** | Find issues at development time — not after breach |
| **Compliance** | Meet security standards and audit requirements |
| **CI/CD Integration** | Automate security checks in every build |
| **Cost Saving** | Fixing vulnerabilities early is cheaper than post-breach |
| **Supply Chain Security** | Protect against third-party package attacks |

---

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                 DEPENDENCY SCANNING WORKFLOW                     │
└─────────────────────────────────────────────────────────────────┘

  ┌──────────┐     ┌──────────┐     ┌───────────────┐
  │ Developer│────▶│  Commit  │────▶│   CI/CD       │
  │  Writes  │     │  Code    │     │   Pipeline    │
  │   Code   │     │  to Git  │     │   Triggered   │
  └──────────┘     └──────────┘     └───────┬───────┘
                                            │
                                            ▼
                                   ┌────────────────┐
                                   │   pip-audit    │
                                   │   Scans        │
                                   │  Dependencies  │
                                   └───────┬────────┘
                                           │
                                           ▼
                                   ┌────────────────┐
                                   │  Checks CVE    │
                                   │  Database &    │
                                   │  OSV Database  │
                                   └───────┬────────┘
                                           │
                              ┌────────────┴────────────┐
                              │                         │
                              ▼                         ▼
                     ┌────────────────┐       ┌────────────────┐
                     │ Vulnerabilities│       │  No Issues     │
                     │    Found       │       │  Found         │
                     └───────┬────────┘       └───────┬────────┘
                             │                        │
                             ▼                        ▼
                     ┌────────────────┐       ┌────────────────┐
                     │  FAIL - Fix    │       │  PASS - Code   │
                     │  Dependencies  │       │  Proceeds      │
                     └───────┬────────┘       └────────────────┘
                             │
                             ▼
                     ┌────────────────┐
                     │   Developer    │
                     │ Updates Pkgs   │
                     │ & Recommits    │
                     └────────────────┘
```

---

## Different Tools

| Tool | Type | Key Feature |
|------|------|-------------|
| **pip-audit** | Dependency vulnerability scanner | Official PyPA tool, checks CVE & OSV database |
| **Safety** | Dependency checker | Checks against Safety DB, easy to use |
| **Snyk** | Security platform | Cloud-based, detailed reports, CI/CD integration |
| **Bandit** | Security linter | Scans Python code for security issues |

---

## Comparison of Tools

| Feature | pip-audit | Safety | Snyk | Bandit |
|---------|-----------|--------|------|--------|
| **Official PyPA Tool** | Yes | No | No | No |
| **Free** | Yes | Limited | Limited | Yes |
| **CVE Database** | Yes | Yes | Yes | No |
| **CI/CD Ready** | Yes | Yes | Yes | Yes |
| **No Login Required** | Yes | No | No | Yes |
| **Fix Suggestions** | Yes | Yes | Yes | No |
| **Self Hosted** | Yes | No | No | Yes |
| **OSV Database** | Yes | No | No | No |

---

## Advantages

### Advantages of Dependency Scanning:

| Advantage | Description |
|-----------|-------------|
| **Proactive Security** | Find vulnerabilities before attackers do |
| **Automated** | No manual checking of each package needed |
| **Detailed Reports** | CVE IDs, affected versions, fix versions all reported |
| **CI/CD Integration** | Block deployments with vulnerable dependencies |
| **Supply Chain Protection** | Secure the entire dependency chain |

### Advantages of pip-audit:

| Advantage | Description |
|-----------|-------------|
| **Official Tool** | Maintained by PyPA — most trusted |
| **No Login Required** | Unlike Snyk or Safety — works out of the box |
| **OSV + PyPI DB** | Checks two databases for comprehensive coverage |
| **Easy to Use** | Single command — `pip-audit` |
| **CI/CD Friendly** | Exit code 1 on vulnerabilities — easy pipeline integration |
| **Free Forever** | No paid plans or rate limits |

---

## POC

For detailed step-by-step Proof of Concept with screenshots, refer to the POC README below:

📎 **[POC - Dependency Scanning on Attendance & Notification](https://github.com/Abhinavt28/Sprint-2/blob/SCRUM-163-abhinav-POC-Dependency-Scanning/Documentation/Applications/Python_CI_Checks/Dependency_Scanning/POC/README.md)**

---

## Best Practices

| # | Practice | Description |
|---|----------|-------------|
| 1 | **Integrate in CI/CD** | Run pip-audit on every commit/PR automatically |
| 2 | **Fix Critical First** | Address high severity CVEs before low severity |
| 3 | **Regular Scans** | Run scans frequently — new CVEs are added daily |
| 4 | **Update Dependencies** | Keep packages updated to fix versions |

---

## Recommendation & Conclusion

### Tool Recommendation: `pip-audit` 

After evaluating all available dependency scanning tools for Python, **`pip-audit`** is the recommended tool for the following reasons:

| Factor | Reason |
|--------|--------|
| **Official PyPA Tool** | Most trusted — maintained by Python Packaging Authority |
| **No Login Required** | Works out of the box unlike Snyk or Safety |
| **Comprehensive** | Checks both OSV and PyPI Advisory databases |
| **Future Sprints** | Can be reused in Sprint 3-6 for pipeline integration |

### Conclusion

Dependency scanning is a **non-negotiable security practice** in modern DevOps. For the **Attendance API** and **Notification Worker** (Python microservices), running `pip-audit` revealed **51 vulnerabilities** in 14 packages including critical issues in `cryptography`, `urllib3`, `twisted`, and `jinja2` — all without executing the code. For all future sprints and projects, `pip-audit` will be the primary dependency scanning tool because it is free, official, requires no login, and integrates seamlessly into CI/CD pipelines.

---

## Contact Information
| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References
| Description | Link |
|------------|------|
| pip-audit Official Docs | https://pypi.org/project/pip-audit/ |
| pip-audit GitHub | https://github.com/pypa/pip-audit |
| OSV Database | https://osv.dev/ |
| PyPI Advisory Database | https://github.com/pypa/advisory-database |
| Attendance API Repository | https://github.com/OT-MICROSERVICES/attendance-api |
| Notification Worker Repository | https://github.com/OT-MICROSERVICES/notification-worker |
