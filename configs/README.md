# ⚙️ Configs Folder
Store configuration files for VMs, networks, or services here.
# 🧪 Home Lab Configuration

## 🖥️ Host Machine (Physical System)
**System Name:** `Main-PC`  
**Operating System:** Windows 11 Pro  
**Purpose:** Primary workstation and host for virtualized lab environments  

**Specifications:**
- **Processor:** [fill in CPU model]
- **RAM:** [fill in total GB]
- **Storage:** [SSD/HDD details]
- **Network Adapter:** Intel / Realtek Gigabit Ethernet
- **Virtualization Platform:** Hyper-V (enabled) or VirtualBox
- **Static IP:** `192.168.1.10`
- **Subnet Mask:** `255.255.255.0`
- **Default Gateway:** `192.168.1.1`
- **DNS:** `8.8.8.8`, `1.1.1.1`

---

## 🐧 Virtual Machine 1 – Ubuntu Server

**System Name:** `ubuntuServer-Lab`  
**Operating System:** Ubuntu Server 22.04 LTS  
**Purpose:** Network services, SSH access, and connectivity verification.  
**Virtualization Platform:** VirtualBox  

### 🧰 Configuration
| Setting | Value |
|----------|-------|
| **vCPUs** | 2 |
| **RAM** | 4 GB |
| **Storage** | 40 GB (Dynamic) |
| **Network Adapter Mode** | [Confirm: Bridged or Internal?] |
| **Static IP** | `192.168.10.20` |
| **Subnet Mask** | `255.255.255.0` |
| **Gateway** | [Please confirm – likely `192.168.10.1`] |
| **DNS Servers** | [Confirm – external (`8.8.8.8`) or internal?] |
| **Primary User** | `izthemann` |

## 🪟 Virtual Machine 2 – Windows 11 Lab

**System Name:** `win11-lab01`  
**Operating System:** Windows 11 Pro (Evaluation)  
**Purpose:** Client-side testing, Active Directory prep, and network connectivity verification.  
**Virtualization Platform:** VirtualBox  

### 🧰 Configuration
| Setting | Value |
|----------|-------|
| **vCPUs** | 2 |
| **RAM** | 6 GB |
| **Storage** | 60 GB (Dynamic) |
| **Network Adapter Mode** | [Confirm: Bridged or Internal?] |
| **Static IP** | `192.168.10.11` |
| **Subnet Mask** | `255.255.255.0` |
| **Gateway** | [Please confirm – likely `192.168.10.1`] |
| **DNS Servers** | [Confirm: using `192.168.10.20` (Ubuntu) or external like `8.8.8.8`?] |
| **Workgroup / Domain** | `WORKGROUP` *(until AD setup)* |
| **Primary User** | `labadmin` |
| **Password** | 'Sigmanurho1992!'| 
