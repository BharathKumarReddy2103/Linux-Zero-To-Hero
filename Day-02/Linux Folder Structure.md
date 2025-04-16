# Linux Folder Structure:

Welcome to Day 2 of the **Linux Zero to Hero** series. In this article, we’ll take a deep dive into the **Linux folder structure**—a crucial foundation for every DevOps Engineer and Cloud Practitioner. Whether you're working on an EC2 instance, Docker container, or your own Linux setup, understanding these directories is essential for navigating, configuring, and managing a Linux-based environment.

---

## Table of Contents

- [Introduction](#introduction)
- [How to Access Linux Environments](#how-to-access-linux-environments)
- [Understanding the Linux Prompt](#understanding-the-linux-prompt)
- [Key Linux Directories and Their Use Cases](#key-linux-directories-and-their-use-cases)
  - [/ (Root)](#-root)
  - [/bin vs /sbin](#bin-vs-sbin)
  - [/usr](#usr)
  - [/etc](#etc)
  - [/home](#home)
  - [/opt](#opt)
  - [/srv](#srv)
  - [/mnt](#mnt)
  - [/tmp](#tmp)
  - [/var](#var)
  - [/proc, /dev, /sys, /run](#proc-dev-sys-run)
  - [/boot](#boot)
- [How Commands Are Located and Executed](#how-commands-are-located-and-executed)
- [Conclusion](#conclusion)

---

## Introduction

When you launch a Linux instance—on Docker, WSL, AWS EC2, or a local VM—you are greeted with a series of folders and a terminal prompt. But what do these directories actually do? Why are some commands available to everyone while others are restricted to root users?

This article explains the **purpose of each folder in a Linux system**, how system binaries are organized, and where to store configurations, logs, user data, and temporary files—essentials for anyone managing Linux environments in DevOps.

---

## How to Access Linux Environments

You can access a Linux environment in several ways:

- **Docker**: Spin up a container using a pre-built Docker image.
- **WSL** (Windows Subsystem for Linux): Run Ubuntu directly on your Windows machine.
- **Cloud Instances**: Use EC2 (AWS) or a VM (Azure/GCP).

```bash
# Example Docker command to start Linux environment
docker run -it -v /c/Users/yourname/data:/data ubuntu /bin/bash
```

---

## Understanding the Linux Prompt

Your terminal prompt usually looks like:

```
root@ubuntu:/#
```

It indicates:
- `root`: current user (admin)
- `ubuntu`: hostname
- `/`: current working directory (root of the file system)

If you log into an EC2 instance, the default user might be `ubuntu` and the path will typically be `/home/ubuntu`.

---

## Key Linux Directories and Their Use Cases

### `/` (Root)

- The top-level directory.
- Every other folder is a subdirectory of `/`.
- Equivalent to "My Computer" or "C:\" on Windows.

---

### `/bin` vs `/sbin`

#### `/bin` – User Binaries
- Contains basic Linux commands usable by all users.
- Examples: `ls`, `date`, `diff`, `cat`

#### `/sbin` – System Binaries
- Contains admin-level tools used for system management.
- Examples: `useradd`, `groupadd`, `reboot`

```bash
ls /bin
ls /sbin
```

---

### `/usr`

- Contains read-only user binaries, libraries, documentation.
- Often a larger directory with:
  - `/usr/bin`: user-level commands
  - `/usr/sbin`: system admin commands
  - `/usr/lib`: system libraries

```bash
ls /usr/bin
ls /usr/sbin
```

---

### `/etc`

- **One of the most important directories**.
- Stores configuration files for the system.
- Examples:
  - `/etc/hosts`: local DNS mapping
  - `/etc/os-release`: OS version details
  - `/etc/passwd`: user account info

```bash
cat /etc/os-release
```

---

### `/home`

- Contains directories for all non-root users.
- Example: `/home/ubuntu`, `/home/bharath`
- Each user has private space here.

---

### `/opt`

- Used for installing **third-party software** or custom tools.
- Ideal for enterprise deployments (e.g., Java, Tomcat, custom CLI tools).

```bash
cd /opt
mkdir myapp
```

---

### `/srv`

- "Server" directory.
- Stores data for web or FTP servers (e.g., `/srv/http`, `/srv/ftp`).
- Often used in production servers.

---

### `/mnt`

- Mount point for external storage like additional volumes.
- Example use case: attaching and mounting a 30GB EBS volume in AWS.

---

### `/tmp`

- Temporary files.
- Automatically cleaned up by system.
- Useful for scripts and short-lived logs.

```bash
cd /tmp
mkdir temp_folder
```

---

### `/var`

- Stores variable files, especially **logs**.
- Examples:
  - `/var/log/syslog`
  - `/var/log/apache2/error.log`
- Some packages store runtime or cache data here.

---

### `/proc`, `/dev`, `/sys`, `/run`

- These are **virtual and runtime-specific directories**.
- `/proc`: system process info
- `/dev`: device files (disks, USB, etc.)
- `/sys`: kernel and device info
- `/run`: runtime process data

---

### `/boot`

- Contains bootloader-related files (GRUB, kernel images).
- Mostly used during startup.
- Empty in Docker containers but essential in EC2 or bare metal systems.

---

## How Commands Are Located and Executed

Even when you type just `ls`, Linux knows how to find the executable using the `PATH` environment variable.

```bash
echo $PATH
# Output includes: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

which ls
# Output: /usr/bin/ls
```

The system searches each path in `PATH` until it finds the command. If the binary isn’t in one of those folders, you’ll get a “command not found” error.

---

## Conclusion

Understanding the Linux folder structure helps you:
- Troubleshoot systems effectively
- Organize custom tools and scripts
- Secure your environments by controlling user access
- Follow best practices in DevOps infrastructure management

Each directory has a purpose. Whether you're writing automation scripts, installing software, managing storage, or configuring services—this knowledge will empower you to work confidently in real-world Linux environments.
