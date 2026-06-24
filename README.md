# linux-learning-journey

# Linux Learning Journey and Documentation Hub

This repository serves as a professional, comprehensive knowledge base for Linux administration, file system mechanics, and security operations, specifically tailored for standard Linux distributions and Kali Linux environment workflows.

---

## Table of Contents
1. Linux File System Structure (FHS)
2. Core Navigation Commands
3. Basic Kali and Linux System Commands
4. Users and Groups Management
5. Linux File Permissions and Ownership

---

## 1. Linux File System Structure (FHS)

Linux organizes files in a hierarchical tree structure where everything starts from the root directory designated by a single forward slash (/).

```text
/ (Root)
├── bin         (Essential user command binaries)
├── sbin        (Essential system binaries for root user)
├── etc         (System configuration files)
├── home        (User home directories for standard users)
├── root        (Home directory for the root superuser)
├── var         (Variable data files like system logs and queues)
├── tmp         (Temporary files cleared upon reboot)
├── dev         (Device files representing hardware components)
└── proc        (Virtual file system documenting kernel and process states)

2. Core Navigation Commands
Navigation utilities allow users to traverse the file system hierarchy efficiently.
pwd (Print Working Directory)
Displays the absolute path of the current directory.
Terminal Execution Example:

kali@kali:~$ ls -la
total 24
drwxr-xr-x  4 kali kali 4096 Jun 24 04:30 .
drwxr-xr-x  3 root root 4096 Jun 24 04:28 ..
-rw-r--r--  1 kali kali  220 Jun 24 04:28 .bash_logout
-rw-r--r--  1 kali kali 3526 Jun 24 04:28 .bashrc
drwxr-xr-x  2 kali kali 4096 Jun 24 04:30 Desktop
drwxr-xr-x  2 kali kali 4096 Jun 24 04:30 Documents

cd (Change Directory)

Changes the current working directory.

cd /etc-Move to absolute path /etc.

...

cd Move up one level to the parent directory.

cd 2 Move directly to the current user's home directory.

Terminal Execution Example:

3. Basic Kali and Linux System Commands
These foundational commands are essential for system enumeration, network troubleshooting, and security profiling.

whoami and id:
whoami prints the current effective username. id prints real and effective user and group IDs.
Terminal Execution Example:

kali@kali:~$ cd /etc
kali@kali:/etc$ pwd
/etc

kali@kali:~$ pwd
/home/kali

ls (List)
Lists directory contents. Common flags include -l for long listing format (shows permissions, owner, size) and -a for listing all files including hidden ones starting with a dot (.).
Terminal Execution Example:

kali@kali:~$ whoami
kali
kali@kali:~$ id
uid=1000(kali) gid=1000(kali) groups=1000(kali),27(sudo),142(kaboxer)

uname -a
Prints detailed system architecture, kernel release, and operating system information.
Terminal Execution Example:

kali@kali:~$ uname -a
Linux kali 6.1.0-kali7-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.1.16-1kali1 x86_64 GNU/Linux

Network Configuration (ip a / ifconfig)
Displays active network interfaces, hardware MAC addresses, and assigned IP configurations.
Terminal Execution Example:

kali@kali:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:3e:4f:01 brd ff:ff:ff:ff:ff:ff
    inet 192.168.23.130/24 brd 192.168.23.255 scope global dynamic eth0

4. Users and Groups Management
Linux handles multi-user environments strictly via specialized configurations located inside /etc/passwd and /etc/group.
Creating a User and Group
sudo groupadd techops - Creates a new network security or operations group.
sudo useradd -m -g techops analyst - Creates a new user named "analyst", creates their home directory (-m), and assigns them to the "techops" primary group.
Terminal Execution Example:

kali@kali:~$ sudo groupadd techops
kali@kali:~$ sudo useradd -m -g techops analyst
kali@kali:~$ grep analyst /etc/passwd
analyst:x:1001:1001::/home/analyst:/bin/sh

5. Linux File Permissions and Ownership
File access security is dictated by permissions belonging to three tiers: User (Owner), Group, and Others.

Reading the Triad System
When viewing file permissions via ls -l, you encounter a 10-character string like -rwxr-xr--.
Character 1: File type (- = regular file, d = directory).
Characters 2-4: Owner permissions (Read, Write, Execute).
Characters 5-7: Group permissions (Read, Write, Execute).
Characters 8-10: Others permissions (Read, Write, Execute).
Numerical (Octal) Notation Values
Read (r) = 4
Write (w) = 2
Execute (x) = 1
Modifying Permissions (chmod) and Ownership (chown)
chmod 755 script.sh - Grants full access (7) to owner, read/execute (5) to group, and read/execute (5) to others.
sudo chown root:techops target_file.txt - Changes file owner to root and group association to techops.
Terminal Execution Example:

kali@kali:~$ touch script.sh
kali@kali:~$ chmod 755 script.sh
kali@kali:~$ ls -l script.sh
-rwxr-xr-x 1 kali kali 0 Jun 24 04:45 script.sh
