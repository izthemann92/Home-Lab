---
title: Mr.Robot Hack box
author: Blake Mann
repo: izthemann92/Home-Lab
version: 1.0
---

# 🧪 Mr.Robot 
In this lab assignment we will be downloading Mr.Robot vm to use as a simulated target.
CTF 

---

## 🎯 Objective
This VM has three keys hidden in different locations. Your goal is to find all three. Each key is progressively difficult to find.

The VM isn't too difficult. There isn't any advanced exploitation or reverse engineering. The level is considered beginner-intermediate.



---

## 🔧 Lab Procedure

### Step 1 — Run Nmap (kali)

```bash
nmap 10.10.10.100-200
Starting Nmap 7.95 ( https://nmap.org ) at 2025-11-06 13:03 EST
Nmap scan report for 10.10.10.103
Host is up (0.00042s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE  SERVICE
22/tcp  closed ssh
80/tcp  open   http
443/tcp open   https
MAC Address: 08:00:27:48:75:1E (PCS Systemtechnik/Oracle VirtualBox virtual NIC)

```bash

<details>
<summary> </summary>

```bash
# Replace with your actual commands
sudo apt update
sudo apt install -y nmap
nmap -sV 192.168.10.0/24
```
</details>

<details>
<summary>🪟 Example – Windows Commands</summary>

```powershell
# Replace with Windows equivalent
ipconfig /all
Test-NetConnection 8.8.8.8
```
</details>

### Step 2 — Continue the Lab
- Include screenshots as needed.
- Mention expected results or output indicators.

---

## ✅ Completion Checklist
- [x] flag1: 073403c8a58a1f80d943455fb30724b9
- [] flag2:
- [] flag3:  

📸 **Screenshot Evidence:** Add proof of command outputs, GUI confirmations, or configuration screens.

---

## 🧾 Reflection
> Summarize what you learned or observed.  
> Describe any issues encountered and how you solved them.  
> Note one real-world use case for this skill.

---

## 🧩 Version Control
- Version: 1.0  
- Linked Curriculum: _(Add relevant Professor Messer domain/topic here)_  
- Last Updated: _{{ date }}_

---

