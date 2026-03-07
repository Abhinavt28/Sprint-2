# Python CI Checks - Unit Testing
---

# Document Information
| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 07-03-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents
- [Introduction](#introduction)
- [What is Unit Testing](#what-is-unit-testing)
- [Why Unit Testing](#why-unit-testing)
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

In modern software development, ensuring that individual components of an application work correctly is critical. **Unit Testing** is the practice of testing individual functions, methods, and modules in isolation to verify that they produce the expected output for a given input.

For Python-based microservices like the **Attendance API** and **Notification Worker**, unit testing ensures that each component works correctly before integration. This document covers unit testing tools available for Python, with a focus on `pytest` as the primary tool.

---

## What is Unit Testing

Unit Testing is the process of **testing individual units of code in isolation** to verify that each unit performs as expected. A unit is the smallest testable part of an application — typically a function or method.

### What it covers:

| Category | Description |
|----------|-------------|
| **Function Testing** | Verify individual functions return expected output |
| **Edge Cases** | Test boundary conditions and unusual inputs |
| **Error Handling** | Verify functions handle errors correctly |
| **Logic Validation** | Ensure business logic works as expected |

### Types of Tests:

| Type | Description | Example |
|------|-------------|---------|
| **Unit Test** | Tests single function in isolation | Test `calculate_tax()` function |
| **Integration Test** | Tests multiple units together | Test API endpoint with database |
| **Regression Test** | Ensures old bugs don't reappear | Re-run tests after code change |

---

## Why Unit Testing

| Reason | Description |
|--------|-------------|
| **Early Bug Detection** | Find bugs at development time — not in production |
| **Code Quality** | Forces developers to write clean, modular code |
| **Refactoring Safety** | Safely refactor code without breaking functionality |
| **CI/CD Integration** | Automate test runs in every build pipeline |
| **Documentation** | Tests serve as living documentation of code behavior |
| **Cost Saving** | Fixing bugs early is 10x cheaper than production fixes |

---

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    UNIT TESTING WORKFLOW                         │
└─────────────────────────────────────────────────────────────────┘

  ┌──────────┐     ┌──────────┐     ┌───────────────┐
  │ Developer│────▶│  Commit  │────▶│   CI/CD       │
  │  Writes  │     │  Code    │     │   Pipeline    │
  │   Code   │     │  to Git  │     │   Triggered   │
  └──────────┘     └──────────┘     └───────┬───────┘
                                            │
                                            ▼
                                   ┌────────────────┐
                                   │    pytest      │
                                   │    Discovers   │
                                   │    Tests       │
                                   └───────┬────────┘
                                           │
                                           ▼
                                   ┌────────────────┐
                                   │    Runs All    │
                                   │    Test Cases  │
                                   └───────┬────────┘
                                           │
                              ┌────────────┴────────────┐
                              │                         │
                              ▼                         ▼
                     ┌────────────────┐       ┌────────────────┐
                     │  Tests FAIL    │       │  Tests PASS    │
                     └───────┬────────┘       └───────┬────────┘
                             │                        │
                             ▼                        ▼
                     ┌────────────────┐       ┌────────────────┐
                     │  Fix Code &    │       │  Code Merged   │
                     │  Re-run Tests  │       │  to Main       │
                     └────────────────┘       └────────────────┘
```

---

## Different Tools

| Tool | Type | Key Feature |
|------|------|-------------|
| **pytest** | Testing framework | Simple syntax, powerful features, widely used |
| **unittest** | Built-in testing framework | Standard library, no installation needed |
| **nose2** | Testing framework | Extends unittest, plugin support |
| **hypothesis** | Property-based testing | Generates test cases automatically |

---

## Comparison of Tools

| Feature | pytest | unittest | nose2 | hypothesis |
|---------|--------|----------|-------|------------|
| **Easy Syntax** | Yes | No | No | No |
| **Built-in Python** | No | Yes | No | No |
| **Plugin Support** | Yes | No | Yes | No |
| **CI/CD Ready** | Yes | Yes | Yes | Yes |
| **Fixtures Support** | Yes | Limited | Yes | No |
| **Parallel Testing** | Yes | No | Yes | No |
| **Free** | Yes | Yes | Yes | Yes |
| **Community** | Very Large | Large | Medium | Medium |

---

## Advantages

### Advantages of Unit Testing:

| Advantage | Description |
|-----------|-------------|
| **Early Bug Detection** | Catch bugs before they reach production |
| **Safe Refactoring** | Change code confidently without breaking things |
| **Living Documentation** | Tests describe what code is supposed to do |
| **Faster Development** | Less time debugging in production |

### Advantages of pytest:

| Advantage | Description |
|-----------|-------------|
| **Simple Syntax** | No classes needed — just write `def test_()` |
| **Auto Discovery** | Automatically finds all test files |
| **Rich Output** | Detailed failure messages |
| **Plugin Ecosystem** | 300+ plugins available |
| **CI/CD Friendly** | Works with GitHub Actions, Jenkins, GitLab CI |

---

## POC

For detailed step-by-step Proof of Concept with screenshots, refer to the POC README below:

> 📎 **[POC - Unit Testing on Attendance API & Notification Worker](./POC-unit-testing.md)**

---

## Best Practices

| # | Practice | Description |
|---|----------|-------------|
| 1 | **Integrate in CI/CD** | Run pytest on every commit/PR automatically |
| 2 | **Test One Thing** | Each test should test only one function/behavior |
| 3 | **Meaningful Names** | Test names should describe what they test |
| 4 | **Fix Failing Tests First** | Never ignore failing tests |

---

## Recommendation & Conclusion

### Tool Recommendation: `pytest` 

After evaluating all available unit testing tools for Python, **`pytest`** is the recommended tool for the following reasons:

| Factor | Reason |
|--------|--------|
| **Industry Standard** | Most widely used Python testing framework |
| **Simple Syntax** | Easy to write and read tests |
| **Auto Discovery** | Automatically finds all test files |
| **CI/CD Ready** | Seamless integration with all major CI/CD platforms |
| **Future Sprints** | Can be reused in Sprint 3-6 for pipeline integration |

### Conclusion

Unit testing is a **fundamental practice** in modern DevOps. For the **Attendance API** (Python microservice), running `pytest` discovered **9 test files** and successfully executed **15 tests** — all passed. The **Notification Worker** had no existing test files, which is a gap that should be addressed in future sprints. For all future sprints and projects, `pytest` will be the primary unit testing tool because it is the industry standard, easy to use, and integrates seamlessly into CI/CD pipelines.

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
| pytest GitHub | https://github.com/pytest-dev/pytest |
| Attendance API Repository | https://github.com/OT-MICROSERVICES/attendance-api |
| Notification Worker Repository | https://github.com/OT-MICROSERVICES/notification-worker |
