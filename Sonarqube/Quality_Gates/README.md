# SonarQube – Quality Gates Documentation
<img width="1500" height="200" alt="image" src="https://github.com/user-attachments/assets/6765636f-b6b3-44d9-9b89-ea36ff72fdad" />

---

## Document Information

| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|----------|----------------|------------|------------|------------|
| Abhinav Tiwari | 27-02-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

# Table of Contents

- [Introduction](#introduction)
- [What is SonarQube?](#what-is-sonarqube)
- [What is a Quality Gate?](#what-is-a-quality-gate)
- [Why Quality Gates are Important?](#why-quality-gates-are-important)
- [Workflow Diagram](#workflow-diagram)
- [Identification of Quality Gates](#identification-of-quality-gates)
  - [Default Quality Gate – Sonar Way](#default-quality-gate--sonar-way)
  - [Custom Quality Gate](#custom-quality-gate)
- [Advantages](#advantages)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)
- [Author](#author)
- [References](#references)

---

# Introduction

Maintaining high code quality is essential in modern DevOps and CI/CD practices. SonarQube helps teams continuously inspect and improve code quality by detecting bugs, vulnerabilities, code smells, and security issues.

Quality Gates act as a control mechanism to ensure that only quality-approved code progresses through the pipeline.

---

# What is SonarQube?

SonarQube is a static code analysis platform used to inspect code quality and security.

It analyzes source code to detect:

- Bugs  
- Vulnerabilities  
- Code Smells  
- Security Hotspots  
- Code Duplication  
- Test Coverage Issues  
- Technical Debt  

It integrates seamlessly with CI/CD tools like Jenkins and GitHub Actions.

---

# What is a Quality Gate?

A Quality Gate is a set of predefined conditions that code must meet before it is considered acceptable.

If the code meets the defined conditions → Pass  
If the code fails to meet the conditions → Fail  

Quality Gates help automate code quality enforcement within CI/CD pipelines.

---

# Why Quality Gates are Important?

- Prevent poor-quality code from reaching production  
- Enforce coding standards  
- Improve security posture  
- Reduce technical debt  
- Automate quality checks  
- Integrate with CI/CD pipelines  
- Ensure maintainability and reliability  

Without Quality Gates, code quality validation becomes manual and inconsistent.

---

# Workflow Diagram
- Developer → Push Code → CI Pipeline → SonarQube Scan → Quality Gate Evaluation → Pass / Fail

<img width="402" height="908" alt="Workflow Diagram - visual selection (1)" src="https://github.com/user-attachments/assets/cc14332b-d684-41c8-9e83-cde01d3ca0c1" />

### Workflow Explanation:

1. Developer commits and pushes code  
2. CI pipeline triggers SonarQube scan  
3. SonarQube analyzes code metrics  
4. Quality Gate evaluates defined conditions  
5. Build either passes or fails based on result  

---

# Identification of Quality Gates

## Default Quality Gate – Sonar Way

SonarQube provides a built-in default Quality Gate called:

### Sonar Way

It typically includes conditions such as:
 
- No new Security vulnerabilities  
- Code coverage threshold on new code  
- Maintainability rating requirement  

This gate focuses on maintaining clean and secure new code while preventing the introduction of serious issues.

---

## Custom Quality Gate

Organizations can create custom Quality Gates based on project requirements.

### Example Custom Quality Gate:

- Coverage ≥ 80%  
- No Critical vulnerabilities  
- Maintainability Rating = A  
- Security Rating = A  

### Steps to Create Custom Gate:

1. Navigate to **Quality Gates** in SonarQube  
2. Click **Create**  
3. Define conditions and thresholds  
4. Save and assign to specific projects  

Custom Quality Gates allow fine-grained control aligned with enterprise standards.

---

# Advantages

- Improves software reliability  
- Enhances application security  
- Reduces production defects  
- Provides measurable quality metrics  

---

# Best Practices

- Use "Sonar Way" as baseline  
- Focus on **New Code** metrics  
- Set realistic coverage targets (≥ 80%)  
- Regularly review and adjust thresholds  
- Fail builds automatically on gate failure  
 

---

## Conclusion

Quality Gates are essential for maintaining consistent code quality and security in CI/CD environments. After evaluating using **Sonar Way** as the baseline standard combined with a **Custom Quality Gate** with stricter enterprise thresholds is the recommended approach.

---

## Author

| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

# References

| # | Reference Title | Official Documentation Link |
|---|-----------------|----------------------------|
| 1 | SonarQube Official Documentation | [SonarQube Docs](https://docs.sonarsource.com/sonarqube/latest/) |
| 2 | Quality Gates Documentation | [Quality Gates Guide](https://docs.sonarsource.com/sonarqube/latest/user-guide/quality-gates/) |
| 3 | Sonar Way Default Gate | [Sonar Way Explanation](https://docs.sonarsource.com/sonarqube/latest/user-guide/quality-gates/#default-quality-gate) |

---
