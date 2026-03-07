# POC - Static Code Analysis
---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 06-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents
- [Objective](#objective)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Step 1: Launch AWS EC2 Instance](#step-1-launch-aws-ec2-instance)
  - [Step 2: Update System](#step-2-update-system)
  - [Step 3: Install Java](#step-3-install-java)
  - [Step 4: Verify Java Installation](#step-4-verify-java-installation)
  - [Step 5: Download SonarQube](#step-5-download-sonarqube)
  - [Step 6: Unzip SonarQube](#step-6-unzip-sonarqube)
  - [Step 7: Setup SonarQube Permissions](#step-7-setup-sonarqube-permissions)
  - [Step 8: Start SonarQube](#step-8-start-sonarqube)
  - [Step 9: Access SonarQube UI](#step-9-access-sonarqube-ui)
  - [Step 10: Login to SonarQube](#step-10-login-to-sonarqube)
  - [Step 11: Create Project](#step-11-create-project)
  - [Step 12: Generate Token](#step-12-generate-token)
  - [Step 13: Select Analysis Method](#step-13-select-analysis-method)
  - [Step 14: Get Scanner Command](#step-14-get-scanner-command)
  - [Step 15: Install Sonar Scanner](#step-15-install-sonar-scanner)
  - [Step 16: Verify Scanner Version](#step-16-verify-scanner-version)
  - [Step 17: Clone Repository](#step-17-clone-repository)
  - [Step 18: Run Sonar Scanner](#step-18-run-sonar-scanner)
  - [Step 19: View Results on Dashboard](#step-19-view-results-on-dashboard)
  - [Step 20: View Issues](#step-20-view-issues)
  - [Step 21: View Security Hotspots](#step-21-view-security-hotspots)
- [Results](#results)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Objective

To demonstrate the usage of **SonarQube** for static code analysis on the **Employee API** (Golang microservice) running on an AWS EC2 Ubuntu instance.

---

## Steps

---

### Step 1: Launch AWS EC2 Instance

Launch a new EC2 instance with the following Security Group settings — make sure **Port 9000** is open for SonarQube UI access.

---

### Step 2: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

<img width="1113" height="588" alt="ss2-update" src="https://github.com/user-attachments/assets/a26d21fb-54c8-4ef7-aa44-93102a2221b4" />

---

### Step 3: Install Java

SonarQube requires Java 17 to run.

```bash
sudo apt install openjdk-17-jdk -y
```
<img width="773" height="138" alt="ss3-java-install" src="https://github.com/user-attachments/assets/c7f11d27-b984-4c65-ab94-78b3e28d7287" />

---

### Step 4: Verify Java Installation

```bash
java -version
```

**Expected Output:**
```
openjdk version "17.x.x"
```
<img width="831" height="101" alt="ss4-java-version" src="https://github.com/user-attachments/assets/be4cb1cf-ab24-4b4e-ab19-df28cfce44d1" />

---

### Step 5: Download SonarQube

```bash
cd /opt
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip
```

<img width="1109" height="272" alt="ss5-sonarqube-download" src="https://github.com/user-attachments/assets/9168dea4-e051-4653-bb2c-f115bbf6f917" />

---

### Step 6: Unzip SonarQube

```bash
sudo apt install unzip -y
sudo unzip sonarqube-9.9.0.65466.zip
```

<img width="1366" height="715" alt="ss6-sonarqube-unzip" src="https://github.com/user-attachments/assets/a8d7d897-5cad-40bc-a660-e674d19c33ef" />

---

### Step 7: Setup SonarQube Permissions

```bash
sudo mv sonarqube-9.9.0.65466 sonarqube
sudo chmod -R 755 sonarqube
sudo useradd -M -d /opt/sonarqube -r -s /bin/bash sonarqube
sudo chown -R sonarqube:sonarqube /opt/sonarqube
```

<img width="1366" height="735" alt="ss7-sonarqube-setup" src="https://github.com/user-attachments/assets/a14819f7-b6f3-411e-b755-b91e6ec3b69a" />

---

### Step 8: Start SonarQube

```bash
sudo -u sonarqube /opt/sonarqube/bin/linux-x86-64/sonar.sh start
sudo -u sonarqube /opt/sonarqube/bin/linux-x86-64/sonar.sh status
```

**Expected Output:**
```
SonarQube is running (XXXX)
```

<img width="1366" height="160" alt="ss8-sonarqube-start" src="https://github.com/user-attachments/assets/c7e6c7ce-f0ba-4464-b929-a0f9ef252dba" />
<img width="1358" height="91" alt="ss9-sonarqube-status" src="https://github.com/user-attachments/assets/6b71f8de-a0ad-4939-8913-147bae66f06f" />

---

### Step 9: Access SonarQube UI

Open browser and navigate to:

```
http://<YOUR-PUBLIC-IP>:9000
```

<img width="1366" height="731" alt="ss10-sonarqube-login" src="https://github.com/user-attachments/assets/372f990b-d31c-4281-a962-d02923ca7712" />

---

### Step 10: Login to SonarQube

Use default credentials to login:

| Field | Value |
|-------|-------|
| **Username** | `admin` |
| **Password** | `admin` |

<img width="1366" height="734" alt="ss11-sonarqube-dashboard" src="https://github.com/user-attachments/assets/130a1ea0-3c38-4752-8b33-016eefa922c2" />

---

### Step 11: Create Project

Click **"Manually"** to create a new project and fill in the details:

| Field | Value |
|-------|-------|
| **Project Display Name** | `employee-api` |
| **Project Key** | `employee-api` |
| **Main Branch** | `main` |

<img width="1366" height="731" alt="ss12-sonarqube-project-create" src="https://github.com/user-attachments/assets/c77e1230-c6f2-4cb8-8cac-02ed9c7bcb0a" />

---

### Step 12: Generate Token

Generate a project token for authentication:

| Field | Value |
|-------|-------|
| **Token Name** | `employee-api-token` |
| **Expires In** | 30 days |

<img width="1366" height="728" alt="ss13-sonarqube-token" src="https://github.com/user-attachments/assets/e6e6716b-867a-49ed-b7b8-679f47e97a0a" />

---

### Step 13: Select Analysis Method

Select **"Other (for JS, TS, Go, Python, PHP, ...)"** as the build type and **"Linux"** as the OS.

<img width="1366" height="732" alt="ss14-sonarqube-analyze" src="https://github.com/user-attachments/assets/e5dc690c-7454-4616-ae17-f9c2414713d4" />

---

### Step 14: Get Scanner Command

SonarQube provides the scanner command — copy it for use in next steps.

<img width="1366" height="732" alt="ss15-sonarqube-scanner-command" src="https://github.com/user-attachments/assets/1616362c-26f2-44ca-afa9-003df1176a0b" />

---

### Step 15: Install Sonar Scanner

```bash
cd /opt
sudo wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
sudo unzip sonar-scanner-cli-5.0.1.3006-linux.zip
sudo mv sonar-scanner-5.0.1.3006-linux sonar-scanner
export PATH=$PATH:/opt/sonar-scanner/bin
```

<img width="1366" height="735" alt="ss16-scanner-install" src="https://github.com/user-attachments/assets/d2382832-45f2-4bf6-b7fd-52a9ef721b10" />

---

### Step 16: Verify Scanner Version

```bash
sonar-scanner --version
```

**Expected Output:**
```
INFO: SonarScanner 5.0.1.3006
INFO: Java 17.0.7 Eclipse Adoptium (64-bit)
```

<img width="1366" height="729" alt="ss17-scanner-version" src="https://github.com/user-attachments/assets/1da0f6c4-a6fe-4441-98df-fa62fc5e06eb" />

---

### Step 17: Clone Repository

```bash
cd /home/ubuntu
git clone https://github.com/OT-MICROSERVICES/employee-api.git
cd employee-api
```

<img width="1366" height="273" alt="ss18-repo-clone" src="https://github.com/user-attachments/assets/dcfcd4fd-ae69-4ece-a059-f674b2e61c6e" />

---

### Step 18: Run Sonar Scanner

```bash
sonar-scanner \
  -Dsonar.projectKey=employee-api \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://<YOUR-PUBLIC-IP>:9000 \
  -Dsonar.login=<YOUR-TOKEN>
```

**Expected Output:**
```
INFO: EXECUTION SUCCESS
INFO: Analysis total time: 10.825s
```
<img width="1366" height="733" alt="ss19-sonarqube-scan-success" src="https://github.com/user-attachments/assets/cbdf4aed-32c7-4265-a84d-beca80a65097" />

---

### Step 19: View Results on Dashboard

Navigate to SonarQube dashboard to view the analysis results:

```
http://<YOUR-PUBLIC-IP>:9000/dashboard?id=employee-api
```

<img width="1366" height="734" alt="ss20-sonarqube-overview" src="https://github.com/user-attachments/assets/c1509af0-8bb3-4ff7-8941-7680a28a035d" />

---

### Step 20: View Issues

Click on **"Issues"** tab to see all detected issues in detail.

<img width="1366" height="734" alt="ss21-sonarqube-issues" src="https://github.com/user-attachments/assets/ff3fa55a-794a-4f79-aa45-b46e4ff4eef9" />

---

### Step 21: View Security Hotspots

Click on **"Security Hotspots"** tab to see security related findings.

<img width="1366" height="732" alt="ss22-sonarqube-security" src="https://github.com/user-attachments/assets/63b69d75-cbe1-4c52-af79-0214992ceee6" />

---

### Summary:

| Metric | Value |
|--------|-------|
| **Total Issues** | 11 |
| **Open Issues** | 11 |
| **Security Hotspots** | Reviewed |


---

## Conclusion

SonarQube successfully analyzed the **Employee API** codebase and detected **11 issues** across multiple files. The rich dashboard provides detailed insights into code quality, security, and maintainability — making it the ideal tool for static code analysis in Go-based microservices.

---

## Contact Information
| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References
| Description | Link |
|------------|------|
| SonarQube Official Docs | https://docs.sonarqube.org/ |
| Sonar Scanner Docs | https://docs.sonarqube.org/latest/analyzing-source-code/scanners/sonarscanner/ |
| Employee API Repository | https://github.com/OT-MICROSERVICES/employee-api |
