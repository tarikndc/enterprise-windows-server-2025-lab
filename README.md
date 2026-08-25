# Enterprise Windows Server 2025 Infrastructure Lab

## 1. Project Overview
This repository documents the implementation, management, and security baselines of an on-premises enterprise IT environment built on **Windows Server 2025** inside VMware.

---

## 2. Infrastructure Inventory & Network Plan

| Hostname | Role / Purpose | OS | IP Address | Subnet Mask | Default Gateway | DNS Server |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **WS25-DC01** | Primary Domain Controller (AD DS, DNS, DHCP) | Windows Server 2025 | `192.168.17.3` (Static) | `255.255.255.0` | `192.168.17.2` | `127.0.0.1` |
| **guest01** | Test Workstation (Client Endpoint) | Windows 11 Pro | `192.168.17.131` (DHCP) | `255.255.255.0` | `192.168.17.2` | Assigned via VMware DHCP |

---

## 3. Implementation Logs & Runbooks

* [01 - Base Server & Client Workstation Setup](docs/01-base-server-setup.md)
* [02 - AD DS & DNS Deployment](docs/02-ad-ds-dns-setup.md)
* [03 - Active Directory OU Architecture](docs/03-ou-design-hierarchy.md)
* [04 - DHCP Service Architecture & Deployment](docs/04-dhcp-service-deployment.md)
* [05 - Enterprise Group Policy Baseline](docs/05-group-policy-baseline.md)
* [06 - Departmental File Server & ABE Drive Maps](docs/06-file-server-abe-and-gpo-drive-maps.md)
* [07 - AD Delegation, RBAC & Tiered Administration](docs/07-ad-delegation-rbac-tiered-access.md)
* [08 - Centralized Print Management & Auditing](docs/08-print-management-and-auditing.md)
* [09 - Workstation Admin Logon Restrictions](docs/09-workstation-admin-logon-restrictions.md)
* [10 - Native Windows LAPS & Endpoint Credential Management](docs/10-native-windows-laps-deployment.md)
