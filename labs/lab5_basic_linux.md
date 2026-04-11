# 🧪 Lab 5 : Linux Security Hardening

**Goal:** Learn how to secure a Linux system by reducing vulnerabilities, controlling access, and monitoring system activity.  
**Tools:** Linux Terminal (Ubuntu, Kali, Parrot OS)

---

## 🧠 Learning Objectives

By the end of this lab, you should be able to:
- Secure user accounts and passwords  
- Configure firewall rules  
- Disable unnecessary services  
- Monitor system logs for suspicious activity  
- Manage permissions and file security  
- Apply basic system hardening techniques  

---

## ⚙️ Prerequisites
- A Linux system (Kali, Ubuntu, etc.)  
- Terminal access (`Ctrl + Alt + T`)  
- Basic knowledge of Linux commands  
---
## 🧩 Step-by-Step Practical Guide

### Step 1 — Update Your System
```bash
sudo apt update && sudo apt upgrade -y
```
**Explanation:**
This command performs two important security tasks:
- apt update
Downloads the latest list of available packages from repositories
Ensures your system knows about the newest software versions
- apt upgrade -y
Installs updated versions of all installed packages
Automatically accepts prompts (-y)

### Why it is important:
Most attackers exploit known vulnerabilities in outdated software.
By running this command, you:
- Patch security holes
- Fix bugs and system weaknesses
- Improve system stability
**Example Output:**
```bash
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Reading package lists... Done
Building dependency tree... Done
0 upgraded, 0 newly installed, 0 to remove

```
---

### Step 2 — Remove Unused Packages
```bash
sudo apt autoremove
```
**Explanation:** 
Meaning:
- Removes packages that are no longer needed.

### Why it is important:

Unused software:
- May contain vulnerabilities
- Increases attack surface

**Example Output:**
```bash
(No output if successful)
```

---
### Step 3 — Create a New User
```bash
sudo adduser testuser
```
**Meaning:** 
This command creates a new user account in the system.
Behind the scenes, Linux:
- Creates a home directory /home/testuser
- Assigns a unique User ID (UID)
- Adds the user to default groups
- Prompts for password and user details
### Why it is important:
Using separate user accounts:
- Prevents sharing of credentials
- Limits damage if one account is compromised
- Supports proper access control
  
**Example Output:**
```bash
Adding user `testuser' ...
Adding new group `testuser' (1001) ...
Creating home directory `/home/testuser' ...
New password:
Retype new password:
```

---

### Step 4 — Check Active Users
```bash
who
```
**Explanation:** 
Shows users currently logged into the system.

**Example Output:**
```bash
user    pts/0   2026-04-10 10:00 (:0)
```

---

### Step 5 — View Login History
```bash
last
```
**Explanation:** 
Displays history of user logins and logouts.
**Example Output:**
```bash
user pts/0 192.168.1.5 Fri Apr 10 10:00 still logged in```
```
---


### Step 6 — Restrict File Access
```bash
chmod 600 sensitive.txt
```
**Explanation:** 
Meaning:

Changes file permissions so that:
Owner → read & write
Group → no access
Others → no access

### Why it is important:

Protects sensitive files like:
Passwords
Config files
Private data
**Example Output:**
```bash
(No output if successful)
```

---

### Step 7 —  Install Firewall (UFW)
```bash
sudo apt install ufw -y
htop
```
**Explanation:**
This command installs UFW (Uncomplicated Firewall), a user-friendly tool used to manage Linux firewall rules.

What happens internally:
- Downloads the UFW package from repositories
- Installs required dependencies
- Registers UFW as a system service
### Why it is important:
Without a firewall:
- Your system is exposed to the network
- Attackers can scan and access open ports
- Unauthorized connections may be allowed

**Expected Output:**
```bash
Reading package lists... Done
Building dependency tree... Done
The following NEW packages will be installed:
  ufw
Setting up ufw (0.36-6) ...
```

---

### Step 8 — Verify Installation
```bash
ufw status
```
**Explanation:**
Checks if UFW is installed and whether it is active.

**Expected Output:**
```bash
Status: inactive
```

---

### Step 9 — Enable Firewall
```bash
sudo ufw enable
```
**Explanation:** 
Activates the firewall and starts enforcing rules.

What happens internally:
- UFW loads default rules
- Blocks incoming traffic by default
- Allows outgoing traffic
This is where your system actually becomes protected.
**Expected Output:**
```bash
Firewall is active and enabled on system startup
```

---

### Step 10 — Set Default Policy (DENY ALL INCOMING)
```bash
sudo ufw default deny incoming
```
**Explanation:**
This command tells the firewall: “Block ALL incoming connections unless I explicitly allow them.”
### What happens internally:
- Any device trying to connect to your system will be rejected
- Only allowed ports/services will be accessible

#### Why it is important:
- Prevents unauthorized access
- Stops attackers from scanning your ports
- Reduces attack surface

**Expected Output:**
```bash
Default incoming policy changed to 'deny'
(be sure to update your rules accordingly)
```

---

### Step 11 — Allow Outgoing Connections
```bash
sudo ufw default allow outgoing
```
**Explanation:**
Allows your system to initiate connections to the internet.
### Why it is important:
- Without this You won’t be able to browse, update, or connect outward
**Expected Output:**
```bash
Default outgoing policy changed to 'allow'
```

---

### Step 12 — Enable Firewall
```bash
sudo ufw enable
```

**Explanation:**
Activates the firewall and starts enforcing rules.
### What happens internally:
- UFW loads default rules
- Blocks incoming traffic by default
- Allows outgoing traffic
### Why it is important:
- This is where your system actually becomes protected.
**Expected Output:**
```bash
Firewall is active and enabled on system startup
```
---

### Step 13 — Allow Only Required Services
```bash
sudo ufw allow 22/tcp
```
**Explanation:**
Allows incoming SSH connections on port 22.
### Why it is critical:
If you don’t allow SSH before enabling firewall:
- You can lose remote access to your system

**Expected Output:**
```bash
Rule added
Rule added (v6)
```

---

### Step 14 — Verify Firewall Rules
```bash
sudo ufw status verbose
```
**Explanation:**
Displays active rules and default policies.
**Example Output:**
```bash
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere
22/tcp (v6)                ALLOW       Anywhere (v6)
```

---

## ✅ Summary
You learned:
- System Updates: `apt update`, `apt upgrade`
- Users & Passwords: `adduser`, `passwd`
- Firewall Security: `ufw (deny incoming, allow SSH)`
- Services: `systemctl`
- File Permissions: `chmod`

---

## 📸 Optional Exercises

Automate system monitoring every 5 minutes using cron or a script.
1. Install UFW and verify it is installed correctly.  
2. Set firewall to **deny all incoming traffic by default**.  
3. Allow only SSH access on port 22.  
4. Enable UFW and check its status.  
5. Add a rule to allow HTTP (port 80) and test it.  
6. Block a specific IP address using UFW.  
7. Remove an existing firewall rule.  
8. Check active firewall rules using `ufw status verbose`.   


Practice these steps until you can do them **without looking at instructions**.
