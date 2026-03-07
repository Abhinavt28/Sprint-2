# VCS POC – Setup Notification for Branch Merge

---

# Document Information

| Author | Created On | Version | Last Updated By | Reviewer L0 | Reviewer L1 | Reviewer L2 |
|--------|------------|---------|----------------|------------|------------|------------|
| Abhinav Tiwari | 24-02-2026 | v1.0 | Abhinav Tiwari | Nikita Joshi | Prashant | Piyush Upadhayay |

---

## Project Overview

This Proof of Concept (POC) demonstrates:
- Branch Protection on `main`
- Mandatory Pull Request approval
- GitHub Actions automation
- Slack Webhook integration
- Automated Slack notification when PR is merged into `main`

This setup simulates a production-level DevOps workflow.

---

## Table of Contents

- [Project Overview](#project-overview)
<details>
<summary><strong>Branch Protection Configuration</strong></summary>

- [Step 1 – Navigate to Rulesets](#step-1--navigate-to-rulesets)
- [Step 2 – Create New Ruleset](#step-2--create-new-ruleset)
- [Step 3 – Enable Enforcement](#step-3--enable-enforcement)
- [Step 4 – Target Branch = main](#step-4--target-branch--main)
- [Step 5 – Require Pull Request Approval](#step-5--require-pull-request-approval)
- [Step 6 – Ruleset Created Successfully](#step-6--ruleset-created-successfully)
</details>

<details>
<summary><strong>Slack Webhook & Secrets Setup</strong></summary>

- [Step 1 – Create Slack Webhook](#step-1--create-slack-webhook)
- [Step 2 – Add GitHub Secret](#step-2--add-github-secret)
</details>

<details>
<summary><strong>GitHub Actions Workflow Setup</strong></summary>

- [Step 1 – Open Actions Tab](#step-1--open-actions-tab)
- [Step 2 – Create Custom Workflow](#step-2--create-custom-workflow)
- [Step 3 – Add Workflow Code](#step-3--add-workflow-code)
</details>

<details>
<summary><strong>Feature Branch & PR Creation</strong></summary>

- [Step 1 – Create Feature Branch](#step-1--create-feature-branch)
- [Step 2 – Create PR (Approval Required)](#step-2--create-pr-approval-required)
</details>

<details>
<summary><strong>Workflow PR Approval & Merge</strong></summary>

- [Step 1 – Workflow PR Created](#step-1--workflow-pr-created)
- [Step 2 – Approval Required](#step-2--approval-required)
- [Step 3 – Reviewer Approved](#step-3--reviewer-approved)
- [Step 4 – PR Merged into main](#step-4--pr-merged-into-main)
</details>

<details>
<summary><strong>Workflow Execution</strong></summary>

- [GitHub Actions Triggered](#github-actions-triggered)
- [Slack Workflow PR](#slack-workflow-pr)
- [Reviewer Approved Slack PR](#reviewer-approved-slack-pr)
</details>

<details>
<summary><strong>Email & Notification Validation</strong></summary>

- [GitHub Email Notification](#github-email-notification)
- [Slack Notification Received](#slack-notification-received)
</details>

- [Architecture Flow](#architecture-flow)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## Branch Protection Configuration

### Step 1 – Navigate to Rulesets
Navigating to Settings → Rules → Rulesets.

<img width="1366" height="729" alt="SS-02-Rulesets-Page" src="https://github.com/user-attachments/assets/cd9fddc8-e92b-4bd3-b8f3-58c07545474f" />


---

### Step 2 – Create New Ruleset
Creating a new branch ruleset for main branch protection.

<img width="1365" height="731" alt="SS-03-New-Ruleset-Configuration" src="https://github.com/user-attachments/assets/482cd345-e4d1-475d-9f83-653a6527e81e" />

---

### Step 3 – Enable Enforcement
Ruleset enforcement status set to Active.

<img width="1366" height="731" alt="SS-04-Ruleset-Enforcement-Active" src="https://github.com/user-attachments/assets/23dc6a75-7335-40c0-9f7d-01a3b9aee02e" />

---

### Step 4 – Target Branch = main
Selecting `main` as the protected target branch.

<img width="1366" height="729" alt="SS-05-Target-Branch-Main" src="https://github.com/user-attachments/assets/893b8db0-d2b5-449d-9496-b94e46cd5f2d" />

---

### Step 5 – Require Pull Request Approval
Enabling "Require a pull request before merging" with 1 approval required.

<img width="1366" height="732" alt="SS-06-Require-PR-Approval" src="https://github.com/user-attachments/assets/e05cdb3f-d83e-48bc-ac0d-81f5e3cda064" />

---

### Step 6 – Ruleset Created Successfully
Branch protection rule successfully created.

<img width="1366" height="734" alt="SS-07-Ruleset-Created-Successfully" src="https://github.com/user-attachments/assets/0bfc83e8-cd0a-43ef-8d1f-7a1bfb03a9b3" />

</details>

---

## Slack Webhook & Secrets Setup

### Step 1 – Create Slack Webhook
Slack Incoming Webhook generated.

<img width="1366" height="731" alt="SS-18-Slack-Webhook-Created" src="https://github.com/user-attachments/assets/8e06e8db-73e1-46ad-b879-85edef75b466" />

---

### Step 2 – Add GitHub Secret
Slack webhook stored securely as repository secret.

**Secret Name:**
```
SLACK_WEBHOOK_URL
```

<img width="1366" height="735" alt="SS-19-GitHub-Slack-Secret-Added" src="https://github.com/user-attachments/assets/2526f61b-a6d7-4508-a0f2-03143dea2738" />

</details>

---

## GitHub Actions Workflow Setup

### Step 1 – Open Actions Tab
Opening GitHub Actions tab.

<img width="1365" height="728" alt="SS-10-Actions-Tab-Opened" src="https://github.com/user-attachments/assets/fbabec9f-befb-4b22-865f-499820744017" />

---

### Step 2 – Create Custom Workflow
Creating a custom workflow.

<img width="1363" height="728" alt="SS-11-Create-Custom-Workflow" src="https://github.com/user-attachments/assets/c007e3ae-7d13-4650-9235-3de40f994194" />

---

### Step 3 – Add Workflow Code
Adding YAML workflow file in `.github/workflows`.

<img width="1366" height="683" alt="SS-12-Workflow-Code-Added" src="https://github.com/user-attachments/assets/0bbf1aff-eb77-4476-b740-cd753ba5ea40" />

---

### Workflow Code Used

```yaml
name: Branch Merge Notification

on:
  pull_request:
    types: [closed]

jobs:
  notify:
    if: github.event.pull_request.merged == true && github.event.pull_request.base.ref == 'main'
    runs-on: ubuntu-latest

    steps:
      - name: Send Slack Notification
        run: |
          curl -X POST -H "Content-type: application/json" \
          --data "{
            \"text\": \" PR merged into main branch!\nRepository: ${{ github.repository }}\nMerged by: ${{ github.actor }}\nPR Title: ${{ github.event.pull_request.title }}\"
          }" \
          ${{ secrets.SLACK_WEBHOOK_URL }}
```

</details>

---

## Feature Branch & PR Creation

### Step 1 – Create Feature Branch
New feature branch created for testing branch protection.

<img width="1366" height="726" alt="SS-08-Feature-Branch-Created" src="https://github.com/user-attachments/assets/aad4123f-b761-4297-aaa4-506b9c3d4839" />

---

### Step 2 – Create PR (Approval Required)
Pull request created; merge blocked until approval.

<img width="1366" height="732" alt="SS-09-PR-Created-Approval-Required" src="https://github.com/user-attachments/assets/c0a4e986-4333-40fd-a22d-2b1ddd7b8651" />

</details>

---

## Workflow PR Approval & Merge

### Step 1 – Workflow PR Created
Workflow pull request created.

<img width="908" height="452" alt="SS-13-Workflow-PR-Created" src="https://github.com/user-attachments/assets/60e7f1bf-0be1-4ae1-b247-e7ff7897e38a" />

---

### Step 2 – Approval Required
Approval required before merge.

<img width="1366" height="732" alt="SS-14-Workflow-PR-Approval-Required" src="https://github.com/user-attachments/assets/2b1070b1-03b8-4e5c-8c6f-b5934e658fde" />

---

### Step 3 – Reviewer Approved
Reviewer approved the workflow PR.

<img width="1366" height="731" alt="SS-15-Reviewer-Approved-PR" src="https://github.com/user-attachments/assets/abc2f9c8-e99c-47f0-be9b-dbe79a5d9228" />

---

### Step 4 – PR Merged into main
Workflow successfully merged into main branch.

<img width="1366" height="730" alt="SS-16-PR-Merged-Into-Main" src="https://github.com/user-attachments/assets/2dd69f6f-0929-4783-8a49-b9d014cc9382" />

</details>

---

## Workflow Execution

### GitHub Actions Triggered
GitHub Actions triggered automatically on merge.

<img width="1366" height="734" alt="SS-17-Workflow-Triggered-On-Merge" src="https://github.com/user-attachments/assets/fd120b68-630d-4225-a3d9-fb3e9b34c221" />

---

### Slack Workflow PR
Pull request created for Slack-integrated workflow.

`SS-21-Slack-Workflow-PR-Created`
<img width="1366" height="731" alt="SS-21-Slack-Workflow-PR-Created" src="https://github.com/user-attachments/assets/2059be25-f287-4020-9c3e-df78300fca33" />

---

### Reviewer Approved Slack PR
Reviewer approved the Slack workflow PR.

`slack pr`

</details>

---

## Email & Notification Validation

### GitHub Email Notification
GitHub email confirming approval and merge.

<img width="1366" height="731" alt="SS-18-GitHub-Email-Notification" src="https://github.com/user-attachments/assets/69ead5e3-972e-4b1f-ba2e-5e12f46c42d1" />

---

### Slack Notification Received
Slack notification received on merge.

<img width="1366" height="734" alt="SS-21-Slack-notification" src="https://github.com/user-attachments/assets/45bf8934-c6f4-41ab-a565-9bde488f5198" />

</details>

---

## Architecture Flow

```
Developer → Feature Branch
        ↓
Create PR
        ↓
Approval Required
        ↓
Merge into main
        ↓
GitHub Actions Triggered
        ↓
Slack Notification Sent
```

---

## Conclusion

This POC successfully demonstrates secure branch governance with mandatory code review, GitHub Actions CI automation, secure secrets management via GitHub Secrets, and real-time Slack integration — mirroring a production-level DevOps CI/CD workflow.

---

## Contact Information

| Name | Email |
|------|-------|
| Abhinav Tiwari | abhinav.tiwari.snaatak@mygurukulam.co |

---

## References

| # | Reference Title | Link |
|---|----------------|------|
| 1 | GitHub Branch Protection & Rulesets | https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets |
| 2 | GitHub Actions – Workflow Events & Conditions | https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows |
| 3 | Slack Incoming Webhooks Integration | https://api.slack.com/messaging/webhooks |
