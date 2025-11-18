# 🧪 Lab 01 - Static IP Configuration and Connectivity

## 🎯 Objective
Set static IP addresses on both host and Ubuntu Server VM, and verify communication between the two systems.

## ⚙️ Environment Setup
| Component | Details |
|------------|----------|
| Host OS | Windows 11 Pro |
| Virtualization | VirtualBox 7.0 |
| VM OS | Ubuntu Server 24.04 LTS |
| Network Mode | Host-Only Adapter |
| Host IP | 192.168.56.1 |
| Ubuntu IP | 192.168.56.10 |

## static ips assigned
windows ip - 192.168.10.11
ubuntu ip: 192.168.10.20


## 🧩 Steps Performed
1. Configured Host-Only Adapter in VirtualBox.
2. Modified Ubuntu network config file:
   ```bash
   sudo nano /etc/netplan/00-installer-config.yaml

Troubleshooting notes: 
## Troubleshooting notes:
initially lost connectivity after applying netplan due to wrong gateway.