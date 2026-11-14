
# Day 5 – Bash Scripting for DevOps 🚀

**75 Days of DevOps Learning Journey**

**Level:** Beginner  
**Platform:** RHEL 9  
**Topic:** Bash Scripting and Linux Automation

---

## 🎯 Learning Objectives

Today I learned how to:

1. Understand Bash and Shell Scripting.
2. Create and execute Bash scripts.
3. Work with variables and user input.
4. Use command-line arguments.
5. Apply conditional statements (`if`, `else`).
6. Work with `for` and `while` loops.
7. Create and use functions.
8. Understand exit status and error handling.
9. Debug Bash scripts.
10. Automate basic Linux administration tasks.

---

## 1. What is Bash Scripting?

Bash stands for **Bourne Again Shell**.

Bash scripting allows us to automate Linux commands by writing them inside a script file.

Instead of executing commands individually, we can execute multiple commands through one script.

### Example

```bash
pwd
ls -l
free -h
df -h
uptime
```

These commands can be placed inside a single Bash script and executed together.

### Real-world DevOps Usage

- Server monitoring
- Backup automation
- Application deployment
- Log monitoring
- Linux administration

---

## 2. Understanding Bash Script Structure

Every basic Bash script generally starts with:

```bash
#!/bin/bash
```

This is called the **Shebang**. It specifies the Bash interpreter.

Example:

```bash
#!/bin/bash

echo "Hello, DevOps!"
echo "Welcome to Day 5"
echo "Learning Bash Scripting"
```

---

## 3. First Hands-on Bash Script

Create a practice directory:

```bash
mkdir -p ~/day-05-bash-scripting
cd ~/day-05-bash-scripting
```

Create the script:

```bash
touch hello.sh
vi hello.sh
```

Add:

```bash
#!/bin/bash

echo "Hello, DevOps!"
echo "Welcome to Day 5"
echo "Learning Bash Scripting"
```

Execute:

```bash
bash hello.sh
```

Make it executable:

```bash
chmod +x hello.sh
./hello.sh
```

---

## 4. Variables in Bash

Variables store information that can be reused in a script.

Example:

```bash
#!/bin/bash

name="Amit"
course="DevOps"
day=5

echo "Name: $name"
echo "Course: $course"
echo "Day: $day"
```

**Important rules:**

- Do not use spaces around `=`.
- Use `$` to access a variable.
- Variable names are case-sensitive.

---

## 5. Taking User Input

The `read` command accepts input from the user.

Example:

```bash
#!/bin/bash

echo "Enter your name:"
read name

echo "Welcome, $name"
```

### Practical Example

```bash
#!/bin/bash

echo "Enter server name:"
read server

echo "Enter environment:"
read environment

echo "Server Name: $server"
echo "Environment: $environment"
```

---

## 6. Command-line Arguments

Arguments allow users to pass information while executing a script.

Example:

```bash
bash arguments.sh Amit DevOps
```

Important variables:

| Variable | Meaning |
|---|---|
| `$0` | Script name |
| `$1` | First argument |
| `$2` | Second argument |
| `$#` | Number of arguments |
| `$@` | All arguments |

Example script:

```bash
#!/bin/bash

echo "Script Name: $0"
echo "First Argument: $1"
echo "Second Argument: $2"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

---

## 7. Conditional Statements (if/else)

Conditional statements allow scripts to make decisions.

### Practical: Disk Usage Check

```bash
#!/bin/bash

usage=$(df -P / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Current Disk Usage: $usage%"

if [ "$usage" -ge 80 ]
then
    echo "WARNING: Disk usage is high!"
else
    echo "Disk usage is normal."
fi
```

This script checks the root filesystem and displays a warning when usage reaches 80% or higher.

---

## 8. Loops in Bash

Loops execute commands repeatedly.

### A. For Loop

```bash
#!/bin/bash

for i in 1 2 3 4 5
do
    echo "DevOps Learning Day $i"
done
```

### B. While Loop

```bash
#!/bin/bash

count=1

while [ "$count" -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done
```

### Practical: Check Multiple Services

```bash
#!/bin/bash

for service in sshd crond
do
    echo "Checking service: $service"
    systemctl is-active "$service"
done
```

This script checks the status of two Linux services without restarting or modifying them.

---

## 9. Functions in Bash

Functions help us reuse code instead of writing the same commands repeatedly.

Example:

```bash
#!/bin/bash

greeting() {
    echo "Welcome to DevOps!"
}

greeting
```

### Practical: System Information

```bash
#!/bin/bash

show_hostname() {
    echo "Hostname:"
    hostname
}

show_uptime() {
    echo "System Uptime:"
    uptime
}

show_memory() {
    echo "Memory Information:"
    free -h
}

show_hostname
show_uptime
show_memory
```

---

## 10. Exit Status and Error Handling

Linux commands return an exit status after execution.

- `0` means success.
- Non-zero generally indicates failure.

Check exit status:

```bash
ls
echo $?
```

Try an invalid command:

```bash
some_invalid_command
echo $?
```

### Check Whether a Directory Exists

```bash
#!/bin/bash

directory="/tmp/devops-day4"

if [ -d "$directory" ]
then
    echo "Directory exists."
else
    echo "Directory does not exist."
fi
```

Common file tests:

| Condition | Meaning |
|---|---|
| `-f` | File exists |
| `-d` | Directory exists |
| `-e` | File or directory exists |
| `-r` | File is readable |
| `-w` | File is writable |
| `-x` | File is executable |

### Bonus: Stop on Certain Command Failures

```bash
set -e
```

This makes Bash exit when certain commands fail. It has exceptions, so important commands should still be checked explicitly.

---

## 11. Main DevOps Project – Linux Server Health Check

**Project:** Server Health Check Script

The objective is to automate basic server monitoring.

Create:

```bash
vi server-health.sh
```

Add:

```bash
#!/bin/bash

echo "================================"
echo "       SERVER HEALTH CHECK"
echo "================================"

echo ""

echo "Hostname:"
hostname

echo ""

echo "Date and Time:"
date

echo ""

echo "System Uptime:"
uptime

echo ""

echo "Disk Usage:"
df -h /

echo ""

echo "Memory Usage:"
free -h

echo ""

echo "CPU Load:"
uptime

echo ""

echo "================================"
echo "     HEALTH CHECK COMPLETED"
echo "================================"
```

Execute:

```bash
chmod +x server-health.sh
./server-health.sh
```

### Information Displayed

- Server hostname
- Current date and time
- System uptime
- Disk utilization
- Memory usage
- CPU load information

**Project Outcome:** Created a Bash script to automate basic Linux server health checks.

---

## 12. Bash Script Debugging

Useful debugging commands:

### Check Script Syntax

```bash
bash -n server-health.sh
```

No output generally means Bash found no syntax errors.

### Execute in Debug Mode

```bash
bash -x server-health.sh
```

This displays commands as Bash executes them.

### Check File Permissions

```bash
ls -l server-health.sh
```

### Check Interpreter

```bash
head -n 1 server-health.sh
```

Expected:

```bash
#!/bin/bash
```

---

## 13. Common Bash Scripting Mistakes

| Problem | Solution |
|---|---|
| Permission denied | Check `chmod +x` |
| Command not found | Check spelling and PATH |
| Incorrect variable output | Check `$variable` syntax |
| Spaces around `=` | Remove unnecessary spaces |
| Script syntax error | Run `bash -n` |
| Infinite loop | Verify loop condition |
| Wrong file path | Check using `pwd` and `ls` |

---

## 14. Interview Preparation

**Q1. What is Bash scripting?**

Bash scripting is used to automate Linux commands by writing them inside a script file. It helps reduce manual work and automate repetitive administrative tasks.

**Q2. What is a Shebang?**

Shebang is the first line of a script, usually `#!/bin/bash`. It specifies which interpreter should execute the script.

**Q3. What is the difference between Shell and Bash?**

Shell is a command-line interpreter that allows users to interact with the operating system. Bash is one specific type of shell.

**Q4. How do you execute a Bash script?**

I can execute it using `bash script.sh`, or make it executable using `chmod +x` and run it with `./script.sh`.

**Q5. What is the difference between `$1` and `$@`?**

`$1` represents the first command-line argument, whereas `$@` represents all arguments passed to the script.

**Q6. What is the difference between for and while loops?**

A for loop is generally used to iterate over a list of values. A while loop continues executing as long as a specified condition remains true.

**Q7. What is exit status in Linux?**

Exit status indicates whether a command completed successfully. Zero means success, and a non-zero value generally indicates failure.

**Q8. How do you debug a Bash script?**

I use `bash -n script.sh` to check syntax and `bash -x script.sh` to execute the script in debug mode.

**Q9. Why is Bash scripting important in DevOps?**

Bash scripting helps automate repetitive Linux administration tasks, server monitoring, backups, deployment activities and troubleshooting.

---

## 15. Day 5 Practical Assignment

- [ ] Create the `day-05-bash-scripting` directory.
- [ ] Create and execute `hello.sh`.
- [ ] Practise variables and user input.
- [ ] Practise command-line arguments.
- [ ] Create a disk usage checking script.
- [ ] Practise for and while loops.
- [ ] Create a function-based system information script.
- [ ] Practise exit status and file checking.
- [ ] Create the `server-health.sh` project.
- [ ] Run `bash -n` and `bash -x` to practise debugging.

---

## 💡 Key Takeaway

Bash scripting helps DevOps Engineers automate repetitive tasks, save time, reduce manual errors and improve operational efficiency.

The goal is not just to memorize commands but to understand how to use them in real-world automation.

**Day 5 Completed – Bash Scripting for DevOps! 🚀**

#75DaysOfDevOps #DevOps #BashScripting #Linux #RHEL9 #Automation
