# Runbook 09: Workstation Admin Logon Restrictions & Credential Protection via User Rights Assignment GPO

## Objective
Harden domain security on Windows Server 2025 (`WS25-DC01`) by enforcing the Tiered Administrative Model. Implement **User Rights Assignment** policies via Group Policy to explicitly prevent Tier 0 (Domain / Enterprise Admins) and Tier 1 (Server Admins) accounts from logging into standard client workstations (`guest01`). This mitigates credential harvesting (e.g., Mimikatz LSASS memory dumping) and prevents lateral movement from compromised endpoints to critical domain infrastructure.

---

## 1. Threat Model & Security Rationale

### The Attack Vector: LSASS Memory Harvesting
When any user logs into a Windows endpoint interactively or via Remote Desktop Services (RDP), the Local Security Authority Subsystem Service (`lsass.exe`) caches authentication material (Kerberos Ticket Granting Tickets, NTLM hashes, and session tokens) in memory.

```text
[Phishing / Web Exploit]
         │
         ▼
[Compromised Client (guest01)]
         │
         ▼ (Domain Admin logs in to troubleshoot)
[LSASS Memory Dump via Mimikatz]
         │
         ▼
[Tier 0 Golden / Kerberos Credentials Stolen]
         │
         ▼
[Complete Forest / Domain Takeover]
