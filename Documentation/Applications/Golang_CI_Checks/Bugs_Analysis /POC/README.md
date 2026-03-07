# POC - GoLang CI Checks | Bugs analysis
---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 05-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents
- [Objective](#objective)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Step 1: Update System](#step-1-update-system)
  - [Step 2: Install Go](#step-2-install-go)
  - [Step 3: Verify Go Installation](#step-3-verify-go-installation)
  - [Step 4: Clone Repository](#step-4-clone-repository)
  - [Step 5: Install golangci-lint](#step-5-install-golangci-lint)
  - [Step 6: Run golangci-lint](#step-6-run-golangci-lint)
- [Results](#results)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Objective

To demonstrate the usage of `golangci-lint` for bug detection on the **Employee API** (Golang microservice) running on an AWS EC2 Ubuntu instance.

---

## Steps

---

### Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

<img width="1113" height="576" alt="SS #1 - Update Complete" src="https://github.com/user-attachments/assets/c68c3b80-1630-467c-8044-1c8cb4fc6e93" />

---

### Step 2: Install Go

```bash
wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.profile
source ~/.profile
```
<img width="1117" height="349" alt="SS #2 - Go Installation" src="https://github.com/user-attachments/assets/d4cd3c79-deea-43c6-8277-99b88f357c03" />

---

### Step 3: Verify Go Installation

```bash
go version
```

**Expected Output:**
```
go version go1.22.0 linux/amd64
```

<img width="1110" height="120" alt="SS #3 - Go Version Verify" src="https://github.com/user-attachments/assets/abb233e7-c9db-4a74-8055-f85c47bc57e0" />

---

### Step 4: Clone Repository

```bash
git clone https://github.com/OT-MICROSERVICES/employee-api.git
cd employee-api
```

<img width="1104" height="160" alt="ss5-repo-clone" src="https://github.com/user-attachments/assets/9e9b5c29-8121-448f-a723-8a838aeebded" />

---

### Step 5: Install golangci-lint

```bash
curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.56.2
export PATH=$PATH:$(go env GOPATH)/bin
golangci-lint --version
```

**Expected Output:**
```
golangci-lint has version 1.56.2 built with go1.22.0 from 58a724a0 on 2024-02-15T18:01:51Z
```

<img width="1105" height="175" alt="ss4-golangci-lint-version" src="https://github.com/user-attachments/assets/dff04748-728c-45a1-a64c-72f9304ea8b5" />

---

### Step 6: Run golangci-lint

```bash
golangci-lint run ./... --timeout 5m
```

<img width="1366" height="661" alt="ss6-golangci-lint-output" src="https://github.com/user-attachments/assets/87fefb34-b924-4718-aa43-8db93df3cb10" />

---

## Results

**Total Issues Found: 11**

| File | Line | Issue Type | Description |
|------|------|------------|-------------|
| `config/viper_test.go` | 36 | errcheck | Error return value of `viperReadInConfig()` not checked |
| `client/scylladb_test.go` | 40 | errcheck | Error return value of `gocqlCreateSessionMock()` not checked |
| `api/api.go` | 71 | errcheck | Error return value of `json.Unmarshal` not checked |
| `api/api.go` | 95 | errcheck | Error return value of `json.Unmarshal` not checked |
| `api/api.go` | 128 | errcheck | Error return value of `json.Unmarshal` not checked |
| `api/health_test.go` | 82 | errcheck | Error return value of `.Err` not checked |
| `main.go` | 47 | errcheck | Error return value of `router.Run` not checked |
| `api/api.go` | 73 | gosimple | Redundant `return` statement |
| `api/api.go` | 130 | gosimple | Redundant `return` statement |
| `config/viper.go` | 19 | ineffassign | Ineffectual assignment to `err` |
| `api/api.go` | 235 | staticcheck | Surrounding loop is unconditionally terminated |

### Summary:

| Issue Type | Count | Severity |
|------------|-------|----------|
| errcheck | 7 | Medium |
| gosimple | 2 | Low |
| ineffassign | 1 | Low |
| staticcheck | 1 | High |
| **Total** | **11** | - |

---

## Conclusion

`golangci-lint` successfully detected **11 issues** in the Employee API codebase without executing the code. The tool was easy to install, configure, and run — making it the ideal choice for Bugs Analysis in Go-based microservices.

---

## Contact Information
| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References
| Description | Link |
|------------|------|
| golangci-lint Official Docs | https://golangci-lint.run/ |
| golangci-lint GitHub | https://github.com/golangci/golangci-lint |
| Employee API Repository | https://github.com/OT-MICROSERVICES/employee-api |
