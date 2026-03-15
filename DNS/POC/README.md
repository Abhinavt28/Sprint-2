# DNS Implementation POC

---

## Document Control

| Author         | Created On | Version | Last Updated By | L0 Reviewer  | L1 Reviewer | L2 Reviewer     |
| -------------- | ---------- | ------- | --------------- | ------------ | ----------- | --------------- |
| Abhinav Tiwari | 07-02-2026 | v1.0    | Abhinav Tiwari  | Nikita Joshi | Prashant    | Piyush Upadhyay |
| Abhinav Tiwari | 15-03-2026 | v1.1    | Abhinav Tiwari  | Nikita Joshi | Prashant    | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#introduction)
2. [POC Objective](#poc-objective)
3. [Prerequisites](#prerequisites)
4. [DNS Setup Details](#dns-setup-details)

<details>
<summary><strong>5. DNS Implementation Steps</strong></summary>

&nbsp;&nbsp;5.1 [Step 1: Purchase / Use Domain](#step-1-purchase--use-domain)  
&nbsp;&nbsp;5.2 [Step 2: Create Hosted Zone in Route 53](#step-2-create-hosted-zone-in-route-53)  
&nbsp;&nbsp;5.3 [Step 3: Update Nameservers in Hostinger](#step-3-update-nameservers-in-hostinger)  
&nbsp;&nbsp;5.4 [Step 4: Add A Record in Route 53](#step-4-add-a-record-in-route-53)  
&nbsp;&nbsp;5.5 [Step 5: Verify DNS Propagation](#step-5-verify-dns-propagation)  
&nbsp;&nbsp;5.6 [Step 6: Verify via Browser](#step-6-verify-via-browser)  

</details>

6. [Conclusion](#conclusion)
7. [Contact Information](#contact-information)
8. [Reference Table](#reference-table)

---

## Introduction

This document provides a **Proof of Concept (POC)** for implementing **DNS (Domain Name System)** configuration for a domain.  
The objective is to map a domain name (`innovitisolutions.in`) to a server IP address using **AWS Route 53** as the DNS provider and **Hostinger** as the domain registrar. DNS resolution is validated using command-line tools and browser-based verification.

---

## POC Objective

| Objective | Description |
|----------|-------------|
| **Domain Mapping** | Map `innovitisolutions.in` to server IP `51.21.3.40` |
| **DNS Configuration** | Configure DNS records via AWS Route 53 |
| **Nameserver Update** | Point Hostinger domain to Route 53 nameservers |
| **Validation** | Verify DNS resolution via `nslookup` |
| **Outcome** | Domain accessible via browser |

---

## Prerequisites

| Requirement | Description |
|------------|-------------|
| **Domain Name** | Registered domain — `innovitisolutions.in` (Hostinger) |
| **AWS Account** | Access to AWS Console with Route 53 permissions |
| **Server** | Linux VM / Cloud instance with public IP |
| **Public IP** | Server public IP — `51.21.3.40` |
| **Internet Access** | Required for DNS propagation |

---

## DNS Setup Details

| Item | Value |
|-----|------|
| **Domain** | innovitisolutions.in |
| **Domain Registrar** | Hostinger |
| **DNS Provider** | AWS Route 53 |
| **Record Type** | A Record |
| **Target IP** | 51.21.3.40 |

---

## Step 1: Purchase / Use Domain

Use an existing domain or purchase a new domain from a registrar. In this POC, domain `innovitisolutions.in` is already purchased and active on **Hostinger**.

![Hostinger Domain Portfolio](https://github.com/user-attachments/assets/f902c167-3514-4cf1-ae51-2fe4fcf9f72b)

---

## Step 2: Create Hosted Zone in Route 53

1. Login to **AWS Console**
2. Navigate to **Route 53 → Hosted Zones**
3. Click **Create Hosted Zone**
4. Enter:
   - Domain name: `innovitisolutions.in`
   - Type: **Public Hosted Zone**
5. Click **Create**

AWS automatically creates:
- **NS records** (4 nameservers)
- **SOA record**

Once created, the hosted zone will show all records including the A record and NS records as shown below:


> **Note:** Copy the 4 NS record values — these will be needed in the next step.

---

## Step 3: Update Nameservers in Hostinger

After creating the hosted zone, update the nameservers in Hostinger to point to Route 53:

1. Login to **Hostinger**
2. Go to **Domains → Manage → innovitisolutions.in**
3. Open **Nameservers**
4. Select **Custom Nameservers**
5. Paste the 4 NS values from Route 53:
   - `ns-1504.awsdns-60.org`
   - `ns-1877.awsdns-42.co.uk`
   - `ns-272.awsdns-34.com`
   - `ns-654.awsdns-17.net`
6. Save changes

![Hostinger Nameservers Updated](https://github.com/user-attachments/assets/hostinger_ns_placeholder)

> **Note:** Nameserver propagation may take **30 minutes to 24 hours**

---

## Step 4: Add A Record in Route 53

Once nameservers are propagated, add an A record in Route 53 to map the domain to the server IP:

| Field | Value |
|------|------|
| **Record Name** | `@` (leave blank for root domain) |
| **Record Type** | A |
| **Value / IP** | `51.21.3.40` |
| **TTL** | 300 |
| **Routing Policy** | Simple |

The Route 53 hosted zone with all records configured:

![Route 53 Records](https://github.com/user-attachments/assets/aws_route53_records_placeholder)

---

## Step 5: Verify DNS Propagation

After DNS propagation, verify resolution using `nslookup`:

```bash
nslookup innovitisolutions.in
```

Expected output:
```
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:    innovitisolutions.in
Address: 51.21.3.40
```

![nslookup Output](https://github.com/user-attachments/assets/nslookup_placeholder)

---

## Step 6: Verify via Browser

Open the domain in a browser to confirm it is live and accessible:

```
https://innovitisolutions.in
```

![Browser Verification](https://github.com/user-attachments/assets/browser_placeholder)

---

## Conclusion

This Proof of Concept (POC) confirms that DNS has been successfully configured for `innovitisolutions.in`. The domain was purchased via **Hostinger**, DNS management was delegated to **AWS Route 53** by updating the nameservers, and an **A record** was added pointing to server IP `51.21.3.40`. Successful resolution was verified via `nslookup` and browser access.

---

## Contact Information

| **Name** | **Email** |
|----------|----------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## Reference Table

| **Reference Type** | **Description** | **Link** |
|------------------|----------------|----------|
| **AWS Route 53 Docs** | Official Route 53 hosted zone documentation | https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zones-working-with.html |
| **DNS Documentation** | DNS and domain management concepts | https://www.cloudflare.com/learning/dns/what-is-dns/ |
| **nslookup Guide** | DNS lookup command usage | https://linux.die.net/man/1/nslookup |
| **dig Command** | DNS query tool documentation | https://linux.die.net/man/1/dig |
| **SSL Reference Doc** | DNS/SSL documentation reference | https://github.com/Snaatak-Error-404/Sprint-1/blob/SCRUM-120-neha/Domain_Security%20/SSL/Documentation%20/README.md |
