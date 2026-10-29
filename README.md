# NETWORKWALKS-B084I-WK1-CYBERSECURITY-LAB-SETUP
Cybersecurity Lab Setup
🛡️ Virtual Cybersecurity Lab | Kali Linux & VirtualBox

<p align="center">
<img src="https://img.shields.io/badge/CYBERSECURITY-HOME%20LAB-111827?style=for-the-badge&logo=kalilinux&logoColor=white" alt="Cybersecurity Lab"/>
<img src="https://img.shields.io/badge/PLATFORM-VirtualBox-1E70C1?style=for-the-badge&logo=virtualbox&logoColor=white" alt="VirtualBox"/>
<img src="https://img.shields.io/badge/OS-Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white" alt="Kali Linux"/>
<img src="https://img.shields.io/badge/OS-Parrot%20OS-15AABF?style=for-the-badge&logo=parrotsecurity&logoColor=white" alt="Parrot OS"/>
<img src="https://img.shields.io/badge/OS-Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white" alt="Ubuntu"/>
</p>

<p align="center">
<b>A hands-on virtual lab for learning Linux administration, network security, and ethical hacking in a controlled environment.</b>
</p>

<p align="center">
<img src="https://img.shields.io/badge/Project-01-C62828?style=flat-square" alt="Project 01"/>
<img src="https://img.shields.io/badge/Focus-Network%20Security-008577?style=flat-square" alt="Network Security"/>
<img src="https://img.shields.io/badge/Environment-Virtual%20Lab-6A5ACD?style=flat-square" alt="Virtual Lab"/>
<img src="https://img.shields.io/badge/Practice-Ethical%20Hacking-E87500?style=flat-square" alt="Ethical Hacking"/>
</p>

📖 About the Project

This project documents my hands-on experience building a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux.

The lab provides a dedicated environment for exploring Linux networking, security tools, network discovery, packet analysis, and authorized penetration-testing exercises.

The initial setup consists of a Kali Linux virtual machine connected to a dedicated VirtualBox NAT Network. The architecture can be expanded with additional Linux distributions and deliberately vulnerable target machines for future exercises.

The repository includes configuration details, screenshots, verification commands, troubleshooting notes, and lessons learned throughout the setup process.

🎯 Project Objectives
Install and configure Oracle VirtualBox.
Import and configure Kali Linux.
Create a dedicated NAT Network for lab virtual machines.
Configure and verify IPv4 networking.
Test gateway connectivity and DNS resolution.
Create a clean recovery snapshot.
Document configuration issues and troubleshooting steps.
Prepare a foundation for future cybersecurity projects.
🏗️ Lab Architecture

<p align="center">
<img src="1-screenshot-title-image.png" alt="Virtual Cybersecurity Lab Architecture" width="850"/>
</p>

Network Topology
text
                    HOST SYSTEM
                     Windows 10
                         |
                  Oracle VirtualBox
                         |
                   NAT Network
                    NatNetwork
                   10.0.0.0/24
                         |
                 +------------------+
                 |    Kali Linux    |
                 |   10.0.0.2/24   |
                 |  Security VM     |
                 +------------------+
                         |
                  Future Lab VMs
                         |
             +-----------+-----------+
             |           |           |
        +---------+ +---------+ +---------+
        | Parrot  | | Ubuntu  | | Vuln.   |
        | OS      | | Server  | | Target  |
        +---------+ +---------+ +---------+
          Planned     Planned     Planned

Note: Kali Linux is the initial lab VM. Parrot OS, Ubuntu, and the vulnerable target are planned additions, not confirmed components of the current setup.
Network Design
Network Component	Description
Network Mode	VirtualBox NAT Network
Network Name	NatNetwork
IPv4 Prefix	10.0.0.0/24
Initial Security VM	Kali Linux
Kali IP Address	10.0.0.2/24
Intended Gateway	10.0.0.1
Future Expansion	Additional lab VMs

A NAT Network allows connected virtual machines to communicate with one another and provides outbound network connectivity. The actual gateway address must be verified in the VirtualBox network configuration.

⚙️ Lab Specifications
Component	Configuration
Host Operating System	Windows 10
Host Memory	8 GB RAM
Processor	Intel Core i7
Hypervisor	Oracle VirtualBox 7.2
Guest Operating System	Kali Linux 2026.2
Allocated VM Memory	2048 MB
Network Type	NAT Network
Network Name	NatNetwork
IPv4 Network	10.0.0.0/24
Kali IPv4 Address	10.0.0.2/24
Intended Gateway	10.0.0.1
DNS Server	8.8.8.8
Planned VM Address Range	10.0.0.3–10.0.0.99
Recovery Method	VirtualBox Snapshot
Configuration note: Verify the actual gateway and DHCP pool before assigning a static address. Ensure the address is not already assigned to another device or reserved by DHCP.
🧰 Tools & Technologies
Tool / Technology	Purpose
Oracle VirtualBox	Virtual machine creation and management
Kali Linux	Security testing and Linux administration
Parrot OS	Planned additional security workstation
Ubuntu	Planned Linux server or general-purpose VM
7-Zip	Extracting compressed VM archives
NetworkManager	Managing network connections
ip	Inspecting IP addresses and routes
ping	Testing network reachability
nslookup	Testing DNS resolution
Nmap	Network discovery and port scanning
Wireshark	Planned packet capture and analysis
🚀 Implementation Guide
Step 1 — Prepare the Host System

Install 7-Zip if the downloaded VM package is compressed. Install VirtualBox and verify that hardware virtualization is enabled.

Tool	Official Download
7-Zip	Download
VirtualBox	Download
Kali Linux	Download
Step 2 — Configure the NAT Network

Create a dedicated NAT Network in VirtualBox.

Setting	Value
Network Name	NatNetwork
IPv4 Prefix
