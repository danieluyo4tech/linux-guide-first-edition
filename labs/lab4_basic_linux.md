# 🧪 Lab 4 : Linux Networking

**Goal:** Learn how to check network settings, test connectivity, and understand how Linux communicates over a network.  
**Tools:** Linux Terminal (Ubuntu, Kali, Parrot OS, etc.)

---

## 🧠 Learning Objectives

By the end of this lab, you should be able to:
- Check your IP address and network configuration  
- Test internet connectivity using ping  
- View active network interfaces  
- Identify network routes and gateways  
- Troubleshoot basic network issues  
- Use essential Linux networking commands confidently  

---

## ⚙️ Prerequisites
- A Linux system (Kali, Ubuntu, etc.)  
- Terminal access (`Ctrl + Alt + T`)  
- Active internet connection (WiFi or Ethernet)  
- Basic knowledge of Linux commands  
---
## 🧩 Step-by-Step Practical Guide

### Step 1 — Check Your IP Address
```bash
ip a
```
**Explanation:**
This command displays all network interfaces available on your system along with their full configuration details.
It shows:
- Interface names (e.g. wlan0 for WiFi, eth0 for Ethernet, lo for loopback)
- IP addresses (IPv4 & IPv6) assigned to each interface
- MAC address (physical hardware address of your device)
- Interface status (UP = active, DOWN = inactive)

**Example Output:**
```bash
2: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 192.168.1.5/24 brd 192.168.1.255 scope global wlan0
    link/ether aa:bb:cc:dd:ee:ff

```
---

### Step 2 — Quickly View Your IP Address
```bash
hostname -I
```
**Meaning:** 
This command prints only the IP address(es) assigned to your system without showing extra technical details.
Why it is important:
Useful when you quickly need your IP address for:
- Connecting to another device
- Setting up servers
- Sharing your IP with others
  
**Example Output:**
```bash
192.168.1.5
```

---

### Step 3 — Test Internet Connectivity (Domain)
```bash
ping google.com
```
**Explanation:** 
This command sends ICMP echo requests (small packets) to a remote server (google.com) to check if your system can reach it.
It measures:
- Connectivity (is the server reachable?)
- Latency (how fast the response comes back)
- Packet loss (if any data is lost)
**Example Output:**
```bash
64 bytes from google.com (142.250.190.78): icmp_seq=1 ttl=117 time=45.2 ms
```

---

### Step 4 — Check Network Device Status
```bash
nmcli device status
htop
```
**Explanation:**
This command shows the current status of all network interfaces managed by NetworkManager.
It displays:
- Device name (wlan0, eth0)
- Device type (WiFi, Ethernet)
- Connection state (connected, disconnected)

**Expected Output:**
```bash
DEVICE   TYPE      STATE
wlan0    wifi      connected
eth0     ethernet  disconnected
```

---

### Step 5 — View Network Routing Information
```bash
ip route
```
**Explanation:**
Displays the routing table, which tells your system how to send data to other networks.
Key parts:
- Default gateway → where internet traffic is sent
- Network routes → paths to local networks
Why it is important:
- Without proper routing, your system cannot access the internet, even if it has an IP address.

**Expected Output:**
```bash
default via 192.168.1.1 dev wlan0
192.168.1.0/24 dev wlan0 proto kernel scope link
```

---

### Step 6 — View Open Ports and Services
```bash
ss -tuln
```
**Explanation:** 
Shows all active network ports and services currently running on your system.
Breakdown:
- t → TCP connections
- u → UDP connections
- l → listening services
- n → numeric format
Why it is important:
Helps you:
- Identify running services (e.g. SSH, web server)
- Detect unwanted or suspicious open ports
- Understand what your system is exposing to the network
**Expected Output:**
```bash
Netid  State   Local Address:Port
tcp    LISTEN  0.0.0.0:22
tcp    LISTEN  0.0.0.0:80
```

---

### Step 7 — Check DNS Configuration
```bash
cat /etc/resolv.conf
```
**Explanation:**
Displays the DNS servers your system uses to resolve domain names.
Why it is important:
If DNS is misconfigured:
- Websites won’t load by name
- Internet may appear “broken”

**Expected Output:**
```bash
nameserver 8.8.8.8
nameserver 1.1.1.1
```

---

### Step 8 — Test DNS Resolution
```bash
nslookup google.com
```
**Explanation:**
Queries a DNS server to translate a domain name into an IP address.
Why it is important:
Helps confirm:
- DNS server is working
- Domain names are resolving correctly
**Expected Output:**
```bash
Server: 8.8.8.8
Address: 8.8.8.8#53
Name: google.com
Address: 142.250.190.78
```

---

### Step 9 — Restart Network Service
```bash
sudo systemctl restart NetworkManager
```
**Explanation:**
Restarts the NetworkManager service, which controls network connections.
Why it is important:
Used to fix issues like:

- Network not connecting
- IP not assigned
- WiFi not responding

**Expected Output:**
```bash
(No output if successful)
```

---

### Step 10 — Discover Devices on Your Network
```bash
sudo netdiscover
```

**Explanation:**
Scans your local network using ARP requests to discover all connected devices.
What it reveals:
- IP addresses of devices
- MAC addresses
- Device vendors
**Expected Output:**
```bash
IP              MAC Address         Vendor
192.168.1.1     aa:bb:cc:dd:ee      TP-Link
192.168.1.5     11:22:33:44:55      Android Device
192.168.1.8     66:77:88:99:00      Laptop
```
---

### Step 11 — sudo wireshark
```bash
systemctl status ssh
```
**Explanation:**
Wireshark is a network protocol analyzer used to capture and inspect packets traveling through your network in real time.

It allows you to:
- See all incoming and outgoing traffic
- Analyze protocols like HTTP, DNS, TCP
- Monitor network activity at a deep level
What to do:
- Select your active interface (e.g. wlan0)
- Click Start Capturing
- Open a browser and visit any website
- What you will observe:
- Live packets flowing across the network
Protocols like:
- DNS (domain lookup)
- TCP (connection)
- HTTP/HTTPS (web traffic)
**Example Output:**
```bash
No.   Time      Source        Destination     Protocol Length Info
1     0.000     192.168.1.5   8.8.8.8         DNS      74     Query google.com
2     0.020     8.8.8.8       192.168.1.5     DNS      90     Response 142.250.190.78
3     0.050     192.168.1.5   142.250.190.78  TCP      66     SYN
```

---

## ✅ Summary
You learned:
- IP Configuration: `ip a`, `hostname -I`  
- Connectivity Testing: `ping`  
- Network Devices: `nmcli`  
- Routing & Gateway: `ip route`  
- Open Ports & Services: `ss`  
- DNS Configuration: `cat /etc/resolv.conf`  
- DNS Testing: `nslookup`  
- Network Restart: `systemctl restart NetworkManager`  
- Network Discovery: `netdiscover`  
- Traffic Monitoring: Wireshark  

---

## 📸 Optional Exercises




Automate system monitoring every 5 minutes using cron or a script.
1. Find your IP address using two different commands.  
2. Test internet connectivity using both domain and IP address.  
3. Identify your default gateway using `ip route`.  
4. Display all open ports and identify active services.  
5. Check your DNS servers and verify them using `nslookup`.  
6. Scan your local network and list at least 3 connected devices.  
7. Restart your network service and confirm connectivity.  
8. Monitor your network traffic and identify at least one protocol in use (e.g. TCP, DNS).  


Practice these steps until you can do them **without looking at instructions**.

