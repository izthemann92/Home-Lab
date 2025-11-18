---
title: "Lab 2.6 – SOHO Firewall and Port Forwarding (Finalized Setup Guide)"
author: "Blake Mann"
date: "2025-10-11"
difficulty: Intermediate
lab_type: Networking / Security
objectives:
  - Configure pfSense as a virtual gateway and firewall
  - Create an isolated internal lab network (`Lab-net`)
  - Add Kali as an external attacker from the host/bridged network
  - Validate connectivity and simulate external attack through pfSense
---

# 🧪 Lab 2.6 – SOHO Firewall and Port Forwarding

## ✅ Overview
This lab creates a secure, isolated network where **Kali Linux** (attacker) connects from the host/bridged network into a private lab environment through **pfSense**, simulating external attacks in a controlled environment.

---

## 🧭 Network Layout

```
[Host PC / Kali (Bridged)]
          |
      [pfSense]
  WAN (NAT to host)
  LAN (10.10.10.1/24)
          |
  ---------------------------
  |         |         |
[Ubuntu] [Win11] [Target3]
10.10.10.20 10.10.10.30 10.10.10.40
```

---

## ⚙️ Step-by-Step Guide

### 🧩 Step 1 — Create pfSense VM
- [x] Download pfSense ISO and create new VM.
- [x] **Adapter 1:** NAT → pfSense WAN
- [x] **Adapter 2:** Internal Network → Name: `Lab-net`
- [x] Boot and install pfSense.
- [x] Set **LAN IP:** 10.10.10.1/24
- [x] Enable **DHCP** on LAN (range 10.10.10.100–200).

### 🧩 Step 2 — Configure Targets (Ubuntu + Windows)
- [x] Attach both VMs to `Lab-net` internal network.
- [x] Confirm IPs via DHCP or set static:
  - Ubuntu: 10.10.10.20
  - Windows: 10.10.10.30
- [x] Ping pfSense gateway (10.10.10.1) to confirm connectivity.

### 🧩 Step 3 — Create Kali (Attacker)
- [x] Create Kali VM (Bridged adapter to host network).
- [x] Update and install tools:
  ```bash
  sudo apt update && sudo apt full-upgrade -y
  sudo apt install -y nmap tcpdump
  ```

### 🧩 Step 4 — Create VirtualBox Port Forwarding (Host → pfSense WAN)
1. pfSense → Settings → Network → Adapter 1 (NAT) → Advanced → Port Forwarding.
2. Add rules:
   | Name | Protocol | Host Port | Guest Port |
   |-------|-----------|------------|-------------|
   | pf-ssh | TCP | 2222 | 2222 |
   | pf-http | TCP | 8080 | 8080 |

### 🧩 Step 5 — pfSense NAT Rules (WAN → LAN Target)
1. pfSense Web UI → **Firewall → NAT → Port Forward → Add**
2. Example SSH rule:
   - Interface: WAN
   - Protocol: TCP
   - Destination: WAN address
   - Destination Port: 2222
   - Redirect IP: 10.10.10.20
   - Redirect Port: 22
   - Description: Host 2222 → 10.10.10.20:22
3. Save & Apply.

### 🧩 Step 6 — Test Connectivity
- From **Kali (bridged)**, test SSH through pfSense:
  ```bash
  ssh -p 2222 user@127.0.0.1
  ```
- From **Ubuntu**, verify response to pfSense ping:
  ```bash
  ping 10.10.10.1
  ```

### 🧩 Step 7 — Snapshot and Documentation
- [x] Snapshot all VMs after configuration.
- [x] Snapshot again before and after attack simulation.
- [x] Record verification screenshots and logs.

---

## 🧾 Verification Checklist

| Task | Status |
|------|--------|
| pfSense Installed | ☑️ |
| Internal Network Configured | ☑️ |
| Static/DHCP IPs Assigned | ☑️ |
| Kali Configured (Bridged) | ☑️ |
| pfSense NAT Rules Created | ☑️ |
| Connection Verified (SSH/HTTP) | ☑️ |
| Snapshots Taken | ☑️ |

---

## 🧠 Reflection & Notes
- pfSense effectively isolates and controls all ingress/egress traffic.
- Kali simulates external adversary behavior through NAT translation.
- Reverting snapshots maintains a safe testing cycle.
- This setup provides a reusable framework for future A+ Core 1 and security labs.

---

**End of Lab Report**  
© 2025 Blake Mann | Home Lab Project
