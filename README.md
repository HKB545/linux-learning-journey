#  Linux Learning Journey & Documentation Hub

A professional and comprehensive Linux knowledge repository focused on Linux administration, filesystem architecture, user management, permissions, and Kali Linux workflows.

This repository serves as a structured reference guide for beginners, cybersecurity students, system administrators, and Linux enthusiasts who want to build a strong foundation in Linux environments.

---

#  Table of Contents

* [Overview](#overview)
* [Linux File System Structure (FHS)](#linux-file-system-structure-fhs)
* [Core Navigation Commands](#core-navigation-commands)
* [Basic Linux & Kali Commands](#basic-linux--kali-commands)
* [Users and Groups Management](#users-and-groups-management)
* [Linux File Permissions & Ownership](#linux-file-permissions--ownership)
* [Future Topics](#future-topics)

---

#  Overview

Linux uses a hierarchical filesystem structure where every file and directory originates from a single root directory (`/`).

Understanding filesystem organization, navigation, permissions, and user management is essential for:

* Linux Administration
* System Engineering
* DevOps
* Cybersecurity
* Ethical Hacking
* Penetration Testing
* Cloud Infrastructure

This repository documents practical Linux concepts with real-world examples and terminal outputs.

---

#  Linux File System Structure (FHS)

Linux follows the **Filesystem Hierarchy Standard (FHS)**.

```text
/ (Root)
├── bin
├── sbin
├── etc
├── home
├── root
├── var
├── tmp
├── dev
└── proc
```

## Important Directories

| Directory | Purpose                                                      |
| --------- | ------------------------------------------------------------ |
| `/`       | Root directory of the entire filesystem                      |
| `/bin`    | Essential user command binaries                              |
| `/sbin`   | Essential system administration binaries                     |
| `/etc`    | System-wide configuration files                              |
| `/home`   | Home directories of standard users                           |
| `/root`   | Home directory of the root user                              |
| `/var`    | Variable data such as logs and spool files                   |
| `/tmp`    | Temporary files                                              |
| `/dev`    | Hardware and device files                                    |
| `/proc`   | Virtual filesystem containing process and kernel information |

---

#  Core Navigation Commands

Navigation commands help users move through the Linux filesystem efficiently.

---

## 1. pwd (Print Working Directory)

Displays the absolute path of the current directory.

### Example

```bash
kali@kali:~$ pwd
/home/kali
```

---

## 2. ls (List Directory Contents)

Lists files and directories.

### Common Options

| Option   | Description                             |
| -------- | --------------------------------------- |
| `ls`     | Basic listing                           |
| `ls -l`  | Detailed listing                        |
| `ls -a`  | Show hidden files                       |
| `ls -la` | Detailed listing including hidden files |

### Example

```bash
kali@kali:~$ ls -la

total 24
drwxr-xr-x  4 kali kali 4096 Jun 24 04:30 .
drwxr-xr-x  3 root root 4096 Jun 24 04:28 ..
-rw-r--r--  1 kali kali  220 Jun 24 04:28 .bash_logout
-rw-r--r--  1 kali kali 3526 Jun 24 04:28 .bashrc
drwxr-xr-x  2 kali kali 4096 Jun 24 04:30 Desktop
drwxr-xr-x  2 kali kali 4096 Jun 24 04:30 Documents
```

---

## 3. cd (Change Directory)

Changes the current working directory.

### Common Usage

```bash
cd /etc
```

Move to the `/etc` directory.

```bash
cd ..
```

Move one level up.

```bash
cd ~
```

Move directly to the current user's home directory.

### Example

```bash
kali@kali:~$ cd /etc
kali@kali:/etc$ pwd

/etc
```

---

#  Basic Linux & Kali Commands

These commands are frequently used during Linux administration, troubleshooting, and security assessments.

---

## whoami

Displays the current logged-in user.

### Example

```bash
kali@kali:~$ whoami

kali
```

---

## id

Displays user ID (UID), group ID (GID), and associated groups.

### Example

```bash
kali@kali:~$ id

uid=1000(kali) gid=1000(kali) groups=1000(kali),27(sudo),142(kaboxer)
```

---

## uname -a

Displays kernel version and operating system information.

### Example

```bash
kali@kali:~$ uname -a

Linux kali 6.1.0-kali7-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.1.16-1kali1 x86_64 GNU/Linux
```

---

## ip a

Displays network interfaces and IP addresses.

### Example

```bash
kali@kali:~$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP>
    inet 127.0.0.1/8 scope host lo

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 192.168.23.130/24 scope global dynamic eth0
```

---

#  Users and Groups Management

Linux is a multi-user operating system that controls access through users and groups.

Important configuration files:

```text
/etc/passwd
/etc/group
```

---

## Creating a Group

```bash
sudo groupadd techops
```

Creates a new group called `techops`.

---

## Creating a User

```bash
sudo useradd -m -g techops analyst
```

### Explanation

| Option       | Purpose               |
| ------------ | --------------------- |
| `-m`         | Create home directory |
| `-g techops` | Assign primary group  |
| `analyst`    | Username              |

---

## Verification

```bash
grep analyst /etc/passwd
```

### Output

```bash
analyst:x:1001:1001::/home/analyst:/bin/sh
```

---

#  Linux File Permissions & Ownership

Linux security relies heavily on permissions and ownership.

Each file and directory has permissions assigned to:

1. User (Owner)
2. Group
3. Others

---

## Permission Structure

Example:

```text
-rwxr-xr--
```

### Breakdown

| Position | Meaning            |
| -------- | ------------------ |
| 1        | File Type          |
| 2-4      | Owner Permissions  |
| 5-7      | Group Permissions  |
| 8-10     | Others Permissions |

---

## File Types

| Symbol | Type          |
| ------ | ------------- |
| `-`    | Regular File  |
| `d`    | Directory     |
| `l`    | Symbolic Link |

---

## Permission Values

| Permission  | Value |
| ----------- | ----- |
| Read (r)    | 4     |
| Write (w)   | 2     |
| Execute (x) | 1     |

### Examples

| Octal | Meaning             |
| ----- | ------------------- |
| 777   | Full Access         |
| 755   | Standard Executable |
| 644   | Standard File       |
| 600   | Private File        |

---

## chmod (Change Permissions)

```bash
chmod 755 script.sh
```

### Meaning

* Owner = Read + Write + Execute (7)
* Group = Read + Execute (5)
* Others = Read + Execute (5)

---

## chown (Change Ownership)

```bash
sudo chown root:techops target_file.txt
```

Changes:

* Owner → root
* Group → techops

---

## Example Workflow

```bash
touch script.sh

chmod 755 script.sh

ls -l script.sh
```

### Output

```bash
-rwxr-xr-x 1 kali kali 0 Jun 24 04:45 script.sh
```

---

#  Future Topics

This repository will continue expanding with:

* Linux Package Management
* Process Management
* Bash Scripting
* Cron Jobs
* Systemd Services
* Networking Fundamentals
* SSH Administration
* Firewall Configuration
* Log Analysis
* Kali Linux Tools
* Privilege Escalation Basics
* Linux Hardening
* Cybersecurity Workflows
* Penetration Testing Notes

---

#  Contributing

Contributions, improvements, and corrections are welcome.

Feel free to fork this repository and submit pull requests.

---

### Happy Learning 🐧

### Keep Exploring Linux & Cybersecurity 🚀
