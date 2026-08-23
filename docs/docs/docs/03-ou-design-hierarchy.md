# Runbook 03: Active Directory Organizational Unit (OU) Architecture

## Objective
Design and deploy a structured Organizational Unit (OU) hierarchy in `tarikndc.com` following Microsoft Tiered Administration and Least-Privilege principles, and configure default computer object redirection to automate endpoint OU placement.

---

## 1. Directory Tree Hierarchy

```text
tarikndc.com
└── tarikndc_corp (Root Parent OU)
    ├── Admins
    ├── Departments
    │   ├── IT
    │   ├── HR
    │   └── Finance
    ├── Worksations
    └── Servers
