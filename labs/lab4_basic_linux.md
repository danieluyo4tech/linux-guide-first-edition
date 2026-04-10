# 🧪 Lab 3: System Monitoring & Process Management

**Goal:** Learn to monitor system resources, processes, CPU/memory usage, and manage running services in Linux.  
**Tools:** Linux Terminal (Ubuntu, Kali, or any Linux distribution)

---

## 🧠 Learning Objectives
By the end of this lab, you should be able to:
- Monitor running processes and system performance
- Inspect CPU, memory, and disk usage
- Identify resource-hogging processes
- Manage services with `systemctl`
- Use advanced commands like `top`, `htop`, `vmstat`, `iostat`, `uptime`, `dstat`
- Automate monitoring tasks with command combinations

---

## ⚙️ Prerequisites
- Completion of Lab 1 & Lab 2
- Terminal access (`Ctrl + Alt + T`)
- Understanding of files, permissions, and basic commands

---
## 🧩 Step-by-Step Practical Guide

### Step 1 — Check System Uptime and Load
```bash
uptime
```
**Explanation:**
Shows how long the system has been running, number of users logged in, and system load averages over 1, 5, and 15 minutes.

**Example Output:**
```bash
10:45:32 up 3 days, 2 users, load average: 0.15, 0.10, 0.05

```
---

### Step 2 — Monitor Processes with ps
```bash
ps aux
```
**Meaning:** Lists all running processes, showing:
- USER → process owner
- PID → process ID
- %CPU → CPU usage
- %MEM → memory usage
- COMMAND → command that started the process
- 
**Example Output:**
```bash
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
daniel    1234  0.0  0.1  23456  1234 pts/0    Ss   09:00   0:00 bash
root      5678  0.1  1.2 123456 12345 ?       Ss   08:59   0:05 sshd
```

---

### Step 3 — Real-Time Monitoring with top
```bash
top
```
**Explanation:**Displays real-time CPU, memory, and process statistics.
- Press q to quit.

**Example Output:**
```bash
top - 10:46:01 up 3 days, 2 users, load average: 0.15, 0.10, 0.05
Tasks: 123 total,   1 running, 122 sleeping,   0 stopped,   0 zombie
%Cpu(s):  5.0 us,  1.0 sy,  0.0 ni, 94.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem : 2048000 total, 1024000 free,  512000 used,  512000 buff/cache
KiB Swap: 1024000 total, 1024000 free,       0 used.  1500000 avail Mem
```

---

### Step 4 — Interactive Process Monitor with htop
```bash
sudo apt install htop -y
htop
```
**Explanation:**
More visual, interactive process manager than top.
- Use arrow keys to scroll, F9 to kill a process.

**Expected Output:**
```bash
PID USER   PRI  NI  VIRT   RES  SHR S CPU% MEM%  TIME+  Command
1234 daniel 20   0 23456  1234  456 S  0.0  0.1   0:00  bash
5678 root   20   0 123456 12345 567 S  0.1  1.2   0:05  sshd
```

---

### Step 5 — Monitor CPU and Memory Usage with vmstat
```bash
vmstat 2 5
```
**Explanation:**
Shows virtual memory, CPU, and process statistics every 2 seconds, 5 times.

**Expected Output:**
```bash
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 1024000  5120 204800   0    0     2     1  123  456  5  1 94  0  0

```

---

### Step 6 — Monitor Disk I/O with iostat
```bash
sudo apt install sysstat -y
iostat -xz 2 3
```
**Explanation:** 
Displays extended disk I/O stats per device.

**Expected Output:**
```bash
Device:            rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda                 0.00     1.00    0.50    2.00    12.00    24.00    36.00     0.01    5.00    2.00    6.00   0.50  0.10
```

---

### Step 7 — Monitor Network Usage
```bash
sudo netstat -tulpn
```
**Explanation:**
Lists all active network connections, listening ports, and processes.

**Expected Output:**
```bash
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      5678/sshd
tcp6       0      0 :::80                   :::*                    LISTEN      4321/apache2
```

---

### Step 8 — Interactive Network Monitor with iftop
```bash
sudo apt install iftop -y
sudo iftop
```
**Explanation:**
Shows bandwidth usage per host in real-time  

**Expected Output:**
```bash
Linux Essentials Lab 1
Practice navigating directories and files
```

---

### Step 9 — Monitor Logs and Events
```bash
journalctl -xe
```
**Explanation:**
View system logs

**Expected Output:**
```bash
Oct 29 10:50:01 ubuntu systemd[1]: Starting Daily apt download activities...
Oct 29 10:50:01 ubuntu systemd[1]: Started Daily apt download activities.
```

---

### Step 10 — Filter logs for SSH service:
```bash
journalctl -u ssh -n 10
```

**Explanation:**
Filter logs for SSH service: 

**Expected Output:**
```bash
Oct 29 10:52:01 ubuntu sshd[5678]: Accepted password for daniel from 192.168.1.5 port 55874 ssh2
```
---

### Step 11 — Manage Services with systemctl
```bash
systemctl status ssh
```
**Explanation:**
Check if SSH is running and enabled at boot.

**Example Output:**
```bash
ssh.service - OpenBSD Secure Shell server
Loaded: loaded (/lib/systemd/system/ssh.service; enabled)
Active: active (running) since Thu 2025-10-29 08:59:01 UTC; 2h 45min ago
```

**Start/Stop/Restart services:**
```bash
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
```

**Enable/Disable at boot:**
```bash
sudo systemctl enable ssh
sudo systemctl disable ssh
```

---

### Step 12 - Kill and Manage Processes
```bash
ps aux | grep firefox
kill -9 <PID>
```
**Explanation:**
Finds processes by name and terminates them.

**Example Output:**
```bash
daniel   6789  5.0  2.5 234567 54321 pts/0  S+   10:50   0:03 firefox
```

---

### Step 13 — Advanced Monitoring Tools

**Disk usage per directory:**
```bash
du -sh /home/daniel/*
```
**Example output:**
```bash
4.0K    /home/daniel/mylab
1.2G    /home/daniel/Videos
500M    /home/daniel/Downloads
```

**Combined monitoring with dstat**
```bash
sudo apt install dstat -y
dstat -c -d -n -m -y 2
```  
**Example output:**
```bash
----total-cpu-usage---- -dsk/total- ---net/total- ---memory- ---system--
usr sys idl wai hiq siq| read  writ| recv  send| used  buff  cach| int   csw
  5   1  94   0   0   0|  12k  24k|  0     0 |  500M 5120 2048k| 123   456

```


---

## ✅ Summary
You learned:
- Uptime: uptime
- Processes: ps, top, htop
- Memory: vmstat
- Disk: iostat, du
- Network: netstat, ss, iftop
- Logs: journalctl
- Services: systemctl
- Kill processes: kill
- Automation: Bash loops and batch commands

---

## 📸 Optional Exercises




Automate system monitoring every 5 minutes using cron or a script.
1. Track CPU/memory usage of a process every 10 seconds.  
2. Identify top 5 memory-hogging processes and safely terminate one. 
3. Monitor all listening ports and report unusual activity.  
4. Display contents with `cat`  
5. Save disk usage report for /var/log to a file.  

Practice these steps until you can do them **without looking at instructions**.

---

### Step 14 - Automation Example
```bash
for i in {1..5}; do top -b -n1 >> top_log.txt; sleep 60; done
```
**Explanation:**
Saves CPU/memory snapshot every minute.

---
