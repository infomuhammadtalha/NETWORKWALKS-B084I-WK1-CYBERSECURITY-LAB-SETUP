# NETWORKWALKS-B084I-WK1-CYBERSECURITY-LAB-SETUP
Cybersecurity Lab Setup
🛡️ Virtual Cybersecurity Lab | Kali Linux + VirtualBox

<p align="center">
<img src="https://img.shields.io/badge/CYBERSECURITY-HOME%20LAB-111827?style=for-the-badge&logo=kalilinux&logoColor=white" alt="Cybersecurity Home Lab"/>
<img src="https://img.shields.io/badge/PLATFORM-VirtualBox-1E70C1?style=for-the-badge&logo=virtualbox&logoColor=white" alt="VirtualBox"/>
<img src="https://img.shields.io/badge/OS-Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white" alt="Kali Linux"/>
</p>

<p align="center">
<b>A hands-on project for building a virtual environment for network security, Linux administration, and ethical hacking practice.</b>
</p>

<p align="center">
<img src="https://img.shields.io/badge/Project-01-C62828?style=flat-square" alt="Project 01"/>
<img src="https://img.shields.io/badge/Focus-Virtual%20Networking-008577?style=flat-square" alt="Virtual Networking"/>
<img src="https://img.shields.io/badge/Environment-Isolated%20Lab-6A5ACD?style=flat-square" alt="Isolated Lab"/>
<img src="https://img.shields.io/badge/Status-Initial%20Setup-2E8B57?style=flat-square" alt="Initial Setup"/>
</p>

📖 About This Project

This repository documents my practical journey of building a virtual cybersecurity lab using Oracle VirtualBox and Kali Linux.

The goal is to establish a reusable environment where I can learn Linux networking, explore security tools, investigate network traffic, and perform authorized security assessments without using real-world systems as test targets.

The lab currently consists of a Kali Linux virtual machine connected to a dedicated VirtualBox NAT Network. The environment is designed to support additional virtual machines as I progress toward more advanced cybersecurity exercises.

This is a hands-on learning project, with configuration notes, screenshots, verification commands, and troubleshooting observations.

🎯 Project Goals
Install and configure a desktop virtualization platform.
Deploy Kali Linux as a virtual machine.
Create a dedicated virtual network for lab systems.
Configure and verify IPv4 networking.
Test gateway reachability, Internet access, and DNS resolution.
Create a recovery snapshot of the configured VM.
Document technical issues and their solutions.
Prepare a foundation for future penetration-testing exercises.
🏗️ Lab Architecture

<p align="center">
<img src="1-screenshot-title-image.png" alt="Virtual cybersecurity lab architecture" width="850"/>
</p>

Network design

The lab uses a VirtualBox NAT Network with the private IPv4 prefix 10.0.0.0/24.

text
                  HOST COMPUTER
                   Windows 10
                        |
                 Oracle VirtualBox
                        |
                 NAT Network
                  NatNetwork
                 10.0.0.0/24
                        |
                +----------------+
                |   Kali Linux   |
                |  10.0.0.2/24  |
                | Security VM    |
                +----------------+
                        |
              Future lab expansion
                        |
              +-------------------+
              | Vulnerable Target  |
              | VM (Planned)       |
              +-------------------+


Network design notes:

The Kali VM is the initial security workstation.
Additional test machines can be connected to the same NAT Network.
NAT Network connectivity supports communication between connected VMs and outbound connectivity.
A dedicated lab network helps separate practical exercises from the physical network, but it is not a complete security boundary by itself.
Future target machines will be added for authorized testing.
⚙️ Lab Specifications
Component	Configuration
Host operating system	Windows 10
Host RAM	8 GB
Processor	Intel Core i7
Virtualization platform	Oracle VirtualBox 7.2
Security operating system	Kali Linux 2026.2
Allocated VM memory	2048 MB
Network mode	NAT Network
Network name	NatNetwork
IPv4 network	10.0.0.0/24
Kali IPv4 address	10.0.0.2/24
Intended gateway	10.0.0.1
DNS server	8.8.8.8
Planned additional VM addresses	10.0.0.3–10.0.0.99
Recovery method	VirtualBox snapshot
Networking note: The gateway address must match the actual VirtualBox NAT Network configuration. If DHCP is enabled, verify the assigned address, gateway, and DNS settings before configuring a static address. Ensure static addresses do not conflict with DHCP assignments.
🧰 Tools Used
Tool	Purpose
Oracle VirtualBox	Creating and managing virtual machines
Kali Linux	Linux-based security testing environment
7-Zip	Extracting compressed VM files
NetworkManager (nmcli)	Managing network connections
ping	Testing IP connectivity
nslookup	Checking DNS resolution
Nmap	Network discovery and port-scanning practice
🚀 Implementation Guide
Step 1 — Prepare the host

Install 7-Zip to extract the downloaded virtual machine archive when necessary.

Then install Oracle VirtualBox and confirm that hardware virtualization is enabled in the system firmware.

Tools:

Download 7-Zip
Download VirtualBox
Step 2 — Create the virtual network

Create a dedicated NAT Network in VirtualBox and configure it for the lab environment.

Setting	Value
Network name	NatNetwork
IPv4 prefix	10.0.0.0/24
DHCP	Enabled
IPv6	Disabled for this lab

<p align="center">
<img src="2-screenshot-network-settings-1.png" alt="VirtualBox NAT Network configuration" width="800"/>
</p>

A NAT Network is useful when multiple virtual machines need to communicate with one another while retaining outbound network connectivity.

Step 3 — Import Kali Linux

Download the Kali Linux virtual machine from the official Kali website and import the VM into VirtualBox.

Configure the VM with the following initial settings:

text
Operating System: Kali Linux
Memory:           2048 MB
Network Adapter:  Adapter 1
Attached To:      NAT Network
Network Name:     NatNetwork
Adapter Type:     Intel PRO/1000 MT Desktop


<p align="center">
<img src="3-screenshot-kali-linux.png" alt="Kali Linux virtual machine in VirtualBox" width="800"/>
</p>

A shared folder was also configured to transfer selected files between the Windows host and Kali Linux.

Only share folders that are necessary for the lab, and avoid exposing sensitive host files to experimental VMs.

Official download: Kali Linux

Step 4 — Configure Kali networking

Inspect the current network configuration before making changes.

bash
ip -br address
ip route
nmcli connection show


The intended network configuration is:

text
IPv4 Address: 10.0.0.2/24
Gateway:      10.0.0.1
DNS Server:   8.8.8.8


<p align="center">
<img src="4-screenshot-kali-network-settings.png" alt="Kali Linux network configuration" width="800"/>
</p>

Configure the address using the Kali network settings or NetworkManager, ensuring that the connection name matches the one reported by nmcli connection show.

Before applying a static IP, verify the actual gateway and DHCP address pool in VirtualBox. If the gateway or DNS settings differ, use the values appropriate for your network.

Step 5 — Verify network connectivity

Run the following commands in Kali Linux to check the main network functions.

1. Inspect the IP address

bash
ip -br address


Confirm that the expected IPv4 address appears on the active network interface.

2. Check the default route

bash
ip route


Confirm that the default route points to the configured gateway.

3. Test gateway reachability

bash
ping -c 4 10.0.0.1


Successful replies indicate that the gateway is reachable, provided ICMP traffic is permitted.

4. Test external IP connectivity

bash
ping -c 4 8.8.8.8


If this succeeds, outbound IP connectivity is working. A failed ping alone does not prove that Internet access is unavailable, because ICMP may be filtered.

5. Test DNS resolution

bash
nslookup networkwalks.com


A successful response indicates that the DNS query was resolved.

6. Verify Nmap

bash
nmap --version


This checks whether Nmap is installed and available in the terminal.

Step 6 — Create a recovery snapshot

Once the operating system and network configuration are stable, create a VirtualBox snapshot.

Suggested snapshot name:

text
Kali-Baseline-Network-Configured


A clean snapshot provides a convenient recovery point before installing additional tools or conducting experiments.

Restore the snapshot when necessary and recheck the VM configuration before beginning another exercise.

🧪 Verification Checklist

Use this checklist to document the results from your own machine.

Kali Linux boots successfully.
The VM is attached to NatNetwork.
The expected IPv4 address is configured.
The default gateway is correct.
The gateway connectivity test has been performed.
Outbound connectivity has been tested.
DNS resolution has been checked.
Nmap is available.
A baseline snapshot has been created.
The snapshot recovery process has been tested.

Important: Mark a check as complete only after you have run the relevant test and verified its result.

🐛 Troubleshooting Notes
Issue 1 — Internet connectivity problems

Static network configuration can introduce errors if the IP address, gateway, DNS server, or NetworkManager profile is incorrect.

Start by checking the current settings:

bash
ip -br address
ip route
nmcli connection show
nmcli device status


Check the connection profile and verify that its configured address, gateway, and DNS values match the VirtualBox network.

Useful troubleshooting steps:

Confirm that the VM is attached to the correct NAT Network.
Verify the actual gateway address in VirtualBox.
Check that the static IP does not conflict with another VM or DHCP lease.
Review the active NetworkManager connection profile.
Test IP connectivity separately from DNS resolution.

Avoid applying unrelated network workarounds without first identifying the cause. For example, ipv4.dad-timeout is not a general-purpose fix for Internet connectivity issues.

Issue 2 — VT-x or hardware virtualization error

If VirtualBox reports that hardware virtualization is unavailable:

Restart the host computer.
Enter the BIOS/UEFI configuration.
Enable Intel VT-x or the equivalent hardware virtualization setting.
Save the changes and restart.
Launch the VM again.

The exact firmware menu and setting name vary by computer model.

📚 Key Takeaways
Virtualization and lab design

I learned how a hypervisor can be used to create a repeatable environment for cybersecurity practice without requiring a separate physical computer for every lab machine.

Virtual networking

I explored the role of NAT Networks in connecting multiple VMs and providing outbound connectivity. I also learned why the network prefix, gateway, and DHCP configuration must be consistent.

Linux network administration

I practiced inspecting IPv4 addresses, routing information, and NetworkManager profiles, along with testing connectivity and DNS resolution.

Recovery and reproducibility

Creating a clean snapshot established a baseline that can be restored before future security experiments.

Technical documentation

Recording the configuration, screenshots, commands, and troubleshooting observations makes it easier to reproduce the setup and understand problems later.

🔮 Future Improvements

This repository is the foundation for a larger hands-on cybersecurity learning environment.

Planned additions include:

Add a deliberately vulnerable target VM.
Document host-to-VM and VM-to-VM connectivity.
Perform basic network discovery using Nmap against authorized lab targets.
Capture and inspect lab traffic with Wireshark.
Practice service enumeration on intentionally vulnerable systems.
Explore web application security in a dedicated test environment.
Document findings, remediation recommendations, and lessons learned.
Maintain separate snapshots for the baseline and individual exercises.

These are future goals, not claims that the exercises have already been completed.

🔐 Responsible Use

This environment is intended for education, defensive security learning, and authorized testing.

Test only systems you own or have explicit permission to assess.
Use intentionally vulnerable targets in the lab.
Avoid scanning or attacking public systems without authorization.
Keep sensitive host data out of shared folders.
Review network exposure before connecting experimental VMs to external networks.

A virtual lab reduces risk when configured carefully, but it does not automatically eliminate every route between a guest VM and the host or external networks.

🔗 Official Resources
Kali Linux — Download
VirtualBox — Downloads
VirtualBox — User Manual
7-Zip — Downloads
Nmap — Official Website
Wireshark — Official Website
👨‍💻 About the Author

Waqas Karim

Cybersecurity learner | Linux | Virtualization | Network Security

LinkedIn: Connect with me

This project is part of my practical cybersecurity learning journey with Networkwalks, documenting the skills I develop through hands-on exercises.

<p align="center">
<b>Learn by building. Improve by testing. Grow by documenting.</b>
</p>

<p align="center">
<i>Project 01 — Virtual Cybersecurity Lab Setup</i>
</p>
  <img src="https://img.shields.io/badge/Waqas%20Karim%20CCIE-C00000?style=flat-square" />
</p>
