# Runbook 07: Active Directory Identity Hierarchy, RBAC, Delegation & Tiered Administration

## Objective
Establish a complete Role-Based Access Control (RBAC) and Tiered Administration framework on Windows Server 2025 (`WS25-DC01`). Define clear boundaries between forest-level master administration, operational system engineers, endpoint technicians, delegated helpdesk personnel, resource access groups, and standard end-user identities.

---

## 1. Enterprise Identity & Privilege Taxonomy

Active Directory identities are segmented into distinct structural tiers based on the Principle of Least Privilege:

| Tier / Role Class | Identity / Group | Scope of Power & System Authority | Best Practice Usage |
| :--- | :--- | :--- | :--- |
| **Tier 0: Ultimate / Forest Root** | `adm.tarik`<br>`Enterprise Admins`<br>`Schema Admins` | • Full root authority across all domains in the forest.<br>• Modifies AD schema blueprint and manages forest trusts.<br>• Controls Domain Controllers directly. | Break-glass / master architectural changes. Kept isolated from daily workstation use. |
| **Tier 0: Domain Control** | `Domain Admins`<br>`Builtin\Administrators` | • Full administrative authority across the entire domain (`tarikndc.com`).<br>• Controls directory database (`NTDS.dit`), GPOs, and all joined systems. | Primary directory operations and domain infrastructure maintenance. |
| **Tier 1: Server & Infrastructure** | `SG_Server_Admins`<br>`server.admin01` | • Local administrative rights across Member Servers (File, Web, Print, DB).<br>• Manages server software, disk storage, and background services. | Daily member server maintenance without holding Domain Controller access. |
| **Tier 1: Network & Security** | `SG_Security_Auditors`<br>`sec.engineer01` | • Read-only directory visibility, Event Log reader, and SIEM forwarding access.<br>• Manages edge appliances, firewalls, and security policies. | Infrastructure monitoring, compliance auditing, and threat detection. |
| **Tier 2: Endpoint / Desktop Support** | `SG_Workstation_Admins`<br>`desktop.admin01` | • Local `Administrators` rights on client workstations (`guest01`) via GPO.<br>• Software deployment, OS patching, and hardware troubleshooting. | End-user device support; blocked from server and directory management. |
| **Tier 3: Delegated Helpdesk** | `SG_Helpdesk_Tier1`<br>`helpdesk01` | • Scoped Active Directory permissions strictly over `Departments` OU.<br>• Resets forgotten passwords, unlocks accounts, and creates/removes staff. | First-line IT support using remote RSAT tools without direct DC logon. |
| **Resource Groups (Access Badges)** | `SG_HR_Department`<br>`SG_Finance_Department`<br>`SG_IT_Department` | • No administrative system privileges.<br>• Used exclusively for Access-Based Enumeration (ABE) and file permissions. | Assigning file share folders, printers, and departmental resources. |
| **Standard Domain Users** | `Domain Users`<br>`hr.user01`, `fin.user01` | • Basic workstation logon and execution of daily productivity applications.<br>• Access to authorized departmental shares (`S:\`). | Standard employees. Cannot install software or modify system settings. |

---

## 2. Directory Hierarchy Architecture

```text
tarikndc.com
└── tarikndc_corp
    ├── Admins
    │   ├── Master Identity: adm.tarik (Domain / Enterprise / Schema Admin)
    │   ├── Server Admins: SG_Server_Admins (server.admin01)
    │   ├── Security Engineers: SG_Security_Auditors (sec.engineer01)
    │   └── Desktop Support: SG_Workstation_Admins (desktop.admin01)
    │
    ├── Departments
    │   ├── HR
    │   │   ├── User: hr.user01
    │   │   └── Resource Group: SG_HR_Department
    │   ├── Finance
    │   │   ├── User: fin.user01
    │   │   └── Resource Group: SG_Finance_Department
    │   └── IT
    │       ├── Delegated User: helpdesk01
    │       ├── Delegated Group: SG_Helpdesk_Tier1 (Scoped to 'Departments' OU)
    │       └── Staff User: it.user01
    │
    ├── Workstations
    │   └── guest01 (Target for Workstation Admin GPO)
    │
    └── Servers
        └── Member Servers (Target for Server Admin GPO)
