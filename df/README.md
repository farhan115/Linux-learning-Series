# Linux `df` Command – 10 Hands-On Disk Monitoring Projects

## Overview

This repository contains 10 hands-on Linux system administration projects using the `df` (Disk Free) command.

The projects demonstrate how to monitor filesystem utilization, analyze disk capacity, identify storage issues, generate reports, and automate disk usage alerts using Bash scripting.

**Focus:** Linux System Administration | RHCSA | Bash Scripting | Disk Management | Troubleshooting

## Technologies Used

- Linux (RHEL, Rocky Linux, Ubuntu)
- Bash Shell Scripting
- `df`, `awk`, `sort`, `grep`, `head`
- Linux Filesystem Management
- Disk and Inode Monitoring
- System Performance Troubleshooting

---

## Common `df` Commands

| Command | Description |
|---|---|
| `df` | Display filesystem disk usage |
| `df -h` | Display sizes in human-readable format |
| `df -T` | Display filesystem types |
| `df -i` | Display inode usage |
| `df -h /` | Check root filesystem usage |
| `df -h /home` | Check filesystem containing `/home` |
| `df -a` | Include all filesystems |
| `df -H` | Display sizes using powers of 1000 |
| `df --total -h` | Display total disk usage |
| `df -x tmpfs` | Exclude tmpfs filesystems |

## Example: Check Disk Space

```bash
df -h
```

Example output:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3        50G   18G   30G  38% /
/dev/sda1       1.0G  208M  793M  21% /boot
/dev/sda4       200G   45G  155G  23% /home
```

---

## Project 1: Disk Usage Report

**Objective:** Generate a disk usage report and save it to a text file.

**Script:** `disk_report.sh`

```bash
#!/bin/bash

REPORT="disk_report.txt"

echo "===== Disk Usage Report =====" > "$REPORT"
echo "Date: $(date)" >> "$REPORT"
echo "" >> "$REPORT"

df -hT >> "$REPORT"

echo "Report saved to $REPORT"
```

**Run:**

```bash
chmod +x disk_report.sh
./disk_report.sh
cat disk_report.txt
```

**Skills:** Disk reporting, filesystem monitoring, output redirection.

---

## Project 2: Disk Usage Alert

**Objective:** Identify filesystems exceeding 80% disk utilization.

**Script:** `check_disk.sh`

```bash
#!/bin/bash

THRESHOLD=80

echo "Checking disk usage..."

df -P | awk -v threshold="$THRESHOLD" '
NR > 1 {
    usage=$5
    gsub("%", "", usage)
    if (usage > threshold) {
        print "WARNING:", $6, "is", usage "% full"
    }
}'
```

**Run:**

```bash
chmod +x check_disk.sh
./check_disk.sh
```

**Skills:** Disk alerts, AWK filtering, threshold monitoring.

---

## Project 3: Monitor `/home` Filesystem

**Objective:** Check the filesystem containing `/home` and warn when usage reaches 80%.

**Script:** `home_usage.sh`

```bash
#!/bin/bash

THRESHOLD=80

USAGE=$(df -P /home | awk 'NR==2 {
    gsub("%", "", $5)
    print $5
}')

echo "/home filesystem usage: ${USAGE}%"

if [ "$USAGE" -ge "$THRESHOLD" ]; then
    echo "WARNING: High disk usage!"
else
    echo "Disk usage is normal."
fi
```

**Run:**

```bash
chmod +x home_usage.sh
./home_usage.sh
```

**Skills:** Filesystem monitoring, conditional statements, Bash variables.

---

## Project 4: Find Largest Filesystems

**Objective:** Display the five largest mounted filesystems by total capacity.

**Script:** `largest_filesystems.sh`

```bash
#!/bin/bash

echo "===== Top 5 Largest Filesystems ====="

df -P -B1 | awk 'NR>1 {
    print $2, $6
}' | sort -nr | head -5 |
awk '{
    printf "Size: %.2f GiB | Mount: %s\n",
    $1/1073741824, $2
}'
```

**Run:**

```bash
chmod +x largest_filesystems.sh
./largest_filesystems.sh
```

**Skills:** Capacity analysis, sorting, AWK, reporting.

---

## Project 5: Filesystem Type Report

**Objective:** Identify filesystem types and save the information to a report.

**Script:** `fs_type_report.sh`

```bash
#!/bin/bash

REPORT="filesystem_types.txt"

echo "===== Filesystem Type Report =====" > "$REPORT"
echo "Date: $(date)" >> "$REPORT"

df -T >> "$REPORT"

echo "Report saved to $REPORT"
```

**Run:**

```bash
chmod +x fs_type_report.sh
./fs_type_report.sh
```

**Skills:** Filesystem identification, storage administration, reporting.

---

## Project 6: Inode Usage Monitoring

**Objective:** Detect filesystems with inode utilization above 80%.

**Script:** `check_inode.sh`

```bash
#!/bin/bash

THRESHOLD=80

echo "===== Inode Usage Check ====="

df -Pi | awk -v threshold="$THRESHOLD" '
NR > 1 {
    usage=$5
    gsub("%", "", usage)
    if (usage > threshold) {
        print "WARNING:", $6,
        "inode usage:", usage "%"
    }
}'
```

**Run:**

```bash
chmod +x check_inode.sh
./check_inode.sh
```

**Skills:** Inode monitoring, filesystem troubleshooting, storage alerts.

---

## Project 7: Exclude Temporary Filesystems

**Objective:** Display disk usage while excluding common virtual and temporary filesystem types.

**Script:** `real_disk_usage.sh`

```bash
#!/bin/bash

echo "===== Disk Usage Without Virtual Filesystems ====="

df -h \
    -x tmpfs \
    -x devtmpfs \
    -x squashfs \
    -x overlay
```

**Run:**

```bash
chmod +x real_disk_usage.sh
./real_disk_usage.sh
```

**Skills:** Filesystem filtering, disk analysis, Linux administration.

**Note:** This excludes common virtual filesystem types but does not guarantee that every remaining filesystem is a physical disk.

---

## Project 8: Identify Filesystem for a Directory

**Objective:** Determine which filesystem contains a specified directory.

**Script:** `find_fs.sh`

```bash
#!/bin/bash

DIR="${1:-/}"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory does not exist."
    exit 1
fi

echo "===== Filesystem Information ====="

df -hT "$DIR"
```

**Run:**

```bash
chmod +x find_fs.sh
./find_fs.sh /home
```

**Skills:** Mount point identification, filesystem troubleshooting, disk usage analysis.

---

## Project 9: Root Filesystem Health Check

**Objective:** Check available disk space on the root filesystem and generate a health status.

**Script:** `root_health.sh`

```bash
#!/bin/bash

THRESHOLD=85

USAGE=$(df -P / | awk 'NR==2 {
    gsub("%", "", $5)
    print $5
}')

echo "Root Filesystem Usage: ${USAGE}%"

if [ "$USAGE" -ge "$THRESHOLD" ]; then
    echo "STATUS: CRITICAL"
else
    echo "STATUS: HEALTHY"
fi
```

**Run:**

```bash
chmod +x root_health.sh
./root_health.sh
```

**Skills:** Root filesystem monitoring, system health checks, automated status reporting.

---

## Project 10: Automated Disk Usage Logging

**Objective:** Create a timestamped disk usage log that can be run periodically.

**Script:** `disk_logger.sh`

```bash
#!/bin/bash

LOGFILE="$HOME/disk_usage.log"

{
    echo "===== Disk Usage Snapshot ====="
    echo "Date: $(date)"
    df -hT
    echo "================================"
    echo ""
} >> "$LOGFILE"

echo "Disk usage logged to $LOGFILE"
```

**Run:**

```bash
chmod +x disk_logger.sh
./disk_logger.sh
```

To schedule logging every hour using cron:

```bash
crontab -e
```

Add the following line, replacing the path with the absolute location of your script:

```text
0 * * * * /home/youruser/Linux-df-Projects/disk_logger.sh
```

**Skills:** Bash automation, cron scheduling, log management, capacity monitoring.

---

## Suggested Repository Structure

```text
Linux-df-Command-Projects/
│
├── README.md
├── disk_report.sh
├── check_disk.sh
├── home_usage.sh
├── largest_filesystems.sh
├── fs_type_report.sh
├── check_inode.sh
├── real_disk_usage.sh
├── find_fs.sh
├── root_health.sh
└── disk_logger.sh
```

## Real-World Applications

These projects demonstrate tasks relevant to Linux System Administrator, DevOps, IT Infrastructure, and Technical Support roles.

- Monitor production server disk capacity.
- Detect filesystems approaching full utilization.
- Troubleshoot inode exhaustion.
- Generate filesystem reports.
- Identify mount points and filesystem types.
- Automate disk usage monitoring and logging.

## RHCSA Skills Practiced

- Managing and inspecting Linux filesystems.
- Monitoring disk space and inode utilization.
- Working with shell commands and pipelines.
- Writing Bash scripts for administrative tasks.
- Using conditional statements and AWK.
- Automating routine system checks.

## Learning Outcomes

Through these projects, I developed practical experience with Linux disk space monitoring, filesystem analysis, Bash scripting, disk usage alerts, and automated system administration reporting.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Focus:** Linux System Administration | RHCSA | Cybersecurity | IAM | DevOps
