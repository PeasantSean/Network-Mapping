## Setting Up a Virtual Lab for Network Mapping

1. **Create Virtual Machines**
- Install Ubuntu Server or Ubuntu Desktop as your main Linux machine.

- Add a second VM to simulate another device.
***
<br>

2. **Configure Network Settings in VirtualBox**

**Option 1:** Isolated Virtual Network 
- Go to VirtualBox > Settings > Network.

- Set the network adapter to "Internal Network" for isolated communication between VMs.
<br>


**Option 2:** Bridged Adapter (For Real Network Testing)

- Set network adapter to "Bridged Adapter".

- (Caution: Be mindful of using nmap or Wireshark on a real network.)
***
<br>

3. **Identify Devices on Your Virtual Network**
- Run `ip a | grep inet` on each VM to find IP addresses.

- Note down the IPs of all your VMs.
***
<br>

4. **Scan the Network with Nmap**
- Install Nmap: sudo apt update && sudo apt install nmap -y.

- Scan your internal network: `nmap -sn <target-IP>`.

- To get detailed info on a VM: `nmap -A <target-IP>`.
***
<br>

5. **Capture Network Traffic**
- Install Wireshark or tcpdump: `sudo apt install wireshark -y`.

- Start capturing traffic: `sudo tcpdump -i eth0`