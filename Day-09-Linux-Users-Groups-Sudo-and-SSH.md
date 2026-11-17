
# Day 09 – Linux Users, Groups, Sudo and SSH

## 1. Introduction

Linux user and access management is an important responsibility of a DevOps Engineer.

It helps administrators control who can access a Linux server, what resources they can use, and which administrative operations they can perform.

In this lesson, I learned about:

- Linux users and user management
- Linux groups and group management
- Root access and sudo privileges
- SSH (Secure Shell)
- Password-based and SSH key-based authentication
- Basic SSH troubleshooting

---

## 2. Linux User Management

Linux uses user accounts to control access to system resources.

### Types of Users

1. Root User
   - Superuser account.
   - Has UID 0.
   - Has administrative privileges.

2. Normal User
   - Used for regular system activities.
   - Has limited permissions.

3. System User
   - Used by system services and applications.
   - Usually does not require interactive login.

### Important Commands

```bash
whoami
id
who
w
```

### Create a User

```bash
sudo useradd -m devuser
sudo passwd devuser
```

### Modify a User

```bash
sudo usermod -s /bin/bash devuser
```

### Lock and Unlock a User

```bash
sudo passwd -l devuser
sudo passwd -u devuser
```

### Important User Configuration Files

| File | Purpose |
|---|---|
| `/etc/passwd` | Stores user account information |
| `/etc/shadow` | Stores password hashes and password aging information |

---

## 3. Linux Group Management

Groups allow administrators to manage permissions for multiple users efficiently.

### Types of Groups

- Primary Group: The default group associated with a user.
- Supplementary Group: Additional groups assigned to a user.

### Important Commands

Create a group:

```bash
sudo groupadd devops
```

Add a user to a supplementary group:

```bash
sudo usermod -aG devops devuser
```

Check group membership:

```bash
id devuser
groups devuser
```

List groups:

```bash
cat /etc/group
```

### Important Group Configuration Files

| File | Purpose |
|---|---|
| `/etc/group` | Stores group information |
| `/etc/gshadow` | Stores secure group information |

**Important:** Always use `-aG` when adding a supplementary group with `usermod`. Without `-a`, existing supplementary group memberships may be replaced.

---

## 4. Sudo and Root Privileges

`sudo` allows authorized users to execute commands with elevated privileges.

### Check Sudo Permissions

```bash
sudo -l
```

### Execute a Command as Administrator

```bash
sudo systemctl status sshd
```

### Configure Sudo Permissions Safely

```bash
sudo visudo
```

The sudoers configuration controls which users and groups can execute administrative commands.

On RHEL-based systems, members of the `wheel` group commonly receive sudo privileges when the relevant sudoers rule is enabled.

### Principle of Least Privilege

Users should receive only the permissions required to perform their responsibilities.

This improves security and reduces accidental changes.

---

## 5. SSH – Secure Shell

SSH is a secure protocol used to connect to remote Linux servers.

It normally uses TCP port 22.

### SSH Client and Server

- SSH Client: Initiates a connection.
- SSH Server (`sshd`): Accepts incoming SSH connections.

### Check SSH Service

On RHEL 9:

```bash
sudo systemctl status sshd
```

Check whether it is running:

```bash
systemctl is-active sshd
```

### Connect to a Remote Server

```bash
ssh username@server-ip
```

Example:

```bash
ssh devuser@192.168.1.100
```

Replace the example IP address with your actual server IP.

---

## 6. SSH Authentication Methods

### Password-Based Authentication

The user connects to a remote server and authenticates using a password.

### SSH Key-Based Authentication

SSH key authentication uses:

- Private Key: Kept securely on the client machine.
- Public Key: Stored on the remote server.

### Generate an SSH Key

```bash
ssh-keygen -t ed25519
```

### Public Key Location

```bash
~/.ssh/id_ed25519.pub
```

### Private Key Location

```bash
~/.ssh/id_ed25519
```

Never share your private key.

### Authorized Keys

The server stores permitted public keys in:

```bash
~/.ssh/authorized_keys
```

Typical Linux permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519
```

The private key permissions apply on the client machine.

---

## 7. SSH Troubleshooting

Useful commands:

Check the server IP:

```bash
ip addr
```

Check listening ports:

```bash
sudo ss -tlnp
```

Check SSH service:

```bash
sudo systemctl status sshd
```

Check SSH logs:

```bash
sudo journalctl -u sshd
```

Test SSH connectivity from Windows PowerShell:

```powershell
Test-NetConnection SERVER_IP -Port 22
```

Connect with verbose debugging:

```bash
ssh -v username@server-ip
```

Common SSH errors:

| Error | Possible Cause |
|---|---|
| Connection refused | SSH service not listening |
| Connection timed out | Network or firewall issue |
| Permission denied | Authentication or account permission issue |
| Host key verification failed | Remote host key changed or does not match |

---

## 8. Practical Exercises

### Exercise 1: Check Current User

```bash
whoami
id
```

### Exercise 2: Create a User

```bash
sudo useradd -m testuser
sudo passwd testuser
```

### Exercise 3: Create a Group

```bash
sudo groupadd testgroup
sudo usermod -aG testgroup testuser
id testuser
```

### Exercise 4: Check Sudo Permissions

```bash
sudo -l
```

### Exercise 5: Check SSH Service

```bash
sudo systemctl status sshd
```

### Exercise 6: Test SSH Connectivity

From Windows PowerShell:

```powershell
Test-NetConnection SERVER_IP -Port 22
```

Only perform account creation and modification exercises on your own test VM. Avoid deleting or modifying existing system accounts.

---

## 9. Real-World DevOps Applications

1. User Access Management:
   Administrators create separate accounts for developers and operations teams.

2. Secure Server Access:
   SSH keys provide secure authentication for remote Linux servers.

3. CI/CD Automation:
   Deployment systems use controlled credentials to connect to servers.

4. Team Permission Management:
   Groups simplify permission management for multiple team members.

5. Security:
   Sudo and least privilege reduce unnecessary administrative access.

---

## 10. Interview Questions

**Q1. What is the root user in Linux?**

The root user is the superuser account with UID 0 and full administrative privileges.

**Q2. What is the difference between a primary and supplementary group?**

A primary group is the default group associated with a user, while supplementary groups provide additional group memberships.

**Q3. What is sudo?**

Sudo allows authorized users to execute commands with elevated privileges.

**Q4. What is SSH?**

SSH is a secure protocol used to connect to remote systems over a network.

**Q5. What is the difference between a public and private SSH key?**

The public key is placed on the remote server, while the private key remains securely on the client machine.

**Q6. What is the default SSH port?**

The default SSH port is TCP 22.

**Q7. What is the purpose of the /etc/shadow file?**

It stores password hashes and password aging information for Linux accounts.

---

## 11. Key Takeaways

- Linux users control access to system resources.
- Groups simplify permission management.
- Sudo provides controlled administrative access.
- SSH enables secure remote server connectivity.
- SSH key authentication is commonly used in DevOps automation.
- Least privilege is an important security principle.

---

## 12. Day 09 Completion Status

- [x] Linux User Management
- [x] Linux Group Management
- [x] Root and Sudo Privileges
- [x] SSH Fundamentals
- [x] SSH Authentication Methods
- [x] SSH Troubleshooting
- [x] Practical Exercises
- [x] Interview Preparation

**Status: COMPLETED**

**Learning Journey: Day 9 of 77**

Next Topic: Day 10 – Linux Permissions, Ownership and ACL
