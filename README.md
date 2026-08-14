                                                        Cybersecurity Home Lab
                                                        
                                          Professional Lab Setup Guide — VirtualBox + Kali Linux
1. Project Objective
   
This document describes how to build an isolated and reproducible cybersecurity laboratory using 7-Zip, Oracle VirtualBox, and Kali Linux.
The objective is to establish a professional lab environment that can be used for cybersecurity exercises such as:
•	Network configuration and administration
•	System administration
•	Network traffic analysis
•	Security testing
•	Vulnerability assessment
•	System hardening
•	Cybersecurity demonstrations and practical exercises
________________________________________
2. Target Architecture
The recommended virtual network configuration is:
Component	Configuration
Network Type	VirtualBox NAT Network
Network	10.0.0.0/24
Gateway	10.0.0.1
Kali Linux IP	10.0.0.2/24
DHCP	Enabled initially
DNS	NAT Network DNS or configured DNS server
The objective is to keep the cybersecurity lab logically separated while allowing controlled Internet access when required.

<img width="1302" height="606" alt="image" src="https://github.com/user-attachments/assets/8c4f2b35-3991-42fe-a97d-fcd1e0398589" />

3. Prerequisites
Before starting, make sure you have:
•	A laptop or desktop computer with hardware virtualization enabled (Intel VT-x or AMD-V).
•	At least 4 GB RAM recommended; 8 GB or more is preferable for multiple virtual machines.
•	At least 60 GB of available disk space.
•	An Internet connection.
•	Administrator privileges on the host computer.
•	Windows, Linux, or another supported operating system capable of running VirtualBox.
________________________________________
4. Step 1 — Download and Install 7-Zip
Download and install 7-Zip from the official website:
https://7-zip.org/download.html
Installation
1.	Download the appropriate version for your operating system.
2.	Run the installer.
3.	Follow the installation wizard.
4.	Keep the default settings unless you have specific requirements.
5.	Verify that 7-Zip is working correctly.
Why do we need 7-Zip?
Kali Linux virtual machine images are often distributed as compressed archives such as .7z or .zip.
7-Zip will therefore be used to extract the downloaded files before importing the virtual machine into VirtualBox.
________________________________________

5. Step 2 — Download and Install VirtualBox
Download Oracle VirtualBox from the official website:
urlVirtualBox Official Downloadshttps://www.virtualbox.org/wiki/Downloads
Installation
1.	Download the latest supported version of VirtualBox.
2.	Run the installer.
3.	Follow the installation wizard.
4.	Accept the required network components.
5.	Restart the computer if requested.
6.	Launch VirtualBox.
7.	Verify that VirtualBox starts correctly.

8.	<img width="1897" height="1007" alt="image" src="https://github.com/user-attachments/assets/62076038-3110-4ffd-8d2b-d327626b6801" />

________________________________________

6. Step 3 — Configure the VirtualBox Network
Create a dedicated NAT Network for the cybersecurity laboratory.
Recommended configuration
Network CIDR : 10.0.0.0/24
DHCP         : Enabled
The network provides addresses in the following range:
Network:    10.0.0.0/24
Gateway:    10.0.0.1
Usable IPs: 10.0.0.1 - 10.0.0.254
Important
A NAT Network is different from the standard VirtualBox NAT mode.
A NAT Network allows multiple virtual machines to:
•	Communicate with each other.
•	Share the same virtual network.
•	Access external networks through NAT.
This configuration is particularly useful for a cybersecurity laboratory.

<img width="1275" height="912" alt="image" src="https://github.com/user-attachments/assets/c53a980e-6885-468b-b4be-4a0c686458d3" />

________________________________________

7. Step 4 — Download and Import Kali Linux
Download Kali Linux from the official website:
urlKali Linux Official Download Pagehttps://www.kali.org/get-kali/
Procedure
1.	Download the VirtualBox version of Kali Linux.
2.	Extract the downloaded archive using 7-Zip if necessary.
3.	Open VirtualBox.
4.	Import the Kali Linux virtual machine.
5.	Allocate appropriate resources.
Recommended VM resources
CPU : 2–4 vCPUs
RAM : 4–8 GB
Disk: According to the downloaded Kali image
These values should be adjusted according to the resources available on the host computer.
Configure the network adapter
In the Kali VM settings:
Settings
   ↓
Network
   ↓
Adapter 1
   ↓
Attached to: NAT Network
   
Then start the Kali Linux virtual machine.

<img width="1452" height="905" alt="image" src="https://github.com/user-attachments/assets/28f25921-ba59-4b3d-bad1-9ba186502a62" />

________________________________________

8. Step 5 — Configure the Kali Linux IP Address
After starting Kali Linux, identify the network interfaces:
Example static IP configuration
The recommended Kali IP address for this lab is:
IP Address : 10.0.0.2
Subnet     : 255.255.255.0
Gateway    : 10.0.0.1
First identify the connection:
nmcli connection show
Then configure the connection:
sudo nmcli connection modify "<CONNECTION_NAME>" \
ipv4.method manual \
ipv4.addresses 10.0.0.2/24 \
ipv4.gateway 10.0.0.1
Configure DNS:8.8.8.8

<img width="1891" height="977" alt="image" src="https://github.com/user-attachments/assets/6b598ed7-0ec8-42dc-89e6-fc7aac3db00e" />

9. Step 6 — Create a Virtual Machine Snapshot
    
Once Kali Linux is correctly configured and connectivity has been verified, create a snapshot.
Recommended snapshot name:
00-My Backup of Fresh Kali linux (13 August 2026)
Recommended description:
Clean Kali Linux baseline.
Network configured and connectivity verified.
Ready for cybersecurity laboratory exercises.
The snapshot allows you to quickly return to a known-good state after performing experiments.
Important: A VirtualBox snapshot should not be considered a replacement for a proper backup.
<img width="1278" height="925" alt="image" src="https://github.com/user-attachments/assets/09e0c8dc-abf3-48d1-af12-2ac8c6830f55" />

10. Expected Final Result
At the end of this procedure, the project should have:
•	A fully functional VirtualBox environment.
•	A dedicated NAT network using 10.0.0.0/24.
•	A working Kali Linux virtual machine.
•	A documented Kali Linux IP configuration.
•	Verified network and DNS connectivity.
•	A clean Kali Linux snapshot.

