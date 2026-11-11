
# Day 4 – Linux for DevOps

**75 Days of DevOps Learning Journey**

**Today's Topic:** Linux Administration and Troubleshooting

**Environment:** Red Hat Enterprise Linux 9 (RHEL 9)

---

## Learning Objectives

Today, I focused on strengthening my Linux fundamentals and understanding how Linux administration is used in DevOps.

By the end of this session, I learned:

1. Linux filesystem structure and navigation.
2. Essential Linux commands.
3. File and directory management.
4. Linux users and groups.
5. Linux file permissions.
6. Process management.
7. Service management using systemd.
8. Log monitoring and troubleshooting.
9. Disk and memory troubleshooting.
10. Basic Linux administration.

---

## Part 1 – Linux Filesystem Structure

Linux follows a hierarchical filesystem structure that starts from the root directory `/`.

Important Linux directories:

| Directory | Purpose |
|---|---|
| `/` | Root filesystem |
| `/home` | User home directories |
| `/root` | Root user's home directory |
| `/etc` | System configuration files |
| `/var` | Logs and changing data |
| `/tmp` | Temporary files |
| `/boot` | Boot-related files |
| `/usr` | Applications and utilities |
| `/opt` | Optional software |
| `/dev` | Device files |
| `/proc` | Process and kernel information |
| `/sys` | Kernel and hardware information |

### Commands Practiced

```bash
cat /etc/redhat-release
hostname
hostnamectl
whoami
pwd
date
uptime
uname -r
```

---

## Part 2 – Essential Linux Commands

### Directory Navigation

| Command | Purpose |
|---|---|
| `pwd` | Display current directory |
| `ls` | List files and directories |
| `ls -l` | Detailed listing |
| `ls -la` | Display hidden files |
| `cd /tmp` | Change directory |
| `cd ..` | Move one directory back |
| `cd ~` | Go to home directory |

### File Management

| Command | Purpose |
|---|---|
| `touch file.txt` | Create an empty file |
| `mkdir test` | Create a directory |
| `cp file1 file2` | Copy a file |
| `mv file1 file2` | Move or rename a file |
| `cat file.txt` | Display file contents |
| `less file.txt` | Read files page by page |
| `head file.txt` | Display first lines |
| `tail file.txt` | Display last lines |
| `rm file.txt` | Delete a file |
| `rmdir test` | Remove an empty directory |

### Practical Exercise

```bash
cd /tmp
mkdir devops-day4
cd devops-day4

touch linux-notes.txt
echo "Day 4 Linux learning" > linux-notes.txt

cat linux-notes.txt

cp linux-notes.txt backup.txt
mv backup.txt linux-backup.txt

ls -l
cat linux-backup.txt
```

Appending content:

```bash
echo "Learning Linux administration" >> linux-notes.txt
cat linux-notes.txt
```

**Important:**
- `>` overwrites existing file contents.
- `>>` appends content to an existing file.

---

## Part 3 – Linux Users and Groups

Linux supports multiple users and groups.

Every user has a User ID (UID), and every group has a Group ID (GID).

### Important Commands

| Command | Purpose |
|---|---|
| `whoami` | Display current username |
| `id` | Display user and group IDs |
| `who` | Show logged-in users |
| `groups` | Display group membership |
| `getent passwd` | Display user account entries |
| `getent group` | Display group entries |
| `useradd` | Create a user |
| `passwd` | Set user password |
| `groupadd` | Create a group |
| `usermod -aG` | Add user to a supplementary group |

### Practical Exercise

Check current user information:

```bash
whoami
id
groups
getent passwd root
```

Optional test user and group creation:

```bash
sudo groupadd devops-team
sudo useradd -m devopsuser
sudo usermod -aG devops-team devopsuser

id devopsuser
```

Optional cleanup of the test account:

```bash
sudo userdel -r devopsuser
sudo groupdel devops-team
```

Note: Only execute cleanup commands if you created these test accounts.

---

## Part 4 – Linux File Permissions

Linux permissions control who can read, write and execute files.

There are three permission categories:

- User (Owner)
- Group
- Others

### Permission Values

| Permission | Symbol | Numeric Value |
|---|---|---|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |

Example:

`chmod 755 script.sh`

Permission breakdown:

- Owner: 7 = Read + Write + Execute
- Group: 5 = Read + Execute
- Others: 5 = Read + Execute

### Important Commands

```bash
chmod 644 file.txt
chmod 755 script.sh
ls -l
```

Changing ownership:

```bash
sudo chown user:group file.txt
```

### Practical Exercise

```bash
cd /tmp/devops-day4

touch testfile.txt
chmod 644 testfile.txt

ls -l testfile.txt

chmod 755 testfile.txt

ls -l testfile.txt
```

Expected permissions:

- 644 = `-rw-r--r--`
- 755 = `-rwxr-xr-x`

**Important:** Avoid using `chmod 777` unnecessarily because it gives everyone full permissions.

---

## Part 5 – Linux Process Management

A process is a running instance of a program.

Linux assigns a unique Process ID (PID) to each running process.

### Important Commands

| Command | Purpose |
|---|---|
| `ps` | Display processes |
| `ps aux` | Detailed process listing |
| `top` | Live process monitoring |
| `pgrep sshd` | Find matching process IDs |
| `free -h` | Check memory usage |
| `kill PID` | Send a signal to a process |

### Practical Exercise

```bash
ps
ps aux
top
```

Press `q` to exit top.

Check SSH processes:

```bash
pgrep -a sshd
```

---

## Part 6 – Service Management Using systemd

RHEL 9 uses systemd to manage system services.

`systemctl` is the command-line utility used to manage these services.

### Important Commands

| Command | Purpose |
|---|---|
| `systemctl status sshd` | Check service status |
| `systemctl is-active sshd` | Check whether service is active |
| `systemctl start sshd` | Start service |
| `systemctl stop sshd` | Stop service |
| `systemctl restart sshd` | Restart service |
| `systemctl enable sshd` | Enable automatic startup |
| `systemctl disable sshd` | Disable automatic startup |

### Practical Exercise

Check SSH service status:

```bash
sudo systemctl status sshd
```

Check whether it is active:

```bash
sudo systemctl is-active sshd
```

Check whether it is enabled at boot:

```bash
sudo systemctl is-enabled sshd
```

**Important:**

- `start` runs a service immediately.
- `enable` configures automatic startup during boot.
- These commands perform different operations.

Avoid stopping SSH if you are using it for remote access.

---

## Part 7 – Linux Logs and Troubleshooting

Logs help administrators identify problems and investigate system failures.

### Important Log Locations

| Location | Purpose |
|---|---|
| `/var/log/messages` | General system messages |
| `/var/log/secure` | Authentication and security events |
| `/var/log/cron` | Cron job activity |
| `journalctl` | Systemd journal logs |

Log file availability depends on system configuration.

### Important Commands

Display the latest 20 log entries:

```bash
sudo journalctl -n 20
```

Check SSH service logs:

```bash
sudo journalctl -u sshd
```

Display recent error-level logs:

```bash
sudo journalctl -p err -n 20
```

Follow logs live:

```bash
sudo journalctl -f
```

Press `Ctrl + C` to exit.

### Troubleshooting Approach

If an application fails to start:

1. Check the application service status.
2. Review the service logs.
3. Identify the error.
4. Investigate the root cause.
5. Apply the required fix.
6. Restart the service if necessary.
7. Verify application functionality.

---

## Part 8 – Disk and Memory Troubleshooting

Disk and memory monitoring are important Linux administration activities.

### A. Check Disk Usage

```bash
df -h
```

Displays filesystem size, used space and available space.

### B. Identify Large Directories

```bash
sudo du -sh /var/log
sudo du -h --max-depth=1 /var/log
```

### C. Check Memory Usage

```bash
free -h
```

Important memory metrics:

- Total memory
- Used memory
- Free memory
- Available memory
- Swap usage

### D. Check CPU and System Load

```bash
uptime
top
```

### E. Identify Processes Using the Most Memory

```bash
ps aux --sort=-%mem | head
```

### Practical Troubleshooting Exercise

```bash
df -h
free -h
uptime
ps aux --sort=-%mem | head
```

These commands help identify disk utilization, memory availability, system load and resource-consuming processes.

**Important:** Never delete system logs or application data blindly. Investigate the root cause before cleaning anything.

---

## Part 9 – Practical Linux Administration Challenge

### Scenario

A company needs a directory for application logs with appropriate file permissions.

### Step 1: Create a directory

```bash
mkdir -p /tmp/devops-app/logs
```

### Step 2: Create a log file

```bash
touch /tmp/devops-app/logs/application.log
```

### Step 3: Add sample log entries

```bash
echo "Application started successfully" >> /tmp/devops-app/logs/application.log

echo "Database connection successful" >> /tmp/devops-app/logs/application.log
```

### Step 4: Read log contents

```bash
cat /tmp/devops-app/logs/application.log
```

Expected output:

```text
Application started successfully
Database connection successful
```

### Step 5: Configure permissions

```bash
chmod 755 /tmp/devops-app
chmod 755 /tmp/devops-app/logs
chmod 644 /tmp/devops-app/logs/application.log
```

### Step 6: Verify permissions

```bash
ls -ld /tmp/devops-app
ls -ld /tmp/devops-app/logs
ls -l /tmp/devops-app/logs/
```

### Step 7: Check system resources

```bash
df -h
free -h
```

**Practical Outcome:** Created application log directories, added sample log entries, configured permissions and verified system resources.

---

## Part 10 – Common Linux Administration Mistakes

| Mistake | Correct Approach |
|---|---|
| Using `rm -rf` without checking paths | Verify paths before deleting |
| Giving every file 777 permissions | Apply minimum required permissions |
| Confusing start with enable | Understand runtime and boot configuration |
| Deleting logs blindly | Investigate disk usage first |
| Restarting services without checking | Review status and logs |
| Ignoring memory cache | Check available memory using `free -h` |
| Using sudo for every command | Use elevated privileges only when needed |

---

## Part 11 – Interview Preparation

### 1. What is Linux?

Linux is an open-source operating system commonly used in servers, cloud infrastructure and DevOps environments.

### 2. Difference between chmod and chown?

`chmod` changes file permissions, while `chown` changes file ownership.

### 3. Difference between a process and a service?

A process is a running instance of a program. A service is a background application managed by the operating system, usually through systemd.

### 4. Difference between systemctl start and enable?

`start` runs the service immediately, while `enable` configures the service to start automatically during system boot.

### 5. How do you check disk and memory usage?

For disk usage, I use `df -h` and `du -sh`. For memory usage, I use `free -h` and `top`.

### 6. How do you troubleshoot a slow Linux server?

First, I check CPU and system load using `top` and `uptime`. Then I check memory using `free -h`, disk usage using `df -h` and identify resource-consuming processes. Finally, I check system logs to investigate the root cause.

### 7. How do you check Linux system logs?

I use `journalctl` to check system logs. For example, `journalctl -n 20` displays the latest 20 entries, and `journalctl -u sshd` displays SSH service logs.

---

## Part 12 – Day 4 Completion Checklist

- [x] Linux filesystem structure
- [x] Essential Linux commands
- [x] File and directory management
- [x] User and group management
- [x] Linux file permissions
- [x] Process management
- [x] systemctl and systemd services
- [x] Linux logs and troubleshooting
- [x] Disk usage monitoring
- [x] Memory monitoring
- [x] Practical Linux administration challenge
- [x] Interview preparation

---

## Day 4 – Key Takeaways

Linux is the foundation of many DevOps tools and technologies.

A DevOps Engineer should understand Linux administration, filesystem management, permissions, process management, services, logs and troubleshooting.

Practical command-line knowledge is essential for managing servers and supporting reliable application deployments.

**Day 4 Status: Completed**

**Next Topic: Day 5 – Advanced Linux Administration and Bash Scripting**

**75 Days of DevOps Learning Journey**
