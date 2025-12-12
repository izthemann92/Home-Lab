# 🛠️ Arc Raiders System Freeze Diagnosis & Resolution

## 📌 Overview
This document outlines a **real-world hardware-level troubleshooting case** involving repeat system freezes when running **Arc Raiders** on a high-performance gaming PC. The issue was traced to **unsafe CPU power behavior** caused by motherboard default settings, resulting in **WHEA hardware errors** and full system lockups.

This case demonstrates skills in:
- Hardware diagnostics
- Power and thermal analysis
- BIOS configuration
- Log analysis (HWInfo + Windows Event Viewer)
- Root cause isolation and validation

---

## 🖥️ System Specifications
- **CPU:** Intel Core i9-12900K
- **Motherboard:** ASUS PRIME Z790-V WIFI
- **GPU:** NVIDIA RTX 4060
- **RAM:** 32 GB DDR4
- **OS:** Windows 11
- **Monitoring Tools:** HWInfo64, Windows Event Viewer

---

## 🚨 Problem Description

### Symptoms
- Full system freezes (no BSOD)
- Lockups occurring **only during or after Arc Raiders gameplay**
- System required hard reboot
- No application crash logs

### Initial Clues
- Windows Event Viewer logged **WHEA-Logger – Event ID 1**
- CPU temperatures appeared normal
- GPU temperatures and power draw were within spec

---

## 🔍 Investigation & Findings

### 1. Event Viewer Analysis
- **WHEA-Logger (Event ID 1)** indicated a **fatal hardware error**
- Confirmed the issue was occurring **below the OS/application layer**

### 2. HWInfo Monitoring (Critical Discovery)
During Arc Raiders gameplay:
- **CPU Package Power spiked to ~400W**
- Intel i9-12900K official boost limit is **~241W**
- No thermal throttling occurred due to short-duration spikes

➡️ Conclusion: **Electrical instability caused by unrestricted CPU power limits**

---

## ⚠️ Root Cause

The ASUS PRIME Z790-V WIFI motherboard ships with:
- **ASUS MultiCore Enhancement enabled by default**
- Intel power limits removed automatically

This allowed the CPU to:
- Exceed safe electrical limits
- Trigger WHEA hardware faults under Unreal Engine 5 workloads

Arc Raiders acted as the **trigger**, not the cause.

---

## ✅ Solution Implemented

### BIOS Configuration Changes

**BIOS Path:** `Advanced Mode → AI Tweaker`

- **ASUS MultiCore Enhancement:** Disabled (Enforce All Limits)
- **Intel Adaptive Boost Technology:** Disabled
- **PL1 (Long Duration Power):** 190 W
- **PL2 (Short Duration Power):** 190 W
- **Tau (Time Window):** 56 seconds

**Additional:**
- XMP disabled temporarily for validation

---

## 📊 Validation & Results

### Post-Fix HWInfo Metrics
- **CPU Package Power:** ≤ 190 W (stable)
- **CPU Temps:** ~50–60°C under load
- **VRM Temps:** ~37°C
- **No thermal throttling**
- **No WHEA-Logger events**

### Gameplay Testing
- Arc Raiders played for extended sessions
- No freezes during or after gameplay
- System stability fully restored

---

## 🎯 Key Takeaways

- Motherboard defaults are **not always safe**, even on premium hardware
- WHEA errors often indicate **power or signal instability**, not software bugs
- Unreal Engine 5 workloads can expose hidden hardware misconfigurations
- Proper power limiting can dramatically improve stability with **negligible performance loss**

---

## 🧠 Skills Demonstrated
- Hardware-level troubleshooting
- BIOS power management
- Interpreting WHEA hardware errors
- Log analysis (HWInfo CSV, Event Viewer)
- Root cause analysis & validation
- Documentation for reproducibility

---

## 📁 Artifacts
- HWInfo sensor logs (CSV)
- Event Viewer screenshots
- BIOS configuration screenshots

---

## ✅ Final Outcome
The system was stabilized **without replacing hardware**, solely through:
- Correct diagnosis
- Power behavior correction
- Data-driven validation

This case highlights practical, hands-on problem-solving applicable to **IT support, systems administration, and hardware-focused roles**.

