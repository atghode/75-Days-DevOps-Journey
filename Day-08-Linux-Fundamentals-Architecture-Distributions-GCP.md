
# Day 08 – Linux Fundamentals: Architecture, Distributions and GCP Introduction

## 1. Introduction

Linux is an open-source, Unix-like operating system widely used in DevOps, cloud computing, servers, containers, and automation.

Linux knowledge is essential for managing servers, troubleshooting infrastructure, deploying applications, and working with cloud platforms.

## 2. Linux Architecture

Linux architecture consists of the following major components:

1. Hardware
2. Kernel
3. System Call Interface
4. System Libraries and Utilities
5. Shell and Applications

### Kernel

The kernel is the core component of Linux. It manages communication between software and hardware.

Major responsibilities:
- Process management
- Memory management
- Device management
- Filesystem management
- Network management
- Security and permissions

### System Libraries

System libraries provide standard functions that applications use to interact with the kernel.

Example: glibc.

### Shell

A shell is a command interpreter that accepts user commands and executes them.

Popular Linux shells:
- Bash
- Zsh
- Fish
- Dash
- Ksh

### Terminal

A terminal provides an interface where users can interact with the shell.

**Important differences:**
- Kernel: Manages hardware and system resources.
- Shell: Interprets and executes commands.
- Terminal: Provides the interface to enter commands.

## 3. User Space vs Kernel Space

### User Space
- Runs regular applications and processes.
- Applications cannot directly access protected kernel memory.
- Provides isolation and security.

### Kernel Space
- Runs the Linux kernel.
- Handles hardware and critical system operations.
- Has privileged access to system resources.

## 4. Linux Boot Process

The Linux boot process generally follows these stages:

1. BIOS/UEFI initializes hardware.
2. GRUB2 loads the selected kernel.
3. Linux kernel initializes system resources.
4. initramfs provides the initial temporary filesystem.
5. systemd starts as PID 1.
6. systemd starts required services and targets.
7. The system becomes ready for login.

### Useful systemd Commands

```bash
systemctl status
systemctl get-default
systemctl list-units --type=service
systemctl list-units --type=target
ps -p 1 -o pid,comm,args
```

## 5. Linux Distributions

A Linux distribution combines the Linux kernel with system utilities, libraries, package management tools, and other software.

| Distribution | Package Format | Package Manager |
|---|---|---|
| RHEL | RPM | DNF |
| Fedora | RPM | DNF |
| Ubuntu | DEB | APT |
| Debian | DEB | APT |
| SUSE | RPM | Zypper |
| Amazon Linux 2023 | RPM | DNF |

### RHEL vs Ubuntu

**RHEL:**
- Enterprise-focused Linux distribution.
- Uses RPM packages.
- Uses DNF for package management.

**Ubuntu:**
- Based on Debian.
- Widely used for cloud servers and development.
- Uses APT for package management.

### Package Installation Examples

RHEL:
```bash
sudo dnf install nginx
```

Ubuntu:
```bash
sudo apt install nginx
```

Note: These commands install software and modify the system. Review the package and environment before executing them.

## 6. Linux Practical Commands

The following commands help inspect a Linux system.

| Command | Purpose |
|---|---|
| `cat /etc/os-release` | Check Linux distribution |
| `uname -r` | Display kernel version |
| `uname -a` | Display system information |
| `uname -m` | Check system architecture |
| `lscpu` | Display CPU information |
| `free -h` | Check memory usage |
| `uptime` | Check system uptime |
| `df -h` | Check disk space |
| `hostnamectl` | Display hostname and OS details |
| `dnf --version` | Check DNF version |
| `systemctl get-default` | Check default systemd target |
| `systemctl status sshd` | Check SSH service status |

## 7. Introduction to Google Cloud Platform (GCP)

Google Cloud Platform is Google's cloud computing platform.

It provides infrastructure and managed services for hosting applications, databases, storage, networking, monitoring, and containerized workloads.

### Important GCP Services

| GCP Service | Purpose |
|---|---|
| Compute Engine | Virtual machines |
| Cloud Storage | Object storage |
| VPC | Cloud networking |
| IAM | Identity and access management |
| GKE | Managed Kubernetes |
| Cloud SQL | Managed relational databases |
| Cloud Monitoring | Infrastructure monitoring |
| Cloud Logging | Centralized log management |

## 8. GCP Resource Hierarchy

The common GCP resource hierarchy is:

Organization → Folders → Projects → Resources

Organizations and folders are optional depending on the account structure.

### Important GCP Concepts

**Project:** Logical container for cloud resources.

**Region:** Geographic area where cloud resources are deployed.

**Zone:** Deployment area within a region.

**Compute Engine:** GCP service used to create and manage virtual machines.

## 9. AWS vs GCP Comparison

| AWS | GCP |
|---|---|
| EC2 | Compute Engine |
| S3 | Cloud Storage |
| VPC | VPC |
| EKS | GKE |
| RDS | Cloud SQL |
| IAM | IAM |
| CloudWatch | Cloud Monitoring |
| CloudWatch Logs | Cloud Logging |

## 10. Linux in GCP – Basic Workflow

A typical Linux server deployment workflow:

1. Create or select a GCP project.
2. Configure VPC networking.
3. Select a Linux VM image.
4. Create a Compute Engine instance.
5. Connect to the VM using SSH.
6. Install required dependencies.
7. Deploy the application.
8. Monitor the VM using Cloud Monitoring and Cloud Logging.

**Important:** Always review cloud pricing and free-tier eligibility before creating resources. Avoid creating paid resources without understanding the billing implications.

## 11. Real-World DevOps Scenarios

### Scenario 1: Linux Server Boot Failure
Check system boot logs, GRUB configuration, kernel status, and systemd services.

### Scenario 2: High Memory Usage
Useful commands:

```bash
free -h
top
ps aux --sort=-%mem | head
```

### Scenario 3: Package Installation Failure
Identify the Linux distribution first, then use its appropriate package manager.

### Scenario 4: Cloud Migration
An on-premises Linux application can be migrated to GCP Compute Engine after planning networking, security, storage, and monitoring.

## 12. Interview Questions

1. What is Linux?
2. What is the Linux kernel?
3. Explain Linux architecture.
4. What is the difference between shell and terminal?
5. What is the Linux boot process?
6. What is GRUB2?
7. What is systemd?
8. What is the difference between RHEL and Ubuntu?
9. What is the difference between DNF and APT?
10. What is Google Cloud Platform?
11. What is Compute Engine?
12. What is the difference between a GCP region and zone?

## 13. Practical Assignment

Complete the following exercises on your RHEL 9 virtual machine.

### Exercise 1: Operating System Information

```bash
cat /etc/os-release
uname -r
uname -m
hostnamectl
```

### Exercise 2: Hardware and Resource Information

```bash
lscpu
free -h
df -h
uptime
```

### Exercise 3: Process and Service Information

```bash
ps -p 1 -o pid,comm,args
systemctl get-default
systemctl status sshd
```

### Exercise 4: GCP Exploration

Explore the official Google Cloud website and identify:

- Compute Engine
- Cloud Storage
- VPC
- IAM
- Google Kubernetes Engine

No paid resources need to be created for this exercise.

## 14. Day 08 Key Takeaways

- Linux is a fundamental technology for DevOps engineers.
- The kernel manages hardware and system resources.
- Shell and terminal provide command-line interaction.
- GRUB2 and systemd are important parts of the Linux boot process.
- Different Linux distributions use different package managers.
- GCP provides cloud infrastructure and managed services.
- Compute Engine allows users to run Linux virtual machines in GCP.


