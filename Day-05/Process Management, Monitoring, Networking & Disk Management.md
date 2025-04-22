# Process Management, Monitoring, Networking & Disk Management

Welcome to Day 5 of the **Linux Zero to Hero** series. In this comprehensive guide, we explore four critical areas for any DevOps Engineer or Linux Administrator:

- Process Management  
- System Monitoring  
- Networking (with resources)  
- Disk Management  

This article includes practical commands, real-world use cases, and actionable insights to help you master Linux in production environments.

---

## 🧠 1. What is a Process in Linux?

A **process** is a running instance of a program. It can be:

- A Python script executing a task
- A cron job performing scheduled actions
- A web server like Nginx or Apache serving pages

Linux manages processes via the operating system kernel, which schedules CPU, memory, and I/O access.

### 💡 Real-world Example

If a Python-based ML model is consuming 90% of the CPU, other processes (like a shell script or web server) will get throttled. This can cause performance degradation or system hangs.

---

## ⚙️ 2. Process Management in Linux

As a DevOps engineer, you are expected to:

- View all running processes
- Kill or stop misbehaving processes
- Resume stopped processes
- Prioritize or deprioritize process scheduling

### 🔍 View Running Processes

```bash
ps aux            # Show all processes with CPU and memory usage
ps -ef            # Similar, but without memory usage columns
ps aux | nl       # Number each process line
ps aux | wc -l    # Count running processes
```

### 💀 Kill a Process

```bash
kill <PID>        # Normal kill
kill -9 <PID>     # Force kill
kill -3 <PID>     # Get thread dumps (Java)
```

Use `grep` to find a specific process:

```bash
ps aux | grep java
ps aux | grep java | grep -v grep
```

### ⏸ Stop / Resume a Process

```bash
kill -STOP <PID>  # Temporarily pause a process
kill -CONT <PID>  # Resume a paused process
```

### 🔼 Prioritize / Deprioritize a Process

```bash
renice -n 10 -p <PID>     # Lower priority (less CPU time)
renice -n -5 -p <PID>     # Increase priority (more CPU time)
```

Range:
- `-20` = highest priority
- `19` = lowest priority

---

## 🔁 3. Services in Linux

**Services** are special background processes that start on boot.

### Examples:
- Apache / Nginx web servers
- cron jobs
- cloud-init on AWS EC2

### 🔧 Manage Services using `systemctl`

```bash
systemctl list-units --type=service  # List all active services
systemctl start <service>            # Start service
systemctl stop <service>             # Stop service
```

---

## 📊 4. System Monitoring in Linux

Linux administrators regularly monitor:

- CPU usage
- Memory usage
- Disk utilization

### 🧰 Useful Commands

```bash
top                 # Real-time view of system processes
htop                # Enhanced visual interface (if installed)
vmstat              # System performance overview
free -h             # Memory usage in human-readable format
nproc               # Number of CPUs
df -h               # Disk usage of mounted filesystems
du -sh *            # Disk usage per directory
```

---

## 🌐 5. Networking Fundamentals

Networking is crucial for DevOps.
 
Learn about:

- IP addressing and subnets
- OSI model
- Private vs public networks
- DNS and latency troubleshooting

---

## 💽 6. Disk Management in Linux

As applications grow, so do log files and installed packages. Managing disk efficiently is vital.

### 🔍 Check Attached Volumes

```bash
lsblk                 # List block devices and partitions
sudo fdisk -l         # Detailed disk layout
```

### ➕ Add and Mount a New Volume

1. Create an EBS volume (e.g., 10 GB in same AZ)
2. Attach volume to instance (e.g., `/dev/xvdf`)
3. Format and mount:

```bash
sudo mkfs -t ext4 /dev/xvdf               # Format to ext4
sudo mkdir -p /mnt/demo-volume            # Create mount directory
sudo mount /dev/xvdf /mnt/demo-volume     # Mount it
```

4. Confirm disk:

```bash
df -h
```

5. Optional: Unmount when needed

```bash
sudo umount /mnt/demo-volume
```

---

## 🔧 Advanced Monitoring Tools

For production environments, integrate with:

- **Prometheus** (scrapes metrics using Node Exporter)
- **Grafana** (visual dashboards and alerts)
- **AWS CloudWatch** (monitoring EC2 instances)

---

## ✅ Summary: Essential Linux Commands

| Task                    | Command |
|-------------------------|---------|
| View Processes          | `ps aux`, `ps -ef` |
| Kill Process            | `kill <PID>`, `kill -9 <PID>` |
| Stop / Resume Process   | `kill -STOP`, `kill -CONT` |
| Prioritize Process      | `renice -n <value> -p <PID>` |
| Monitor System          | `top`, `htop`, `vmstat`, `free -h`, `df -h`, `du -sh *` |
| Manage Services         | `systemctl start/stop <service>` |
| Check CPUs / Memory     | `nproc`, `free -h` |
| Disk / Volume Handling  | `lsblk`, `fdisk -l`, `mount`, `umount`, `mkfs` |

---

## 📌 Best Practices

- Regularly monitor high CPU/memory-consuming processes
- Use services for critical apps to auto-start on reboot
- Integrate with Prometheus + Grafana for visibility
- Keep logs compressed and rotated to save disk
- Always validate volume formatting and mount points

---

## 🚀 Conclusion

Understanding Linux internals such as process management, service lifecycle, resource monitoring, and disk operations is essential for any DevOps or Cloud Engineer. These foundational skills help with:

- Efficient system debugging
- Ensuring high availability
- Optimizing performance
- Automating infrastructure tasks


If you found this guide helpful, consider **star ⭐ the repo**, **fork it**, and **follow** me for more DevOps content.
