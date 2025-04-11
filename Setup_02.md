## Understand & Map Your Network

**Identify Devices on Your Network**

 - `ip a` (preferred) or `ifconfig` (older)
Find your router’s IP (usually ends in .1 or .254)
***
<br>

**Scan Your Network for Active Devices**

- Install a network scanner:
	`sudo apt update && sudo apt install nmap -y`

- Scan your network:
`nmap -sn <Target Subnet>`  
  
***
<br>

**Assign Static IPs to Devices**
- Log into your router admin panel (192.168.1.1 or 
 192.168.0.1)
  
- Assign static IPs to at least 3 devices (PC, Raspberry Pi, printer, etc.)

***
<br>


## Network Security & Traffic Analysis

**Capture Network Traffic (Wireshark)**
- Install Wireshark (https://www.wireshark.org/)

- Capture packets while using ping and nmap
Identify MAC addresses & protocols

***
<br>

**Set Up a Basic Firewall**
- Configure iptables or ufw
	  *Goal: Block/allow traffic to specific ports*
***
<br>

**Port Scanning & Service Discovery**
- Use nmap to scan your own network and identify open ports
	  ` nmap -sV 192.168.1.100`  *Replace with an IP from your network*
- Identify running services

***