Content
1. [Linux](#linux)

# LINUX
Linux is a family of open-source Unix-like operating systems inspired by UNIX., based on the Linux kernel, a computer program that manages the system's hardware and software.

kernel that is used in a distribution, but most people just refer to it as an OS.
> 90% of application runs on **Linux**.

**Unix** is a proprietary (requiring a license for use), multitasking operating system, e.g. macOS, Debian. While **Linux** is a free and open-source, Unix-like operating system. e.g. Ubuntu, Kali Linux

### How to Use Linux
1.  **WSL (Windows Subsystem for Linux)** – Enable it on Windows to run Linux distributions natively.
2.  **Virtual Machine** – Use applications like [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  to run Linux in a virtual environment.
3.  **Cloud Platforms** – Use Linux-based instances on AWS, GCP, or Azure.
4.  **Vagrant** – Try Linux environments locally using [Vagrant](https://developer.hashicorp.com/vagrant)

## Linux - OS
The kernel is the **heart**  of the operating system. It is written primarily in the **C programming language**  and acts as the bridge between the system hardware and software.
-   It manages system resources such as CPU, memory, and I/O devices.
-   Users interact with the kernel via a **shell** (command-line interface).    
-   Common shell commands include `mkdir`, `ls`, `cd`, etc.
- **root** is the most powerful account that can create, modify, delete accounts and make changes to system configuration files.
> **GRUB** (Grand Unified Bootloader) is the program responsible for loading and managing the boot process. It loads the **kernel**  of the OS into memory at startup.

Linux itself is not one single operating system. It has many versions called distributions (distros).

Examples:

- Ubuntu
- CentOS
- Debian
- Fedora
- Red Hat Enterprise Linux

Linux has hundreds of distributions (Linux OS versions). They are all based on the Linux kernel but are made for different purposes.

**Here are the most popular Linux OS families:**


**1. Debian Family** One of the oldest, free and most stable Linux families. e.x **ubuntu, kali linux, linux Mint**

**2. Red Hat Family** Popular in companies and enterprise servers. **Red Hat Enterprise Linux (RHEL), Fedora Linux, CentOS**

| |Debian| Red Hat | 
|--|--| -- |
| Package Management | apt + .deb packages | yum/dnf + .rpm packages |
|Where they are mostly used|Web servers, Cloud servers, Personal computers | Large companies, Banks, Government systems, Corporate servers |
|Cost Difference|Free|Paid|
|Package Commands|`apt`,`apt update`, `apt install`, `.deb`|`dnf/yum`, `dnf update`, `dnf install`, `.rpm`|
|Real-world example|A startup might use `AWS server -> Ubuntu -> Website`| A bank might use `Data Center -> RHEL -> Banking application`|


# 2. File System
OS stores files and directories in an organized and structured way. There are many different types of filesystems. 
e.g. ext3, ext4, xfs, NTFS, FAT etc.
```bash
cd /
ls -l  # list all the files structure
/boot # contains file that is used by the boot loader (grub.cfg)
/root # root user home directory. It is not same as /
/dev # systems devices (e.x. disk, speakers, keyboards, etc)
/etc # all configuration files
/bin --> /usr/bin # everyday users commands
/opt # optional add-on applications (not part of OS apps)
/proc # running processes 
/tmp # directory for temporary files
/home # directory for user
/var # system logs
/run # system daemons that start very early to store temporary runtime file like PID files
/mnt # to mount external filesystem (e.x NFS)
```
