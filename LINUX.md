# LINUX
Linux is a family of open-source Unix-like operating systems, based on the Linux kernel, a computer program that manages the system's hardware and software.
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
> **GRUB** (Grand Unified Bootloader) is the program responsible for loading and managing the boot process. It loads the **kernel**  of the OS into memory at startup.

## 1. Basic Commands

| **Command**        | **Description**                                                                 | **Example to Run**                                |
|--------------------|----------------------------------------------------------------------------------|---------------------------------------------------|
| **ls**             | List files and directories in the current directory.                             | `ls` or `ls -l`                                   |
| **cd**             | Change the current directory.                                                    | `cd Documents`                                    |
| **pwd**            | Print the current working directory.                                             | `pwd`                                             |
| **mkdir**          | Create a new directory.                                                          | `mkdir myfolder`                                  |
| **rm**, **rmdir**  | Remove files or directories. `rmdir` only removes empty directories.             | `rm file.txt`, `rmdir myfolder`                   |
| **cat**, **zcat**  | Display contents of files; `zcat` works with compressed files.                   | `cat file.txt`, `zcat file.txt.gz`                |
| **touch**          | Create an empty file or update timestamp.                                        | `touch newfile.txt`                               |
| **head**           | Show the first 10 lines of a file.                                               | `head file.txt`                                   |
| **tail**, **tail -f** | Show the last lines of a file; `-f` follows the file for new lines.           | `tail file.txt`, `tail -f logs.txt`               |
| **less**, **more** | View file content one screen at a time.                                          | `less file.txt`, `more file.txt`                  |
| **cp**             | Copy files or directories.                                                       | `cp file1.txt file2.txt` or `cp -r dir1 dir2`     |
| **mv**             | Move or rename files or directories.                                             | `mv file.txt newfolder/` or `mv old.txt new.txt`  |
| **wc**             | Count lines, words, characters in a file.                                        | `wc file.txt`, `wc -l file.txt`                   |
| **vi**             | Open the `vi` text editor.                                                       | `vi file.txt`                                     |
| **ln**             | Create symbolic or hard links.                                                   | `ln -s original.txt link.txt`                     |
| **cut**            | Extract sections from input lines.                                               | `cut -d':' -f1 /etc/passwd`                        |
| **tee**            | Write to a file and display output at the same time.                             | `echo "Hello" | tee hello.txt`                    |
| **sort**           | Sort lines of a file.                                                            | `sort names.txt`                                  |
| **clear**          | Clear the terminal screen.                                                       | `clear`                                           |
| **diff**           | Show differences between two files.                                              | `diff file1.txt file2.txt`                        |
| **df**             | Show disk space usage.                                                           | `df -h`                                           |
| **du**             | Estimate file or directory size.                                                 | `du -sh folder/`                                  |
| **ssh**            | Connect securely to a remote system.                                             | `ssh user@192.168.1.10`                           |
| **ps**             | Show running processes.                                                          | `ps aux`                                          |
| **top**            | Show real-time system resource usage.                                            | `top`                                             |
| **fuser**          | Identify processes using a file or socket.                                       | `fuser filename.txt`                              |
| **kill**           | Terminate a process using its PID.                                               | `kill 1234`                                       |
| **nohup**          | Run a command immune to logout or terminal hangups.                              | `nohup ./script.sh &`                             |
| **free**           | Show memory usage.                                                               | `free -h`                                         |
| **vmstat**         | Display performance stats (CPU, memory, IO).                                     | `vmstat 1`                                        |




  ## 2. Users & Files Management

### System Level Commands

| **Command**     | **Definition**                                                    | **Example to Run**                            |
|-----------------|-------------------------------------------------------------------|-----------------------------------------------|
| **uname**       | Shows system information.                                         | `uname -a`                                     |
| **uptime**      | Displays how long the system has been running.                   | `uptime`                                       |
| **date**        | Shows or sets the system date and time.                          | `date` or `date "+%Y-%m-%d %H:%M:%S"`          |
| **who**         | Lists users currently logged in.                                 | `who`                                          |
| **whoami**      | Shows the username of the current user.                          | `whoami`                                       |
| **which**       | Displays the path of an executable command.                      | `which python3`                                |
| **id**          | Shows UID, GID, and group info of the current user.              | `id`                                           |
| **sudo**        | Runs commands with superuser privileges.                         | `sudo apt update`                              |
| **shutdown**    | Turns off the system.                                            | `sudo shutdown -h now`                         |
| **reboot**      | Restarts the system.                                             | `sudo reboot`                                  |
| **apt**         | Debian-based package installer.                                  | `sudo apt install curl`                        |
| **yum**         | RHEL/CentOS-based package manager.                               | `sudo yum install wget`                        |
| **dnf**         | Fedora/RHEL-based modern package manager.                        | `sudo dnf install git`                         |
| **pacman**      | Arch Linux package manager.                                      | `sudo pacman -S firefox`                       |
| **portage**     | Gentoo Linux package management system.                          | `sudo emerge --ask nano`                       |

---

### Users & Group Management

| **Command**     | **Definition**                                                    | **Example to Run**                            |
|-----------------|-------------------------------------------------------------------|-----------------------------------------------|
| **sudo**        | Run a command as another user (root by default).                 | `sudo useradd newuser`                        |
| **useradd**     | Adds a new user to the system.                                   | `sudo useradd -m john`                        |
| **whoami**      | Prints current user's username.                                  | `whoami`                                       |
| **su**          | Switches to another user account.                                | `su - john`                                    |
| **passwd**      | Changes a user's password.                                       | `sudo passwd john`                             |
| **userdel**     | Deletes a user account.                                          | `sudo userdel -r john`                         |
| **groupadd**    | Adds a new group.                                                | `sudo groupadd developers`                     |
| **gpasswd**     | Adds user(s) to a group.                                         | `sudo gpasswd -a john developers`              |
| **groupdel**    | Deletes an existing group.                                       | `sudo groupdel developers`                     |

---

### File Permissions

| **Command**     | **Definition**                                                    | **Example to Run**                            |
|-----------------|-------------------------------------------------------------------|-----------------------------------------------|
| **umask**       | Displays or sets default permission settings.                    | `umask` or `umask 022`                         |
| **ls -l**       | Lists files with permission and ownership details.               | `ls -l`                                        |
| **chmod**       | Changes file permission.                                         | `chmod 755 script.sh`                          |
| **chown**       | Changes file ownership.                                          | `sudo chown john:john file.txt`               |
| **chgrp**       | Changes the group ownership of a file.                           | `sudo chgrp developers file.txt`              |

---

### Compression

| **Command**         | **Definition**                                                | **Example to Run**                            |
|---------------------|---------------------------------------------------------------|-----------------------------------------------|
| **zip**             | Compresses files into a .zip archive.                        | `zip archive.zip file1.txt file2.txt`         |
| **gzip**            | Compresses a single file using `.gz`.                        | `gzip file.txt`                                |
| **gunzip**          | Decompresses `.gz` files.                                    | `gunzip file.txt.gz`                           |
| **tar**             | Archives multiple files/directories.                         | `tar -cvf archive.tar file1 file2`             |
| **untar**           | Extracts files from a `.tar` archive.                        | `tar -xvf archive.tar`                         |

---

### File Transfer

| **Command**     | **Definition**                                                    | **Example to Run**                            |
|-----------------|-------------------------------------------------------------------|-----------------------------------------------|
| **scp**         | Securely copies files between systems over SSH.                  | `scp file.txt user@192.168.1.10:/home/user/`   |
| **rsync**       | Syncs files/directories locally or remotely.                     | `rsync -avz folder/ user@192.168.1.10:/path/`  |

## Networking Commands

| **Command**      | **Description**                                                  | **Example to Run**                              |
|------------------|------------------------------------------------------------------|-------------------------------------------------|
| **ping**         | Checks network connectivity to a host.                          | `ping google.com`                              |
| **netstat**      | Displays network connections, routing tables, etc.              | `netstat -tuln`                                |
| **ifconfig**     | Shows or configures network interfaces (deprecated in favor of `ip`). | `ifconfig`                                 |
| **ip**           | Replaces `ifconfig` for managing IP addresses and routes.       | `ip a` or `ip link`                            |
| **traceroute**   | Displays route packets take to reach a host.                    | `traceroute google.com`                        |
| **tracepath**    | Similar to traceroute but doesn't require root permissions.     | `tracepath google.com`                         |
| **mtr**          | Combines `ping` and `traceroute` for real-time diagnostics.     | `mtr google.com`                               |
| **nslookup**     | Queries DNS to resolve domain names.                            | `nslookup google.com`                          |
| **telnet**       | Tests port connectivity on remote servers.                      | `telnet google.com 80`                         |
| **hostname**     | Displays or sets the system hostname.                           | `hostname` or `sudo hostname newname`          |
| **iwconfig**     | Configures wireless network interfaces.                         | `iwconfig`                                     |
| **ss**           | Displays socket statistics (replacement for netstat).           | `ss -tuln`                                     |
| **arp**          | Displays or modifies the ARP table.                             | `arp -a`                                       |
| **dig**          | Advanced DNS lookup tool.                                       | `dig google.com`                               |
| **nc (netcat)**  | Reads/writes data across network connections.                   | `nc -zv google.com 80`                         |
| **whois**        | Retrieves domain registration info.                             | `whois google.com`                             |
| **ifplugstatus** | Checks if a network cable is plugged in.                        | `ifplugstatus eth0`                            |
| **route**        | Shows/manages the routing table.                                | `route -n`                                     |
| **nmap**         | Network scanner for open ports and services.                    | `nmap 127.0.0.1`                               |
| **wget**         | Downloads files from web via HTTP, HTTPS, FTP.                  | `wget https://example.com/file.txt`            |
| **curl**         | Transfers data to/from a server using URL syntax.               | `curl https://example.com`                     |
| **watch**        | Runs a command repeatedly at intervals.                         | `watch -n 2 ifconfig`                          |
| **iptables**     | Configures Linux firewall rules.                                | `sudo iptables -L`                             |


## Advanced Text Processing Commands

| **Command**  | **Description**                                                        | **Example to Run**                                       |
|--------------|------------------------------------------------------------------------|----------------------------------------------------------|
| **awk**      | Pattern scanning and processing language, used for extracting columns. | `awk '{print $1}' file.txt`                              |
| **sed**      | Stream editor for filtering and transforming text.                     | `sed 's/apple/orange/g' file.txt`                        |
| **grep**     | Searches for patterns in text using regular expressions.               | `grep "error" logfile.txt`                               |
| **cut**      | Removes sections from each line of input (by delimiter or byte).       | `cut -d',' -f1 file.csv`                                 |
| **sort**     | Sorts lines of text files.                                              | `sort file.txt`                                          |
| **uniq**     | Removes or reports duplicate lines in a file (commonly used with `sort`). | `sort file.txt | uniq`                                 |
| **tr**       | Translates or deletes characters.                                      | `echo "hello" | tr 'a-z' 'A-Z'`                          |
| **paste**    | Merges lines of files side-by-side.                                    | `paste file1.txt file2.txt`                             |
| **xargs**    | Builds and executes command lines from input.                          | `ls *.txt | xargs rm`                                    |
| **tee**      | Reads input and writes it to both stdout and a file.                   | `echo "log entry" | tee logfile.txt`                     |
| **head**     | Displays the first N lines of a file.                                  | `head -n 5 file.txt`                                    |
| **tail**     | Displays the last N lines of a file.                                   | `tail -n 10 file.txt`                                   |
| **wc**       | Prints newline, word, and byte counts for each file.                   | `wc file.txt`                                           |



## Linux Volume Management

#### 1. **Linux Volumes and AWS EBS**

**Linux Volumes**  refer to the storage partitions or logical volumes that a Linux system uses to store data. These can be physical devices, logical volumes, or cloud-based volumes. In **AWS**, **Elastic Block Store (EBS)**  provides persistent storage for EC2 instances.

**AWS EBS**  allows you to attach volumes to EC2 instances, providing data storage that persists even if the instance is stopped or terminated. You can use EBS volumes as block storage devices, which behave like hard drives, allowing you to format, mount, and manage them.

**Example (Attach EBS volume to EC2 instance):**

1.  Create an EBS volume from the AWS Console.    
2.  Attach it to your EC2 instance.
3.  SSH into the EC2 instance and run:

```bash
sudo fdisk -l  # List disks to find the new volume
sudo mkfs.ext4 /dev/xvdf  # Format the volume
sudo mount /dev/xvdf /mnt  # Mount the volume
```

#### 2. **Physical vs Logical vs Volume Groups in Linux**

-   **Physical Volumes (PV):**  These are actual physical devices like hard drives or SSDs.
    -   Example: `/dev/sda`, `/dev/sdb`
        
-   **Volume Groups (VG):**  A volume group is a collection of physical volumes. It is the layer between physical storage and logical volumes.
    -   Example: `vg_data` (which contains multiple physical volumes)
        
-   **Logical Volumes (LV):**  These are virtual partitions that reside within a volume group and can be resized dynamically.
    -   Example: `lv_home`, `lv_data`
        
**LVM (Logical Volume Management)**  allows you to manage storage more flexibly by combining physical storage devices into volume groups and creating logical volumes that can be resized as needed.

#### 3. **Mounting Volumes in Linux**

Mounting a volume in Linux means making a storage device accessible to the operating system.

To mount a volume:
1.  Create a directory (mount point):
    `sudo mkdir /mnt/mydrive` 
    
2.  Mount the volume to the directory:
    `sudo mount /dev/sdb1 /mnt/mydrive` 
    
3.  Verify the mounted volume:
    `df -h` 
    

To make the mount persistent (so it persists after reboot), edit the `/etc/fstab`  file:
`/dev/sdb1 /mnt/mydrive ext4 defaults 0 2`


#### 4. **Managing AWS EBS on EC2 Instances**

When using AWS EC2, you can manage EBS volumes to provide persistent storage for your instances.

-   **Attach an EBS Volume:**
    
    -   Go to the EC2 Console > Volumes > Create Volume > Choose Size and Type.
    -   Attach the volume to your running EC2 instance.
        
-   **Mount the Volume on EC2:**
    
    1.  After the volume is attached, log in to your EC2 instance using SSH.
    2.  Check available disks:
        `sudo fdisk -l` 
        
    3.  Format the volume:
        `sudo mkfs.ext4 /dev/xvdf` 
        
    4.  Mount the volume:    
        `sudo mount /dev/xvdf /mnt` 
        
----------

#### 5. **LVM (Logical Volume Management)**

LVM provides a flexible and dynamic way to manage disk space. With LVM, you can:

-   Combine multiple physical volumes (PVs) into a volume group (VG).
-   Create logical volumes (LVs) from volume groups, which can be resized as needed.
    
**Example:**

1.  Create a Physical Volume:
    `sudo pvcreate /dev/sdb` 
    
2.  Create a Volume Group:
    `sudo vgcreate vg_data /dev/sdb` 
    
3.  Create a Logical Volume:
    `sudo lvcreate -L 10G -n lv_data vg_data` 
    
4.  Format the Logical Volume:
    `sudo mkfs.ext4 /dev/vg_data/lv_data` 
    
5.  Mount the Logical Volume:
    `sudo mount /dev/vg_data/lv_data /mnt` 
    

----------

#### 6. **Using LVM with EBS for Dynamic Storage Management**

By using LVM with AWS EBS, you can dynamically allocate storage, resize volumes, and even move data between volumes without downtime.

**Example (Dynamic Storage Management):**

1.  **Attach multiple EBS volumes**  to an EC2 instance.
2.  Create Physical Volumes for each attached EBS volume:
    `sudo pvcreate /dev/xvdf /dev/xvdg` 
    
3.  Create a Volume Group using the attached volumes:
    `sudo vgcreate vg_aws /dev/xvdf /dev/xvdg` 
    
4.  Create Logical Volumes from the volume group:    
    `sudo lvcreate -L 20G -n lv_aws vg_aws` 
    
5.  Format and mount the logical volume:
    `sudo mkfs.ext4 /dev/vg_aws/lv_aws
    sudo mount /dev/vg_aws/lv_aws /mnt/ebs_volume` 
    

**Benefits of LVM with EBS:**

-   **Dynamic resizing:**  Easily resize logical volumes as data grows.
-   **Snapshots:**  Create snapshots of volumes to back up data or test changes without risk. 
-   **Better utilization of space:**  Combine multiple EBS volumes to form a single logical volume.