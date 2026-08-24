# Runbook 06: Departmental File Server, Access-Based Enumeration (ABE) & GPO Drive Mapping

## Objective
Design, configure, and validate a departmental file server on Windows Server 2025 (`WS25-DC01`) with Access-Based Enumeration (ABE). Enforce Least-Privilege access by breaking NTFS inheritance so domain users only see and open folders for their authorized department, and automatically mount the repository (`S:`) via Group Policy Preferences.

---

## 1. Directory Tree & Security Architecture

```text
tarikndc.com
└── tarikndc_corp
    └── Departments
        ├── HR
        │   ├── User: hr.user01
        │   └── Security Group: SG_HR_Department (Global / Security)
        ├── Finance
        │   ├── User: fin.user01
        │   └── Security Group: SG_Finance_Department (Global / Security)
        └── IT
            ├── User: it.user01
            └── Security Group: SG_IT_Department (Global / Security)
