# POC - Unit Testing on Attendance API & Notification Worker
---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 01-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents
- [Objective](#objective)
<details>
<summary><strong>Attendance API - Unit Testing</strong></summary>

- [Step 1 – Navigate to Attendance API](#step-1--navigate-to-attendance-api)
- [Step 2 – Install pytest](#step-2--install-pytest)
- [Step 3 – Verify pytest Version](#step-3--verify-pytest-version)
- [Step 4 – Find Test Files](#step-4--find-test-files)
- [Step 5 – Run pytest](#step-5--run-pytest)
</details>

<details>
<summary><strong>Notification Worker - Unit Testing</strong></summary>

- [Step 6 – Navigate to Notification Worker](#step-6--navigate-to-notification-worker)
- [Step 7 – Find Test Files](#step-7--find-test-files)
</details>

- [Results](#results)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Objective

To demonstrate the usage of `pytest` for unit testing on **Attendance API** and **Notification Worker** (Python microservices) running on an AWS EC2 Ubuntu instance.

---

## Attendance API - Unit Testing

### Step 1 – Navigate to Attendance API

```bash
cd ~/attendance-api
ls
```

<img width="1231" height="114" alt="ss1-attendance-dir" src="https://github.com/user-attachments/assets/b7c9e67a-3946-4d7e-b68f-ec25575bb0ce" />

---

### Step 2 – Install pytest

```bash
pip3 install pytest
pip3 install flask psycopg2-binary redis peewee python-json-logger flask-caching voluptuous
export PYTHONPATH=$PYTHONPATH:/home/ubuntu/attendance-api
```

<img width="1365" height="350" alt="ss2-pytest-install" src="https://github.com/user-attachments/assets/9e5b8c4c-ee54-436f-943a-cd38780f2b04" />

---

### Step 3 – Verify pytest Version

```bash
pytest --version
```

**Expected Output:**
```
pytest 9.0.2
```
<img width="596" height="72" alt="ss3-pytest-version" src="https://github.com/user-attachments/assets/58f8de6a-a384-46ef-8cdf-8d684a73d69a" />

---

### Step 4 – Find Test Files

```bash
find . -name "test_*.py" -o -name "*_test.py"
```

**Output:**
```
./router/tests/test_cache.py
./router/tests/test_attendance.py
./client/tests/test_postgres_conn.py
./client/tests/test_redis_conn.py
./utils/tests/test_log_encoder.py
./utils/tests/test_validator.py
./utils/tests/test_json_encoder.py
./models/tests/test_user_info.py
./models/tests/test_message.py
```

<img width="968" height="217" alt="ss4-test-files" src="https://github.com/user-attachments/assets/a6ed86be-6dfc-4f61-a907-4eee91bccb72" />

---

### Step 5 – Run pytest

> **Note:** `test_postgres_conn.py` and `test_redis_conn.py` require actual database connections which are not available in POC environment — hence ignored.

```bash
pytest --tb=short --ignore=client/tests/test_postgres_conn.py --ignore=client/tests/test_redis_conn.py
```
<img width="1354" height="520" alt="ss5-attendance-pytest-result" src="https://github.com/user-attachments/assets/b4245032-0349-49e9-86c9-a4f2f5816c72" />

---

## Notification Worker - Unit Testing

### Step 6 – Navigate to Notification Worker

```bash
cd ~/notification-worker
```

---

### Step 7 – Find Test Files

```bash
find . -name "test_*.py" -o -name "*_test.py"
```

**Output:** No test files found

> **Note:** Notification Worker has no existing unit test files — this is a gap that should be addressed in future sprints.

---

## Results

### Attendance API:

| Test File | Tests | Status |
|-----------|-------|--------|
| `models/tests/test_message.py` | 2 | Passed |
| `models/tests/test_user_info.py` | 1 |  Passed |
| `router/tests/test_cache.py` | 3 |  Passed |
| `utils/tests/test_json_encoder.py` | 4 |  Passed |
| `utils/tests/test_log_encoder.py` | 1 | Passed |
| `utils/tests/test_validator.py` | 4 | Passed |
| **Total** | **15** | ** All Passed** |

### Notification Worker:

| Finding | Details |
|---------|---------|
| **Test Files** | None found |
| **Status** | No tests to run |
| **Recommendation** | Write unit tests in future sprints |

---

## Conclusion

`pytest` successfully discovered and executed **15 unit tests** in the **Attendance API** — all passed. The **Notification Worker** had no existing test files. This POC demonstrates that `pytest` is easy to set up and run for Python microservices.

---

## Contact Information
| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References
| Description | Link |
|------------|------|
| pytest Official Docs | https://docs.pytest.org/ |
| Attendance API Repository | https://github.com/OT-MICROSERVICES/attendance-api |
| Notification Worker Repository | https://github.com/OT-MICROSERVICES/notification-worker |
