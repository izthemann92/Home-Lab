## 🌐 Network Configuration (Updated to Match Completed Setup)

| Setting | Details |
|--------|---------|
| **Internal Network Name** | `Lab-net` |
| **Subnet** | `10.10.10.0/24` |
| **Gateway / Firewall** | pfSense VM |
| **pfSense WAN** | NAT (VirtualBox Adapter 1) |
| **pfSense LAN** | Internal Network (`Lab-net`) |
| **LAN Gateway IP** | `10.10.10.1` |
| **DHCP Server** | Enabled on pfSense (`10.10.10.100–200`) |
| **Internal VM IP Assignment** | **DHCP (automatic)** |
| **External Attackers** | None currently |
| **Internal Attacker** | Kali Linux (Lab-net) |
| **Internal Targets** | Ubuntu, Windows 11, Target3 Hack Box |

---

## 🧭 Current Network Diagram (Accurate to Active Lab)

```
===============================================================
                       pfSense Firewall
---------------------------------------------------------------
WAN: NAT (VirtualBox)          LAN: 10.10.10.1/24
DHCP Server: 10.10.10.100–200
===============================================================
                           |
                           v
---------------------------------------------------------------
               Internal Network: Lab-net (10.10.10.0/24)
---------------------------------------------------------------
      |                 |                   |                |
      v                 v                   v                v
+------------+   +------------+     +--------------+   +--------------+
|  Ubuntu    |   | Windows 11 |     |  Target3     |   |   Kali       |
|   DHCP     |   |   DHCP     |     |  Hack Box    |   | Internal Attacker |
+------------+   +------------+     +--------------+   +--------------+

```

---

## 🧩 Virtual Machine Inventory (Updated)

| VM Name | OS | vCPUs | RAM | Storage | Network Mode | IP Assignment | Purpose |
|--------|----|-------|------|---------|----------------|----------------|----------|
| **pfSense Firewall** | pfSense (FreeBSD) | 2 | 1–2 GB | 20 GB | WAN = NAT, LAN = Internal (`Lab-net`) | WAN = DHCP (VB) / LAN = 10.10.10.1 | Gateway, firewall, DHCP, NAT |
| **Ubuntu Server 22.04** | Linux | 2 | 2 GB | 40 GB | Internal Network (`Lab-net`) | DHCP from pfSense | Linux target for scanning & exploitation |
| **Windows 11 Pro** | Windows | 2 | 4 GB | 40 GB | Internal Network (`Lab-net`) | DHCP from pfSense | Windows workstation target |
| **Target3 VM** | Vulnerable Hack Box | 2 | 2 GB | 20–40 GB | Internal Network (`Lab-net`) | DHCP from pfSense | Vulnerability & exploit practice |
| **Kali Linux (Internal)** | Linux (Security) | 2 | 2 GB | 40 GB | Internal Network (`Lab-net`) | DHCP from pfSense | **Internal attacker** in isolated lab |

---

## 🧱 Network Role Summary (Updated)

| Function | Host / VM | Notes |
|----------|------------|-------|
| **Firewall / Gateway** | pfSense | Routes & filters traffic, manages DHCP |
| **DHCP Server** | pfSense | Issues IPs 10.10.10.100–200 |
| **LAN Gateway** | `10.10.10.1` | Used by all internal VMs |
| **Internal Network** | `Lab-net` | Fully isolated VirtualBox network |
| **Linux Target** | Ubuntu Server | Used for service testing & exploitation |
| **Windows Target** | Windows 11 | Client OS for scanning and attack practice |
| **Hack Box** | Target3 | Vulnerable VM for hacking |
| **Internal Attacker** | Kali Linux | Runs Nmap, Gobuster, Metasploit, etc. |
| **External Attackers** | None | (Can be added later if desired) |
| **Host PC** | Windows 11 | Runs VirtualBox; not part of Lab-net |

---

_Last updated: Nov 18, 2025 (Accurate to Active Environment)_
