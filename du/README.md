# Linux `du` Command – 10 Hands-On Disk Usage Projects

## Project Overview

This repository contains 10 practical Linux system administration projects using the `du` (Disk Usage) command.

The projects demonstrate how to analyze file and directory sizes, identify storage-intensive directories, monitor disk usage growth, generate reports, and troubleshoot storage problems using Bash scripting.

**Project Focus:** Linux System Administration | RHCSA | Bash Scripting | Disk Usage Analysis | Storage Troubleshooting

## Technologies Used

- Linux (RHEL, Rocky Linux, Ubuntu)
- Bash Shell Scripting
- `du`, `sort`, `awk`, `find`, `head`
- Linux Filesystem Management
- Disk Usage Monitoring
- Command-Line Interface (CLI)

---

## Common Linux `du` Commands

| Command | Description |
|---|---|
| `du` | Display disk usage for directories |
| `du -h` | Display human-readable sizes |
| `du -s` | Display only the total size |
| `du -sh /home` | Display total disk usage of `/home` |
| `du -a` | Include files and directories |
| `du -h --max-depth=1` | Display usage up to one directory level |
| `du -c` | Display a grand total |
| `du --exclude="*.log"` | Exclude matching files |
| `du -x` | Stay within one filesystem |
| `du -h \| sort -h` | Sort disk usage from smallest to largest |

## Example: Check Directory Size

```bash
du -sh /home
```

Example output:

```text
6.4G    /home
```

---

## Project 1: Directory Size Report

**Objective:** Generate a report showing disk usage for directories in the current location.

**Script:** `dir_report.sh`

```bash
#!/bin/bash

REPORT="directory_report.txt"

echo "===== Directory Size Report =====" > "$REPORT"
echo "Date: $(date)" >> "$REPORT"
echo "" >> "$REPORT"

du -h --max-depth=1 . | sort -h >> "$REPORT"

echo "Report saved to $REPORT"
```

**Run:**

```bash
chmod +x dir_report.sh
./dir_report.sh
cat directory_report.txt
```

**Skills:** Disk usage reporting, Bash scripting, output redirection.

---

## Project 2: Find the 10 Largest Directories

**Objective:** Identify the largest directories inside a specified location.

**Script:** `largest_dirs.sh`

```bash
#!/bin/bash

DIR="${1:-.}"

if [ ! -d "$DIR" ]; then
    echo "Directory does not exist."
    exit 1
fi

echo "===== Top 10 Largest Directories ====="

du -h --max-depth=1 "$DIR" |
sort -hr |
head -10
```

**Run:**

```bash
chmod +x largest_dirs.sh
./largest_dirs.sh /home
```

**Skills:** Directory analysis, sorting, storage troubleshooting.

---

## Project 3: Check a Specific Directory Size

**Objective:** Calculate disk usage for a directory specified by the user.

**Script:** `dir_size.sh`

```bash
#!/bin/bash

DIR="${1:-/home}"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

echo "===== Directory Size ====="

du -sh "$DIR"
```

**Run:**

```bash
chmod +x dir_size.sh
./dir_size.sh /var
```

**Skills:** Directory management, Bash variables, storage monitoring.

---

## Project 4: Find the 10 Largest Files

**Objective:** Identify the largest regular files in a directory.

**Script:** `large_files.sh`

```bash
#!/bin/bash

DIR="${1:-.}"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

echo "===== Top 10 Largest Files ====="

find "$DIR" -type f -printf '%s\t%p\n' 2>/dev/null |
sort -nr |
head -10 |
numfmt --field=1 --to=iec --suffix=B
```

**Run:**

```bash
chmod +x large_files.sh
./large_files.sh /home
```

**Skills:** File size analysis, Linux `find`, sorting, storage troubleshooting.

---

## Project 5: Exclude Specific File Types

**Objective:** Calculate directory disk usage while excluding `.log` and `.tmp` files.

**Script:** `exclude_size.sh`

```bash
#!/bin/bash

DIR="${1:-.}"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

echo "===== Disk Usage Excluding Log and Temp Files ====="

du -sh \
    --exclude="*.log" \
    --exclude="*.tmp" \
    "$DIR"
```

**Run:**

```bash
chmod +x exclude_size.sh
./exclude_size.sh /var
```

**Skills:** File filtering, storage analysis, Linux command options.

---

## Project 6: Disk Usage by User

**Objective:** Display the disk usage of home directories under `/home`.

**Script:** `user_usage.sh`

```bash
#!/bin/bash

echo "===== Home Directory Disk Usage ====="

for dir in /home/*; do
    if [ -d "$dir" ]; then
        du -sh "$dir" 2>/dev/null
    fi
done | sort -hr
```

**Run:**

```bash
chmod +x user_usage.sh
./user_usage.sh
```

**Skills:** User directory monitoring, Bash loops, disk usage reporting.

**Note:** Home directory usage is not the same as total disk usage owned by a user. Some user files may be stored outside `/home`.

---

## Project 7: Directory Tree Size Analysis

**Objective:** Display disk usage for directories up to two levels deep.

**Script:** `tree_size.sh`

```bash
#!/bin/bash

DIR="${1:-.}"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

echo "===== Directory Tree Size ====="

du -h --max-depth=2 "$DIR" |
sort -hr
```

**Run:**

```bash
chmod +x tree_size.sh
./tree_size.sh /home
```

**Skills:** Directory structure analysis, filesystem investigation, Linux administration.

---

## Project 8: Monitor Directory Growth

**Objective:** Compare a directory's current disk usage against a previously recorded measurement.

**Script:** `growth_monitor.sh`

```bash
#!/bin/bash

DIR="${1:-/var}"
LOGFILE="$HOME/du_growth.log"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

CURRENT=$(du -sB1 "$DIR" | awk '{print $1}')

PREVIOUS=$(awk -F '\t' -v dir="$DIR" '
    $2 == dir {value=$3}
    END {print value}
' "$LOGFILE" 2>/dev/null)

echo "Directory: $DIR"
echo "Current usage: $CURRENT bytes"

if [[ "$PREVIOUS" =~ ^[0-9]+$ ]]; then
    GROWTH=$((CURRENT - PREVIOUS))
    echo "Change since last measurement: $GROWTH bytes"
else
    echo "First measurement recorded."
fi

printf '%s\t%s\t%s\n' \
    "$(date '+%Y-%m-%d_%H:%M:%S')" \
    "$DIR" "$CURRENT" >> "$LOGFILE"

echo "Measurement saved to $LOGFILE"
```

**Run:**

```bash
chmod +x growth_monitor.sh
./growth_monitor.sh /var
```

Run it again later to compare measurements.

**Skills:** Storage growth analysis, Bash arithmetic, logging, capacity planning.

---

## Project 9: Directory Usage Summary with Grand Total

**Objective:** Generate a directory usage report that includes a grand total.

**Script:** `summary_size.sh`

```bash
#!/bin/bash

DIR="${1:-.}"

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

echo "===== Directory Usage Summary ====="

du -ch --max-depth=1 "$DIR"
```

**Run:**

```bash
chmod +x summary_size.sh
./summary_size.sh /home
```

**Skills:** Storage reporting, directory usage summaries, capacity analysis.

---

## Project 10: Identify Directories Exceeding a Storage Threshold

**Objective:** Identify directories using more than 1 GiB of disk space to help administrators investigate storage issues.

**Script:** `find_large_dirs.sh`

```bash
#!/bin/bash

DIR="${1:-.}"
THRESHOLD_GIB=1
THRESHOLD_BYTES=$((THRESHOLD_GIB * 1024 * 1024 * 1024))

if [ ! -d "$DIR" ]; then
    echo "Error: Directory not found."
    exit 1
fi

echo "===== Directories Exceeding ${THRESHOLD_GIB} GiB ====="

du -B1 --max-depth=1 "$DIR" 2>/dev/null |
awk -v threshold="$THRESHOLD_BYTES" '
    $1 > threshold {
        print $0
    }
' | sort -nr
```

**Run:**

```bash
chmod +x find_large_dirs.sh
./find_large_dirs.sh /home
```

**Skills:** Storage threshold monitoring, Bash scripting, capacity troubleshooting.

**Safety:** This project identifies large directories only. It does not delete files or perform automatic cleanup.

---

## Suggested GitHub Repository Structure

```text
Linux-du-Command-Projects/
│
├── README.md
├── dir_report.sh
├── largest_dirs.sh
├── dir_size.sh
├── large_files.sh
├── exclude_size.sh
├── user_usage.sh
├── tree_size.sh
├── growth_monitor.sh
├── summary_size.sh
└── find_large_dirs.sh
```

## Real-World Applications

These projects demonstrate tasks relevant to Linux System Administrators, DevOps Engineers, IT Support Specialists, and Infrastructure Engineers.

1. Investigating disk space consumption on Linux servers.
2. Identifying large directories and files.
3. Monitoring user home directory usage.
4. Tracking directory growth over time.
5. Generating automated storage reports.
6. Identifying potential storage capacity issues.
7. Supporting filesystem troubleshooting and capacity planning.

## RHCSA Skills Practiced

- Linux filesystem navigation and analysis
- Disk usage monitoring
- Bash shell scripting
- Command pipelines and output redirection
- AWK and sorting operations
- File and directory management
- System troubleshooting

## Learning Outcomes

Through these projects, I practiced Linux disk usage analysis, Bash scripting, storage reporting, directory monitoring, and filesystem troubleshooting.

The projects demonstrate practical command-line techniques used in Linux system administration environments.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Focus:** Linux System Administration | RHCSA | Cybersecurity | IAM | DevOps
