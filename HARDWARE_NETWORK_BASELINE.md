# 🧰 Home Lab Hardware & Network Baseline

This document serves as the master reference for the hardware, network topology, and virtual machine configurations used in the **Home Lab** project.

---
## 🖥️ Host System
| Component | Specification |
|------------|----------------|
| **Device Name** | Blake-Desktop |
| **Processor** | Intel Core i9-12900K (12th Gen, 3.20 GHz) |
| **Installed RAM** | 32 GB DDR4 (31.7 GB usable) |
| **System Type** | 64-bit Operating System, x64-based processor |
| **Virtualization** | Intel VT-x / VT-d Enabled |
| **Hypervisor** | Oracle VirtualBox 7.x |
| **Operating System** | Windows 11 Pro |
---

## 🌐 Network Configuration

| Setting | Details |
|----------|----------|
| **Internal Network Name** | `Lab-net` |
| **Subnet** | `192.168.10.0/24` |
| **Adapter 1** | Bridged Adapter (WAN access) |
| **Adapter 2** | Internal Network (`Lab-net`) |
| **DHCP** | Disabled — Static IPs assigned manually |

### Example Network Diagram
```
[Host PC/Bridged Internet]
          │
          ▼
   ┌───────────────────┐
   │  VirtualBox Host  │
   └───────────────────┘
        │ (Lab-net)
 ┌────────────┬────────────┐
 │            │            │
 ▼            ▼            ▼
Ubuntu Server  Windows 11  (Kali Planned)
192.168.10.20  192.168.10.11  TBD
```

---

## 🧩 Virtual Machine Inventory

| VM Name | OS | vCPUs | RAM | Storage | Network Mode | Static IP | Purpose |
|----------|----|--------|------|-----------|----------------|-------------|-----------|
| **Ubuntu Server 22.04** | Linux (Server) | 2 | 2 GB | 40 GB | Internal + Bridged | `192.168.10.20` | File, DHCP/DNS, and network services |
| **Windows 11 Pro** | Windows | 2 | 4 GB | 40 GB | Internal + Bridged | `192.168.10.11` | Client testing and user management |
| **Kali Linux** | Linux (Security) | 2 | 2 GB | 40 GB | Bridged (Attacker) | TBD | Pen-testing and external attack simulations |

---
## 🧱 Network Role Summary

| Function | Host / VM | Notes |
|-----------|------------|-------|
| **Gateway (WAN)** | Host (Bridged) | Provides Internet to VMs |
| **Internal Network** | Lab-net | Segregated environment for study |
| **DNS / File Services** | Ubuntu Server | Configured manually |
| **Windows Client** | Windows 11 Pro | Used for remote access and SMB testing |
| **Security Node** | Kali Linux | Isolated attacker environment |

---

_Last updated: Oct 11, 2025_
