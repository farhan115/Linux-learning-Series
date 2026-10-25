# Linux `cut` Command — Text and Column Extraction Lab

## Project Overview

This project demonstrates practical usage of the Linux `cut` command to extract specific characters, fields, and columns from text files.

The lab focuses on CSV data processing, Linux user account information, system administration, and command-line automation.

**Author:** Farhan Muntasir  
**Category:** Linux Administration | RHCSA | Shell Scripting  
**Difficulty:** Beginner

---

## 1. Lab Objectives

- Understand the syntax and options of the `cut` command.
- Extract specific characters from text files.
- Extract fields using delimiters.
- Process CSV and tab-separated files.
- Retrieve Linux usernames, UIDs, and login shells.
- Practice text extraction for system administration.
- Combine `cut` with other Linux utilities.

## 2. Lab Environment

- Operating System: Linux (Ubuntu, RHEL, Rocky Linux, or similar)
- Shell: Bash
- Tools: `cut`, `cat`, `grep`, `sort`, `uniq`
- Permissions: Standard Linux user

## 3. Basic Syntax

```bash
cut [options] filename
```

Example:

```bash
cut -d: -f1 /etc/passwd
```

**Explanation:**

- `-d:` specifies the colon as the delimiter.
- `-f1` extracts the first field.
- `/etc/passwd` contains Linux account information.

## 4. Create a Sample File

Create a CSV file containing employee information.

```bash
cat > employees.csv <<'EOF'
Name,Department,Salary
John,IT,65000
Sarah,HR,55000
Mike,IT,72000
Emma,Finance,68000
David,IT,75000
EOF
```

Verify the contents:

```bash
cat employees.csv
```

Expected output:

```text
Name,Department,Salary
John,IT,65000
Sarah,HR,55000
Mike,IT,72000
Emma,Finance,68000
David,IT,75000
```

---

## 5. Hands-on Labs

### Lab 1 — Extract Employee Names

**Objective:** Extract the first field from a CSV file.

```bash
cut -d, -f1 employees.csv
```

Expected output:

```text
Name
John
Sarah
Mike
Emma
David
```

**Skills:** Field extraction, delimiters, CSV processing.

### Lab 2 — Extract Departments

**Objective:** Display the department column.

```bash
cut -d, -f2 employees.csv
```

Expected output:

```text
Department
IT
HR
IT
Finance
IT
```

### Lab 3 — Extract Names and Salaries

**Objective:** Extract multiple fields simultaneously.

```bash
cut -d, -f1,3 employees.csv
```

Expected output:

```text
Name,Salary
John,65000
Sarah,55000
Mike,72000
Emma,68000
David,75000
```

### Lab 4 — Extract Specific Characters

**Objective:** Extract the first three characters from each line.

```bash
cut -c1-3 employees.csv
```

Expected output:

```text
Nam
Joh
Sar
Mik
Emm
Dav
```

### Lab 5 — Extract Salary Information

**Objective:** Display only the salary column.

```bash
cut -d, -f3 employees.csv
```

Expected output:

```text
Salary
65000
55000
72000
68000
75000
```

### Lab 6 — Extract Multiple Adjacent Fields

**Objective:** Display names and departments.

```bash
cut -d, -f1-2 employees.csv
```

Expected output:

```text
Name,Department
John,IT
Sarah,HR
Mike,IT
Emma,Finance
David,IT
```

---

## 6. Real-World Linux Administration Labs

### Lab 7 — Extract Linux Usernames

```bash
cut -d: -f1 /etc/passwd
```

Example output:

```text
root
bin
daemon
nobody
```

**Use case:** Review Linux account names.

### Lab 8 — Extract Usernames and UIDs

```bash
cut -d: -f1,3 /etc/passwd
```

Example output:

```text
root:0
bin:1
daemon:2
```

**Use case:** Review user identifiers and account information.

### Lab 9 — Extract Login Shells

```bash
cut -d: -f7 /etc/passwd
```

Example output:

```text
/bin/bash
/usr/sbin/nologin
/bin/sh
```

**Use case:** Identify configured login shells.

### Lab 10 — Extract Linux Group Names

```bash
cut -d: -f1 /etc/group
```

Example output:

```text
root
bin
daemon
sudo
```

**Use case:** Review local Linux groups.

---

## 7. Advanced Lab — Combine `cut` with Other Commands

### Find Unique Departments

```bash
tail -n +2 employees.csv | cut -d, -f2 | sort -u
```

Expected output:

```text
Finance
HR
IT
```

### Count Employees in Each Department

```bash
tail -n +2 employees.csv | cut -d, -f2 | sort | uniq -c
```

Expected output:

```text
      1 Finance
      1 HR
      3 IT
```

### Extract IT Employee Names

```bash
grep ',IT,' employees.csv | cut -d, -f1
```

Expected output:

```text
John
Mike
David
```

**Skills:** Command pipelines, filtering, sorting, counting, and data extraction.

---

## 8. Common `cut` Options

| Option | Description |
|---|---|
| `-c` | Extract characters |
| `-b` | Extract bytes |
| `-d` | Specify a field delimiter |
| `-f` | Select fields |
| `--complement` | Select everything except specified fields |
| `--output-delimiter` | Specify an output delimiter |
| `-s` | Suppress lines without the delimiter |

**Note:** `cut` works best with consistently delimited text. It does not fully parse complex CSV files containing quoted commas or multiline fields.

## 9. Skills Demonstrated

- Linux command-line administration
- Text and character extraction
- CSV and field processing
- Linux user and group information analysis
- Command pipelines
- Shell scripting fundamentals
- RHCSA-related Linux skills
- Basic data processing and automation

## 10. Key Takeaways

The Linux `cut` command provides a simple and efficient way to extract structured information from text files.

Through these exercises, the following concepts are demonstrated:

- Extracting columns and character ranges.
- Working with delimiters.
- Processing employee records.
- Retrieving Linux account information.
- Combining multiple commands for data analysis.

---

## 11. Future Improvements

- Create Bash scripts to automate data extraction.
- Combine `grep`, `awk`, `sed`, and `cut`.
- Analyze larger system log files.
- Practice advanced command pipelines.
- Add screenshots of completed terminal exercises.

---

**Author:** Farhan Muntasir  
**Project Series:** Linux Command-Line Administration Labs  
**Focus:** Linux | RHCSA | Cybersecurity | System Administration
