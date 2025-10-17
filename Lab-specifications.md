# 🧩 Home Lab Documentation

## Overview
This repository tracks the setup, configuration, and ongoing development of my personal **IT Home Lab**, used for studying **CompTIA A+**, **Network+**, and **Security+** certifications, as well as gaining hands-on experience in virtualization, networking, and system administration.

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

## 🧠 Virtual Machine Lab Setup

## static IP Address assigned:
Windows 11: 192.168.10.11
ubuntu Server: 192.168.10.20

### 🪟 Win-Lab
Windows 11 (64-bit) – *Client Workstation for Networking and Troubleshooting Practice*

| Resource | Specification |
|-----------|----------------|
| **vCPU** | 2 Cores |
| **Memory** | 4 GB |
| **Storage** | 80 GB (VDI - Dynamic) |
| **Network** | Adapter 1: NAT (Internet)<br>Adapter 2: Internal Network `LAB-NET` |
| **Display** | 128 MB (VBoxSVGA) |
| **Notes** | TPM 2.0 & Secure Boot enabled. VirtualBox Guest Additions installed. |

---

### 🐧 UbuntuServer-Lab
Ubuntu Server 22.04 LTS – *Linux Server for CLI, SSH, and Networking Services*


| Resource | Specification |
|-----------|----------------|
| **vCPU** | 2 Cores |
| **Memory** | 2 GB |
| **Storage** | 25 GB (VDI - Dynamic) |
| **Network** | Adapter 1: NAT (Internet)<br>Adapter 2: Internal Network `LAB-NET` |
| **Display** | 16 MB (VMSVGA) |
| **Notes** | OpenSSH Server installed for remote access. Used for network practice, updates, and server roles. |

---

### 🐉 Kali-Lab *(In Progress)*
Kali Linux 2024.x (Xfce) – *Security and Network Testing Environment*

| Resource | Specification |
|-----------|----------------|
| **vCPU** | 2 Cores |
| **Memory** | 4 GB |
| **Storage** | 40 GB (VDI - Dynamic) |
| **Network** | Adapter 1: NAT<br>Adapter 2: Internal Network `LAB-NET` |
| **Display** | 64 MB (VMSVGA) |
| **Notes** | XFCE Desktop Environment; includes top security tools for testing and training. |

---

## 🌐 Network Topology

```plaintext
          [Internet]
              │
        (NAT Adapter)
              │
        ┌──────────────┐
        │  Host System │
        └──────────────┘
              │
      ┌────────────────────┐
      │ Internal Network:  │  "LAB-NET"
      │ 192.168.10.0/24    │
      └────────────────────┘
        ├── Win-Lab → 192.168.10.11
        ├── UbuntuServer-Lab → 192.168.10.20
        └── Kali-Lab → 192.168.10.30
