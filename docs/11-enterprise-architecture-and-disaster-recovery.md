# Runbook 11: Enterprise Service Placement, Active Directory Recycle Bin & Bare Metal Disaster Recovery

## Objective
Establish enterprise infrastructure standards for network service placement (DNS and DHCP integration), implement granular object-level recovery via the Active Directory Recycle Bin, and deploy scheduled Bare Metal Backups for total server disaster recovery on Windows Server 2025 (`WSDC01`).

---

## 1. Enterprise Architecture & Service Placement Standards

### DNS vs. DHCP Placement Strategy
In an enterprise branch or corporate environment with an edge firewall/router and an Active Directory Domain Controller (AD DC), placement of critical network services follows strict operational boundaries:

```text
[ Internet / Uplink ]
          │
[ Edge Firewall / Router ]  <─── (Handles WAN routing, NAT, Guest/IoT DHCP)
          │
[ Core Switch ]  <────────────── (Forwards Staff DHCP via IP Helper / DHCP Relay)
          │
    ┌─────┴─────────────────────────┐
    ▼                               ▼
[ Windows AD DC: WSDC01 ]      [ Corporate Workstations: HOST01 ]
 ├── Primary DNS Provider       ├── Assigned IP via DHCP (Option 003: Router Gateway)
 ├── AD-Integrated DNS Zones    ├── DNS: Pointed strictly to WSDC01 (Option 006)
 └── Staff DHCP / Dynamic DNS   └── Authentication: Kerberos / NTLM to DC
