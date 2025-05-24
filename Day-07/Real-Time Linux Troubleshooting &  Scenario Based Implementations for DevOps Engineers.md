# 🔧 Real-Time Linux Troubleshooting & Scenario Based Implementations for DevOps Engineers

## 🌟 Introduction

In real-world DevOps and Cloud environments, system performance and uptime are critical. Whether you're managing servers on-prem or in the cloud (AWS, Azure, GCP), being equipped with the right Linux troubleshooting commands can save hours of debugging and downtime. This guide covers 30+ essential Linux commands with real-time examples to help DevOps Engineers diagnose, debug, and optimize their infrastructure effectively.

---

## 🔍 Process & Memory Troubleshooting

### 🧠 Identify High Memory Usage

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -n 5
````

* Sorts processes by memory usage.
* Use `kill -9 <PID>` to terminate any unresponsive memory-hogging process.

### 🧠 Kill Process with sudo

```bash
sudo kill -9 <PID>
```

Use when normal kill fails due to permission issues.

---

## 🛠️ File Change Auditing

### 🔄 Find Recently Modified Files (last 2 hours)

```bash
find /your/dir -type f -mmin -120
```

* Helpful to debug issues after recent code or config changes.

---

## 👤 Temporary User Access Management

```bash
sudo useradd -e 2025-06-01 user1
sudo passwd user1
sudo chage -d 0 user1
```

* Creates a user that expires after 1 week.
* Forces password reset on first login.

---

## 🚪 Port Conflict Troubleshooting

### 🔎 Check Which Process Is Using a Port

```bash
sudo lsof -i :8080
```

* Useful when Docker container fails to start due to port conflicts.

---

## ⏰ Scheduled Jobs Debugging

### 📋 List User's Cron Jobs

```bash
crontab -u <username> -l
```

---

## 💾 Configuration File Backups

### 📦 Backup Only `.conf` Files using rsync

```bash
rsync -av --include '*/' --include '*.conf' --exclude '*' --prune-empty-dirs /etc/nginx/ ./backup/nginx/
```

---

## 🚀 CPU Monitoring in Real-Time

```bash
top -o %CPU
```

* Sorts processes by CPU usage in real-time.

---

## 📜 Previous Boot Logs

```bash
journalctl -b -1
```

* Check logs before a system reboot.

---

## 🧟 Identify Zombie Processes

```bash
ps -eo pid,stat,cmd | awk '$2 ~ /Z/ { print }'
```

* Z state means zombie processes.

---

## ⏳ System Uptime

```bash
uptime
```

---

## ✅ Check Executable Files in Directory

```bash
find /your/dir -type f -executable
```

---

## 🌐 Active TCP Connections

```bash
sudo netstat -ntu | grep ESTABLISHED | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr | head
```

---

## 📊 INode Usage

```bash
df -i
```

* Helps identify inode exhaustion issues.

---

## 🔴 Watch Logs in Real-Time for Errors

```bash
tail -f /var/log/syslog | grep --line-buffered -i error
```

---

## 🌍 DNS Resolution (Find IP from Domain)

```bash
nslookup google.com
```

---

## 📉 Limit Bandwidth While Downloading

```bash
wget --limit-rate=1m <url>
```

---

## 🧩 Remote Maintenance Shutdown via Message

```bash
sudo shutdown -r +1 "Rebooting for maintenance. Save your work."
```

---

## 👥 List Logged In Users

```bash
w
```

---

## 🧨 Kill All Processes for a User

```bash
sudo pkill -u <username>
```

---

## 🔍 View Nginx Live Logs

```bash
sudo journalctl -u nginx.service -f
```

---

## 🌲 Visualize Process Tree

```bash
pstree -p
```

---

## 📌 Best Practices

* Always validate commands in non-production environments first.
* Use `sudo` judiciously.
* Maintain proper log rotation and monitoring tools (e.g., Prometheus, Grafana).
* Document every operational task and automate when possible.

---

## 🚀 Conclusion

These 30+ Linux commands are your Swiss Army knife for daily DevOps operations. Whether you’re debugging a failing deployment, tracking down memory leaks, or monitoring real-time logs, mastering these commands gives you control over any production Linux system.
