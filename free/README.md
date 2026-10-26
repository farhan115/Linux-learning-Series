# Linux `free` Command – 10 Hands-On Memory Monitoring Projects

## Project Overview

This repository contains 10 hands-on Linux system administration projects using the `free` command to monitor RAM, swap memory, available memory, and system performance.

These projects demonstrate practical Linux memory management, Bash scripting, automated monitoring, resource analysis, and system troubleshooting.

**Focus:** Linux System Administration | RHCSA | Bash Scripting | Memory Monitoring | Performance Troubleshooting

## Technologies Used

- Linux (RHEL, Rocky Linux, Ubuntu)
- Bash Shell Scripting
- `free`, `awk`, `grep`, `date`, `sleep`
- Linux Memory Management
- RAM and Swap Monitoring
- System Performance Analysis

---

## Common Linux `free` Commands

| Command | Description |
|---|---|
| `free` | Display memory and swap usage |
| `free -h` | Show human-readable memory sizes |
| `free -m` | Display memory in MiB |
| `free -g` | Display memory in GiB |
| `free -t` | Show combined RAM and swap totals |
| `free -s 2` | Refresh memory statistics every 2 seconds |
| `free -c 5` | Display five memory snapshots |
| `free -w` | Show buffers and cache separately |
| `free -l` | Display low and high memory statistics |
| `free -b` | Display memory in bytes |

## Example: Display Memory Usage

```bash
free -h
```

Example output:

```text
               total       used       free     shared  buff/cache   available
Mem:            15Gi      5.1Gi      7.2Gi      512Mi      2.7Gi       9.1Gi
Swap:          4.0Gi          0B      4.0Gi
```

**Important:** The `available` column estimates memory that can be used by new applications without swapping. It is generally more useful than the `free` column for assessing memory pressure.

---

## Project 1: Memory Usage Report

**Objective:** Generate a system memory report and save it to a text file.

**Script:** `memory_report.sh`

```bash
#!/bin/bash

REPORT="memory_report.txt"

{
    echo "===== Linux Memory Usage Report ====="
    echo "Date: $(date)"
    echo ""
    free -h
} > "$REPORT"

echo "Report saved to $REPORT"
```

**Run:**

```bash
chmod +x memory_report.sh
./memory_report.sh
cat memory_report.txt
```

**Skills:** Memory reporting, Bash scripting, output redirection.

---

## Project 2: Real-Time Memory Monitoring

**Objective:** Monitor RAM and swap utilization every two seconds for five updates.

**Script:** `realtime_memory.sh`

```bash
#!/bin/bash

echo "===== Real-Time Memory Monitoring ====="

free -h -s 2 -c 5
```

**Run:**

```bash
chmod +x realtime_memory.sh
./realtime_memory.sh
```

**Skills:** Real-time system monitoring, performance analysis, memory observation.

---

## Project 3: Check Available Memory

**Objective:** Display the amount of RAM available for new applications.

**Script:** `available_memory.sh`

```bash
#!/bin/bash

echo "===== Available System Memory ====="

free -h | awk '
/^Mem:/ {
    print "Total RAM:", $2
    print "Used RAM:", $3
    print "Available RAM:", $NF
}'
```

**Run:**

```bash
chmod +x available_memory.sh
./available_memory.sh
```

**Skills:** RAM analysis, AWK filtering, system resource monitoring.

---

## Project 4: Low Available Memory Alert

**Objective:** Generate a warning when available memory falls below 2 GiB.

**Script:** `memory_alert.sh`

```bash
#!/bin/bash

THRESHOLD_MIB=2048

AVAILABLE=$(free -m | awk '/^Mem:/ {print $NF}')

echo "Available Memory: ${AVAILABLE} MiB"

if [ "$AVAILABLE" -lt "$THRESHOLD_MIB" ]; then
    echo "WARNING: Available memory is below 2 GiB!"
else
    echo "STATUS: Available memory is sufficient."
fi
```

**Run:**

```bash
chmod +x memory_alert.sh
./memory_alert.sh
```

**Skills:** Threshold alerts, conditional statements, Bash automation.

---

## Project 5: Display Memory in MiB and GiB

**Objective:** Compare system memory information using different units.

**Script:** `memory_units.sh`

```bash
#!/bin/bash

echo "===== Memory Usage in MiB ====="
free -m

echo ""
echo "===== Memory Usage in GiB ====="
free -g

echo ""
echo "===== Human-Readable Memory ====="
free -h
```

**Run:**

```bash
chmod +x memory_units.sh
./memory_units.sh
```

**Skills:** Memory unit conversion, Linux command options, system reporting.

---

## Project 6: RAM and Swap Summary

**Objective:** Generate a summary of physical memory and swap utilization.

**Script:** `memory_swap_summary.sh`

```bash
#!/bin/bash

echo "===== RAM and Swap Summary ====="

free -t -h

echo ""
echo "===== Detailed Memory Statistics ====="

free -w -h
```

**Run:**

```bash
chmod +x memory_swap_summary.sh
./memory_swap_summary.sh
```

**Skills:** Swap monitoring, memory statistics, Linux resource analysis.

---

## Project 7: Continuous Memory Logging

**Objective:** Collect memory usage snapshots every five seconds and save them to a log file.

**Script:** `memory_logger.sh`

```bash
#!/bin/bash

LOGFILE="$HOME/memory_log.txt"

echo "Memory logging started."
echo "Press Ctrl+C to stop."

while true; do
    {
        echo "===== $(date) ====="
        free -h
        echo ""
    } >> "$LOGFILE"

    sleep 5
done
```

**Run:**

```bash
chmod +x memory_logger.sh
./memory_logger.sh
```

**View the log:**

```bash
tail -20 ~/memory_log.txt
```

**Skills:** Continuous monitoring, Bash loops, logging, troubleshooting.

---

## Project 8: Memory Usage Trend Analysis

**Objective:** Record timestamped RAM usage measurements in a CSV file for trend analysis.

**Script:** `memory_trend.sh`

```bash
#!/bin/bash

LOGFILE="$HOME/memory_trend.csv"

if [ ! -f "$LOGFILE" ]; then
    echo "timestamp,total_mib,used_mib,available_mib" > "$LOGFILE"
fi

for i in {1..5}; do

    TIMESTAMP=$(date '+%Y-%m-%d %H:%M:%S')

    free -m | awk -v timestamp="$TIMESTAMP" '
    /^Mem:/ {
        printf "%s,%s,%s,%s\n",
        timestamp, $2, $3, $NF
    }' >> "$LOGFILE"

    sleep 2
done

echo "Memory trend saved to $LOGFILE"
```

**Run:**

```bash
chmod +x memory_trend.sh
./memory_trend.sh
cat ~/memory_trend.csv
```

**Skills:** CSV reporting, time-series data collection, memory trend analysis.

---

## Project 9: Identify Top Memory-Consuming Processes

**Objective:** Combine `free` and `ps` to identify applications consuming the most memory.

**Script:** `top_memory_processes.sh`

```bash
#!/bin/bash

echo "===== Current Memory Status ====="
free -h

echo ""
echo "===== Top 10 Memory-Consuming Processes ====="

ps aux --sort=-%mem | head -11
```

**Run:**

```bash
chmod +x top_memory_processes.sh
./top_memory_processes.sh
```

**Skills:** Process monitoring, RAM troubleshooting, performance investigation.

---

## Project 10: Automated Memory Health Dashboard

**Objective:** Create a terminal-based memory dashboard showing total RAM, used RAM, available RAM, memory utilization percentage, and swap usage.

**Script:** `memory_dashboard.sh`

```bash
#!/bin/bash

echo "=================================="
echo "     LINUX MEMORY DASHBOARD"
echo "=================================="

free -m | awk '
/^Mem:/ {
    total=$2
    used=$3
    available=$NF

    if (total > 0) {
        usage=(total-available)/total*100
    } else {
        usage=0
    }

    printf "Total RAM:       %d MiB\n", total
    printf "Used RAM:        %d MiB\n", used
    printf "Available RAM:   %d MiB\n", available
    printf "RAM Pressure Estimate: %.1f%%\n", usage
}

/^Swap:/ {
    printf "Total Swap:      %d MiB\n", $2
    printf "Used Swap:       %d MiB\n", $3
}'
```

**Run:**

```bash
chmod +x memory_dashboard.sh
./memory_dashboard.sh
```

The RAM pressure estimate measures the fraction of RAM not currently estimated as available. It is not a direct measure of application memory usage or kernel memory pressure.

**Skills:** System dashboards, AWK calculations, RAM and swap analysis, Bash scripting.

---

## GitHub Repository Structure

```text
Linux-free-Command-Projects/
│
├── README.md
├── memory_report.sh
├── realtime_memory.sh
├── available_memory.sh
├── memory_alert.sh
├── memory_units.sh
├── memory_swap_summary.sh
├── memory_logger.sh
├── memory_trend.sh
├── top_memory_processes.sh
├── memory_dashboard.sh
│
└── screenshots/
    ├── project-01.png
    ├── project-02.png
    ├── project-03.png
    ├── project-04.png
    ├── project-05.png
    ├── project-06.png
    ├── project-07.png
    ├── project-08.png
    ├── project-09.png
    └── project-10.png
```

## Real-World Applications

These projects simulate common Linux system administration and IT infrastructure tasks:

1. Monitoring Linux server RAM utilization.
2. Detecting low available memory.
3. Investigating high memory consumption.
4. Monitoring swap utilization.
5. Generating automated memory reports.
6. Collecting memory performance logs.
7. Analyzing resource utilization trends.
8. Troubleshooting memory-related performance issues.
9. Identifying memory-intensive applications.
10. Building command-line monitoring dashboards.

## RHCSA Skills Practiced

- Linux process and memory monitoring
- Shell scripting and automation
- Command-line pipelines
- AWK text processing
- Conditional statements and loops
- System resource troubleshooting
- Linux administration reporting

## Learning Outcomes

Through these projects, I practiced monitoring Linux memory resources, interpreting RAM and swap statistics, developing Bash scripts, creating threshold-based alerts, and generating performance reports.

These skills support practical Linux system administration, infrastructure operations, and RHCSA preparation.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Focus:** Linux System Administration | RHCSA | Cybersecurity | IAM | DevOps
