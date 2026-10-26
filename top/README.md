# Linux `top` Command – Real-Time Process Monitoring Projects

## Project Overview

This repository demonstrates practical Linux system administration projects using the `top` command to monitor system performance, CPU utilization, memory consumption, and running processes in real time.

These projects focus on Linux performance monitoring, Bash scripting, process management, and system troubleshooting.

**Project Focus:** Linux System Administration | RHCSA | Bash Scripting | Performance Monitoring

---

## Technologies Used

- Linux (RHEL, Ubuntu, CentOS)
- Bash Shell Scripting
- Linux Command-Line Interface (CLI)
- `top` Command
- CPU and Memory Monitoring
- Process Management
- System Performance Troubleshooting

## Common Linux `top` Commands

| Command | Description |
|---|---|
| `top` | Start real-time process monitoring |
| `top -u username` | Monitor processes belonging to a user |
| `top -p 1234` | Monitor a process using its PID |
| `top -d 5` | Refresh every 5 seconds |
| `top -n 1` | Run one iteration and exit |
| `top -b -n 1` | Generate a noninteractive snapshot |
| `top -o %CPU` | Sort processes by CPU usage |
| `top -o %MEM` | Sort processes by memory usage |
| `top -c` | Display full command lines |
| `top -H -p 1234` | Monitor threads belonging to a process |

---

# Project 1: Linux System Resource Monitoring

## Objective

Create a Bash script that captures system performance information and saves the results to a log file for troubleshooting.

### Script: `system_monitor.sh`

```bash
#!/bin/bash

LOGFILE="top_snapshot.txt"

echo "===== Linux System Monitoring =====" > "$LOGFILE"
echo "Date: $(date)" >> "$LOGFILE"
echo "" >> "$LOGFILE"

top -b -n 1 >> "$LOGFILE"

echo "System monitoring report saved to $LOGFILE"
```

### Execute the Script

```bash
chmod +x system_monitor.sh
./system_monitor.sh
```

### View the Results

```bash
cat top_snapshot.txt
```

### Skills Demonstrated

- System resource monitoring
- CPU utilization analysis
- Memory usage monitoring
- Bash scripting
- Generating system performance reports

---

# Project 2: Monitor Processes for a Specific User

## Objective

Develop a Bash script that displays CPU and memory usage for processes owned by a specific Linux user.

### Script: `user_top.sh`

```bash
#!/bin/bash

if [ -z "$1" ]; then
    echo "Usage: $0 <username>"
    exit 1
fi

USER_NAME="$1"

if ! id "$USER_NAME" >/dev/null 2>&1; then
    echo "Error: User does not exist."
    exit 1
fi

echo "===== Monitoring Processes for $USER_NAME ====="

top -b -n 1 -u "$USER_NAME" | head -20
```

### Execute the Script

```bash
chmod +x user_top.sh
./user_top.sh root
```

### Skills Demonstrated

- User-based process monitoring
- Linux account management
- CPU and memory troubleshooting
- Bash scripting and input validation

---

# Project 3: Identify High-Memory Processes

## Objective

Create a Bash script that identifies Linux processes exceeding a specified memory utilization threshold.

### Script: `high_memory.sh`

```bash
#!/bin/bash

THRESHOLD=10

echo "===== High Memory Usage Report ====="
echo "Threshold: ${THRESHOLD}%"
echo ""

top -b -n 1 -w 512 |
awk -v threshold="$THRESHOLD" '
/^[[:space:]]*PID[[:space:]]+USER/ {
    for (i = 1; i <= NF; i++) {
        if ($i == "%MEM") mem_col = i
    }
    next
}
mem_col && $1 ~ /^[0-9]+$/ {
    if ($(mem_col) > threshold) {
        print "PID:", $1, "| Memory:", $(mem_col) "%", "| Command:", $NF
    }
}'
```

### Execute the Script

```bash
chmod +x high_memory.sh
./high_memory.sh
```

### Skills Demonstrated

- Memory consumption analysis
- Process troubleshooting
- Bash and AWK scripting
- Performance threshold monitoring
- Linux resource management

**Note:** The script uses the `%MEM` column reported by Linux `top`. Output formatting may vary across Linux distributions and versions.

---

## Interactive `top` Keyboard Shortcuts

While `top` is running, use these keys:

| Key | Action |
|---|---|
| `P` | Sort by CPU usage |
| `M` | Sort by memory usage |
| `k` | Send a signal to a process |
| `r` | Change process priority |
| `u` | Filter by user |
| `1` | Display individual CPU statistics |
| `c` | Toggle full command line |
| `q` | Quit `top` |
| `h` | Display help |

---

## Real-World Applications

These projects simulate tasks performed by Linux administrators and infrastructure engineers:

1. **Performance Monitoring:** Analyze CPU utilization and memory consumption.
2. **Troubleshooting:** Identify resource-intensive processes affecting server performance.
3. **User Monitoring:** Investigate processes running under specific Linux accounts.
4. **System Reporting:** Generate performance snapshots for administrative review.
5. **Automation:** Use Bash scripts to collect and analyze system information.

## Learning Outcomes

Through these projects, I practiced:

- Monitoring Linux processes in real time.
- Investigating CPU and memory utilization.
- Using Bash scripts to automate monitoring tasks.
- Filtering processes by Linux user.
- Identifying resource-intensive applications.
- Troubleshooting system performance issues.

## RHCSA Relevance

These projects support practical Linux administration skills involving process management, resource monitoring, command-line troubleshooting, and shell scripting.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Areas of Interest:** Linux System Administration | Cybersecurity | IAM | DevOps | IT Infrastructure
