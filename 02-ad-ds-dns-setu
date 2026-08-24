# Runbook 02: Active Directory Domain Services & DNS Deployment (GUI)

## Objective
Install Active Directory Domain Services (AD DS) and DNS server roles on `WS25-DC01` using Server Manager GUI, promote the server to the root Domain Controller for `tarikndc.com`, and configure upstream DNS forwarders for external name resolution.

---

## Configuration Parameters
* **Target Server:** `WS25-DC01` (`192.168.17.3`)
* **Deployment Type:** Add a new forest
* **Root Domain Name (FQDN):** `tarikndc.com`
* **NetBIOS Domain Name:** `TARIKNDC`
* **Domain & Forest Functional Level:** Windows Server 2025
* **Integrated Services:** DNS Server, Global Catalog (GC)
* **Upstream DNS Forwarders:** `8.8.8.8` (Google Public DNS), `1.1.1.1` (Cloudflare DNS)

---

## Implementation Steps (Server Manager GUI)

### 1. Role Installation
1. Opened **Server Manager** > **Manage** > **Add Roles and Features**.
2. Selected **Role-based or feature-based installation** targeting `WS25-DC01`.
3. Checked **Active Directory Domain Services** and accepted default management features.
4. Completed the wizard and executed the installation.

### 2. Domain Controller Promotion
1. Selected the notification flag in Server Manager and clicked **Promote this server to a domain controller**.
2. **Deployment Configuration:** Selected **Add a new forest** and set Root domain name to `tarikndc.com`.
3. **Domain Controller Options:** Configured DSRM restore password; verified **Domain Name System (DNS) server** and **Global Catalog (GC)** were selected.
4. **DNS Options:** Acknowledged the expected delegation warning for an isolated internal forest and proceeded.
5. **Additional Options:** Confirmed NetBIOS domain name populated as `TARIKNDC`.
6. **Paths:** Retained default database/log paths (`C:\Windows\NTDS`) and SYSVOL path (`C:\Windows\SYSVOL`).
7. **Prerequisites Check & Install:** Verified prerequisite validation passed and initiated deployment. The server automatically rebooted upon completion.

### 3. DNS Forwarders Configuration
Configured upstream recursive resolvers to ensure internal clients and the DC can resolve external internet domains:
1. Opened **Server Manager** > **Tools** > **DNS**.
2. Right-clicked server node **WS25-DC01** and selected **Properties**.
3. Navigated to the **Forwarders** tab and clicked **Edit**.
4. Added external public DNS IP addresses:
   * `8.8.8.8` (Primary Forwarder)
   * `1.1.1.1` (Secondary Forwarder)
5. Applied changes and saved configuration.

---

## Post-Installation Verification

### 1. Active Directory Services State
```powershell
Get-Service adws, ntds, kdc, netlogon, dns
