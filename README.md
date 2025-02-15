# Active Directory Lab
This repository contains a **simulated Active Directory (AD) environment** for learning **Windows security monitoring, attack detection, and forensic analysis**. The setup includes **Windows Server, Virtual Machines, Splunk, Sysmon, and Atomic Red Team**.

## Table of Contents
- [Setup Requirements](#setup-requirements)
- [Installation Steps](#installation-steps)
- [Folder Overview](#folder-overview)
- [Tools Used](#tools-used)

---

## Setup Requirements
To replicate this lab, you will need:
- VirtualBox (or VMware)
- Windows Server 2019/2022
- Windows 10/11 VM (Client Machine)
- Kali Linux (Attacker Machine)
- Splunk
- Sysmon
- Atomic Red Team

---

## Installation Steps
1. Set up Virtual Machines in VirtualBox or VMware.
2. Configure Active Directory (AD) on Windows Server.
3. Install Sysmon for endpoint monitoring.
4. Deploy Splunk for log collection.
5. Run Atomic Red Team attacks to generate logs.
6. Analyze logs using Splunk dashboards.

---

## Folder Overview
| Folder | Description |
|--------|------------|
| `Brute-Force-Attack` | Documents a brute-force RDP attack and log analysis in Splunk. |
| `Network_setup` | Contains network configuration files for the lab. |
| `Splunk-Config` | Splunk configurations for parsing Windows event logs. |
| `Sysmon-Config` | Custom Sysmon configuration file. |
| `Sysmon` | Sysmon installation files. |
| `VirtualBox-Setup` | Instructions for setting up VMs in VirtualBox. |

---

## Tools Used
- Windows Server AD - Active Directory environment setup.
- Sysmon - Windows system monitoring.
- Splunk - Log collection and analysis.
- Atomic Red Team - Simulating real-world attacks.

---

## Next Steps
- Explore individual folders for detailed documentation.
- Follow the setup guide to build your own Active Directory lab.
