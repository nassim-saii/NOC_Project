# Network Operations Center (NOC) – Open Source Implementation

## 📌 Project Overview
This project presents the design and implementation of a complete **Network Operations Center (NOC)** in a simulated enterprise environment.  
It integrates monitoring, security, centralized logging, and incident management using open-source tools.

The infrastructure is deployed and tested using **GNS3** and **VMware Workstation**, simulating a real-world enterprise network with VLAN segmentation and security controls.

## 🎯 Objectives
- Centralized monitoring of network devices and servers
- Real-time detection of failures and security incidents
- Centralized log collection and analysis
- Structured incident and asset management
- Simulation of an enterprise-grade NOC architecture

## 🏗️ Architecture Overview
The network is segmented into multiple VLANs:

| VLAN | Name        | Network           | Purpose |
|-----:|------------|------------------|---------|
| 10  | Management | 172.16.2.0/24    | Admin access, monitoring tools |
| 20  | DMZ        | 172.16.1.0/24    | NOC servers |
| 30  | LAN1       | 172.16.3.0/24    | User clients |
| 40  | LAN2       | 172.16.4.0/24    | Additional clients |

Key components:
- **pfSense**: Firewall, VLAN routing, DHCP, NAT
- **Zabbix**: Performance & availability monitoring
- **Wazuh**: Security monitoring & centralized logging
- **Snort**: Intrusion Detection System (IDS)
- **GLPI**: IT asset management & ticketing

Architecture diagrams are available in the `diagrams/` directory.

## 🧰 Technologies Used
- pfSense
- Zabbix
- Wazuh
- Snort
- GLPI
- Ubuntu Server 22.04
- GNS3
- VMware Workstation

## 🖥️ Environment
| Component | OS | Role |
|---------|----|------|
| Wazuh v4.14.1 OVA | 22.04 | Wazuh Server |
| Ubuntu Server | 22.04 | Zabbix Server |
| Ubuntu Server | 22.04 | GLPI + MariaDB |
| pfSense | FreeBSD | Firewall & Router |
| Clients | Windows / VPCS | End-user simulation |

## 🧪 Testing & Validation
The infrastructure was validated through:
- VLAN connectivity tests
- DHCP assignment verification
- Zabbix performance alerts
- Snort intrusion detection (scan, ICMP flood)
- Centralized log validation in Wazuh
- Ticket creation and resolution in GLPI

Detailed test cases are documented in the `tests/` directory.

## 📂 Repository Structure
- `docs/` – Project documentation
- `diagrams/` – Network and technical diagrams
- `configs/` – Tool configuration references
- `gns3/` – GNS3 project files
- `tests/` – Validation and testing procedures
- `report/` – Full academic report (PDF)

## 👨‍🎓 Authors
- **Saii Nassim**
- **Abidli Roudaina**

Supervisor: **Taker Hadiji**  
Class: **ING-5-SSIR-B**  
Academic Year: **2025–2026**

## 📜 License
This project is for academic and educational purposes.
