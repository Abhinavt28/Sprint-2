# Generic CI Operation - Credential Scanning

---

| Author | Created On | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|----------------|----------------|------------|------------|------------|
| Abhinav Tiwari | 06-03-2026 | v1.0 | Abhinav Tiwari | 06-03-2026 | Nikita Joshi | Prashant | Piyush Upadhayay |

---

## Table of Contents

- [Introduction](#introduction)
- [What is Credential Scanning?](#what-is-credential-scanning)
- [Why Credential Scanning?](#why-credential-scanning)
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

In modern software development, developers often accidentally commit sensitive information such as passwords, API keys, tokens, and other credentials into source code repositories. Once pushed to a remote repository, these credentials can be exploited by attackers to gain unauthorized access to systems and services.

**Credential Scanning** is the practice of automatically scanning source code and git history to detect and prevent such accidental exposure of sensitive information. This document covers credential scanning tools, best practices, and a practical demonstration using **Gitleaks** on the OT-Microservices project.

---

## What is Credential Scanning?

Credential Scanning is the process of **automatically scanning source code, configuration files, and git commit history** to detect hardcoded secrets, passwords, API keys, tokens, and other sensitive credentials.

### What it detects?

| Credential Type | Example |
|----------------|---------|
| **API Keys** | AWS Access Keys, GitHub Tokens |
| **Passwords** | Hardcoded DB passwords |
| **Private Keys** | RSA/SSH private keys |
| **Tokens** | OAuth tokens, JWT secrets |
| **Connection Strings** | Database connection URLs with credentials |
| **Certificates** | Hardcoded SSL certificates |

### Types of Scanning:

| Type | Description |
|------|-------------|
| **Pre-commit** | Scan before code is committed locally |
| **CI/CD Pipeline** | Scan on every push/PR automatically |
| **Historical Scan** | Scan entire git history for old secrets |

---

## Why Credential Scanning?

| Reason | Description |
|--------|-------------|
| **Prevent Data Breach** | Exposed credentials can lead to unauthorized access |
| **Compliance** | Meet security standards like SOC2, PCI-DSS |
| **Early Detection** | Catch secrets before they reach remote repos |
| **CI/CD Integration** | Automate scanning in every build pipeline |
| **Cost Saving** | Prevent expensive security incidents |

---

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                 CREDENTIAL SCANNING WORKFLOW                     │
└─────────────────────────────────────────────────────────────────┘

  ┌──────────┐     ┌──────────┐     ┌───────────────┐
  │ Developer│────▶│  Commit  │────▶│   CI/CD       │
  │  Writes  │     │  Code    │     │   Pipeline    │
  │   Code   │     │  to Git  │     │   Triggered   │
  └──────────┘     └──────────┘     └───────┬───────┘
                                            │
                                            ▼
                                   ┌────────────────┐
                                   │   Gitleaks     │
                                   │   Scans Code   │
                                   │   & Git History│
                                   └───────┬────────┘
                                           │
                              ┌────────────┴────────────┐
                              │                         │
                              ▼                         ▼
                     ┌────────────────┐       ┌────────────────┐
                     │ Credentials    │       │  No Secrets    │
                     │    Found       │       │  Found         │
                     └───────┬────────┘       └───────┬────────┘
                             │                        │
                             ▼                        ▼
                     ┌────────────────┐       ┌────────────────┐
                     │  FAIL - Alert  │       │  PASS - Code   │
                     │  Developer     │       │  Proceeds      │
                     └───────┬────────┘       └────────────────┘
                             │
                             ▼
                     ┌────────────────┐
                     │   Developer    │
                     │ Removes Secret │
                     │ & Recommits    │
                     └────────────────┘
```

---

## Different Tools

| Tool | Type | Key Feature |
|------|------|-------------|
| **Gitleaks** | Secret scanner | Fast, lightweight, 100+ built-in rules, CI/CD ready |
| **Trufflehog** | Secret scanner | Deep git history scan, entropy-based detection |
| **git-secrets** | Pre-commit hook | AWS focused, prevents commits with secrets |
| **Detect-secrets** | Secret scanner | Baseline approach, tracks known secrets |

---

## Comparison of Tools

| Feature | Gitleaks | Trufflehog | git-secrets | Detect-secrets |
|---------|----------|------------|-------------|----------------|
| **Easy Setup** | Yes | No | No | No |
| **Git History Scan** | Yes | Yes | No | No |
| **Speed** | Very Fast | Slow | Fast | Medium |
| **Free** | Yes | Yes | Yes | Yes |
| **Active Maintenance** | Yes | Yes | Limited | Yes |

---

## Advantages

### Advantages of Credential Scanning:

| Advantage | Description |
|-----------|-------------|
| **Proactive Security** | Find secrets before attackers do |
| **Automated** | No manual code review needed for secrets |
| **Git History** | Scans all past commits — not just current code |
| **Fast Feedback** | Developers notified immediately |

---

## POC

For detailed step-by-step Proof of Concept with screenshots, refer to the POC README below:

> 📎 **[POC - Credential Scanning using Gitleaks](./POC-cred-scanning.md)**

---

## Best Practices

| # | Practice | Description |
|---|----------|-------------|
| 1 | **Never hardcode secrets** | Always use environment variables or secret managers |
| 2 | **Integrate in CI/CD** | Run Gitleaks on every commit/PR automatically |
| 3 | **Scan git history** | New repos should scan entire git history |
| 4 | **Use .gitignore** | Never commit .env files or config files with secrets |

---

## Conclusion

Credential Scanning is a **critical security practice**. Accidentally committed secrets can lead to data breaches, unauthorized access, and costly security incidents. Using **Gitleaks**, the **Attendance API** repository was scanned — **14 commits were analyzed in just 161ms and no credentials were found**, confirming the repo is clean.

---

## Contact Information

| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References

| Description | Link |
|------------|------|
| Gitleaks Official GitHub | https://github.com/gitleaks/gitleaks |
| Gitleaks Documentation | https://gitleaks.io/ |
| git-secrets GitHub | https://github.com/awslabs/git-secrets |
