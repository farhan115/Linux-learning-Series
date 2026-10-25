# Linux `tail` Command — Real-Time Log Monitoring & Security Analysis

## Project Overview

This project demonstrates practical experience using the Linux `tail` command to inspect recent file entries, monitor logs in real time, and investigate authentication and system events.

The lab focuses on Linux system administration, security monitoring, troubleshooting, and RHCSA-related command-line skills.

**Author:** Farhan Muntasir  
**Category:** Linux Administration | RHCSA | Cybersecurity  
**Difficulty:** Beginner to Intermediate

---

## 1. Lab Objectives

- Understand the syntax and options of `tail`.
- Display the last lines of text files.
- Monitor files for real-time updates.
- Identify failed login attempts.
- Analyze SSH authentication logs.
- Combine `tail` with `grep`.
- Monitor system services using `journalctl`.
- Practice Linux troubleshooting techniques.

## 2. Lab Environment

- **Operating System:** RHEL, Rocky Linux, Ubuntu, or similar
- **Shell:** Bash
- **Tools:** `tail`, `cat`, `echo`, `grep`, `journalctl`
- **Permissions:** Standard user for sample files; `sudo` may be required for protected logs

## 3. Basic Syntax

```bash
tail [options] filename
```

Example:

```bash
tail -n 5 file.txt
```

Displays the last five lines of a file.

By default, `tail` displays the last 10 lines.

---

## 4. Create a Sample Security Log

Create a sample log file:

```bash
cat > security.log <<'EOF'
10:00 Login successful user=admin
10:05 Failed password user=root
10:10 Login successful user=john
10:15 Failed password user=admin
10:20 Failed password user=root
10:25 Login successful user=emma
10:30 Failed password user=root
EOF
```

Verify the contents:

```bash
cat security.log
```

---

## 5. Hands-on Labs

### Lab 1 — Display the Last Five Lines

**Objective:** Retrieve the five most recent log entries.

```bash
tail -n 5 security.log
```

Expected output:

```text
10:10 Login successful user=john
10:15 Failed password user=admin
10:20 Failed password user=root
10:25 Login successful user=emma
10:30 Failed password user=root
```

**Skills:** File inspection and log analysis.

### Lab 2 — Display the Last Three Lines

```bash
tail -n 3 security.log
```

Expected output:

```text
10:20 Failed password user=root
10:25 Login successful user=emma
10:30 Failed password user=root
```

### Lab 3 — Monitor Logs in Real Time

**Objective:** Observe newly appended log entries.

Open Terminal 1:

```bash
tail -f security.log
```

Open Terminal 2:

```bash
echo "10:35 Failed password user=admin" >> security.log
```

**Expected result:** Terminal 1 displays the new entry automatically.

Press `Ctrl+C` to stop monitoring.

### Lab 4 — Display Logs Starting from a Specific Line

```bash
tail -n +4 security.log
```

Expected output after completing Lab 3:

```text
10:15 Failed password user=admin
10:20 Failed password user=root
10:25 Login successful user=emma
10:30 Failed password user=root
10:35 Failed password user=admin
```

### Lab 5 — Monitor Failed Login Attempts

**Objective:** Filter authentication failures from live log updates.

```bash
tail -n 0 -f security.log | grep --line-buffered "Failed password"
```

In a second terminal:

```bash
echo "10:40 Failed password user=root" >> security.log
```

Expected output:

```text
10:40 Failed password user=root
```

**Skills:** Real-time log monitoring, command pipelines, and security filtering.

### Lab 6 — Display the Last 100 Bytes

```bash
tail -c 100 security.log
```

**Result:** Displays the final 100 bytes of the file.

### Lab 7 — Follow a File Across Log Rotation

```bash
tail -F security.log
```

**Explanation:** Unlike `tail -f`, which normally follows the file descriptor, `tail -F` follows the filename and can continue monitoring when the file is rotated or recreated.

---

## 6. Real-World Linux Administration Labs

### Lab 8 — Monitor SSH Logs on RHEL

```bash
sudo tail -f /var/log/secure
```

**Use case:** Monitor authentication activity and investigate failed SSH login attempts.

### Lab 9 — Monitor Authentication Logs on Ubuntu

```bash
sudo tail -f /var/log/auth.log
```

**Use case:** Observe authentication events on Ubuntu systems where this log file is available.

### Lab 10 — Monitor System Messages

```bash
sudo tail -f /var/log/messages
```

**Use case:** Monitor system messages and troubleshoot Linux issues on systems using this log file.

### Lab 11 — Monitor Apache Access Logs

For a typical RHEL Apache installation:

```bash
sudo tail -f /var/log/httpd/access_log
```

**Use case:** Observe incoming HTTP requests and investigate web server activity.

### Lab 12 — Monitor a systemd Service

```bash
sudo journalctl -u sshd -f
```

**Use case:** Monitor new SSH service events through the systemd journal.

---

## 7. Common `tail` Options

| Option | Description |
|---|---|
| `-n 5` | Display last five lines |
| `-n +5` | Display from line five onward |
| `-f` | Follow appended file content |
| `-F` | Follow a filename across rotation |
| `-c 100` | Display last 100 bytes |
| `-q` | Suppress filename headers |
| `-v` | Always display filename headers |
| `-n 0 -f` | Monitor only newly appended lines |

## 8. Combining `tail` with Other Linux Commands

### Display Recent Failed Logins

```bash
grep "Failed password" security.log | tail -n 5
```

### Count Failed Login Attempts

```bash
grep -c "Failed password" security.log
```

### Monitor Only Newly Added Error Messages

```bash
tail -n 0 -f security.log | grep --line-buffered -i "error"
```

### Display the Most Recent 20 System Journal Entries

```bash
journalctl -n 20
```

---

## 9. Skills Demonstrated

- Linux command-line administration
- Real-time file monitoring
- SSH authentication log analysis
- Security event investigation
- Linux troubleshooting
- Command pipelines
- Systemd journal monitoring
- RHCSA-related system administration
- Cybersecurity fundamentals

## 10. Key Takeaways

The Linux `tail` command is essential for monitoring system activity and troubleshooting issues.

Through these exercises, I practiced retrieving recent log entries, following file updates, filtering failed authentication events, and inspecting Linux system and service logs.

**Important:** Log locations depend on the Linux distribution and logging configuration. Some systems primarily store authentication events in the systemd journal.

---

## 11. Future Improvements

- Create automated log monitoring scripts.
- Combine `tail`, `grep`, `awk`, and `sort`.
- Analyze failed SSH login trends.
- Build a basic Linux security monitoring dashboard.
- Add screenshots demonstrating each completed lab.
- Practice log rotation using `logrotate`.

---

**Author:** Farhan Muntasir  
**Project Series:** Linux Command-Line Administration Labs  
**Focus:** Linux | RHCSA | Cybersecurity | System Administration
