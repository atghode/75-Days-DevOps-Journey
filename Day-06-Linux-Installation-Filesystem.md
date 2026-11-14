
# Day 6 – Linux Installation, Filesystem and Directory Structure

## Overview
As part of my 77-Day DevOps Learning Journey, Day 6 focuses on Linux installation concepts, filesystem hierarchy, directory navigation, and file management.

Linux is widely used in DevOps, cloud computing, server administration, automation, and application deployment.

## Learning Objectives
- Understand different Linux installation methods.
- Understand Linux filesystem hierarchy.
- Learn absolute and relative paths.
- Practise Linux directory navigation.
- Create, copy, move, and rename files.
- Perform basic filesystem checks.

## 1. Linux Installation Methods

Common Linux installation methods:

1. Virtual Machine (Hyper-V, VMware, VirtualBox)
2. Physical Server
3. Cloud Virtual Machine (AWS EC2, Azure VM, Google Compute Engine)
4. Dual Boot (Windows and Linux)

### General Installation Process
1. Download a Linux ISO image.
2. Create a bootable USB or virtual machine.
3. Boot the system using the ISO.
4. Configure language, network, and disk partitions.
5. Create a user account.
6. Complete installation and reboot.

## 2. Linux Filesystem Hierarchy

| Directory | Purpose |
|---|---|
| `/` | Root directory |
| `/home` | Normal users' home directories |
| `/root` | Root user's home directory |
| `/etc` | System configuration files |
| `/var` | Logs and frequently changing data |
| `/tmp` | Temporary files |
| `/boot` | Bootloader and kernel-related files |
| `/dev` | Device files |
| `/proc` | Process and kernel information |
| `/sys` | Kernel and hardware information |
| `/usr` | Applications and utilities |
| `/opt` | Optional third-party applications |
| `/mnt` | Temporary mount points |
| `/media` | Removable media mount points |

### Important DevOps Directories
- `/var/log` – System and application logs.
- `/etc/ssh` – SSH configuration.
- `/home` – User files.
- `/tmp` – Temporary application files.

## 3. Absolute Path vs Relative Path

### Absolute Path
An absolute path starts from the root directory `/`.

Example:
```bash
/home/user/documents/file.txt
```

### Relative Path
A relative path starts from the current working directory.

Example:
```bash
documents/file.txt
```

### Special Symbols

| Symbol | Meaning |
|---|---|
| `/` | Root directory |
| `.` | Current directory |
| `..` | Parent directory |
| `~` | Current user's home directory |

## 4. Linux Navigation Commands

| Command | Description |
|---|---|
| `pwd` | Display current directory |
| `ls` | List files and directories |
| `ls -l` | Detailed file listing |
| `ls -la` | Show hidden files |
| `cd /etc` | Navigate to /etc |
| `cd ..` | Move to parent directory |
| `cd ~` | Navigate to home directory |
| `clear` | Clear terminal |

## 5. File and Directory Management

| Command | Description |
|---|---|
| `mkdir test` | Create directory |
| `mkdir -p a/b/c` | Create nested directories |
| `touch file.txt` | Create an empty file |
| `cp file.txt backup/` | Copy file |
| `mv old.txt new.txt` | Rename or move file |
| `rmdir test` | Remove empty directory |
| `rm file.txt` | Delete file |

**Note:** The `rm` command deletes files. Always verify the target path before using it.

## 6. Hands-on Practical

### Step 1: Navigate to Home Directory
```bash
cd ~
pwd
```

### Step 2: Create Workspace
```bash
mkdir -p day-06-linux-filesystem/practice/backup
```

### Step 3: Enter Workspace
```bash
cd ~/day-06-linux-filesystem
```

### Step 4: Create Files
```bash
touch file1.txt file2.txt
```

### Step 5: Add Content
```bash
echo "Linux Filesystem Practice" > file1.txt
echo "Learning Linux Commands" > file2.txt
```

### Step 6: Verify Files
```bash
ls -l
cat file1.txt
cat file2.txt
```

### Step 7: Copy File to Backup
```bash
cp file1.txt practice/backup/
```

### Step 8: Rename File
```bash
mv file2.txt linux-notes.txt
```

### Step 9: Verify Directory Structure
```bash
find ~/day-06-linux-filesystem -type f
```

Expected structure:
```text
day-06-linux-filesystem/
├── file1.txt
├── linux-notes.txt
└── practice/
    └── backup/
        └── file1.txt
```

### Step 10: Verify File Contents
```bash
cat file1.txt
cat linux-notes.txt
cat practice/backup/file1.txt
```

## 7. Additional Useful Linux Commands

| Command | Description |
|---|---|
| `df -h` | Check disk space |
| `du -sh directory` | Check directory size |
| `lsblk` | Display block devices |
| `free -h` | Check memory usage |
| `uname -r` | Display kernel version |
| `find /path -type f` | Find files |

## 8. Common Errors and Troubleshooting

| Error | Possible Reason | Solution |
|---|---|---|
| Permission denied | Insufficient permissions | Check file permissions |
| No such file or directory | Incorrect path | Verify using `pwd` and `ls` |
| File exists | Same name already exists | Check existing files |
| Directory not empty | Directory contains files | Check directory contents |
| Command not found | Command is not installed | Check installation or use an alternative |

## 9. Interview Questions

**Q1. What is the root directory in Linux?**

The root directory `/` is the starting point of the Linux filesystem hierarchy.

**Q2. What is the difference between /root and /home?**

`/root` is the root user's home directory, whereas `/home` contains normal users' home directories.

**Q3. What is the purpose of /etc?**

It stores system-wide configuration files.

**Q4. Where are Linux system logs stored?**

Most system and application logs are stored under `/var/log`.

**Q5. What is the difference between cp and mv?**

`cp` copies files, while `mv` moves or renames files.

**Q6. What is the difference between an absolute and relative path?**

An absolute path starts from `/`, whereas a relative path depends on the current working directory.

## 10. Key Takeaways

- Understood Linux installation methods.
- Learned Linux filesystem hierarchy.
- Practised absolute and relative paths.
- Used Linux navigation commands.
- Created and managed files and directories.
- Practised copying and renaming files.
- Learned basic filesystem troubleshooting commands.

## Learning Environment
- Operating System: Red Hat Enterprise Linux 9
- Virtualization: Microsoft Hyper-V
- Practice Environment: Linux Terminal
- Learning Track: 77-Day DevOps Learning Journey

## Progress
Day 6 – Linux Installation, Filesystem and Directory Structure.

**Status:** Update after completing practical exercises and knowledge assessment.

---

#DevOps #Linux #RHEL9 #LinuxAdministration #CloudComputing #DevOpsLearning
