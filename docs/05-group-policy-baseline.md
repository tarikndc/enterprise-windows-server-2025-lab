# Runbook 05: Enterprise Group Policy (GPO) Baseline

## Objective
Implement, link, and validate an enterprise Group Policy baseline targeting user and computer scopes in `tarikndc.com`. This baseline manages mapped network drives, enforces idle screen locks, establishes Data Loss Prevention (DLP) for removable media, and deploys corporate lock screen branding.

---

## 1. Directory Tree & Policy Placement

```text
tarikndc.com
└── tarikndc_corp (Root Container)
    ├── Admins
    ├── Departments (User Scope Container)
    │   ├── GPO: User Security and Styling Policy
    │   ├── GPO: User Environment and Storage Policy
    │   ├── GPO: User Inactivity Screen Lock Policy
    │   ├── IT
    │   ├── HR
    │   └── Finance
    ├── Worksations (Computer Scope Container)
    │   ├── GPO: Endpoint Hardware Restriction Policy
    │   └── GPO: Workstation Branding Policy
    └── Servers
