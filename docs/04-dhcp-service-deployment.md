# Runbook 04: DHCP Service Architecture & Deployment

## Objective
Deploy and authorize an enterprise DHCP Server on Windows Server 2025 (`WS25-DC01`), configure dynamic address pools with scope options for internal DNS and routing, and establish network isolation for static hardware devices.

---

## 1. Network Architecture & Subnet Planning

* **Subnet:** `192.168.17.0/24` (Subnet Mask: `255.255.255.0`)
* **Default Gateway:** `192.168.17.2` (VMware NAT Router)
* **Primary DC / DNS:** `192.168.17.3` (`tarikndc.com`)

### Subnet Allocation Blueprint
| IP Range | Assignment | Target Device / Purpose |
| :--- | :--- | :--- |
| `192.168.17.1` - `192.168.17.2` | Static | VMware Host Link & Virtual NAT Gateway |
| `192.168.17.3` | Static | Primary Domain Controller (`WS25-DC01`) |
| `192.168.17.4` - `192.168.17.49` | Static | Infrastructure Servers & Future Member DCs |
| `192.168.17.50` - `192.168.17.99` | Static (Manual Only) | Hardware Isolation Zone (Printers & Scanners outside DHCP) |
| `192.168.17.100` - `192.168.17.200` | Dynamic DHCP | Managed Client Workstations (`Lab Clients` Scope) |

---

## 2. Implementation Steps

### A. Role Installation
1. Opened **Server Manager** > **Manage** > **Add Roles and Features**.
2. Selected **DHCP Server** and completed installation with default administrative tools.

### B. Active Directory Authorization & Binding
1. Ensured network adapter binding to primary static IP `192.168.17.3`.
2. Restarted the DHCP service to register new security group bindings:
```cmd
net stop dhcpserver && net start dhcpserver
