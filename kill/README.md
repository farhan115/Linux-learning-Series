# Linux `kill` Command – 10 Hands-On Process Management Projects

## Project Overview

This repository contains 10 practical Linux system administration projects using the `kill` command and related process management utilities.

The projects demonstrate how to identify running processes, send Linux signals, gracefully terminate applications, pause and resume processes, troubleshoot unresponsive applications, and automate process management using Bash scripting.

**Project Focus:** Linux System Administration | RHCSA | Bash Scripting | Process Management | Troubleshooting

## Technologies Used

- Linux (RHEL, Rocky Linux, Ubuntu)
- Bash Shell Scripting
- `kill`, `ps`, `pgrep`, `pkill`, `sleep`, `wait`
- Linux Signals
- Process Identification (PID)
- System Monitoring and Troubleshooting

---

## Common Linux `kill` Commands

| Command | Description |
|---|---|
| `kill PID` | Send SIGTERM to a process |
| `kill -15 PID` | Request graceful termination |
| `kill -9 PID` | Force termination using SIGKILL |
| `kill -l` | List available signals |
| `kill -0 PID` | Check whether a process exists and is accessible |
| `kill -STOP PID` | Pause a running process |
| `kill -CONT PID` | Resume a stopped process |
| `kill -HUP PID` | Send a hangup signal |
| `kill -INT PID` | Send an interrupt signal |
| `kill -USR1 PID` | Send a user-defined signal |
| `pkill -x name` | Signal processes matching an exact name |
| `pgrep -a name` | Find matching processes and their command lines |

**Important:** `kill` sends a signal. SIGTERM requests termination, but a process may handle or ignore it. SIGKILL cannot be caught or ignored by the target process.

## Lab Safety

All projects should be practiced on processes you own in a Linux VM.

Start a safe test process:

```bash
sleep 300 &
PID=$!
echo "Test process PID: $PID"
```

Avoid terminating critical system processes, SSH sessions, databases, or production services. Do not use `sudo` unless your lab specifically requires it.

---

# Project 1: Terminate a Process by PID

**Objective:** Create a script to gracefully terminate a process using its PID.

**Script:** `kill_pid.sh`

```bash
#!/bin/bash

PID="$1"

if ! [[ "$PID" =~ ^[0-9]+$ ]] || (( PID <= 1 )); then
    echo "Usage: $0 <valid PID greater than 1>"
    exit 1
fi

echo "Process information:"
ps -p "$PID" -o pid,user,comm || exit 1

read -r -p "Send SIGTERM to PID $PID? (yes/no): " confirm

if [ "$confirm" = "yes" ]; then
    kill -TERM "$PID" &&
        echo "SIGTERM sent to PID $PID"
else
    echo "Operation cancelled."
fi
```

**Run:**

```bash
sleep 300 &
./kill_pid.sh $!
```

**Skills:** PID identification, signal handling, process termination, Bash input validation.

---

# Project 2: Terminate a Process by Name

**Objective:** Identify and gracefully terminate test processes using their exact process name.

**Script:** `kill_by_name.sh`

```bash
#!/bin/bash

NAME="$1"

if [ -z "$NAME" ]; then
    echo "Usage: $0 <process_name>"
    exit 1
fi

echo "Matching processes:"
pgrep -a -u "$(id -u)" -x "$NAME" || exit 1

read -r -p "Terminate matching processes? (yes/no): " answer

if [ "$answer" = "yes" ]; then
    pkill -TERM -u "$(id -u)" -x "$NAME"
    echo "SIGTERM sent to matching processes."
else
    echo "Cancelled."
fi
```

**Run in an isolated lab:**

```bash
sleep 300 &
./kill_by_name.sh sleep
```

**Skills:** Process name filtering, `pgrep`, `pkill`, user-scoped process management.

**Note:** This script can signal multiple processes owned by the current user. Check the list before confirming.

---

# Project 3: Force Terminate an Unresponsive Process

**Objective:** Practice sending SIGKILL to a disposable test process after attempting graceful termination.

**Script:** `force_kill.sh`

```bash
#!/bin/bash

PID="$1"

if ! [[ "$PID" =~ ^[0-9]+$ ]] || (( PID <= 1 )); then
    echo "Usage: $0 <valid PID>"
    exit 1
fi

ps -p "$PID" -o pid,user,comm || exit 1

read -r -p "Attempt graceful termination? (yes/no): " answer

if [ "$answer" != "yes" ]; then
    exit 0
fi

kill -TERM "$PID" || exit 1

sleep 2

if kill -0 "$PID" 2>/dev/null; then
    echo "Process still accessible."
    read -r -p "Force termination with SIGKILL? (yes/no): " confirm

    if [ "$confirm" = "yes" ]; then
        kill -KILL "$PID"
    fi
else
    echo "Process exited or is no longer accessible."
fi
```

**Run:**

```bash
sleep 300 &
./force_kill.sh $!
```

**Skills:** SIGTERM, SIGKILL, process troubleshooting, termination escalation.

**Safety:** SIGKILL does not allow normal application cleanup. Use only on disposable lab processes. A production-grade script must also protect against PID reuse.

---

# Project 4: Pause and Resume a Process

**Objective:** Use SIGSTOP and SIGCONT to suspend and resume a process.

**Script:** `pause_resume.sh`

```bash
#!/bin/bash

sleep 300 &
PID=$!

echo "Started test process: $PID"

kill -STOP "$PID"
echo "Process paused."

ps -p "$PID" -o pid,stat,comm

sleep 3

kill -CONT "$PID"
echo "Process resumed."

ps -p "$PID" -o pid,stat,comm

kill -TERM "$PID"
wait "$PID" 2>/dev/null
```

**Run:**

```bash
chmod +x pause_resume.sh
./pause_resume.sh
```

**Skills:** SIGSTOP, SIGCONT, process states, Linux job management.

---

# Project 5: List and Understand Linux Signals

**Objective:** Explore available Linux signals and their purposes.

**Script:** `list_signals.sh`

```bash
#!/bin/bash

echo "===== Available Linux Signals ====="
kill -l

echo ""
echo "===== Common Signals ====="

for signal in TERM KILL STOP CONT HUP INT USR1 USR2; do
    echo "$signal"
done
```

**Run:**

```bash
chmod +x list_signals.sh
./list_signals.sh
```

**Skills:** Linux signal identification, process control fundamentals, RHCSA preparation.

---

# Project 6: Identify High-CPU Processes

**Objective:** Find processes consuming significant CPU resources without automatically terminating them.

**Script:** `high_cpu_processes.sh`

```bash
#!/bin/bash

THRESHOLD=50

echo "===== Processes Above ${THRESHOLD}% CPU ====="

ps -eo pid,user,pcpu,comm --no-headers |
awk -v threshold="$THRESHOLD" '
    $3 > threshold {
        printf "PID: %s | USER: %s | CPU: %s%% | COMMAND: %s\n",
        $1, $2, $3, $4
    }
'
```

**Run:**

```bash
chmod +x high_cpu_processes.sh
./high_cpu_processes.sh
```

**Skills:** CPU monitoring, `ps`, `awk`, process troubleshooting.

**Note:** The CPU percentage reported by `ps` is not necessarily instantaneous. Investigate sustained CPU usage before deciding whether termination is appropriate.

---

# Project 7: Find Long-Running Processes

**Objective:** Identify processes running longer than one hour.

**Script:** `long_running_processes.sh`

```bash
#!/bin/bash

THRESHOLD=3600

echo "===== Processes Running Over One Hour ====="

ps -eo pid,user,etimes,comm --no-headers |
awk -v threshold="$THRESHOLD" '
    $3 > threshold {
        printf "PID: %s | USER: %s | SECONDS: %s | COMMAND: %s\n",
        $1, $2, $3, $4
    }
'
```

**Run:**

```bash
chmod +x long_running_processes.sh
./long_running_processes.sh
```

**Skills:** Process runtime analysis, monitoring, Linux troubleshooting.

**Note:** Long-running processes are often normal. This project identifies them for investigation rather than automatically terminating them.

---

# Project 8: Graceful Shutdown of Multiple Test Processes

**Objective:** Start several disposable processes and gracefully terminate them together.

**Script:** `graceful_shutdown.sh`

```bash
#!/bin/bash

PIDS=()

for i in 1 2 3; do
    sleep 300 &
    PIDS+=("$!")
done

echo "Started test processes: ${PIDS[*]}"

echo "Sending SIGTERM..."

for pid in "${PIDS[@]}"; do
    kill -TERM "$pid"
done

for pid in "${PIDS[@]}"; do
    wait "$pid" 2>/dev/null
done

echo "Test process shutdown completed."
```

**Run:**

```bash
chmod +x graceful_shutdown.sh
./graceful_shutdown.sh
```

**Skills:** Bash arrays, loops, multiple PID management, graceful shutdown.

---

# Project 9: Interactive Process Management Menu

**Objective:** Create a simple command-line menu to inspect and manage disposable processes.

**Script:** `process_menu.sh`

```bash
#!/bin/bash

while true; do
    echo ""
    echo "===== PROCESS MANAGEMENT MENU ====="
    echo "1. View current user's processes"
    echo "2. Start a test process"
    echo "3. Stop a test process"
    echo "4. Exit"

    read -r -p "Choose an option: " choice

    case "$choice" in
        1)
            ps -u "$(id -un)" -o pid,stat,comm
            ;;
        2)
            sleep 300 &
            echo "Test PID: $!"
            ;;
        3)
            read -r -p "Enter test process PID: " pid

            if [[ "$pid" =~ ^[0-9]+$ ]] && (( pid > 1 )); then
                ps -p "$pid" -o pid,user,comm

                read -r -p "Send SIGTERM? (yes/no): " answer

                if [ "$answer" = "yes" ]; then
                    kill -TERM "$pid"
                fi
            else
                echo "Invalid PID."
            fi
            ;;
        4)
            exit 0
            ;;
        *)
            echo "Invalid option."
            ;;
    esac
done
```

**Run:**

```bash
chmod +x process_menu.sh
./process_menu.sh
```

**Skills:** Interactive Bash scripting, process inspection, signal management.

**Safety:** Only enter PIDs of disposable processes you started for testing. This simple menu does not verify that a PID belongs to a test process.

---

# Project 10: Automatically Restart a Test Process

**Objective:** Demonstrate basic process supervision by restarting a disposable process after it exits.

**Script:** `process_restart.sh`

```bash
#!/bin/bash

MAX_RESTARTS=3
COUNT=0

echo "===== Test Process Supervisor ====="
echo "Press Ctrl+C to stop."

while (( COUNT < MAX_RESTARTS )); do
    sleep 5 &
    PID=$!

    echo "Started process PID: $PID"

    wait "$PID"
    STATUS=$?

    COUNT=$((COUNT + 1))

    echo "Process exited with status: $STATUS"

    if (( COUNT < MAX_RESTARTS )); then
        echo "Restarting test process..."
        sleep 2
    fi
done

echo "Maximum restart count reached."
```

**Run:**

```bash
chmod +x process_restart.sh
./process_restart.sh
```

**Skills:** Process supervision, Bash loops, exit status handling, restart logic.

**Note:** This is a learning demonstration, not a production service manager. For production Linux services, use `systemd` and its restart policies.

---

## GitHub Repository Structure

```text
Linux-kill-Command-Projects/
│
├── README.md
├── kill_pid.sh
├── kill_by_name.sh
├── force_kill.sh
├── pause_resume.sh
├── list_signals.sh
├── high_cpu_processes.sh
├── long_running_processes.sh
├── graceful_shutdown.sh
├── process_menu.sh
├── process_restart.sh
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

These projects demonstrate Linux administration techniques relevant to:

- Linux System Administrator
- IT Support Specialist
- Infrastructure Operations Analyst
- DevOps Engineer
- Site Reliability Engineer
- Technical Support Engineer

Practical applications include identifying unresponsive processes, managing process signals, investigating resource consumption, and understanding basic process supervision.

## RHCSA Skills Practiced

- Managing running processes
- Identifying processes using PIDs
- Sending Linux signals
- Pausing and resuming processes
- Troubleshooting unresponsive applications
- Using `ps`, `pgrep`, and `pkill`
- Writing Bash scripts
- Understanding process lifecycle management

## Learning Outcomes

By completing these projects, I practiced Linux process management, signal handling, Bash scripting, process troubleshooting, and basic automation.

The projects demonstrate practical command-line techniques relevant to Linux administration and RHCSA preparation.

## Author

**Farhan Muntasir**

B.S. Computer Science – Texas Southern University

GitHub: https://github.com/farhan115

**Focus:** Linux System Administration | RHCSA | Cybersecurity | IAM | DevOps
