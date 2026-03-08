# POC - Credential Scanning using Gitleaks

---

| Author | Created On | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|----------------|----------------|------------|------------|------------|
| Abhinav Tiwari | 08-03-2026 | v1.0 | Abhinav Tiwari | 08-03-2026 | Nikita Joshi | Prashant | Piyush Upadhayay |

---

## Table of Contents

- [Objective](#objective)
<details>
<summary><strong>Setup & Scan Steps</strong></summary>

- [Step 1 – Install Gitleaks](#step-1--install-gitleaks)
- [Step 2 – Navigate to Attendance API](#step-2--navigate-to-attendance-api)
- [Step 3 – Run Gitleaks Scan](#step-3--run-gitleaks-scan)
</details>

- [Results](#results)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Objective

To demonstrate the usage of **Gitleaks** for credential scanning on the **Attendance API** repository — scanning all commits and source code for accidentally committed secrets, passwords, API keys, or tokens.

---

## Setup & Scan Steps

### Step 1 – Install Gitleaks

```bash
wget https://github.com/gitleaks/gitleaks/releases/download/v8.18.2/gitleaks_8.18.2_linux_x64.tar.gz
tar -xzf gitleaks_8.18.2_linux_x64.tar.gz
sudo mv gitleaks /usr/local/bin/
gitleaks version
```
<img width="1339" height="688" alt="ss1-gitleaks-install" src="https://github.com/user-attachments/assets/820b4a3f-23b0-47e7-bb65-276a5f47d49e" />

---

### Step 2 – Navigate to Attendance API

```bash
cd ~/attendance-api
ls
```
<img width="1192" height="80" alt="ss2-gitleaks-scan" src="https://github.com/user-attachments/assets/b069848a-48c8-4c87-a702-6d41da942605" />

---

### Step 3 – Run Gitleaks Scan

```bash
gitleaks detect --source . --verbose
```

**Output:**
```
    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

8:00PM INF 14 commits scanned.
8:00PM INF scan completed in 161ms
8:00PM INF no leaks found
```
<img width="1076" height="216" alt="ss3-gitleaks-scan" src="https://github.com/user-attachments/assets/11923fbf-1e7b-4143-8df1-d3d91805a628" />

---

## Results

| Property | Value |
|----------|-------|
| **Repository** | attendance-api |
| **Commits Scanned** | 14 |
| **Scan Time** | 161ms |
| **Credentials Found** | 0 |
| **Status** | Clean — No leaks found |

---

## Conclusion

Gitleaks successfully scanned the **Attendance API** repository — all **14 commits were analyzed in just 161ms** and **no credentials were found**. The repository is clean with no hardcoded secrets, passwords, or API keys. This POC demonstrates that Gitleaks is extremely fast and easy to use for credential scanning in any project.

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
| Attendance API Repository | https://github.com/OT-MICROSERVICES/attendance-api |
