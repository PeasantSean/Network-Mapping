<br>

### Setting Up My Virtual Lab

- Installed 2 VMs - Ubuntu Server and Ubuntu Desktop
- Switched the network settings to "Internal Network". (for now... this will change constantly)
- Installed and used `nmap` to scan my network
- *(Future task: capture network traffic with wireshark)*
<br>

***


### Questions & Roadblocks So Far...

*(future updates will be documented through main branch commits)*
<br>

***

<br>

Why is it important to be careful when using `nmap` and Wireshark on a real network?
- **Security flags**: Firewalls may detect scans as suspicious activity.
- **Legality**: Unauthorized scanning could violate policies or laws.
- **Agressive scans**( -A & -T4): Can cause congestion and possibly crash older routers.
<br>

***

<br>

The IP adresses on both VMs are listed as "127.0.0.1". Why is that, and will it cause issues?
- "127.0.0.1" refers to the VM itself rather than the network, so yes it will cause issues.
- Possible Fixes:
	- Double check the network adapter settings to make sure it's set to NAT. (I haven't figured out how to get unique IP adresses when it's set to Internal Network. )
	- *(Still troubleshooting how to get unique IPs when using "Internal Network")*
	- Restart Network: `sudo systemctl restart network manager` 
	- Request new IP address: `sudo dhclient -v`
	- Check to see if network adapter is detected: `ls /sys/class/net`
<br>

***

<br>

When installing nmap I received an error message: "unable to fetch some archives"

- I fixed it by running:
	- `sudo apt --fix-missing update`
	- Also checked internet access: `ping google.com`
	- Switched network settings back to NAT for now.
<br>

***

<br>

Why does running `nmap` in the VM only show a few active IPs, while running `nmap` on the host machine (same network) shows all devices?

- That's the point of the NAT connection - The VM is using the hosts network but remains isolated.
<br>

***

<br>

What's the real value in nmap anyway?

-  **Visualizes** how devices communicate
- **Finds vulnerabilities** in a network.
- **Monitors a network** for unauthorized devices.
- **Identifies compromized** devices.
- **Scans open ports** to detect running services.
<br>

***

<br>

Why use a VM when I can only scan my home network? I can't sumulate one since I can't generate unique IPs with "Internal Network".

- **Keeps exercises contained** - useful when experimenting with new configurations/tools.
- If scanning an **untrusted network**, the scans remain **isolated from the host machine.**

<br>

***

<br>

In virtualbox's network setting, what does "cable connected" mean?
- Refers to a physical ethernet cable providing internet to the host machine...im currently on wifi, this doesnt apply to me

***
<br>

How do i find out my subnet?
    - 
    
***
<br>

Why did ubuntu server take so long to load when i changed the network settings to "bridged"? 
    - 

***
<br>

Why dont I have internet connection with bridged connention  
- Possibly related to "cable connected" checkbox in virtualbox networ settings?
- Wifi isnt capable, I had to use ethernet

***
<br>

How do I find my host network interface, is that the same as adapter type?
- Yes
 - `ip a`
 - Look for `eth0` or `enp3s0` for wired (ethernet) interfaces and `wlan0` or `wlp2s0` for wifi. 

***
<br>

What is the intel pro/1000 mt desktop (82540em) adapter type?
    - 
***
<br>

Ubuntu server bridged connection troubloeshooting:
- Check network settings and choose correct adapter type: `ip a`
 - Restart network settings: `sudo systemctl restart Networkanager`

***
<br>

Error: `NetworkManager.service not found`
- Check if NetworkManager is Installed: dpkg -l | grep network-manager
- Install: sudo apt update && sudo aps install network-manager -y

***
<br>
