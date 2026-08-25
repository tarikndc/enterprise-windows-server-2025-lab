# Runbook 10: Native Windows LAPS Deployment, AD Schema Extension & Endpoint Credential Management

## Objective
Implement native **Windows Local Administrator Password Solution (LAPS)** on Windows Server 2025 (`WSDC01`) and Windows 11 client endpoints (`HOST01`). This automates the rotation, randomization, and encryption of built-in local administrator passwords in Active Directory, preventing lateral movement and Pass-the-Hash attacks across domain workstations.

---

## 1. Architectural Overview & Threat Mitigation

### The Security Vulnerability: Static Local Credentials
Without LAPS, organizations typically deploy a single shared local administrator password across all endpoints. If an attacker dumps password hashes from memory (LSASS) on a single compromised workstation, they immediately gain local administrative access to every other workstation across the enterprise.

```text
[Compromised Host: HOST01]
          │
          ▼ (Mimikatz memory dump / hash extraction)
[Exposed Local Admin Password: P@ssw0rd123]
          │
  ┌───────┴───────┬───────────────┐
  ▼               ▼               ▼
[HOST02]       [HOST03]       [HOST04]   <-- Complete lateral compromise
