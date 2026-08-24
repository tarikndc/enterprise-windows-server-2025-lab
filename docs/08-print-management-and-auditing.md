# Runbook 08: Centralized Print Server, GPO Deployment, Point-and-Print Hardening & Audit Logging

## Objective
Deploy and configure the **Print and Document Services** role on Windows Server 2025 (`WS25-DC01`), create department-specific network print shares, deploy printer connections automatically via Group Policy Preferences (GPP), remediate Point-and-Print driver restrictions (PrintNightmare mitigations), and implement operational logging to audit print jobs across the domain.

---

## 1. Architectural Overview

```text
               ┌────────────────────────────────────────────────────────┐
               │         Windows Server 2025 (WS25-DC01 / 192.168.17.3) │
               │  Role: Print and Document Services                     │
               │                                                        │
               │  Shared Queues:                                        │
               │  • \\192.168.17.3\PRN-HR-Floor1   (Universal Driver)   │
               │  • \\192.168.17.3\PRN-FIN-Floor2  (Universal Driver)   │
               │                                                        │
               │  Audit Log: PrintService/Operational (Event ID 307)    │
               └──────────────────────────┬─────────────────────────────┘
                                          │
                     ┌────────────────────┴────────────────────┐
                     │ Group Policy Deployment (User Prefs)    │
                     ▼                                         ▼
       ┌───────────────────────────┐             ┌───────────────────────────┐
       │   HR Department Users     │             │ Finance Department Users  │
       │   (hr.user01 on guest01)  │             │ (fin.user01 on guest01)   │
       │   Auto-Mapped:            │             │ Auto-Mapped:              │
       │   PRN-HR-Floor1 (Default) │             │ PRN-FIN-Floor2 (Default)  │
       └───────────────────────────┘             └───────────────────────────┘
