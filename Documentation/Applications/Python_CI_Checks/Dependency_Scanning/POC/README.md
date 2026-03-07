# POC - Dependency Scanning on Attendance API & Notification Worker
---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 01-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents
- [Objective](#objective)
<details>
<summary><strong>Attendance API - Dependency Scanning</strong></summary>

- [Step 1 – System Update](#step-1--system-update)
- [Step 2 – Install Python & Pip](#step-2--install-python--pip)
- [Step 3 – Verify Python Version](#step-3--verify-python-version)
- [Step 4 – Clone Attendance API](#step-4--clone-attendance-api)
- [Step 5 – Install pip-audit](#step-5--install-pip-audit)
- [Step 6 – Run pip-audit on Attendance API](#step-6--run-pip-audit-on-attendance-api)
</details>

<details>
<summary><strong>Notification Worker - Dependency Scanning</strong></summary>

- [Step 7 – Clone Notification Worker](#step-7--clone-notification-worker)
- [Step 8 – Run pip-audit on Notification Worker](#step-8--run-pip-audit-on-notification-worker)
</details>

- [Results](#results)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Objective

To demonstrate the usage of `pip-audit` for dependency scanning on **Attendance API** and **Notification Worker** (Python microservices) running on an AWS EC2 Ubuntu instance.


---

## Attendance API - Dependency Scanning

### Step 1 – System Update

```bash
sudo apt update && sudo apt upgrade -y
```

<img width="1366" height="695" alt="ss1-system-update" src="https://github.com/user-attachments/assets/8c8f26e4-8181-4b45-b6ce-47c46c29a777" />

---

### Step 2 – Install Python & Pip

```bash
sudo apt install python3 python3-pip -y
```
<img width="1352" height="586" alt="ss2-python-install" src="https://github.com/user-attachments/assets/09c85ba9-911b-4754-a7f2-ba897614f9fc" />



---

### Step 3 – Verify Python Version

```bash
python3 --version
pip3 --version
```

**Expected Output:**
```
Python 3.10.12
pip 22.0.2
```

<img width="851" height="102" alt="ss3-python-version" src="https://github.com/user-attachments/assets/99146e3f-ada5-4402-a859-8528d479dfdb" />

---

### Step 4 – Clone Attendance API

```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api
```

<img width="1068" height="197" alt="ss4-attendance-repo-clone" src="https://github.com/user-attachments/assets/28b91085-37e2-4a83-991c-11d67dd381fb" />

---

### Step 5 – Install pip-audit

```bash
pip3 install pip-audit
export PATH=$PATH:~/.local/bin
pip-audit --version
```

**Expected Output:**
```
pip-audit 2.10.0
```

<img width="1055" height="383" alt="ss5-pip-audit-install" src="https://github.com/user-attachments/assets/6076064e-8fbb-43b7-bf2f-8b8e7e591bf1" />

---

### Step 6 – Run pip-audit on Attendance API

```bash
pip-audit
```
<img width="1265" height="664" alt="ss6-attendance-audit-result" src="https://github.com/user-attachments/assets/807227f7-f9b6-48ec-ab26-b112d1fae39d" />

<img width="1229" height="678" alt="ss7-attendance-audit-skip" src="https://github.com/user-attachments/assets/59ba0223-4bf4-4223-a365-cadbec7200e0" />

---

## Notification Worker - Dependency Scanning

### Step 7 – Clone Notification Worker

```bash
cd ~
git clone https://github.com/OT-MICROSERVICES/notification-worker.git
cd notification-worker
```

<img width="865" height="65" alt="ss8-notification-repo-clone" src="https://github.com/user-attachments/assets/89cd727b-f7b2-4766-98b9-c1988a126e48" />

---

### Step 8 – Run pip-audit on Notification Worker

```bash
pip-audit
```

<img width="1083" height="665" alt="ss9-notification-audit-result" src="https://github.com/user-attachments/assets/9eb015ad-dbca-426e-9e63-0cb923aa6138" />

<img width="1361" height="678" alt="ss10-notification-audit-skip" src="https://github.com/user-attachments/assets/fc689245-bdd4-4984-a338-0c8abb0e2e99" />

---

## Results

### Attendance API:

| Package | Version | Vulnerabilities |
|---------|---------|----------------|
| cryptography | 3.4.8 | 10 |
| urllib3 | 1.26.5 | 8 |
| twisted | 22.1.0 | 6 |
| jinja2 | 3.0.3 | 5 |
| setuptools | 59.6.0 | 5 |
| pip | 22.0.2 | 4 |
| certifi | 2020.6.20 | 3 |
| others | - | 10 |
| **Total** | | **51** |

### Notification Worker:

| Package | Version | Vulnerabilities |
|---------|---------|----------------|
| setuptools | 59.6.0 | 5 |
| twisted | 22.1.0 | 6 |
| urllib3 | 1.26.5 | 8 |
| wheel | 0.37.1 | 1 |
| zipp | 1.0.0 | 1 |
| **Total** | | **Similar findings** |

---

## Conclusion

`pip-audit` successfully detected vulnerabilities in both **Attendance API** and **Notification Worker** Python microservices. The tool was easy to install and run — making it the ideal choice for dependency scanning in Python projects.

---

## Contact Information
| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References
| Description | Link |
|------------|------|
| pip-audit GitHub | https://github.com/pypa/pip-audit |
| Attendance API Repository | https://github.com/OT-MICROSERVICES/attendance-api |
| Notification Worker Repository | https://github.com/OT-MICROSERVICES/notification-worker |
