# Active Directory Lab

This repository contains a **simulated Active Directory (AD) environment** designed for **learning Windows security monitoring, attack detection, and forensic analysis**.  
It provides hands-on experience with **defensive logging, attacker techniques, and Splunk-based threat detection**.

## Table of Contents
- [Lab Overview](#lab-overview)
- [Setup Requirements](#setup-requirements)
- [Installation Steps](#installation-steps)
- [Folder Overview](#folder-overview)
- [Tools Used](#tools-used)
- [Next Steps](#next-steps)
- [Acknowledgments](#acknowledgments)

---

## Lab Overview
This lab is designed to simulate **real-world attacks and detections** in an enterprise Windows network. The environment includes:
- **Active Directory (AD)** with organizational units, user accounts, and security policies.
- **Logging & Monitoring** using **Sysmon** and **Windows Event Logs**, with centralized collection in **Splunk**.
- **Simulated Attacks** via **Crowbar (Brute Force) and Atomic Red Team (MITRE ATT&CK techniques)**.
- **Threat Detection & Analysis** using **Splunk queries** to detect suspicious activity.

---

## Setup Requirements
To replicate this lab, you will need:
- **Virtualization Software**: VirtualBox (or VMware)
- **Operating Systems**:
  - Windows Server 2019/2022 (Domain Controller)
  - Windows 10/11 (Client Machine)
  - Kali Linux (Attacker Machine)
- **Security & Monitoring Tools**:
  - Splunk (SIEM & Log Aggregation)
  - Sysmon (System Monitoring)
  - Windows Event Logs (Security Logs)
  - Atomic Red Team (Attack Simulation)
  - Crowbar (Brute Force Testing)
  - MITRE ATT&CK Framework (Tactics & Techniques Reference)

---

## Installation Steps
1. **Set up Virtual Machines** in VirtualBox or VMware.
2. **Configure Active Directory** on Windows Server:
   - Set up **Organizational Units (OUs)**
   - Create **User Accounts**
   - Implement **Domain Policies**
3. **Install Sysmon** on Windows endpoints to enable advanced logging.
4. **Deploy Splunk** and configure **log ingestion**.
5. **Perform Attack Simulations**:
   - **Brute Force Attack** using Crowbar (RDP attack simulation).
   - **MITRE ATT&CK Techniques** with Atomic Red Team.
6. **Analyze Logs in Splunk**:
   - Query Windows Event Logs & Sysmon logs for attack traces.
   - Detect and correlate security events.

---

## Folder Overview
| Folder | Description |
|--------|------------|
| `Active-Directory-Setup` | Instructions for setting up AD, creating users, and configuring the domain. |
| `Brute-Force-Attack` | Documents a brute-force RDP attack using Crowbar and log analysis in Splunk. |
| `Network_Setup` | Contains network configuration files for the lab. |
| `Splunk-Config` | Configuration files for ingesting Windows Event Logs and Sysmon logs. |
| `Sysmon-Config` | Custom Sysmon configuration for enhanced logging. |
| `Atomic-Red-Team` | MITRE ATT&CK-based attack simulations and Splunk queries. |
| `VirtualBox-Setup` | Instructions for setting up VMs and snapshots in VirtualBox. |

---

## Tools Used
### **Security Monitoring & SIEM**
- **Windows Event Logs** - Native security logs from Windows.
- **Sysmon** - Advanced event logging and process tracking.
- **Splunk** - Log collection, query, and analysis.

### **Attack Simulation**
- **Crowbar** - Brute force tool for testing password strength (RDP attack).
- **Atomic Red Team** - Simulated attacks mapped to the **MITRE ATT&CK Framework**.

### **Networking & Environment Setup**
- **Active Directory (Windows Server)** - Domain Controller with OUs and policies.
- **Kali Linux** - Attacker machine for testing various security tools.
- **VirtualBox** - Virtualization platform for the lab environment.

---

## Next Steps
- Explore individual folders for **detailed documentation** and step-by-step guides.
- Run **additional Atomic Red Team techniques** and test how different attacks generate logs.
- Create **custom Splunk dashboards** to visualize attack patterns.
- Map **MITRE ATT&CK techniques to detections** and refine security policies.

> Inspired by techniques demonstrated in various **Active Directory security research projects**.
