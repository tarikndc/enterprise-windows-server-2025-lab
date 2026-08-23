# Runbook 01: Base Server Installation & Network Configuration

## Objective
Deploy the base operating system instance on VMware Workstation, set standard corporate host naming conventions, and assign static IP parameters required for a Domain Controller.

---

## Server Specifications
* **Hostname:** `WS25-DC01`
* **Operating System:** Windows Server 2025
* **Hypervisor:** VMware

---

## Configuration Details

### 1. Hostname Assignment
Renamed the default computer name to standard enterprise convention:
* **Assigned Hostname:** `WS25-DC01`

### 2. Network Configuration (Static IP)
Configured static addressing on the primary network interface to prevent IP drift before deploying directory services:

* **IPv4 Address:** `192.168.17.3`
* **Subnet Mask:** `255.255.255.0` (`/24`)
* **Default Gateway:** `192.168.17.2`
* **Preferred DNS:** `127.0.0.1` (Points to loopback for upcoming DNS/AD DS role)

---

## Verification
Executed `ipconfig /all` in Command Prompt to confirm network adapter binding:

```cmd
IPv4 Address. . . . . . . . . . . : 192.168.17.3
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.17.2
