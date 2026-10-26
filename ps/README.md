# Linux `ps` Command – Process Monitoring Projects

## Overview

This repository demonstrates how to use the Linux `ps` (Process Status) command to monitor running processes, analyze CPU and memory utilization, identify processes by PID, and troubleshoot system performance.

These hands-on projects are designed to strengthen practical Linux System Administration, RHCSA, and troubleshooting skills.

## Technologies Used

- Linux (RHEL, Ubuntu, CentOS)
- Bash Shell Scripting
- Linux Process Management
- CPU and Memory Monitoring
- System Administration
- Command-Line Interface (CLI)

## Common Linux `ps` Commands

| Command | Description |
|---|---|
| `ps` | Display processes in the current terminal |
| `ps -e` | List all running processes |
| `ps -ef` | Display detailed process information |
| `ps aux` | Display processes with CPU and memory usage |
| `ps -u username` | Show processes belonging to a user |
| `ps -p 1234` | Find a process by PID |
| `ps aux --sort=-%cpu` | Sort by highest CPU usage |
| `ps aux --sort=-%mem` | Sort by highest memory usage |
| `ps -ef \| grep sshd` | Search for SSH processes |

---

## Project 1: System Process Monitoring Script

**Objective:** Create a Bash script to identify the top five CPU-consuming and memory-consuming processes.

### Script: `process_monitor.sh`

```bash
#!/bin/bash

echo "===== Top 5 CPU Consuming Processes ====="
ps aux --sort=-%cpu | head -6

echo ""
echo "===== Top 5 Memory Consuming Processes ====="
ps aux --sort=-%mem | head -6
```

### Run the Script

```bash
chmod +x process_monitor.sh
./process_monitor.sh
```

### Skills Demonstrated

- Monitoring CPU utilization
- Analyzing memory consumption
- Sorting Linux processes
- Bash scripting and troubleshooting

---

## Project 2: User Process Report

**Objective:** Generate a report showing processes owned by a specific Linux user and save the results to a text file.

### Script: `user_process_report.sh`

```bash
#!/bin/bash

if [ -z "$1" ]; then
    echo "Usage: $0 <username>"
    exit 1
fi

USER_NAME="$1"

if ! id "$USER_NAME" >/dev/null 2>&1; then
    echo "User does not exist."
    exit 1
fi

echo "Process Report for: $USER_NAME"

ps -u "$USER_NAME" \
    -o pid,ppid,%cpu,%mem,cmd \
    > "${USER_NAME}_processes.txt"

echo "Report saved successfully."
```

### Run the Script

```bash
chmod +x user_process_report.sh
./user_process_report.sh root
```

### Skills Demonstrated

- Linux user process management
- Process ownership identification
- Generating system reports
- Bash scripting and output redirection

---

## Project 3: Identify High-CPU Processes

**Objective:** Detect processes exceeding a defined CPU usage threshold and allow the administrator to terminate a selected process after confirmation.

### Script: `high_cpu_monitor.sh`

```bash
#!/bin/bash

THRESHOLD=50

echo "Processes exceeding ${THRESHOLD}% CPU:"

ps -eo pid,pcpu,comm --no-headers |
awk -v threshold="$THRESHOLD" \
'$2 > threshold {print}'

read -r -p "Enter PID to terminate (or press Enter to exit): " pid

if [ -z "$pid" ]; then
    echo "No process selected."
    exit 0
fi

if ! [[ "$pid" =~ ^[0-9]+$ ]] || [ "$pid" -le 1 ]; then
    echo "Invalid or protected PID."
    exit 1
fi

ps -p "$pid" -o pid,user,comm || exit 1

read -r -p "Terminate this process? (yes/no): " confirm

if [ "$confirm" = "yes" ]; then
    kill -TERM "$pid"
    echo "Termination signal sent to PID $pid."
else
    echo "Operation cancelled."
fi
```

### Run the Script

```bash
chmod +x high_cpu_monitor.sh
./high_cpu_monitor.sh
```

**Safety:** Use this script only in an authorized lab environment. Review the selected PID before termination. The script sends SIGTERM, which requests graceful termination but does not guarantee the process exits.

### Skills Demonstrated

- CPU performance troubleshooting
- Process identification using PID
- Process signal management
- Bash conditional statements
- Linux administration

---

## Additional Practice Commands

### Find SSH Processes

```bash
ps -ef | grep '[s]shd'
```

### Find Processes Owned by Root

```bash
ps -u root
```

### Display a Process by PID

```bash
ps -p 1234 -f
```

### Monitor the Top CPU-Consuming Processes

```bash
watch -n 2 'ps aux --sort=-%cpu | head -10'
```

## Real-World Applications

These projects demonstrate Linux administration tasks used in:

- Linux System Administrator roles
- IT Support and Infrastructure Operations
- DevOps Engineering
- Security Operations Centers (SOC)
- Server Performance Troubleshooting

## Learning Outcomes

By completing these projects, I practiced Linux process monitoring, CPU and memory analysis, process ownership management, Bash scripting, and system troubleshooting.

The projects demonstrate practical command-line skills applicable to enterprise Linux environments and RHCSA preparation.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Project Focus:** Linux System Administration | Bash Scripting | RHCSA | IT Infrastructure
