# 🐧 Top 10 Essential Linux Commands Every Software Engineer Must Know

Linux powers the backbone of DevOps, Cloud, and Production infrastructure. Whether you’re deploying applications on Kubernetes, managing EC2 servers on AWS, or debugging CI/CD pipelines, mastering Linux commands is non-negotiable.

This article highlights the top 10 Linux commands (plus 2 bonus shortcuts) that every DevOps, Cloud, or System Engineer must know. Each command is explained with **real-world use cases**, **troubleshooting scenarios**, and **practical insights**.

---

## 📌 1. `top` and `htop` – Real-Time System Monitoring

### Use Case
Monitor CPU, memory, and process-level utilization in real-time.

### Example
```bash
top
````

If you want a visually enhanced version:

```bash
htop  # May require: sudo apt install htop
```

**Why it matters:** Helps identify resource-hungry processes and take immediate action like killing them or reporting to development teams.

---

## 🔍 2. `ps`, `pgrep`, `pstree` – Process Inspection Tools

### Use Case

Inspect running processes, fetch specific PIDs, and visualize process hierarchies.

### Examples

```bash
ps aux          # List all running processes
pgrep nginx     # Get PID of nginx process
pstree -p       # Show process tree with PIDs
```

**Why it matters:** Useful in scripting, automation, and investigating rogue or unknown processes.

---

## 🌐 3. `netstat` – Inspect Network Connections

### Use Case

View open ports and determine if a port is already in use.

### Example

```bash
netstat -tuln
```

**Why it matters:** Quickly identify port conflicts in microservices, applications, or servers.

---

## 🛠️ 4. `tcpdump` – Network Packet Analysis

### Use Case

Diagnose application or instance-level latency and analyze network packets.

### Example

```bash
sudo tcpdump -i eth0 port 80
```

You can export results and analyze in Wireshark for better visibility.

**Why it matters:** Critical for identifying connectivity issues from upstream/downstream sources.

---

## 🚀 5. `ping` and `traceroute` – Connectivity and Route Testing

### Use Case

Check network connectivity and path latency to external services.

### Examples

```bash
ping google.com
sudo apt install traceroute  # if not available
traceroute google.com
```

**Why it matters:** Helps determine if the issue is internal or external to your infrastructure.

---

## 💾 6. `df -h` and `du -sh` – Disk Space Troubleshooting

### Use Case

Track disk space at the system and folder level.

### Examples

```bash
df -h            # View disk usage across mounts
du -sh /opt      # View size of specific directory
```

**Why it matters:** Essential during “No space left on device” errors, especially in CI/CD agents.

---

## 🧠 7. `free -h` – Memory Utilization

### Use Case

Check memory status in human-readable format.

### Example

```bash
free -h
```

**Why it matters:** Quick view of memory pressure, crucial before scaling apps or debugging OOM issues.

---

## 📘 8. `journalctl` – View Systemd Logs

### Use Case

Review service logs managed by `systemd`.

### Examples

```bash
journalctl
journalctl -u nginx
```

**Why it matters:** Find why services like Nginx or Docker failed or restarted.

---

## 🔒 9. `lsof -i:<port>` – Identify Process Using a Port

### Use Case

Find which process is occupying a specific port.

### Example

```bash
sudo lsof -i:8085
```

**Why it matters:** Detect port clashes before app deployment or when load balancers fail health checks.

---

## 📄 10. `tail` and `head` – Log File Navigation

### Use Case

Read top or bottom lines of large log files.

### Examples

```bash
tail -n 10 /var/log/syslog   # Last 10 lines
head -n 10 /var/log/syslog   # First 10 lines
```

**Why it matters:** Saves time when analyzing thousands of log lines during on-call incidents.

---

## 💡 Bonus Shortcuts for DevOps Productivity

### 🔁 `Ctrl + R` – Reverse Search History

**Use Case:** Instantly recall previous commands.

```bash
# Press Ctrl + R and type "docker" to search past docker commands
```

**Why it matters:** Avoid retyping long commands; saves tons of time during active development.

---

### 🎨 Customize Terminal Prompt (PS1)

**Use Case:** Set personalized terminal prompt.

```bash
export PS1="Bharath@DevOpsShell: "
```

Or show working directory:

```bash
export PS1="\w \$ "
```

**Why it matters:** Visually distinguish between environments (local, staging, prod) to avoid mistakes.

---

## 🧠 Best Practices

* Use `top` + `htop` to proactively monitor resource consumption.
* Combine `ps` with `grep` or `pgrep` in shell scripts for automation.
* Always check open ports with `netstat` before assigning them to services.
* Use `tcpdump` only with `sudo` to capture accurate packet data.
* Rely on `journalctl` for service-level debugging, especially after reboots.
* Reverse search (`Ctrl + R`) instead of memorizing or retyping complex commands.

---

## 🏁 Conclusion

Whether you’re managing AWS EC2, debugging Kubernetes pods, or setting up a GitHub Actions pipeline, mastering these Linux commands can **boost your troubleshooting efficiency**, **reduce downtime**, and **make you a rockstar DevOps engineer**.

If you found this helpful, feel free to ⭐ star the repo, fork it, and contribute.
