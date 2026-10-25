# Linux `sort` Command — Data Sorting & Log Analysis Lab

## Project Overview

This project demonstrates hands-on practice with the Linux `sort` command to organize, filter, and analyze text-based data.

The lab covers alphabetical sorting, numerical sorting, reverse ordering, duplicate removal, employee data processing, Linux user management, and security log analysis.

**Author:** Farhan Muntasir  
**Category:** Linux Administration | RHCSA | Cybersecurity  
**Difficulty:** Beginner to Intermediate

---

## 1. Lab Objectives

- Understand the syntax and options of `sort`.
- Sort text alphabetically and numerically.
- Perform reverse sorting.
- Remove duplicate records.
- Sort files by specific columns.
- Analyze Linux user account information.
- Identify large files and frequently occurring IP addresses.
- Combine `sort` with `cut`, `awk`, `head`, and `uniq`.

## 2. Lab Environment

- **Operating System:** Linux (Ubuntu, RHEL, Rocky Linux, or similar)
- **Shell:** Bash
- **Tools:** `sort`, `cut`, `awk`, `uniq`, `head`, `tail`, `find`
- **Permissions:** Standard Linux user

## 3. Basic Syntax

```bash
sort [options] filename
```

Example:

```bash
sort names.txt
```

This sorts the lines in ascending order according to the current locale.

## 4. Create a Sample File

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

Verify the file:

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

### Lab 1 — Sort Employee Names Alphabetically

**Objective:** Sort employee records alphabetically.

```bash
tail -n +2 employees.csv | sort
```

Expected output:

```text
David,IT,75000
Emma,Finance,68000
John,IT,65000
Mike,IT,72000
Sarah,HR,55000
```

**Skills:** Alphabetical sorting, command pipelines.

### Lab 2 — Reverse Alphabetical Sorting

**Objective:** Sort employee records in reverse alphabetical order.

```bash
tail -n +2 employees.csv | sort -r
```

Expected output:

```text
Sarah,HR,55000
Mike,IT,72000
John,IT,65000
Emma,Finance,68000
David,IT,75000
```

### Lab 3 — Sort Employees by Salary (Lowest to Highest)

**Objective:** Sort the third CSV field numerically.

```bash
tail -n +2 employees.csv | sort -t, -k3,3n
```

Expected output:

```text
Sarah,HR,55000
John,IT,65000
Emma,Finance,68000
Mike,IT,72000
David,IT,75000
```

### Lab 4 — Sort Employees by Salary (Highest to Lowest)

**Objective:** Sort salaries in descending order.

```bash
tail -n +2 employees.csv | sort -t, -k3,3nr
```

Expected output:

```text
David,IT,75000
Mike,IT,72000
Emma,Finance,68000
John,IT,65000
Sarah,HR,55000
```

### Lab 5 — Display Unique Departments

**Objective:** Extract and sort department names without duplicates.

```bash
tail -n +2 employees.csv | cut -d, -f2 | sort -u
```

Expected output:

```text
Finance
HR
IT
```

### Lab 6 — Sort by Department and Salary

**Objective:** Sort by department alphabetically, then salary numerically.

```bash
tail -n +2 employees.csv | sort -t, -k2,2 -k3,3n
```

Expected output:

```text
Emma,Finance,68000
Sarah,HR,55000
John,IT,65000
Mike,IT,72000
David,IT,75000
```

---

## 6. Real-World Linux Administration Labs

### Lab 7 — Sort Linux Usernames

```bash
cut -d: -f1 /etc/passwd | sort
```

**Use case:** Review Linux account names in sorted order.

### Lab 8 — Sort Users by UID

```bash
sort -t: -k3,3n /etc/passwd
```

**Use case:** Organize Linux user accounts by numerical user ID.

### Lab 9 — Identify the Largest Files

```bash
find . -maxdepth 1 -type f -printf '%s %p\n' | sort -nr | head -10
```

**Use case:** Identify the 10 largest regular files in the current directory.

**Note:** This example uses GNU `find`, commonly available on Linux systems.

### Lab 10 — Analyze IP Addresses in Access Logs

Assuming the first field in `access.log` contains the client IP address:

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr
```

Example output:

```text
15 192.168.1.10
10 192.168.1.100
7 10.0.0.5
3 172.16.0.8
```

**Use case:** Identify frequently occurring IP addresses during log analysis.

---

## 7. Common `sort` Options

| Option | Description |
|---|---|
| `-r` | Reverse sorting |
| `-n` | Numerical sorting |
| `-u` | Output unique sorted lines |
| `-f` | Ignore case while sorting |
| `-k` | Specify sorting fields |
| `-t` | Define field delimiter |
| `-o` | Write output to a file |
| `-c` | Check whether input is sorted |
| `-h` | Sort human-readable numbers |
| `-V` | Sort version numbers |

## 8. Combining `sort` with Other Linux Commands

### Count Employees by Department

```bash
tail -n +2 employees.csv | cut -d, -f2 | sort | uniq -c
```

Expected output:

```text
1 Finance
1 HR
3 IT
```

### Sort and Save Output

```bash
sort employees.csv -o sorted_employees.csv
```

This sorts the entire file, including the header, and saves the results to a new file.

### Sort Numbers

```bash
printf '50\n10\n100\n25\n' | sort -n
```

Expected output:

```text
10
25
50
100
```

---

## 9. Skills Demonstrated

- Linux command-line administration
- Alphabetical and numerical sorting
- Text processing and data organization
- Duplicate record handling
- Linux user account analysis
- Security log analysis
- Command pipelines
- Shell scripting fundamentals
- RHCSA-related system administration

## 10. Key Takeaways

The Linux `sort` command is an essential tool for organizing and analyzing text-based information.

Through these labs, I practiced sorting structured records, removing duplicates, processing Linux account information, and combining commands to analyze logs and system data.

**Important:** `sort` normally displays sorted output without modifying the source file. Use `-o` or output redirection to save results.

---

## 11. Future Improvements

- Create Bash scripts for automated sorting.
- Analyze larger security logs.
- Combine `grep`, `awk`, `sed`, `cut`, and `sort`.
- Develop automated Linux reporting scripts.
- Add screenshots showing terminal commands and outputs.

---

**Author:** Farhan Muntasir  
**Project Series:** Linux Command-Line Administration Labs  
**Focus:** Linux | RHCSA | Cybersecurity | System Administration
