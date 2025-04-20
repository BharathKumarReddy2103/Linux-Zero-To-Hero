# 🛡️ Linux File and Folder Permissions – `chmod` & `chown` Deep Dive

Welcome to Day 4 of the **Linux Zero to Hero** series. In this article, we will explore one of the most crucial aspects of Linux administration — **file and folder permissions**.

Properly configuring file permissions is essential in multi-user Linux environments, where developers, QA engineers, and DevOps professionals need different levels of access to system resources.

---

## 🔍 Table of Contents

- [Why File Permissions Matter](#why-file-permissions-matter)
- [Default Permissions in Linux](#default-permissions-in-linux)
- [Understanding Permission Notation](#understanding-permission-notation)
- [Symbolic vs Numeric Mode](#symbolic-vs-numeric-mode)
- [Modifying File Permissions with `chmod`](#modifying-file-permissions-with-chmod)
- [Changing Ownership with `chown`](#changing-ownership-with-chown)
- [Folder vs File Permissions](#folder-vs-file-permissions)
- [Real-World Analogy: Bank vs Locker](#real-world-analogy-bank-vs-locker)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)

---

## ✅ Why File Permissions Matter

Linux is a **multi-user operating system**. Multiple users access the same machine — developers, QA engineers, DevOps engineers — and not everyone should have full control over every file or folder.

Without proper permissions:
- Users can accidentally or maliciously delete critical system files
- Productivity scripts may get overwritten
- File integrity may be compromised

That's why Linux enforces a robust permission system to isolate access and actions between users.

---

## 🔐 Default Permissions in Linux

When a user creates a file or folder, Linux automatically sets default permissions. These defaults allow:
- The **file owner** to read and write
- The **group** (user’s group) to read
- **Others** to read

However, these permissions can be **modified** using commands like:

```bash
chmod   # Change permissions
chown   # Change file owner or group
```

---

## 🧠 Understanding Permission Notation

Every file or directory has a **10-character permission string** shown in `ls -l`:

```bash
-rw-r--r--
```

- First character: file type (`-` = file, `d` = directory)
- Next 9 characters: 3 sets of 3 (user, group, others)
  - `r` = read (4)
  - `w` = write (2)
  - `x` = execute (1)
  - `-` = no permission

### Example

```bash
-rw-r--r--
```

| Entity   | Permissions | Meaning           |
|----------|-------------|-------------------|
| User     | rw-         | Read, Write       |
| Group    | r--         | Read only         |
| Others   | r--         | Read only         |

---

## ✍️ Symbolic vs Numeric Mode

### 1. Symbolic Mode

```bash
chmod u=rwx,g=rw,o=r file.txt
```

- `u` = user
- `g` = group
- `o` = others

### 2. Numeric Mode

Each permission is represented by a number:
- `r = 4`, `w = 2`, `x = 1`
- `rwx = 7`, `rw- = 6`, `r-- = 4`, `--- = 0`

```bash
chmod 755 file.txt
```

| Entity   | Permissions | Value |
|----------|-------------|-------|
| User     | rwx         | 7     |
| Group    | r-x         | 5     |
| Others   | r-x         | 5     |

---

## 🔧 Modifying File Permissions with `chmod`

```bash
chmod 777 script.sh      # Full access to all
chmod 400 secret.txt     # Read-only for owner
chmod u+x file.sh        # Add execute for owner
chmod o-r file.txt       # Remove read for others
```

### Real-World Demo

```bash
# Create two users
adduser developer
adduser qa

# As developer, create a script
su developer
cd /tmp
echo -e '#!/bin/bash\necho Hello World' > hello.sh
chmod 644 hello.sh

# As QA, try editing the file
su qa
vim /tmp/hello.sh  # You'll get "Permission denied"
```

---

## 👥 Changing Ownership with `chown`

```bash
chown qa:qa hello.sh
```

- Changes ownership from `developer` to `qa`
- Requires root privileges

### Example:

```bash
sudo chown bharath:devops_team report.csv
```

---

## 📁 Folder vs File Permissions

**Important:** Folder permissions determine whether a user can:
- Enter the directory (`x`)
- List files (`r`)
- Create/delete files (`w`)

Even if a file is `777`, you can’t access it if its **parent folder denies access**.

### Real-World Analogy: Bank & Locker

- **Bank** = Folder
- **Locker** = File

You can't access the locker without entering the bank. Similarly, a file is useless if you don’t have access to its parent folder.

---

## 💡 Best Practices

- Never use `chmod 777` in production
- Use groups to manage shared access
- Apply the **principle of least privilege**
- Regularly audit file and folder permissions
- Use numeric mode for automation and scripting

---

## 🔚 Conclusion

Linux file and folder permissions are foundational for maintaining a secure, multi-user environment. By mastering `chmod` and `chown`, you can confidently control access across your system.

🔄 Whether you’re automating with scripts, managing cloud infrastructure, or building CI/CD pipelines — understanding Linux permissions is non-negotiable.

---

⭐ **Practice Exercises**
- Set up a directory accessible only to developers
- Create a shared file writable by a group
- Lock down a config file to read-only for everyone

---

> ✅ Don’t forget to fork the repo, try these commands, and explore the power of Linux permissions.
