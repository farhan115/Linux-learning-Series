# Linux `head` Command — File Inspection & Log Analysis

## Project Overview

This project demonstrates hands-on experience using the Linux `head` command to display the beginning of files, inspect text-based data, analyze system information, and work with command pipelines.

The lab focuses on Linux system administration, file inspection, troubleshooting, cybersecurity fundamentals, and RHCSA preparation.

**Author:** Farhan Muntasir  
**Category:** Linux Administration | RHCSA | Cybersecurity  
**Difficulty:** Beginner to Intermediate

---

## 1. Lab Objectives

- Understand the syntax and options of the `head` command.
- Display the first lines of a file.
- Extract specific numbers of lines and bytes.
- Inspect Linux user and group information.
- Preview CSV and text files.
- Analyze system and security logs.
- Combine `head` with `grep`, `sort`, and other Linux commands.
- Practice RHCSA-related Linux administration tasks.

## 2. Lab Environment

- **Operating System:** RHEL, Rocky Linux, Ubuntu, or similar
- **Shell:** Bash
- **Tools:** `head`, `cat`, `grep`, `sort`, `find`
- **Permissions:** Standard Linux user; `sudo` may be required for protected logs

## 3. Basic Syntax

```bash
head [options] filename
```

Example:

```bash
head -n 5 file.txt
```

Displays the first five lines of a file.

By default, `head` displays the first 10 lines.

---

## 4. Create a Sample File

Create a file containing employee records.

```bash
cat > employees.txt <<'EOF'
John IT 65000
Sarah HR 55000
Mike IT 72000
Emma Finance 68000
David IT 75000
Alex Security 80000
Lisa HR 62000
Robert IT 70000
Sophia Finance 73000
James Security 85000
EOF
```

Verify the file:

```bash
cat employees.txt
```

---

## 5. Hands-on Labs

### Lab 1 — Display the First Five Lines

**Objective:** Display the first five employee records.

```bash
head -n 5 employees.txt
```

**Expected output:**

```text
John IT 65000
Sarah HR 55000
Mike IT 72000
Emma Finance 68000
David IT 75000
```

**Skills:** File inspection and text processing.

### Lab 2 — Display the First Three Lines

```bash
head -n 3 employees.txt
```

**Expected output:**

```text
John IT 65000
Sarah HR 55000
Mike IT 72000
```

### Lab 3 — Display the First Line

```bash
head -n 1 employees.txt
```

**Expected output:**

```text
John IT 65000
```

### Lab 4 — Display the First 50 Bytes

```bash
head -c 50 employees.txt
```

**Objective:** Extract the first 50 bytes from the file.

**Note:** The `-c` option counts bytes, not necessarily characters when working with multibyte text.

### Lab 5 — Display All Except the Last Three Lines

```bash
head -n -3 employees.txt
```

**Expected output:**

```text
John IT 65000
Sarah HR 55000
Mike IT 72000
Emma Finance 68000
David IT 75000
Alex Security 80000
Lisa HR 62000
```

### Lab 6 — Preview a CSV Header

Create a sample CSV file:

```bash
cat > employees.csv <<'EOF'
Name,Department,Salary
John,IT,65000
Sarah,HR,55000
Mike,IT,72000
EOF
```

Display the header:

```bash
head -n 1 employees.csv
```

**Expected output:**

```text
Name,Department,Salary
```

### Lab 7 — Inspect Multiple Files

Create two sample files:

```bash
printf 'Line 1\nLine 2\nLine 3\n' > file1.txt
printf 'A\nB\nC\n' > file2.txt
```

Run:

```bash
head -n 3 file1.txt file2.txt
```

**Objective:** Display the beginning of multiple files with filename headers.

---

## 6. Real-World Linux Administration Labs

### Lab 8 — Inspect Linux User Accounts

```bash
head -n 10 /etc/passwd
```

**Use case:** Review the first ten local account records.

### Lab 9 — Inspect Linux Groups

```bash
head -n 10 /etc/group
```

**Use case:** Examine Linux group information.

### Lab 10 — Inspect System Logs

On RHEL-based systems:

```bash
sudo head -n 20 /var/log/messages
```

**Use case:** Inspect the beginning of a system log file.

**Note:** Log availability depends on the Linux distribution and logging configuration.

### Lab 11 — Identify the Five Largest Files

```bash
find . -maxdepth 1 -type f -printf '%s %p\n' | sort -nr | head -n 5
```

**Use case:** Display the five largest regular files in the current directory.

### Lab 12 — Inspect Failed SSH Logins

On RHEL-based systems:

```bash
sudo grep "Failed password" /var/log/secure | head -n 5
```

**Use case:** Display the first five matching failed SSH authentication events in the log file.

---

## 7. Common `head` Options

| Option | Description |
|---|---|
| `-n 5` | Display first five lines |
| `-n 20` | Display first twenty lines |
| `-n -5` | Display all except last five lines |
| `-c 100` | Display first 100 bytes |
| `-q` | Suppress filename headers |
| `-v` | Always display filename headers |
| `--help` | Display command help |
| `--version` | Display version information |

---

## 8. Combining `head` with Other Commands

### Display the First Five Sorted Usernames

```bash
cut -d: -f1 /etc/passwd | sort | head -n 5
```

### Display the First Five IT Employees

```bash
grep ' IT ' employees.txt | head -n 5
```

### Display the Five Largest Files

```bash
find . -maxdepth 1 -type f -printf '%s %p\n' | sort -nr | head -n 5
```

### Display the First Five Unique Departments

```bash
cut -d, -f2 employees.csv | tail -n +2 | sort -u | head -n 5
```

---

## 9. Difference Between `head` and `tail`

| Command | Purpose |
|---|---|
| `head file.txt` | Display first 10 lines |
| `tail file.txt` | Display last 10 lines |
| `head -n 5 file.txt` | Display first 5 lines |
| `tail -n 5 file.txt` | Display last 5 lines |
| `head -c 100 file.txt` | Display first 100 bytes |
| `tail -c 100 file.txt` | Display last 100 bytes |

---

## 10. Skills Demonstrated

- Linux command-line administration
- File inspection and text processing
- Log analysis and troubleshooting
- Linux user and group information
- CSV file inspection
- Command pipelines
- Shell scripting fundamentals
- RHCSA-related Linux administration
- Cybersecurity fundamentals

## 11. Key Takeaways

The Linux `head` command is an efficient utility for quickly inspecting the beginning of text files without opening the entire file in a text editor.

Through these exercises, I practiced extracting lines and bytes, reviewing Linux system information, analyzing logs, and combining Linux commands to process data.

**Important:** `head` is primarily a file-reading utility and does not modify the original file.

---

## 12. Future Improvements

- Create automated Bash scripts for file inspection.
- Combine `head`, `tail`, `grep`, `awk`, `sed`, and `sort`.
- Analyze larger system and security logs.
- Build a Linux troubleshooting toolkit.
- Add terminal screenshots for each completed exercise.

---

**Author:** Farhan Muntasir  
**Project Series:** Linux Command-Line Administration Labs  
**Focus:** Linux | RHCSA | Cybersecurity | System Administration
