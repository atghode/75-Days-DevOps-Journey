
# Day 11 - Linux Package Management, systemd and Processes

## 1. Learning Objectives

In this lesson, I learned three important Linux administration concepts:

1. Linux Package Management
2. systemd and Service Management
3. Linux Process Management

These concepts are essential for DevOps Engineers who work with Linux servers, cloud infrastructure, CI/CD pipelines and production applications.

---

## 2. Linux Package Management

### What is a Linux Package?

A package is a collection of files required to install and run software on a Linux system.

Examples:
- Git
- Nginx
- Apache
- Python
- Vim

### What is a Package Manager?

A package manager helps administrators:

- Install software.
- Update software.
- Remove software.
- Search for packages.
- Manage dependencies.
- Check installed package versions.

### RPM, YUM and DNF

| Tool | Description |
|---|---|
| RPM | Package format and low-level package management tool |
| YUM | Older high-level package manager |
| DNF | Modern high-level package manager used in RHEL 9 |

### Important RPM Commands

```bash
rpm -q git
rpm -qa
rpm -qi git
rpm -ql git
rpm -qf /usr/bin/git
```

### Important DNF Commands

```bash
sudo dnf install git
sudo dnf remove git
sudo dnf update
sudo dnf update git
dnf search nginx
dnf info nginx
dnf list installed
dnf check-update
dnf repolist
dnf repolist all
sudo dnf clean all
sudo dnf makecache
```

### What is a Repository?

A repository is a storage location containing software packages.

Check configured repositories:

```bash
dnf repolist
```

Check repository configuration files:

```bash
ls /etc/yum.repos.d/
```

### What are Dependencies?

Dependencies are additional packages or libraries required by an application to function correctly.

DNF automatically resolves and installs dependencies when they are available through configured repositories.

---

## 3. systemd and Service Management

### What is a Linux Service?

A service is a program that runs in the background and provides functionality to users or other applications.

Examples:

- SSH
- Nginx
- Apache
- Cron
- Firewalld

### What is systemd?

systemd is the system and service manager used in RHEL 9.

Its responsibilities include:

- Starting services during system boot.
- Stopping and restarting services.
- Managing background services.
- Managing service dependencies.
- Managing system targets.

### Linux Boot Process

```text
Power ON
   |
BIOS / UEFI
   |
Bootloader (GRUB)
   |
Linux Kernel
   |
systemd (PID 1)
   |
System Targets
   |
Required Services
   |
Login Screen / Terminal
```

Check PID 1:

```bash
ps -p 1 -o pid,comm,args
```

### What is systemctl?

systemctl is the command-line utility used to manage systemd services and units.

### Important systemctl Commands

```bash
systemctl status sshd

sudo systemctl start sshd

sudo systemctl stop sshd

sudo systemctl restart sshd

sudo systemctl reload nginx

sudo systemctl enable sshd

sudo systemctl disable sshd

sudo systemctl enable --now sshd

systemctl is-active sshd

systemctl is-enabled sshd
```

### Service States

| State | Meaning |
|---|---|
| Active | Service is currently running |
| Inactive | Service is stopped |
| Failed | Service encountered a failure |
| Enabled | Configured for automatic startup |
| Disabled | Not configured for normal automatic startup |
| Static | Not normally enabled independently |

Important difference:

- Start runs a service immediately.
- Enable configures automatic startup during boot.
- Restart stops and starts a service.
- Reload asks a service to reload its configuration, if supported.

### Listing Services

```bash
systemctl list-units --type=service --state=running

systemctl list-units --type=service

systemctl list-unit-files --type=service

systemctl --failed
```

### systemd Unit Types

| Unit | Purpose |
|---|---|
| .service | Background services |
| .target | Groups of units representing system states |
| .socket | Socket-based activation |
| .timer | Scheduled activation |
| .mount | Filesystem mounts |
| .path | Filesystem path monitoring |

### systemd Targets

| Traditional Runlevel | systemd Target | Purpose |
|---|---|---|
| 0 | poweroff.target | Shutdown |
| 1 | rescue.target | Rescue mode |
| 3 | multi-user.target | Command-line mode |
| 5 | graphical.target | Graphical mode |
| 6 | reboot.target | Reboot |

Check default target:

```bash
systemctl get-default
```

---

## 4. Linux Process Management

### What is a Process?

A process is an instance of a program that is currently running in Linux.

Example:

```bash
python app.py
```

Here, app.py is the program and its running instance is a process.

### PID and PPID

- PID: Process ID.
- PPID: Parent Process ID.

Check processes:

```bash
ps
ps -ef
ps aux
```

Check current shell PID:

```bash
echo $$
```

Check PID and PPID:

```bash
ps -o pid,ppid,comm -p $$
```

### Important Process Commands

```bash
ps -ef
ps aux
top
pgrep -a nginx
```

### top Command

The top command provides real-time process information.

It displays:

- CPU usage.
- Memory usage.
- Running processes.
- Process IDs.
- System load.

Useful keys:

| Key | Purpose |
|---|---|
| q | Exit |
| P | Sort by CPU |
| M | Sort by memory |
| k | Send a signal to a process |
| 1 | Show CPU usage per core |

### Process Termination

```bash
kill -15 PID
```

Sends SIGTERM and requests graceful termination.

```bash
kill -9 PID
```

Sends SIGKILL and forces termination.

Important signals:

| Signal | Number | Purpose |
|---|---|---|
| SIGTERM | 15 | Graceful termination request |
| SIGKILL | 9 | Immediate termination |
| SIGHUP | 1 | Hangup signal |
| SIGSTOP | 19 | Stop process |
| SIGCONT | 18 | Continue process |

Always prefer graceful termination before using SIGKILL.

### nice and renice

Start a process with a selected nice value:

```bash
nice -n 10 sleep 300
```

Change the priority of a running process:

```bash
sudo renice 10 -p PID
```

Nice values range from -20 (higher scheduling priority) to +19 (lower scheduling priority).

### Foreground and Background Processes

Run in the foreground:

```bash
sleep 60
```

Run in the background:

```bash
sleep 300 &
```

Check background jobs:

```bash
jobs
```

Bring a job to foreground:

```bash
fg
```

Continue a stopped job in the background:

```bash
bg
```

Useful keyboard shortcuts:

- Ctrl+C: Interrupt foreground process.
- Ctrl+Z: Suspend foreground process.

### Process States

| State | Meaning |
|---|---|
| R | Running or runnable |
| S | Interruptible sleep |
| D | Uninterruptible sleep |
| T | Stopped or traced |
| Z | Zombie |

### Zombie Process

A zombie process has completed execution but its parent has not yet collected its exit status.

### Orphan Process

An orphan process is a running process whose parent has terminated. Linux generally adopts it through an appropriate system process.

---

## 5. Linux Service Troubleshooting

### Check Service Status

```bash
systemctl status nginx
```

### Check Service Logs

```bash
sudo journalctl -u nginx
```

Show latest 50 log entries:

```bash
sudo journalctl -u nginx -n 50
```

Follow logs live:

```bash
sudo journalctl -u nginx -f
```

Show current boot logs:

```bash
sudo journalctl -b
```

### Check Listening Ports

```bash
sudo ss -lntp
```

### Test Local Web Server

```bash
curl -I http://localhost
```

### Troubleshooting Workflow

1. Check whether the application package is installed.
2. Check the service status.
3. Inspect service logs.
4. Check the running process.
5. Inspect CPU and memory usage.
6. Check listening ports.
7. Identify and resolve the root cause.
8. Restart or reload the service if required.
9. Verify application functionality.

---

## 6. Practical Lab

### Lab 1 - Package Management

```bash
cat /etc/redhat-release
dnf --version
dnf repolist
rpm -q git
dnf info git
dnf search nginx
dnf list installed
```

### Lab 2 - systemd

```bash
systemctl status sshd
systemctl is-active sshd
systemctl is-enabled sshd
systemctl --failed
systemctl list-units --type=service --state=running
sudo journalctl -u sshd -n 20
systemctl get-default
```

### Lab 3 - Process Management

Start a test background process:

```bash
sleep 300 &
```

Check jobs:

```bash
jobs
```

Find the process:

```bash
pgrep -a sleep
```

Check PID and PPID:

```bash
ps -eo pid,ppid,stat,comm | grep sleep
```

Check process priority:

```bash
ps -o pid,ni,comm -C sleep
```

Terminate the test process gracefully:

```bash
pkill -15 -x sleep
```

Verify:

```bash
pgrep -a sleep
```

Note: Only use the last termination command if you do not have other sleep processes that you need to keep running.

---

## 7. Real-World DevOps Applications

| Task | Linux Knowledge |
|---|---|
| Install Git on build server | DNF / RPM |
| Install Nginx | DNF |
| Start Jenkins | systemctl |
| Enable service during boot | systemctl enable |
| Troubleshoot service failure | journalctl |
| Find high CPU process | top / ps |
| Terminate unresponsive process | kill |
| Check application process | pgrep |

### Example - Jenkins Service Management

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
systemctl status jenkins
sudo journalctl -u jenkins -n 50
```

---

## 8. Interview Questions

1. What is Linux package management?
2. What is the difference between RPM and DNF?
3. What is the difference between YUM and DNF?
4. What is a Linux repository?
5. What are package dependencies?
6. What is systemd?
7. What is systemctl?
8. What is the difference between start and enable?
9. What is the difference between restart and reload?
10. What is a systemd unit?
11. What is a Linux process?
12. What is the difference between PID and PPID?
13. What is the difference between ps and top?
14. What is the difference between SIGTERM and SIGKILL?
15. What is a zombie process?
16. How do you troubleshoot a failed service?
17. How do you identify a high CPU process?

---

## 9. Key Takeaways

Today I learned:

- How Linux package management works.
- Differences between RPM, YUM and DNF.
- How to manage software packages and repositories.
- How systemd manages Linux services.
- How to start, stop, restart and enable services.
- How to inspect systemd logs.
- How Linux processes work.
- How to monitor and manage processes.
- How to troubleshoot service and process issues.

## 10. Day 11 Completion Checklist

- [ ] Understand RPM, YUM and DNF.
- [ ] Practice package management commands.
- [ ] Understand repositories and dependencies.
- [ ] Practice systemctl commands.
- [ ] Understand systemd units and targets.
- [ ] Practice journalctl.
- [ ] Understand PID and PPID.
- [ ] Practice ps, top and pgrep.
- [ ] Understand process signals.
- [ ] Practice foreground and background processes.
- [ ] Complete practical labs.
- [ ] Complete knowledge assessment.

---

**Learning Journey:** 77 Days of DevOps

**Day:** 11/77

**Topic:** Linux Package Management, systemd and Processes

**Environment:** RHEL 9

**Status:** Lesson Delivered - Practical Assessment Pending
