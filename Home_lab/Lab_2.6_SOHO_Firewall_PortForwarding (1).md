---
title: "Lab 2.6 – SOHO Firewall and Port Forwarding (Finalized Setup Guide)"
author: "Blake Mann"
date: "2025-10-11"
difficulty: Intermediate
lab_type: "Networking / Security"
objectives:
  - Configure pfSense as a virtual gateway and firewall
  - Create an isolated internal lab network (Lab-net)
  - Add Kali as an external attacker (bridged)
  - Add Kali as an internal attacker VM inside Lab-net
  - Validate connectivity and simulate external attacks through pfSense
---

# 🧪 Lab 2.6 – SOHO Firewall and Port Forwarding  
This lab recreates a realistic SOHO network where **pfSense** protects an isolated subnet and **Kali Linux** launches controlled external attack traffic through the pfSense WAN interface.

---

# 🧭 Network Diagram (Final)

```mermaid
flowchart TB

    classDef router fill:#444,stroke:#000,color:#fff,font-weight:bold;
    classDef pfsense fill:#8b0000,stroke:#000,color:#fff,font-weight:bold;
    classDef device fill:#1e90ff,stroke:#000,color:#fff,font-weight:bold;
    classDef server fill:#2e8b57,stroke:#000,color:#fff,font-weight:bold;

    EXT_KALI[External Kali<br>(Bridged to Host Network)]:::device
    HOSTNET[(Home/Host Network<br>DHCP from ISP Router)]:::router

    PFS[pfsense Firewall<br>WAN = NAT (VirtualBox)<br>LAN = Lab-net 10.10.10.1/24]:::pfsense

    LABNET[(Lab-net<br>10.10.10.0/24)]:::router

    UB[Ubuntu Server<br>10.10.10.20]:::server
    WIN[Windows 11<br>10.10.10.30]:::device
    TGT3[Target3 VM<br>10.10.10.40]:::device
    INT_KALI[Internal Kali<br>10.10.10.50]:::device

    EXT_KALI --- HOSTNET
    HOSTNET --- PFS
    PFS --- LABNET
    LABNET --- UB
    LABNET --- WIN
    LABNET --- TGT3
    LABNET --- INT_KALI
```

---

# ⚙️ Step-by-Step Setup Guide

## 🧩 Step 1 — Create the pfSense VM
- [x] Download pfSense ISO.
- [x] VirtualBox → New → Type: BSD → Version: FreeBSD (64-bit)
- [x] Attach 2 adapters:
  - **Adapter 1 (WAN):** NAT  
  - **Adapter 2 (LAN):** Internal Network → `Lab-net`
- [x] Install pfSense normally.
- [x] Set LAN IP → `10.10.10.1/24`.
- [x] Enable DHCP on LAN:  
  ```
  Start: 10.10.10.100
  End:   10.10.10.200
  ```

---

## 🧩 Step 2 — Configure Internal Targets  
Attach Ubuntu, Windows, and Target3 to `Lab-net`:

| VM | Role | Static IP |
|----|-------|-----------|
| Ubuntu | Server | 10.10.10.20 |
| Windows 11 | Workstation | 10.10.10.30 |
| Target3 | Optional vuln box | 10.10.10.40 |

Test connections:

```bash
ping 10.10.10.1
```

---

## 🧩 Step 3 — Kali Linux (External Attacker)
- [x] Create a Kali VM  
- [x] Adapter: **Bridged Adapter** → Host NIC  
- [x] Update tools:

```bash
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y nmap gobuster tcpdump
```

Kali receives an IP from your **real router**, not Lab-net.

---

## 🧩 Step 4 — Kali Linux (Internal Attacker)
This VM simulates an internal threat actor.

- Adapter: **Internal Network → Lab-net**
- Suggested IP: `10.10.10.50`

Update tools as above.

---

## 🧩 Step 5 — VirtualBox Port Forwarding (Host → pfSense WAN)
Required so that **external Kali** can reach pfSense WAN services.

VirtualBox → pfSense → Settings → Network → Adapter 1 → Advanced → Port Forwarding

| Name    | Protocol | Host Port | Guest Port | Purpose |
|---------|----------|-----------|------------|----------|
| pf-ssh  | TCP      | 2222      | 22         | SSH to LAN targets |
| pf-web  | TCP      | 8080      | 80         | Web access to LAN targets |

---

## 🧩 Step 6 — pfSense NAT Rules (WAN → LAN)
Navigate:  
**pfSense → Firewall → NAT → Port Forward → Add**

Example: Forward WAN:2222 → Ubuntu:22

- Interface: WAN  
- Protocol: TCP  
- Destination: WAN Address  
- Destination port: 2222  
- Redirect target IP: `10.10.10.20`  
- Redirect port: 22  
- Description: `External SSH → Ubuntu`  

Click **Save** & **Apply Changes**.

---

## 🧩 Step 7 — Test Connectivity

### ✔️ From External Kali (Bridged):
Test SSH into internal Ubuntu through pfSense NAT:

```bash
ssh -p 2222 user@<pfSense_WAN_IP>
```

Your pfSense WAN IP is listed under **Status → Interfaces**.

### ✔️ From Ubuntu/Windows:
Confirm LAN routing:

```bash
ping 10.10.10.1
```

### ✔️ From Internal Kali:
Try scanning the network:

```bash
nmap -sn 10.10.10.0/24
```

---

# 🧾 Verification Checklist

| Task | Status |
|------|--------|
| pfSense Installed | ☑️ |
| Lab-net Configured | ☑️ |
| Internal Static/DHCP IPs Assigned | ☑️ |
| External Kali (Bridged) Setup | ☑️ |
| Internal Kali Added | ☑️ |
| VirtualBox Port Forwarding | ☑️ |
| pfSense NAT Rules | ☑️ |
| Connectivity Verified | ☑️ |
| Snapshots Created | ☑️ |

---

# 🧠 Reflection & Notes

- pfSense successfully acts as a **SOHO gateway** with NAT + firewall rules.  
- Kali (bridged) provides **external adversary simulation**.  
- Internal Kali provides **insider threat simulation**.  
- This lab builds directly toward **CompTIA A+, Network+, Security+** practical training.  
- Snapshots ensure safe rollback during exploitation and recon tests.  

---

**End of Lab Report**  
© 2025 Blake Mann | Home Lab Project
