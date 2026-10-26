# Linux `uptime` Command – 10 Hands-On System Monitoring Projects

## Project Overview

This repository contains 10 hands-on Linux system administration projects using the `uptime` command and Bash shell scripting.

These projects demonstrate how to monitor server uptime, analyze system load averages, detect system restarts, automate uptime logging, and generate Linux server performance reports.

**Project Focus:** Linux System Administration | RHCSA | Bash Scripting | Server Monitoring | Performance Troubleshooting

## Technologies Used

- Linux (RHEL, Rocky Linux, Ubuntu)
- Bash Shell Scripting
- `uptime`, `awk`, `date`, `hostname`, `nproc`
- `free`, `df`, `ps`, `who`
- Linux Process and Resource Monitoring
- Cron Job Automation
- System Performance Analysis

---

## Common Linux `uptime` Commands

| Command | Description |
|---|---|
| `uptime` | Display uptime, logged-in user count, and load averages |
| `uptime -p` | Display uptime in readable format |
| `uptime -s` | Display system boot time |
| `uptime -h` | Display help |
| `cat /proc/uptime` | Display uptime in seconds and accumulated CPU idle time |
| `watch -n 5 uptime` | Refresh uptime every 5 seconds |
| `uptime \| awk '{print $3}'` | Extract a field, although output format varies |
| `who -b` | Display last system boot time |
| `w` | Display logged-in users and system load |
| `nproc` | Display available processing units |

## Example: Display System Uptime

```bash
uptime
```

Example output:

```text
08:15:30 up 5 days, 3:20, 2 users, load average: 0.45, 0.60, 0.55
```

**Understanding the output:**

- **08:15:30:** Current system time
- **5 days, 3:20:** System uptime
- **2 users:** Number of logged-in user sessions
- **0.45:** Average system load over 1 minute
- **0.60:** Average system load over 5 minutes
- **0.55:** Average system load over 15 minutes

Linux load averages represent average runnable or uninterruptible tasks, not CPU utilization percentages.

---

# Project 1: System Uptime Report

**Objective:** Generate a system report containing hostname, uptime, boot time, and load averages.

**Script:** `uptime_report.sh`

```bash
#!/bin/bash

echo "===== Linux System Uptime Report ====="
echo "Hostname: $(hostname)"
echo "Date: $(date)"
echo "Uptime: $(uptime -p)"
echo "Boot Time: $(uptime -s)"
echo ""
echo "System Load:"
uptime
```

**Run:**

```bash
chmod +x uptime_report.sh
./uptime_report.sh
```

**Skills:** System information collection, Bash scripting, uptime monitoring.

---

# Project 2: Uptime Monitoring Log

**Objective:** Record system uptime information periodically for monitoring and troubleshooting.

**Script:** `uptime_log.sh`

```bash
#!/bin/bash

LOGFILE="$HOME/uptime.log"

echo "===== Uptime Monitoring =====" >> "$LOGFILE"
echo "Date: $(date)" >> "$LOGFILE"
uptime >> "$LOGFILE"
echo "" >> "$LOGFILE"

echo "Uptime information saved to $LOGFILE"
```

**Run:**

```bash
chmod +x uptime_log.sh
./uptime_log.sh
cat ~/uptime.log
```

**Skills:** Logging, output redirection, system monitoring.

---

# Project 3: System Load Average Alert

**Objective:** Generate a warning when the 1-minute load average exceeds a configured threshold.

**Script:** `load_alert.sh`

```bash
#!/bin/bash

THRESHOLD=2.0

LOAD=$(awk '{print $1}' /proc/loadavg)

echo "Current 1-minute load average: $LOAD"

awk -v load="$LOAD" -v threshold="$THRESHOLD" '
BEGIN {
    if (load > threshold) {
        print "WARNING: System load is high!"
        exit 1
    } else {
        print "STATUS: System load is normal."
    }
}'
```

**Run:**

```bash
chmod +x load_alert.sh
./load_alert.sh
```

**Skills:** Load monitoring, AWK, threshold alerts, Bash automation.

**Note:** A threshold of 2.0 is an example. Appropriate thresholds depend on CPU capacity, workload, and whether tasks are waiting on I/O.

---

# Project 4: System Boot Time Tracker

**Objective:** Record the system's latest startup time.

**Script:** `boot_time.sh`

```bash
#!/bin/bash

LOGFILE="$HOME/boot_time.log"

echo "===== System Boot Time ====="
echo "Hostname: $(hostname)"
echo "Boot Time: $(uptime -s)"

{
    echo "Date Checked: $(date)"
    echo "Boot Time: $(uptime -s)"
    echo ""
} >> "$LOGFILE"

echo "Boot information saved to $LOGFILE"
```

**Run:**

```bash
chmod +x boot_time.sh
./boot_time.sh
```

**Skills:** Boot-time analysis, Linux reporting, system administration.

---

# Project 5: Daily Uptime Report

**Objective:** Create a date-stamped system uptime report.

**Script:** `daily_uptime.sh`

```bash
#!/bin/bash

REPORT="$HOME/daily_uptime_$(date +%F).txt"

{
    echo "===== Daily Uptime Report ====="
    echo "Date: $(date)"
    echo "Hostname: $(hostname)"
    echo ""
    echo "System Uptime:"
    uptime -p
    echo ""
    echo "Load Averages:"
    uptime
} > "$REPORT"

echo "Daily report saved to $REPORT"
```

**Run:**

```bash
chmod +x daily_uptime.sh
./daily_uptime.sh
```

**Skills:** Daily reporting, timestamped files, Bash scripting.

---

# Project 6: Linux System Health Dashboard

**Objective:** Combine uptime, RAM, and filesystem monitoring in one terminal dashboard.

**Script:** `system_dashboard.sh`

```bash
#!/bin/bash

echo "===================================="
echo "      LINUX SYSTEM DASHBOARD"
echo "===================================="

echo ""
echo "Hostname: $(hostname)"
echo "Date: $(date)"

echo ""
echo "===== System Uptime ====="
uptime

echo ""
echo "===== Memory Usage ====="
free -h

echo ""
echo "===== Disk Usage ====="
df -h

echo ""
echo "===== CPU Information ====="
echo "Available Processing Units: $(nproc)"
```

**Run:**

```bash
chmod +x system_dashboard.sh
./system_dashboard.sh
```

**Skills:** System health monitoring, Linux CLI, memory and disk analysis.

---

# Project 7: Detect Server Restarts

**Objective:** Identify whether a Linux system has restarted since the previous monitoring check.

**Script:** `restart_check.sh`

```bash
#!/bin/bash

STATEFILE="$HOME/.last_boot_id"

CURRENT_BOOT=$(cat /proc/sys/kernel/random/boot_id)

if [ -f "$STATEFILE" ]; then

    PREVIOUS_BOOT=$(cat "$STATEFILE")

    if [ "$CURRENT_BOOT" != "$PREVIOUS_BOOT" ]; then
        echo "WARNING: System restart detected!"
        echo "Current boot time: $(uptime -s)"
    else
        echo "STATUS: No restart detected."
    fi

else
    echo "First monitoring run. Boot ID recorded."
fi

echo "$CURRENT_BOOT" > "$STATEFILE"
```

**Run:**

```bash
chmod +x restart_check.sh
./restart_check.sh
```

**Skills:** Reboot detection, system state tracking, Bash conditionals.

**Note:** This script compares Linux boot identifiers. It detects a reboot between executions but does not determine why the reboot occurred.

---

# Project 8: CPU Load Analysis

**Objective:** Compare Linux load averages with the number of available processing units.

**Script:** `load_analysis.sh`

```bash
#!/bin/bash

CORES=$(nproc)

read -r LOAD1 LOAD5 LOAD15 _ < /proc/loadavg

echo "===== CPU Load Analysis ====="
echo "Available Processing Units: $CORES"
echo "1-Minute Load: $LOAD1"
echo "5-Minute Load: $LOAD5"
echo "15-Minute Load: $LOAD15"

awk -v load="$LOAD1" -v cores="$CORES" '
BEGIN {
    ratio = load / cores

    printf "Load-to-CPU Ratio: %.2f\n", ratio

    if (ratio > 1) {
        print "WARNING: Load exceeds available CPU count."
    } else {
        print "STATUS: Load is within CPU count."
    }
}'
```

**Run:**

```bash
chmod +x load_analysis.sh
./load_analysis.sh
```

**Skills:** Load average interpretation, CPU capacity comparison, AWK calculations.

**Note:** A load-to-CPU ratio above 1 can indicate contention, but load averages also include tasks waiting in uninterruptible sleep, often related to I/O. This is not a direct CPU utilization measurement.

---

# Project 9: Automated Uptime Monitoring with Cron

**Objective:** Schedule automatic system uptime reports every hour.

**Script:** `cron_uptime.sh`

```bash
#!/bin/bash

LOGFILE="$HOME/uptime_cron.log"

{
    echo "===== $(date) ====="
    uptime
    echo ""
} >> "$LOGFILE"
```

**Run:**

```bash
chmod +x cron_uptime.sh
./cron_uptime.sh
```

Open your crontab:

```bash
crontab -e
```

Add the following entry, replacing the path with the actual location of your script:

```text
0 * * * * /home/youruser/Linux-uptime-Projects/cron_uptime.sh
```

This schedules the script to run every hour at minute zero.

**Skills:** Cron scheduling, automated monitoring, Linux administration.

---

# Project 10: Complete Linux Server Performance Report

**Objective:** Generate a comprehensive server performance report including uptime, CPU load, memory, disk usage, and processes.

**Script:** `performance_report.sh`

```bash
#!/bin/bash

REPORT="$HOME/performance_report_$(date +%F_%H%M%S).txt"

{
    echo "===================================="
    echo "    LINUX SERVER PERFORMANCE REPORT"
    echo "===================================="

    echo "Hostname: $(hostname)"
    echo "Date: $(date)"

    echo ""
    echo "===== SYSTEM UPTIME ====="
    uptime

    echo ""
    echo "===== BOOT TIME ====="
    uptime -s

    echo ""
    echo "===== CPU INFORMATION ====="
    echo "Available CPUs: $(nproc)"
    cat /proc/loadavg

    echo ""
    echo "===== MEMORY USAGE ====="
    free -h

    echo ""
    echo "===== DISK USAGE ====="
    df -h

    echo ""
    echo "===== TOP CPU PROCESSES ====="
    ps aux --sort=-%cpu | head -11

    echo ""
    echo "===== TOP MEMORY PROCESSES ====="
    ps aux --sort=-%mem | head -11

} > "$REPORT"

echo "Performance report saved to $REPORT"
```

**Run:**

```bash
chmod +x performance_report.sh
./performance_report.sh
```

**Skills:** Performance reporting, system resource analysis, Bash scripting, troubleshooting.

---

## GitHub Repository Structure

```text
Linux-uptime-Command-Projects/
│
├── README.md
├── uptime_report.sh
├── uptime_log.sh
├── load_alert.sh
├── boot_time.sh
├── daily_uptime.sh
├── system_dashboard.sh
├── restart_check.sh
├── load_analysis.sh
├── cron_uptime.sh
├── performance_report.sh
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

These projects demonstrate tasks relevant to Linux System Administrator, DevOps, IT Support, and Infrastructure Operations roles.

1. Monitoring Linux server uptime and availability.
2. Detecting unexpected system restarts.
3. Analyzing server load averages.
4. Generating daily system performance reports.
5. Automating server monitoring with cron.
6. Investigating system performance issues.
7. Monitoring CPU capacity and resource utilization.
8. Maintaining system uptime and performance logs.

## RHCSA Skills Practiced

- Linux system monitoring
- Bash shell scripting
- Command-line utilities
- System boot analysis
- Load average interpretation
- Cron job automation
- Performance troubleshooting
- System resource reporting

## Learning Outcomes

Through these projects, I practiced Linux system monitoring, Bash scripting, system uptime analysis, load average interpretation, reboot detection, and automated reporting.

These skills are applicable to Linux administration, infrastructure operations, and RHCSA preparation.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Focus:** Linux System Administration | RHCSA | Cybersecurity | IAM | DevOps
