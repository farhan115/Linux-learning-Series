# 🐧 Linux File System Directory Structure

## 📌 Project Overview

This project explores the **Linux Filesystem Hierarchy Standard (FHS)** and explains the purpose of important directories in Linux.

Understanding the Linux directory structure is an essential skill for **Linux System Administrators, DevOps Engineers, Cloud Engineers, and Cybersecurity Professionals**.

## 📂 Linux Directory Structure

| Directory | Description |
|---|---|
| `/home` | Stores personal files and directories for regular users. |
| `/etc` | Contains system-wide configuration files. |
| `/var` | Stores variable data, including logs, caches, and application data. |
| `/dev` | Contains device files representing hardware and virtual devices. |
| `/boot` | Contains files required for the boot process, including kernel files. |
| `/bin` | Contains essential user commands. |
| `/sbin` | Contains essential system administration commands. |
| `/usr` | Contains applications, utilities, libraries, and shared resources. |
| `/lib` | Contains essential shared libraries and kernel modules on traditional Linux layouts. |
| `/tmp` | Stores temporary files. |
| `/proc` | Virtual filesystem providing process and kernel information. |
| `/media` | Common mount location for removable storage devices. |
| `/mnt` | Common location for manually mounted filesystems. |

**Note:** On many modern Linux distributions, `/bin`, `/sbin`, and `/lib` are symbolic links to directories under `/usr`. Directory layouts can vary by distribution.

## 🛠️ Hands-On Linux Commands

### 1. Explore the Root Directory

```bash
ls /
```

Displays the directories located at the root of the Linux filesystem.

### 2. Explore User Files

```bash
ls /home
```

Lists home directories for regular users.

### 3. View Configuration Files

```bash
ls /etc
cat /etc/os-release
```

Displays configuration files and Linux distribution information.

### 4. Examine System Logs

```bash
ls /var/log
journalctl -n 20
```

Lists available log files and displays recent systemd journal entries.

### 5. Examine Hardware Devices

```bash
ls /dev
lsblk
```

Displays device entries and block storage devices.

### 6. Explore Boot Files

```bash
ls /boot
uname -r
```

Lists boot-related files and displays the running kernel version.

### 7. View System Information

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

Displays CPU and memory information.

### 8. Check Storage

```bash
df -h
lsblk -f
```

Displays filesystem disk usage and block device information.

### 9. Examine Temporary Files

```bash
ls /tmp
```

Lists files in the temporary directory.

### 10. Locate Linux Programs

```bash
which ls
which bash
```

Displays the executable paths used for these commands.

## 🎯 Skills Demonstrated

- Linux filesystem navigation
- Understanding the Filesystem Hierarchy Standard
- System configuration file exploration
- Linux log inspection
- Storage and device identification
- Kernel and system information inspection
- Command-line troubleshooting fundamentals

## 🔐 Linux System Administration Relevance

Understanding Linux directories helps administrators:

- Troubleshoot system errors using logs in `/var/log`.
- Manage configuration files under `/etc`.
- Investigate running processes using `/proc`.
- Identify disks and storage devices.
- Maintain system services and operating system environments.
- Diagnose storage and filesystem problems.

## 🧰 Tools and Technologies

- Linux (RHEL / Ubuntu / Rocky Linux)
- Bash
- Linux CLI
- Systemd
- Filesystem Hierarchy Standard (FHS)

## 📈 Learning Outcomes

After completing this project, I gained foundational knowledge of Linux filesystem organization, system configuration locations, log directories, storage devices, and essential administrative commands.

This project is part of my ongoing hands-on Linux System Administration learning and RHCSA preparation.

## 👨‍💻 Author

**Farhan Muntasir**

B.S. Computer Science | Linux System Administration | IT Infrastructure | Cybersecurity

**GitHub:** https://github.com/farhan115

---

⭐ This project is part of my Linux System Administration hands-on lab portfolio.
