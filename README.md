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
