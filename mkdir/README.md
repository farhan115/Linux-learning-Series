# 🐧 Linux Project 10: Mastering the `mkdir` Command

## 📌 Project Overview

This hands-on Linux project demonstrates how to use the `mkdir` (Make Directory) command to create, organize, and manage directories in Linux.

The project includes **8 practical labs** covering directory creation, nested directory structures, permissions, absolute paths, and Bash brace expansion.

**Project Goal:** Build practical Linux filesystem management skills applicable to System Administration, IT Support, Cybersecurity, Cloud Computing, and Automation.

## 🎯 Project Objectives

- Create individual and multiple directories.
- Build nested directory structures.
- Configure directory permissions during creation.
- Create parent and child directories simultaneously.
- Avoid errors when directories already exist.
- Create directories using absolute paths.
- Use Bash brace expansion for bulk directory creation.
- Understand Linux filesystem organization.

## 🛠️ Lab Environment

- **Operating System:** Ubuntu Linux / Red Hat Enterprise Linux
- **Terminal:** Bash
- **Commands:** `mkdir`, `ls`, `cd`, `pwd`, `tree`, `echo`
- **Skill Level:** Beginner

## 🧪 Lab Setup

Create a dedicated practice environment before starting the labs.

```bash
mkdir -p ~/linux-mkdir-lab
cd ~/linux-mkdir-lab

pwd
ls -la
```

All exercises should be performed inside this practice directory unless otherwise specified.

---

## 💻 Hands-On Labs

### Lab 1: Create a Single Directory

**Objective:** Create a new directory in the current location.

```bash
mkdir test
ls
```

Expected output:

```text
test
```

**Explanation:** The `mkdir` command creates a directory named `test`.

### Lab 2: Create Multiple Directories

**Objective:** Create several directories using a single command.

```bash
mkdir dir1 dir2 dir3
ls -d dir*/
```

Expected output:

```text
dir1/  dir2/  dir3/
```

**Explanation:** Multiple directory names can be supplied to `mkdir` to create them simultaneously.

### Lab 3: Create Nested Directories

**Objective:** Create a directory structure with multiple levels.

```bash
mkdir -p project/app/logs
tree project
```

Expected structure:

```text
project/
└── app/
    └── logs/
```

**Explanation:** The `-p` option automatically creates missing parent directories.

If `tree` is unavailable, use:

```bash
ls -R project
```

### Lab 4: Create a Directory with Specific Permissions

**Objective:** Set directory permissions during creation.

```bash
mkdir -m 755 data
ls -ld data
```

Example output:

```text
drwxr-xr-x 2 farhan farhan 4096 Oct 24 12:00 data
```

**Explanation:** The `-m` option specifies directory permissions.

Permission `755` means:

- Owner: Read, write, execute
- Group: Read and execute
- Others: Read and execute

The execute permission on a directory allows traversal.

### Lab 5: Create Parent and Child Directories Simultaneously

**Objective:** Build a nested organizational structure.

```bash
mkdir -p company/it/support/tickets
tree company
```

Expected structure:

```text
company/
└── it/
    └── support/
        └── tickets/
```

**Explanation:** The `-p` option creates all missing directories in the specified path.

### Lab 6: Avoid Errors When a Directory Already Exists

**Objective:** Create a directory only when necessary.

```bash
mkdir -p backup
mkdir -p backup

echo $?
```

Expected output:

```text
0
```

**Explanation:** The `-p` option prevents an error when the directory already exists.

An exit status of `0` indicates successful execution.

### Lab 7: Create Directories in Different Locations

**Objective:** Create a directory using an absolute path.

```bash
mkdir -p /tmp/linux-mkdir-practice
ls -ld /tmp/linux-mkdir-practice
```

**Explanation:** An absolute path begins with `/` and identifies a location from the filesystem root.

The `/tmp` directory is commonly used for temporary files and directories.

### Lab 8: Create Multiple Directories Using Brace Expansion

**Objective:** Create numbered directories efficiently.

```bash
mkdir project{1..5}
ls -d project[1-5]
```

Expected output:

```text
project1  project2  project3  project4  project5
```

**Explanation:** Bash brace expansion generates multiple directory names automatically.

This technique is useful for organizing projects and automating repetitive tasks.

---

## 🔬 Additional Practice

### Create a Directory with Restricted Permissions

```bash
mkdir -m 700 private
ls -ld private
```

Permission `700` gives the owner full access while denying access to the group and others.

### Display Directory Creation Details

```bash
mkdir -v reports
```

Example output:

```text
mkdir: created directory 'reports'
```

### Create Multiple Nested Directories

```bash
mkdir -p infrastructure/{servers,network,security}
```

Expected structure:

```text
infrastructure/
├── servers/
├── network/
└── security/
```

### Create a Project Folder Structure

```bash
mkdir -p linux-project/{scripts,logs,config,backups}
tree linux-project
```

Expected structure:

```text
linux-project/
├── backups/
├── config/
├── logs/
└── scripts/
```

This structure is useful for Linux administration and automation projects.

## 📸 Project Screenshots

Add screenshots showing the commands executed and their results.

Recommended GitHub repository structure:

```text
linux-mkdir-command-project/
├── README.md
├── screenshots/
│   ├── lab01-single-directory.png
│   ├── lab02-multiple-directories.png
│   ├── lab03-nested-directories.png
│   ├── lab04-directory-permissions.png
│   ├── lab05-parent-child-directories.png
│   ├── lab06-existing-directory.png
│   ├── lab07-absolute-path.png
│   └── lab08-brace-expansion.png
└── scripts/
    └── mkdir-practice.sh
```

## 📚 Key Takeaways

- `mkdir` creates directories in Linux.
- `mkdir -p` creates missing parent directories.
- `mkdir -m` sets directory permissions.
- `mkdir -v` displays directory creation details.
- Absolute paths specify locations from the filesystem root.
- Brace expansion enables bulk directory creation.
- Proper directory organization improves filesystem management and automation.

## 🚀 Skills Demonstrated

- Linux command-line proficiency
- File and directory management
- Linux filesystem hierarchy
- Directory permission configuration
- Bash brace expansion
- Nested directory creation
- Linux system administration
- Basic shell automation

## 🎓 Career Relevance

These skills support practical work in:

- Linux System Administration
- IT Support and Help Desk
- Cybersecurity Operations
- Cloud Infrastructure
- Identity and Access Management (IAM)
- DevOps and Automation

## 👨‍💻 Author

**Farhan Muntasir**

GitHub: https://github.com/farhan115

*Linux Administration | IT Support | Cybersecurity | IAM*

---

## 🐧 Linux Command Project Series

| Project | Command | Topic |
|---|---|---|
| 01 | `ls` | Listing Files and Directories |
| 02 | `cd` | Directory Navigation |
| 03 | `pwd` | Print Working Directory |
| 04 | `echo` | Text Output and Variables |
| 05 | `cat` | Viewing and Combining Files |
| 06 | `cp` | Copying Files and Directories |
| 07 | `mv` | Moving and Renaming Files |
| 08 | `rm` | Removing Files and Directories |
| 09 | `touch` | File Creation and Timestamp Management |
| 10 | `mkdir` | Creating and Organizing Directories |

**Building practical Linux skills one command at a time.**
