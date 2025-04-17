# User Management, File Management & Vim Editor:

Welcome to Day 3 of the **Linux Zero to Hero** series
In this guide, we cover three critical sections of Linux that are essential for any DevOps or Cloud Engineer:

- User Management  
- File and Directory Management  
- Working with the Vim Editor  

By the end of this article, you'll be able to securely manage users and groups, navigate the file system confidently, and use Vim to edit files like a pro.

---

## 📌 Table of Contents

1. [Why User Management is Important](#why-user-management-is-important)
2. [User Management in Linux](#user-management-in-linux)
3. [Group Management in Linux](#group-management-in-linux)
4. [Connecting to a Remote Linux Server via SSH](#connecting-to-a-remote-linux-server-via-ssh)
5. [File and Directory Management](#file-and-directory-management)
6. [Vim Editor: Modes and Shortcuts](#vim-editor-modes-and-shortcuts)
7. [Best Practices and Real-World Use Cases](#best-practices-and-real-world-use-cases)
8. [Conclusion](#conclusion)

---

## Why User Management is Important

Unlike personal laptops, production Linux servers in organizations are accessed by multiple users. Granting all users access to the `root` account creates serious risks:

- **No accountability** for who made what change
- Accidental or malicious deletion of critical directories (e.g., `/sbin`)
- No control over user permissions

To solve this, Linux provides **user and group-based permission management**, making environments secure and auditable.

---

## User Management in Linux

### ➕ Creating a User

```bash
# Basic user creation
useradd bharath

# Check if user is added
cat /etc/passwd | grep bharath
```

### 🔐 Setting a Password

```bash
passwd bharath
```

To verify encrypted passwords:

```bash
cat /etc/shadow | grep bharath
```

> ❗ **Note:** Passwords in `/etc/shadow` are hashed using SHA-256 and are not reversible.

### 🗑️ Deleting a User

```bash
userdel bharath
```

---

### ✅ `useradd` vs `adduser` (Interview Question)

| Command     | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| `useradd`   | Non-interactive. Doesn't create home directory or prompt for details.       |
| `adduser`   | Interactive. Prompts for user info and creates a home directory.            |

Use `useradd` in scripts and automation pipelines. Use `adduser` when working manually.

---

### ⛓️ Locking and Expiring Passwords

```bash
# Set password to expire every 90 days
chage -M 90 bharath

# Lock user account
usermod -L bharath

# Unlock user account
usermod -U bharath
```

---

## Group Management in Linux

### ➕ Creating and Viewing Groups

```bash
# Create group
groupadd devops

# View groups
cat /etc/group | grep devops
```

### 👥 Adding User to a Group

```bash
usermod -aG devops bharath
```

This simplifies managing permissions for teams like `developers`, `QAs`, `DevOps`, etc.

---

## Connecting to a Remote Linux Server via SSH

SSH allows secure remote access to Linux servers.

### 🧑‍💻 What You Need

- **SSH client**: Git Bash (Windows), Terminal (Mac/Linux)
- **Credentials**: Provided by your admin (username, IP, password or `.pem` key)

### 🔐 Connect using password:

```bash
ssh bharath@<IP_ADDRESS>
```

### 🔐 Connect using `.pem` file (AWS-like environments):

```bash
ssh -i "my-key.pem" ec2-user@<IP_ADDRESS>
```

> By default, password login might be disabled in cloud VMs. Admins can modify `/etc/ssh/sshd_config` and restart SSH service:
```bash
sudo systemctl restart sshd
```

---

## File and Directory Management

### 📁 Common Commands

```bash
# List files
ls

# Present working directory
pwd

# Change directory
cd /tmp

# Go back to previous directory
cd ..

# Create directory
mkdir testdir

# Delete directory
rmdir testdir
```

---

### 📄 File Commands

```bash
# Create a file
touch ab.txt

# Copy file
cp ab.txt ab_copy.txt

# Rename file
mv ab.txt ab_renamed.txt

# Delete file
rm ab_renamed.txt
```

---

### 📚 View File Content

```bash
# View entire file
cat filename.txt

# View first 10 lines
head -n 10 filename.txt

# View last 20 lines
tail -n 20 filename.txt

# View file page by page
less filename.txt
```

---

### ➕ Append Content

```bash
# Overwrite file
echo "Hello World" > filename.txt

# Append to file
echo "Another Line" >> filename.txt
```

---

## Vim Editor: Modes and Shortcuts

### 📝 Getting Started with Vim

```bash
# Install vim if not present
sudo apt install vim

# Open a file
vim myfile.txt
```

### 🧠 Vim Modes

| Mode         | Description                              |
|--------------|------------------------------------------|
| Normal       | Default mode; navigate using arrows      |
| Insert       | Press `i` to enter insert (write) mode   |
| Command      | Press `Esc`, then `:` to enter commands  |

### 💾 Save and Quit

```text
:wq     # Save and quit
:q!     # Quit without saving
```

---

## 📈 Best Practices and Real-World Use Cases

- **Never use `root` for daily operations**. Create users with limited permissions.
- **Use groups** to manage teams like `dev`, `qa`, and `devops`.
- **Automate user creation** using `useradd` in bash scripts for scalability.
- **Secure SSH Access** with `.pem` or SSO instead of passwords.
- **Enable password rotation** using `chage` for better compliance.

---

## Conclusion

In this session, we learned the following:

✅ Why user and group management is crucial for security  
✅ How to create, modify, and delete users/groups  
✅ Securely connect to remote Linux servers using SSH  
✅ Master basic file handling and directory commands  
✅ Use the Vim editor to create, edit, and navigate files  

These fundamentals form the **foundation of Linux administration** in real-world DevOps and Cloud environments. Make sure to revisit the README in your GitHub repository for all command references.

---

## ✨ Stay Connected

If you found this helpful, feel free to:

- ⭐ Star this repository
- 🍴 Fork and try the commands yourself
- 🧑‍💻 Share your feedback or contribute improvements

