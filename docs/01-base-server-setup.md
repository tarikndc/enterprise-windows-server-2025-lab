# Runbook 01: Base Server & Client Workstation Setup

## Objective
Deploy the base operating system instances (Windows Server 2025 and Windows 11 Pro) on VMware, establish standard host naming conventions, and verify baseline network connectivity.

---

## Machine Specifications

### 1. Server Node
* **Hostname:** `WS25-DC01`
* **Operating System:** Windows Server 2025
* **Role:** Domain Controller (Designated)
* **IP Configuration:** Static (`192.168.17.3/24`)
* **Default Gateway:** `192.168.17.2`
* **Preferred DNS:** `127.0.0.1`

### 2. Client Node
* **Hostname:** `guest01`
* **Operating System:** Windows 11 Pro
* **Local User:** `user01`
* **IP Configuration:** Dynamic (`192.168.17.131/24`)
* **Default Gateway:** `192.168.17.2`

---

## Implementation Details

### Server (WS25-DC01) Network Configuration
Static IP parameters were bound to the primary virtual adapter to prepare for Active Directory Domain Services (AD DS) and DNS roles:
* **IPv4 Address:** `192.168.17.3`
* **Subnet Mask:** `255.255.255.0`
* **Default Gateway:** `192.168.17.2`

### Workstation (guest01) Baseline
A fresh Windows 11 Pro instance was provisioned to serve as a domain member endpoint for testing Group Policy Objects (GPOs), network shares, and user authentication:
* **Local Account Created:** `user01`
* **Current Lease:** `192.168.17.131` via hypervisor DHCP (to be migrated to Windows Server DHCP later).

---

## Verification & Connectivity Test

Ran `ipconfig` verification on both nodes to confirm active network bindings within the `192.168.17.0/24` subnet:

**Server (`WS25-DC01`):**
```cmd
IPv4 Address. . . . . . . . . . . : 192.168.17.3
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.17.2
