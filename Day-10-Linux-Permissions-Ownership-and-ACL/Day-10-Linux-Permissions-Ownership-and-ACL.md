
# Day 10 – Linux Permissions, Ownership and ACL

## 1. Introduction

Linux permissions are an important part of system administration and DevOps security.

They control who can read, write, and execute files and directories.

In this lesson, I learned:

- Linux file and directory permissions
- Owner, Group and Others
- Read, Write and Execute permissions
- Numeric and symbolic permissions
- chmod, chown and chgrp
- umask
- SUID, SGID and Sticky Bit
- Access Control Lists (ACL)
- SELinux fundamentals

---

## 2. Understanding Linux Permissions

Linux permissions are divided into three categories:

| Category | Meaning |
|---|---|
| User (u) | File owner |
| Group (g) | Group associated with the file |
| Others (o) | All other users |

Check permissions:

```bash
ls -l
```

Example output:

```text
-rw-r--r--. 1 amit devops 1024 Nov 19 10:30 app.txt
```

Permission breakdown:

- `-` = Regular file
- `rw-` = Owner permissions
- `r--` = Group permissions
- `r--` = Others permissions

### File Types

| Symbol | Meaning |
|---|---|
| - | Regular file |
| d | Directory |
| l | Symbolic link |
| c | Character device |
| b | Block device |

---

## 3. Three Basic Linux Permissions

| Permission | Symbol | Numeric Value |
|---|---|---:|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |
| No permission | - | 0 |

### Read (r)

For files, read permission allows viewing file contents.

For directories, it allows listing directory entries.

### Write (w)

For files, write permission allows modifying contents.

For directories, it allows creating, deleting and renaming entries, subject to other required permissions.

### Execute (x)

For files, execute permission allows running an executable or script when other conditions permit.

For directories, it allows entering and traversing the directory.

---

## 4. Numeric Permissions

Linux uses numeric values to represent permissions.

| Permission | Numeric | Symbolic |
|---|---:|---|
| Full permissions | 7 | rwx |
| Read and execute | 5 | r-x |
| Read and write | 6 | rw- |
| Read only | 4 | r-- |
| No permission | 0 | --- |

### Common Permission Combinations

| Numeric | Symbolic | Meaning |
|---:|---|---|
| 777 | rwxrwxrwx | Everyone has full permissions |
| 755 | rwxr-xr-x | Owner full; others read and execute |
| 750 | rwxr-x--- | Owner full; group read and execute |
| 700 | rwx------ | Only owner has full permissions |
| 644 | rw-r--r-- | Owner read/write; others read |
| 640 | rw-r----- | Owner read/write; group read |
| 600 | rw------- | Only owner read/write |

Example:

```bash
chmod 755 script.sh
chmod 644 app.txt
chmod 600 secret.txt
```

**Important:** Avoid using 777 as a general solution for permission issues.

---

## 5. chmod – Change Permissions

The `chmod` command changes file and directory permissions.

### Numeric Method

```bash
chmod 755 script.sh
chmod 644 app.txt
chmod 700 private_dir
```

### Symbolic Method

```bash
chmod u+x script.sh
chmod g-w app.txt
chmod o-r app.txt
chmod a+r app.txt
```

| Symbol | Meaning |
|---|---|
| u | User/Owner |
| g | Group |
| o | Others |
| a | All |
| + | Add permission |
| - | Remove permission |
| = | Set exact permission |

### Recursive Permission Change

```bash
chmod -R 755 /opt/myapp
```

`-R` applies changes recursively to the directory and its contents.

Use recursive permission changes carefully. Files and directories may need different permissions.

---

## 6. chown – Change Ownership

The `chown` command changes file ownership.

Check current ownership:

```bash
ls -l app.txt
```

Change owner:

```bash
sudo chown rahul app.txt
```

Change owner and group:

```bash
sudo chown rahul:devops app.txt
```

Change ownership recursively:

```bash
sudo chown -R rahul:devops /opt/myapp
```

**Important:** Avoid recursive ownership changes on system directories such as `/etc`, `/usr` and `/var`.

---

## 7. chgrp – Change Group Ownership

The `chgrp` command changes the group associated with a file or directory.

```bash
sudo chgrp devops app.txt
```

Recursive group change:

```bash
sudo chgrp -R devops /opt/myapp
```

### Difference Between chmod, chown and chgrp

| Command | Purpose |
|---|---|
| chmod | Change permissions |
| chown | Change owner and optionally group |
| chgrp | Change group ownership |

---

## 8. Understanding umask

`umask` controls which permission bits are removed from the default permissions of newly created files and directories.

Check current umask:

```bash
umask
```

Example:

```text
0022
```

Default base permissions:

| Object | Base Permission |
|---|---:|
| Regular file | 666 |
| Directory | 777 |

With umask 022:

Regular file:

```text
666 - umask 022 = 644
```

Directory:

```text
777 - umask 022 = 755
```

Change umask temporarily:

```bash
umask 027
```

Expected new permissions:

| Object | Permission |
|---|---:|
| File | 640 |
| Directory | 750 |

Practical example:

```bash
touch testfile.txt
mkdir testdir
ls -l testfile.txt
ls -ld testdir
```

Note: umask removes permission bits from the base mode. The result can also depend on the permissions requested by the application creating the object.

---

## 9. Special Permissions

Linux provides three special permission mechanisms:

1. SUID
2. SGID
3. Sticky Bit

### A. SUID – Set User ID

Numeric value: `4`

SUID causes an executable to run with the effective user ID of its file owner.

Example:

```bash
ls -l /usr/bin/passwd
```

Possible output:

```text
-rwsr-xr-x. 1 root root ... /usr/bin/passwd
```

The `s` in the owner's execute position represents SUID.

### B. SGID – Set Group ID

Numeric value: `2`

On executable files, SGID makes the process use the file's group as its effective group.

On directories, new files and subdirectories inherit the directory's group.

Example:

```bash
sudo mkdir -p /opt/devops-shared
sudo chgrp devops /opt/devops-shared
sudo chmod 2770 /opt/devops-shared
```

Expected permission:

```text
drwxrws---.
```

### C. Sticky Bit

Numeric value: `1`

Sticky Bit restricts ordinary users from deleting or renaming files belonging to other users in a shared directory.

Example:

```bash
ls -ld /tmp
```

Typical output:

```text
drwxrwxrwt.
```

Set Sticky Bit:

```bash
sudo chmod 1777 /opt/shared
```

### Special Permission Summary

| Permission | Numeric Value | Purpose |
|---|---:|---|
| SUID | 4 | Executable uses file owner's effective UID |
| SGID | 2 | Directory entries inherit group |
| Sticky Bit | 1 | Restricts deletion of other users' files |

Examples:

```bash
chmod 4755 file
chmod 2770 directory
chmod 1777 shared_directory
```

Do not apply special permissions to unknown executables.

---

## 10. ACL – Access Control Lists

ACL stands for Access Control List.

Standard Linux permissions provide access for:

- Owner
- Group
- Others

ACL provides additional access entries for specific users and groups.

### Why ACL Is Required

Imagine a project directory:

```text
/opt/project/
```

The directory belongs to the `amit` user and `devops` group.

A tester named `priya` needs read-only access.

Instead of changing the owner or adding Priya to the DevOps group, ACL can provide her individual access.

### A. Check ACL Commands

```bash
getfacl --version
setfacl --version
```

Install ACL tools on RHEL 9 if required:

```bash
sudo dnf install acl
```

### B. View ACL

```bash
getfacl /opt/project
```

### C. Give a Specific User Access

```bash
sudo setfacl -m u:priya:rx /opt/project
```

This gives Priya read and execute permissions on the directory.

### D. Give a Group Access

```bash
sudo setfacl -m g:testing:rx /opt/project
```

### E. Remove a Specific User ACL

```bash
sudo setfacl -x u:priya /opt/project
```

### F. Remove Extended ACL Entries

```bash
sudo setfacl -b /opt/project
```

### G. Default ACL

Default ACL entries are inherited by newly created files and subdirectories.

Example:

```bash
sudo setfacl -m d:u:priya:rx /opt/project
```

Check:

```bash
getfacl /opt/project
```

### H. ACL Mask

The ACL mask limits effective permissions for named users, named groups and the owning group entry.

Example:

```text
user:priya:rwx
mask::r-x
```

Priya's effective permissions are `r-x`, not `rwx`.

Check effective permissions:

```bash
getfacl /opt/project
```

---

## 11. Standard Permissions vs ACL

| Feature | Standard Permissions | ACL |
|---|---|---|
| Owner permissions | Yes | Yes |
| Group permissions | Yes | Yes |
| Others permissions | Yes | Yes |
| Specific additional user access | No | Yes |
| Specific additional group access | No | Yes |
| Default access rules | No | Yes |

ACL provides more granular access control.

---

## 12. SELinux Fundamentals

SELinux stands for Security-Enhanced Linux.

It provides an additional layer of security through mandatory access control policies.

Even when normal Linux permissions allow access, SELinux policy may deny the operation.

Check SELinux status:

```bash
getenforce
```

Possible output:

```text
Enforcing
```

Check SELinux context:

```bash
ls -Z app.sh
```

Check detailed status:

```bash
sestatus
```

### Security Mechanisms

| Mechanism | Purpose |
|---|---|
| Standard permissions | Owner, group and others access |
| ACL | Additional named user and group access |
| SELinux | Mandatory access control based on security policy |

Do not disable SELinux to solve permission issues without investigating the actual cause.

---

## 13. Real-World DevOps Applications

1. Application Deployment:
   Ensure deployment scripts have the correct execution permissions.

2. Shared Project Directories:
   Use groups and SGID to manage shared files.

3. Read-Only Access:
   Use ACL to grant testers access without changing ownership.

4. Configuration Security:
   Protect sensitive configuration files with restrictive permissions.

5. Server Security:
   Use standard permissions, ACL and SELinux together.

---

## 14. Practical Lab – RHEL 9

### Exercise 1: Create a Lab Directory

```bash
mkdir -p ~/day10-lab
cd ~/day10-lab
touch app.txt
ls -l app.txt
```

### Exercise 2: Numeric Permissions

```bash
chmod 640 app.txt
ls -l app.txt

chmod 755 app.txt
ls -l app.txt
```

### Exercise 3: Symbolic Permissions

```bash
chmod 644 app.txt
chmod u+x app.txt
ls -l app.txt

chmod u-x app.txt
```

### Exercise 4: Check Ownership

```bash
whoami
id
ls -l app.txt
```

Change group to the current primary group:

```bash
sudo chgrp "$(id -gn)" app.txt
```

### Exercise 5: Check umask

```bash
umask
touch umask-test.txt
mkdir umask-test-dir
ls -l umask-test.txt
ls -ld umask-test-dir
```

### Exercise 6: Sticky Bit

```bash
mkdir shared
chmod 1777 shared
ls -ld shared
```

### Exercise 7: ACL Practice

Use an existing test user:

```bash
sudo setfacl -m u:testuser:rw app.txt
getfacl app.txt
sudo setfacl -x u:testuser app.txt
```

Replace `testuser` with an existing Linux account.

---

## 15. Important Commands Revision Sheet

| Command | Purpose |
|---|---|
| ls -l | View file permissions and ownership |
| ls -ld directory | View directory permissions |
| chmod 755 file | Change permissions |
| chmod u+x file | Add execute permission |
| chown user file | Change owner |
| chown user:group file | Change owner and group |
| chgrp group file | Change group |
| umask | Display current umask |
| getfacl file | Display ACL |
| setfacl -m | Add or modify ACL |
| setfacl -x | Remove ACL entry |
| setfacl -b | Remove extended ACL entries |
| ls -Z file | Display SELinux context |
| getenforce | Check SELinux mode |

---

## 16. Interview Questions

### Q1. What are Linux file permissions?

They control who can read, write or execute files and directories.

### Q2. What is the difference between chmod and chown?

chmod changes permissions, whereas chown changes ownership.

### Q3. What does permission 755 mean?

The owner has full permissions, while group and others have read and execute permissions.

### Q4. What is umask?

Umask determines which permission bits are removed from default permissions when new files and directories are created.

### Q5. What is SUID?

SUID makes an executable run with the effective user ID of its file owner.

### Q6. What is SGID?

SGID on a directory ensures new files and subdirectories inherit the directory's group.

### Q7. What is Sticky Bit?

It restricts ordinary users from deleting or renaming files belonging to other users in a shared directory.

### Q8. What is ACL?

ACL provides additional permissions for specific users and groups.

### Q9. What is the ACL mask?

The ACL mask limits the effective permissions of named users, named groups and the owning group entry.

### Q10. What is SELinux?

SELinux provides mandatory access control and an additional security layer in Linux.

---

## 17. Key Takeaways

- Linux permissions protect files and directories.
- Owner, Group and Others define access categories.
- chmod changes permissions.
- chown changes ownership.
- chgrp changes group ownership.
- umask controls default permission restrictions.
- SUID, SGID and Sticky Bit provide special permission behaviour.
- ACL enables additional user and group access.
- SELinux adds another security layer.

---

## 18. Day 10 Completion Checklist

- [x] Linux Permission Categories
- [x] Read, Write and Execute
- [x] Numeric and Symbolic Permissions
- [x] chmod
- [x] chown
- [x] chgrp
- [x] umask
- [x] SUID, SGID and Sticky Bit
- [x] ACL
- [x] ACL Mask and Default ACL
- [x] SELinux Fundamentals
- [x] Practical Lab
- [x] Interview Preparation

**Learning Journey:** Day 10 of 77

**Status:** Lesson Completed – Practical Assessment Pending

**Next Scheduled Topic:**
Day 11 – Linux Package Management, systemd and Processes
