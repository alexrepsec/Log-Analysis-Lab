# Wazuh-SIEM-Homelab

## Objective

This project demonstrates the deployment of a **Wazuh SIEM (Security Information and Event Management)** in a home lab environment using VMware Workstation. The lab covers the full setup of a Wazuh Manager on Ubuntu Server, agent deployment on a Windows 11 host, and real-time **File Integrity Monitoring (FIM)** using Wazuh's Syscheck module.

### Skills Learned

- Deploying a fully functional SIEM in a virtualized home lab environment 
- Configuring VMware NAT networking for VM-to-host communication 
- Installing and configuring Wazuh all-in-one stack on Ubuntu Server 
- Registering and authenticating Windows endpoints as Wazuh agents 
- Implementing real-time File Integrity Monitoring using Wazuh Syscheck 
- Analyzing security events through the Wazuh web dashboard

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## 🧰 Technologies Used

- **Wazuh 4.9.2** — Open-source SIEM & XDR platform
- **Ubuntu Server 22.04 LTS** — Wazuh Manager host OS
- **Windows 11 Pro** — Monitored endpoint (Wazuh Agent)
- **VMware Workstation** — Virtualization platform
- **OpenSearch** — Wazuh Indexer backend
- **Wazuh Dashboard** — Web-based visualization interface

---

## ⚙️ Environment Setup

### Virtual Machine Specifications

| Parameter | Value |
|---|---|
| OS | Ubuntu Server 22.04.4 LTS |
| RAM | 4 GB |
| CPU | 2 cores |
| Storage | 50 GB (LVM) |
| Network | VMware NAT (VMnet8) |

### Prerequisites

- VMware Workstation installed
- Ubuntu Server 22.04 ISO
- Internet access on the VM
- Administrative access on Windows host

Example below.

## 🏗️ Lab Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     HOST MACHINE                         │
│                  Windows 11 Pro                          │
│              IP: 192.168.248.1                           │
│                                                          │
│   ┌──────────────────┐        ┌──────────────────────┐  │
│   │   Wazuh Agent    │        │   Web Browser        │  │
│   │   v4.9.2         │──────► │   Dashboard Access   │  │
│   │   (ossec-agent)  │        │   https://           │  │
│   └────────┬─────────┘        │   192.168.248.132    │  │
│            │                  └──────────────────────┘  │
│            │ VMware NAT (VMnet8)                         │
│            ▼                                             │
│   ┌──────────────────────────────────────────────────┐  │
│   │           VMware Virtual Machine                  │  │
│   │           Ubuntu Server 22.04 LTS                 │  │
│   │           IP: 192.168.248.132                     │  │
│   │                                                    │  │
│   │   ┌────────────┐ ┌───────────┐ ┌──────────────┐  │  │
│   │   │   Wazuh    │ │  Wazuh    │ │    Wazuh     │  │  │
│   │   │  Manager   │ │  Indexer  │ │  Dashboard   │  │  │
│   │   │            │ │(OpenSearch│ │  (port 443)  │  │  │
│   │   └────────────┘ └───────────┘ └──────────────┘  │  │
│   └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘

```

| Component | Host | IP | Role |
|---|---|---|---|
| Wazuh Manager | Ubuntu Server 22.04 (VMware) | 192.168.248.132 | Collects, analyzes and stores security data |
| Wazuh Agent | Windows 11 Pro (Host) | 192.168.248.1 | Sends logs and system events to the manager |

---
