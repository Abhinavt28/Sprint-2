# VCS (Version Control System) Implementation – Using GitHub

---

| Author | Created On | Version | Last Updated By | Last Edited On | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|----------------|----------------|------------|------------|------------|
| Abhinav Tiwari | 02-03-2026 | v1.0 | Abhinav Tiwari | 02-03-2026 | Nikita Joshi | Prashant | Piyush Upadhayay |

---

## Table of Contents

1. [What is VCS](#1-what-is-vcs)
2. [Why VCS](#2-why-vcs)
3. [Architecture Overview (Git + GitHub)](#3-architecture-overview-git--github)
4. [Step-by-Step Setup VCS (GitHub)](#4-step-by-step-setup-vcs-github)
   - [Step 1 – Install Git](#step-1--install-git)
   - [Step 2 – Configure Git](#step-2--configure-git)
   - [Step 3 – Create Repository on GitHub](#step-3--create-repository-on-github)
   - [Step 4 – Clone Repository](#step-4--clone-repository)
5. [SaaS vs On-Prem VCS Comparison](#5-saas-vs-on-prem-vcs-comparison)
6. [Conclusion](#7-conclusion)
7. [Contact Information](#8-contact-information)
8. [References](#9-references)

---

## 1. What is VCS?

VCS (Version Control System) is a system that tracks changes in source code over time.

We are using:
- **Git** → Version control tool
- **GitHub** → Remote repository hosting platform

---

## 2. Why VCS?

| Reason | Description |
|--------|-------------|
| **Collaboration** | Multiple developers work on same codebase simultaneously |
| **History Tracking** | Complete audit trail of all code changes |
| **Rollback** | Revert to any previous version if something breaks |
| **Branching** | Develop features in isolation without affecting main code |
| **CI/CD Integration** | Trigger automated pipelines on code push |
| **Backup** | Code is safely stored in remote repository |

---

## 3. Architecture Overview (Git + GitHub)

```
Developer (Local Machine)
        │
        │  git add / git commit
        ▼
   Local Git Repo
        │
        │  git push
        ▼
   GitHub (Remote)
        │
        ├── main branch
        ├── develop branch
        └── feature branches
```

---

## 4. Step-by-Step Setup VCS (GitHub)

### Step 1 – Install Git

Refresh package list:
```bash
sudo apt update
```

Install Git:
```bash
sudo apt install git -y
```

Verify installation:
```bash
git --version
```

<img width="998" height="390" alt="ss1-git-install" src="https://github.com/user-attachments/assets/0530bb5e-a99c-4802-bdb5-92c8d436e512" />

---

### Step 2 – Configure Git

```bash
git config --global user.name "Abhinav Tiwari"
git config --global user.email "abhinav.tiwari.snaatak@mygurukulam.co"
```

Verify:
```bash
git config --list
```
<img width="787" height="126" alt="ss2-git-config" src="https://github.com/user-attachments/assets/e40e6ae9-c317-41c2-8218-12cf4ec07e64" />

---

### Step 3 – Create Repository on GitHub

- Login to **GitHub.com**
- Click **"New Repository"**
- Fill in details:

| Field | Value |
|-------|-------|
| **Repository Name** | `vcs-setup-poc` |
| **Visibility** | Public |
| **Initialize with README** | Yes |

- Click **"Create Repository"**

<img width="1366" height="689" alt="ss3-github-repo-create" src="https://github.com/user-attachments/assets/6924ef94-18f7-4421-bb7f-ff2cf95939ff" />

---

### Step 4 – Clone Repository

```bash
cd ~
git clone https://github.com/Abhinavt14/vcs-setup-poc.git
cd vcs-setup-poc
ls
```

**Output:**
```
README.md
```

<img width="787" height="228" alt="ss4-repo-clone" src="https://github.com/user-attachments/assets/808d2955-9534-4d46-bbd8-1d99a69a25da" />

This connects local system to remote GitHub repository.

---

## 5. SaaS vs On-Prem VCS Comparison

| Feature | SaaS (GitHub) | On-Prem (GitLab Self-Hosted) |
|---------|--------------|------------------------------|
| **Setup Time** | Fast | Slow |
| **Maintenance** | Vendor Managed | Self Managed |
| **Infra Cost** | Subscription | Server + Ops Cost |
| **Backup** | Automatic | Manual Setup |
| **Security Control** | Shared | Full Internal Control |
| **Free Tier** | Yes | No |

---

## 6. Conclusion

GitHub (SaaS) is the recommended VCS for this project because it requires no infrastructure setup, provides built-in CI/CD via GitHub Actions, and is the industry standard for modern DevOps workflows. Compared to On-Premises solutions, GitHub offers faster setup, automatic backups, and better collaboration features — making it the most suitable choice for all future sprints.

---

## 7. Contact Information

| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## 8. References

| Description | Link |
|------------|------|
| GitHub Official Docs | https://docs.github.com/ |
| Git Official Docs | https://git-scm.com/doc |
| GitHub Actions | https://docs.github.com/en/actions |
