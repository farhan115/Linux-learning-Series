# Linux sed Command — Stream Editor Lab

## Project Overview

This project demonstrates hands-on experience with the Linux `sed` (Stream Editor) command for searching, replacing, inserting, deleting, and modifying text in files.

The lab focuses on practical Linux system administration tasks, text processing, configuration management, and log analysis.

**Author:** Farhan Muntasir  
**Category:** Linux Administration | RHCSA | Shell Scripting  
**Difficulty:** Beginner to Intermediate

---

## 1. Lab Objectives

- Understand Linux `sed` syntax and options.
- Search and replace text in files.
- Display specific lines and filter records.
- Insert and delete text.
- Modify files while creating backups.
- Process Linux configuration files.
- Analyze system logs.

## 2. Basic Syntax

```bash
sed [options] 'command' filename
```

Example:

```bash
sed 's/Linux/Ubuntu/' file.txt
```

This replaces the first occurrence of `Linux` with `Ubuntu` on each line in the output without modifying the original file.

## 3. Lab Environment

- Operating System: Linux (Ubuntu, Rocky Linux, RHEL, or similar)
- Terminal: Bash
- Tools: `sed`, `cat`
- Required privileges: Standard user; elevated privileges may be needed to access protected logs

## 4. Create a Sample File

```bash
cat > employees.txt <<'EOF'
John IT 65000
Sarah HR 55000
Mike IT 72000
Emma Finance 68000
David IT 75000
EOF
```

Verify:

```bash
cat employees.txt
```

Expected output:

```text
John IT 65000
Sarah HR 55000
Mike IT 72000
Emma Finance 68000
David IT 75000
```

## 5. Hands-on Exercises

### Lab 1 — Replace Text

Replace `IT` with `Technology`.

```bash
sed 's/IT/Technology/g' employees.txt
```

**Expected result:** All occurrences of `IT` are replaced in the displayed output.

### Lab 2 — Print Specific Lines

Display lines 1 through 3.

```bash
sed -n '1,3p' employees.txt
```

Expected output:

```text
John IT 65000
Sarah HR 55000
Mike IT 72000
```

### Lab 3 — Delete a Line

Remove the second line from the output.

```bash
sed '2d' employees.txt
```

**Result:** Sarah's record is excluded from the displayed output. The original file remains unchanged.

### Lab 4 — Insert a Header

```bash
sed '1i\Name Department Salary' employees.txt
```

Expected output begins with:

```text
Name Department Salary
John IT 65000
Sarah HR 55000
```

### Lab 5 — Modify a File and Create a Backup

```bash
sed -i.bak 's/HR/HumanResources/g' employees.txt
```

Verify:

```bash
cat employees.txt
cat employees.txt.bak
```

**Result:** The original file is modified, and `employees.txt.bak` preserves its previous contents.

### Lab 6 — Filter Specific Records

Display employees in the IT department.

```bash
sed -n '/ IT /p' employees.txt
```

**Expected result:** John, Mike, and David are displayed.

### Lab 7 — Remove Blank Lines

```bash
sed '/^[[:space:]]*$/d' employees.txt
```

**Result:** Blank or whitespace-only lines are excluded from the output.

### Lab 8 — Remove Comment Lines

```bash
sed '/^[[:space:]]*#/d' config.txt
```

**Result:** Full-line comments beginning with `#`, including indented comments, are excluded from the output.

## 6. Real-World Linux Administration

### Preview an SSH Configuration Change

```bash
sed 's/^#Port 22/Port 2222/' sshd_config
```

This demonstrates how `sed` can replace a configuration directive in a sample file without modifying it.

### Analyze Failed SSH Login Attempts

On RHEL-based systems:

```bash
sudo sed -n '/Failed password/p' /var/log/secure
```

On Ubuntu-based systems:

```bash
sudo sed -n '/Failed password/p' /var/log/auth.log
```

Log locations and availability depend on the system configuration.

## 7. Common sed Options

| Option | Description |
|---|---|
| `-n` | Suppress automatic output |
| `-i` | Edit files in place |
| `-i.bak` | Edit and create a backup |
| `-e` | Execute multiple expressions |
| `-f` | Read commands from a script file |
| `-E` | Use extended regular expressions |

## 8. Skills Demonstrated

- Linux command-line operations
- Stream editing and text manipulation
- Regular expressions
- Configuration file management
- File backups
- Log filtering and security analysis
- Shell scripting fundamentals
- RHCSA-related Linux administration

## 9. Key Takeaways

The `sed` command helps Linux administrators automate repetitive text-processing tasks, manage configuration files, filter system logs, and perform efficient command-line operations.

**Important:** Without `-i`, `sed` normally does not modify the original file. Create backups before editing important system configuration files.

---

## 10. Future Improvements

- Automate text replacements using Bash scripts.
- Combine `grep`, `awk`, and `sed` for log analysis.
- Practice advanced regular expressions.
- Build configuration-management automation examples.
- Add terminal screenshots demonstrating each exercise.

---

**Author:** Farhan Muntasir  
**Project:** Linux Command-Line Administration Labs  
**Focus:** Linux | RHCSA | Cybersecurity | System Administration
