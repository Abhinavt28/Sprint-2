# Cloud Infrastructure Design – Dev Environment (OT Microservices)

---

## Document Control

| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|-----------------|-------------|-------------|-------------|
| Abhinav Tiwari | 24-02-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhyay |

---

## Table of Contents

- [Introduction](#introduction)
- [Pre-Requisites](#pre-requisites)
- [Infrastructure Overview](#infrastructure-overview)
- [Infrastructure Diagram](#infrastructure-diagram)
- [Infrastructure Description](#infrastructure-description)
- [EC2 Instance Details](#ec2-instance-details)
- [Security Group Configuration](#security-group-configuration)
- [Network ACL Configuration](#network-acl-configuration)
- [Security Justification](#security-justification)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Introduction

This document describes the Cloud Infrastructure Design for the Development Environment of the **OT Microservices (OT-MS)** application.

The OT-MS application consists of the following services:

| Service | Language/Framework | Database |
|---|---|---|
| Frontend | React | — |
| Employee API | Golang | ScyllaDB + Redis |
| Attendance API | Python (Flask) | PostgreSQL + Redis |
| Salary API | Java (Spring Boot) | ScyllaDB |
| Notification Worker | Python | — (SMTP) |

The objective of this infrastructure is to:

- Build a secure and isolated Dev environment for OT-MS
- Follow AWS best practices
- Implement layered security (Network + Instance level)
- Ensure scalable and modular architecture

This design follows a **2-tier architecture** for the Dev environment:

- **Web Layer** (Public Subnet) — Frontend
- **Application Layer** (Private Subnet) — All backend APIs and workers (co-located for dev simplicity)

---

## Pre-Requisites

- AWS Account
- IAM User with appropriate permissions
- Selected Region: **us-east-1 (N. Virginia)**
- SSH Key Pair
- Basic networking knowledge

---

## Infrastructure Overview

### Architecture Type

2-Tier Architecture (Development) — Frontend in Public Subnet, all backend services in Private Subnet

### Components Used

- VPC
- Internet Gateway
- NAT Gateway
- Elastic IP (for NAT Gateway)
- Public Subnet
- Private App Subnet
- Route Tables
- Security Groups
- Network ACLs
- EC2 Instances

---

## Infrastructure Diagram

> _Refer to the attached draw.io diagram for visual reference._

![Infra Diagram](./infra-diagram.png)

---

## Infrastructure Description

### VPC

| Property | Value |
|----------|-------|
| CIDR | 10.0.0.0/16 |
| Region | us-east-1 (N. Virginia) |
| Purpose | Isolated network for OT-MS Dev environment |
| Justification | Logical separation of environment from other workloads |

---

### Subnets

| Subnet Name | CIDR | AZ | Type | Purpose |
|-------------|------|----|------|---------|
| Public-Subnet | 10.0.1.0/24 | us-east-1a | Public | Frontend EC2 |
| Private-App-Subnet | 10.0.2.0/24 | us-east-1a | Private | All backend APIs + Workers |

---

### Gateways & Route Tables

| Component | Attached To | Purpose |
|-----------|-------------|---------|
| IG-A (Internet Gateway) | VPC | Allows internet traffic in/out for public subnet |
| NG-A (NAT Gateway) | Public Subnet | Allows private subnet instances to reach internet (outbound only) |
| pub-rt (Public Route Table) | Public Subnet | Routes internet traffic via IG-A |
| pvt-rt (Private Route Table) | Private App Subnet | Routes outbound traffic via NG-A |

#### Route Table Entries

| Route Table | Destination | Target |
|-------------|-------------|--------|
| pub-rt | 0.0.0.0/0 | IG-A |
| pub-rt | 10.0.0.0/16 | local |
| pvt-rt | 0.0.0.0/0 | NG-A |
| pvt-rt | 10.0.0.0/16 | local |

---

## EC2 Instance Details

| Instance Name | Layer | OS | Instance Type | Subnet | Open Ports | Purpose |
|--------------|-------|----|--------------|--------|------------|---------|
| Frontend | Web | Ubuntu 22.04 | t2.micro | Public (10.0.1.0/24) | 22, 80, 3000 | Hosts React frontend |
| Employee-API | Application | Ubuntu 22.04 | t2.micro | Private-App (10.0.2.0/24) | 8080 | Employee service (Go + ScyllaDB + Redis) |
| Attendance-API | Application | Ubuntu 22.04 | t2.micro | Private-App (10.0.2.0/24) | 8081 | Attendance service (Python + PostgreSQL + Redis) |
| Salary-API | Application | Ubuntu 22.04 | t2.micro | Private-App (10.0.2.0/24) | 8082 | Salary service (Java + ScyllaDB) |
| Notification-Worker | Application | Ubuntu 22.04 | t2.micro | Private-App (10.0.2.0/24) | — | Notification service (Python + SMTP) |

---

## Security Group Configuration

### Frontend-SG

| Type | Port | Source | Purpose |
|------|------|--------|---------|
| SSH | 22 | My IP | Admin access |
| HTTP | 80 | 0.0.0.0/0 | Public web access |
| Custom TCP | 3000 | 0.0.0.0/0 | React dev server access |

---

### Employee-API-SG

| Type | Port | Source | Purpose |
|------|------|--------|---------|
| Custom TCP | 8080 | Frontend-SG | Employee API access from frontend |
| SSH | 22 | My IP | Admin access |

---

### Attendance-API-SG

| Type | Port | Source | Purpose |
|------|------|--------|---------|
| Custom TCP | 8081 | Frontend-SG | Attendance API access from frontend |
| SSH | 22 | My IP | Admin access |

---

### Salary-API-SG

| Type | Port | Source | Purpose |
|------|------|--------|---------|
| Custom TCP | 8082 | Frontend-SG | Salary API access from frontend |
| SSH | 22 | My IP | Admin access |

---

### Notification-Worker-SG

| Type | Port | Source | Purpose |
|------|------|--------|---------|
| SSH | 22 | My IP | Admin access |
| Custom TCP | 587 | 0.0.0.0/0 | SMTP outbound for notifications |

---

## Network ACL Configuration

### Public Subnet NACL

| Rule # | Type | Port | Source | Action |
|--------|------|------|--------|--------|
| 100 | HTTP | 80 | 0.0.0.0/0 | Allow |
| 110 | Custom TCP | 3000 | 0.0.0.0/0 | Allow |
| 120 | SSH | 22 | My IP | Allow |
| 130 | Custom TCP | 1024-65535 | 0.0.0.0/0 | Allow |
| 32767 | All traffic | All | All | Deny |

---

### Private Subnet NACL

| Rule # | Type | Port | Source | Action |
|--------|------|------|--------|--------|
| 100 | Custom TCP | 8080 | 10.0.1.0/24 | Allow |
| 110 | Custom TCP | 8081 | 10.0.1.0/24 | Allow |
| 120 | Custom TCP | 8082 | 10.0.1.0/24 | Allow |
| 130 | SSH | 22 | My IP | Allow |
| 140 | Custom TCP | 1024-65535 | 0.0.0.0/0 | Allow |
| 32767 | All traffic | All | All | Deny |

---

## Security Justification

- Only Frontend layer is exposed to the internet via Public Subnet
- All backend APIs and workers are isolated in Private Subnet — no direct internet access
- NAT Gateway allows private instances to pull packages/updates (outbound only)
- SSH access restricted to admin IP only — not open to public
- Each EC2 has its own Security Group — Principle of Least Privilege followed
- NACL acts as an additional stateless layer of defense — Defense-in-Depth strategy implemented
- Inter-service communication restricted via SG source rules (only Frontend-SG can talk to API SGs)

---

## Conclusion

This Dev Infrastructure for OT Microservices provides a secure, isolated, and cost-effective environment. The Frontend is publicly accessible while all backend services remain in a private subnet, accessible only through controlled Security Group rules. The architecture follows AWS best practices with layered security through both Security Groups and NACLs. The design is modular and can be extended to a full 3-tier setup in staging/production environments by separating database instances into a dedicated subnet.

---

## Contact Information

| Field | Details |
|-------|---------|
| Author | Abhinav Tiwari |
| Email | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References

| Resource | Link |
|----------|------|
| AWS VPC Documentation | https://docs.aws.amazon.com/vpc/ |
| AWS EC2 Documentation | https://docs.aws.amazon.com/ec2/ |
| AWS Security Groups | https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html |
| AWS NAT Gateway | https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html |
| AWS Network ACLs | https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html |
| OT Microservices GitHub | https://github.com/OT-MICROSERVICES |
