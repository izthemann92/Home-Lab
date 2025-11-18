# 🧩 Home Lab Documentation  
_A living document tracking the hardware and virtual machines used in my personal IT & Cybersecurity home lab._

This lab supports hands-on study for **CompTIA A+**, **Network+**, **Security+**, as well as practical experience in virtualization, Linux/Windows administration, and internal network testing.

---

## 🖥️ Host System (Main Hypervisor)

| Component | Specification |
|----------|--------------|
| **Device Name** | Blake-Desktop |
| **Operating System** | Windows 11 Pro |
| **Processor** | Intel Core i9-12900K (12th Gen, 3.20 GHz) |
| **Memory** | 32 GB DDR4 |
| **Storage** | NVMe SSD + Additional Drives |
| **Virtualization** | Intel VT-x / VT-d Enabled |
| **Hypervisor** | Oracle VirtualBox 7.x |
| **GPU** | RTX 4060 |

**Role:**  
The host system provides the compute and virtualization layer for the entire lab environment, running multiple VMs across an isolated internal network.

---

## 🧠 Virtual Machine Inventory  
_This section tracks every VM currently deployed inside the home lab, including compute resources and intended use._

All VMs below are attached to the **internal network (Lab-net)**, with pfSense acting as the gateway and DHCP server.

### 🔥 pfSense Firewall / Gateway  
| Resource | Specification |
|---------|--------------|
| **OS** | pfSense (FreeBSD-based) |
| **vCPU** | 2 |
| **Memory** | 1–2 GB |
| **Storage** | 20 GB |
| **Network** | Adapter 1: NAT (WAN) <br> Adapter 2: Internal Network `Lab-net` |
| **Purpose** | Firewall, DHCP server, LAN gateway, NAT, segmentation |

---

### 🐧 UbuntuServer-Lab  
Ubuntu Server 22.04 LTS — Linux administration, CLI training, service configuration.

| Resource | Specification |
|---------|--------------|
| **vCPU** | 2 |
| **Memory** | 2 GB |
| **Storage** | 40 GB |
| **Network** | Internal Network `Lab-net` |
| **Purpose** | Server administration practice, SSH, services, internal target |

---

### 🪟 Win-Lab (Windows 11 Pro)  
Windows 11 — client OS for troubleshooting, networking, and SMB testing.

| Resource | Specification |
|---------|--------------|
| **vCPU** | 2 |
| **Memory** | 4 GB |
| **Storage** | 40 GB |
| **Network** | Internal Network `Lab-net` |
| **Purpose** | Windows client testing, administrative labs, internal target |

---

### 🎯 Target3 – Vulnerable Hack Box  
A designated vulnerable machine used for safe exploitation, scanning, and Kali practice.

| Resource | Specification |
|---------|--------------|
| **OS** | Vulnerable VM (Hack Box) |
| **vCPU** | 2 |
| **Memory** | 2 GB |
| **Storage** | 20–40 GB |
| **Network** | Internal Network `Lab-net` |
| **Purpose** | Pen-testing practice, exploit testing, recon exercises |

---

### 🐉 Kali-Lab  
Kali Linux — internal attacker VM for tools, scanning, exploitation, and training.

| Resource | Specification |
|---------|--------------|
| **vCPU** | 2 |
| **Memory** | 4 GB |
| **Storage** | 40 GB |
| **Network** | Internal Network `Lab-net` |
| **Purpose** | Internal attacker simulation, enumeration, vulnerabilities research |

---

## 🧱 Network Membership Summary (No IP Details)

| VM | Connected Network | Notes |
|----|-------------------|-------|
| **pfSense** | Lab-net (LAN) + NAT (WAN) | Gateway & DHCP |
| **Ubuntu Server** | Lab-net | Internal target |
| **Windows 11** | Lab-net | Internal target |
| **Target3 Hack Box** | Lab-net | Vulnerable target |
| **Kali Linux** | Lab-net | Internal attacker |

---

## 📌 Notes  
- All VMs receive their IP addresses from the **pfSense DHCP server**  
- The entire Lab-net is fully isolated and safe for internal hacking practice  
- This file tracks **hardware + VM resources**, while network diagrams and full topology are documented separately  

---

_Last Updated: Nov 18, 2025_
