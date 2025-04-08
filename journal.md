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

- refers to a physical ethernet cable providing internet to the host machine...im currently on wifi, this doesnt apply to me
***
<br>

Why did ubuntu server take so long to load when i changed the network settings to "bridged"? 
- It was attempting to make a connection, but wasn't actual connected via ethernet

***
<br>

Why dont I have internet connection with bridged connention  -possibly related to "cable connected" checkbox in virtualbox networ settings?
- Wifi isnt capable, i had to use ethernet

***
<br>

How do i find my host network interface, is that the same as adapter type?

- yes
 - `ip a`
 - look for `eth0` or `enp3s0` for wired (ethernet) interfaces and `wlan0` or `wlp2s0` for wifi. 

***
<br>

Ubuntu server bridged connection troubleshooting:
- Check network settings and choose correct adapter type: `ip a`
 - Restart network settings: `sudo systemctl restart Networkanager`

***
<br>

What does this error mean:
`NetworkManager.service not found`
- Check if NetworkManager is Installed: `dpkg -l | grep network-manager`
- Install: `sudo apt update && sudo aps install network-manager -y`

***
<br>

IP Address breakdown
IP Address: 10.0.x.x/y
- The 10.0.x.x part is the host IP address.

- The /y part is the CIDR notation showing how many bits are used for the network portion of the address.

- Subnet Address: 10.0.x.x

- Subnet Mask: 255.255.255.0

- Range of usable host IPs: 10.0.x.1 to 10.0.x.254

- Broadcast Address: 10.0.x.255
***
<br>

What Is a Subnet?
A subnet a smaller chunk of a larger network. It allows you to:

- Segment devices logically (e.g., servers vs. clients)

- Control traffic more efficiently

- Apply different rules (like firewall policies) per subnet

***
<br>

What does this error mean:
`Host seems down. If it is really up, but blocking our ping probes, try -Pn`

- The target didn’t respond to the ping.

- It might still be online, but not replying to ICMP (ping) because of a firewall or isolated network in a VM

Solution
1. Try -Pn (as Nmap suggested)
This tells Nmap not to ping and just go ahead with the scan: `nmap -Pn 10.0.x.x`

Summary:
That error = Nmap pinged your VM and got no response.

-Pn skips the ping step.

Best fix: use Bridged mode so the VM is on the same network as your host.
***
<br>
Why am I still receiving the same error when connected with bridged network?

1. Could be firewall bloackage:
   `sudo ufw status`

  Temporarily disable it:
   `sudo ufw disable`

   After completing the scan, remember to re-enable it:
   `sudo ufw enable`

2. VM network settings

3. Ensure Devices Are on the Same Subnet  

4. Use a More Specific Nmap Command  
   `sudo nmap -sn 10.x.x.x/y`

5. Increase Timeout or Retry  
   `sudo nmap -sn -T4 10.x.x.x/y`

6. Check Host Device's Network Settings  

7. Scan from the Host Network (to isolate whether the issue is with the VM):
   `sudo nmap -sn 10.x.x.x/y`

***
<br>

How come using nmap without the /y portion of 10.0.x.x/y fails to return a list of devices:

- That scans the net address and not the specific host
***
<br>

What is a network manager, and how do I install it?

