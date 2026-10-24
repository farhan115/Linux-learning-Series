# 🐧 Linux Project 06: Mastering the `cp` Command

## 📌 Project Overview

This hands-on Linux project demonstrates how to use the `cp` (Copy) command to copy files, directories, and preserve file attributes in Linux.

The project covers **8 practical labs** designed to strengthen Linux command-line skills for System Administration, IT Support, Cybersecurity, and Cloud Computing.

**Project Goal:** Develop practical experience with Linux file management, directory copying, backups, and file permissions.

## 🎯 Project Objectives

- Copy files within the Linux filesystem.
- Copy and rename files.
- Copy files between different directories.
- Copy multiple files simultaneously.
- Copy directories recursively.
- Preserve file permissions and timestamps.
- Prevent accidental file overwrites.
- Display detailed copying operations.

## 🛠️ Lab Environment

- **Operating System:** Ubuntu Linux / Red Hat Enterprise Linux
- **Terminal:** Bash
- **Commands:** `cp`, `ls`, `mkdir`, `touch`, `cat`
- **Skill Level:** Beginner

## 🧪 Lab Setup

Create a practice environment before starting the exercises.

```bash
mkdir -p ~/linux-cp-lab/{Documents,Projects,Backups}
cd ~/linux-cp-lab

echo "Linux Administration Project" > file.txt
echo "Learning Linux Commands" > file1.txt
echo "Practicing File Management" > file2.txt

mkdir -p project
echo "Project documentation" > project/README.txt

ls -l
```

## 💻 Hands-On Labs

### Lab 1: Basic File Copy

**Objective:** Copy a file within the same directory.

```bash
cp file.txt copy.txt
ls -l
```

**Expected result:** Both `file.txt` and `copy.txt` exist.

**Explanation:** The `cp` command creates a copy of the source file without deleting the original.

### Lab 2: Copy a File with a New Name

**Objective:** Copy and rename a file.

```bash
cp file.txt backup.txt
ls -l
```

**Expected result:** A new file named `backup.txt` is created.

**Explanation:** The destination argument specifies the new filename.

### Lab 3: Copy to a Different Directory

**Objective:** Copy a file into another directory.

```bash
cp file.txt ~/linux-cp-lab/Documents/
ls ~/linux-cp-lab/Documents/
```

**Expected result:** `file.txt` appears inside the Documents directory.

**Explanation:** The destination directory receives a copy of the original file.

### Lab 4: Copy Multiple Files

**Objective:** Copy multiple files simultaneously.

```bash
cp file1.txt file2.txt ~/linux-cp-lab/Backups/
ls ~/linux-cp-lab/Backups/
```

**Expected result:**

```text
file1.txt  file2.txt
```

**Explanation:** The final argument specifies the destination directory for all source files.

### Lab 5: Copy a Directory Recursively

**Objective:** Copy an entire directory and its contents.

```bash
cp -r project backup_project
ls -R backup_project
```

**Expected result:**

```text
backup_project:
README.txt
```

**Explanation:** The `-r` option recursively copies directories, including nested files and subdirectories.

### Lab 6: Preserve File Attributes

**Objective:** Preserve file permissions and timestamps during copying.

```bash
cp -p file.txt preserved_copy.txt
ls -l file.txt preserved_copy.txt
```

**Explanation:** The `-p` option preserves file mode, ownership where permitted, and timestamps.

**Important:** Preserving ownership may require elevated privileges depending on the user and filesystem.

### Lab 7: Interactive Copy — Prevent Accidental Overwriting

**Objective:** Request confirmation before overwriting an existing file.

```bash
cp -i file.txt copy.txt
```

Example prompt:

```text
cp: overwrite 'copy.txt'?
```

Enter `y` to overwrite or `n` to cancel.

**Explanation:** The `-i` option prompts before overwriting an existing destination file.

### Lab 8: Verbose Copy — Display Operation Details

**Objective:** Display information about the copying process.

```bash
cp -v file.txt verbose_copy.txt
```

Example output:

```text
'file.txt' -> 'verbose_copy.txt'
```

**Explanation:** The `-v` option displays the source and destination during copying.

## 🔬 Additional Practice

### Copy Only When the Source Is Newer

```bash
cp -u file.txt copy.txt
```

The `-u` option copies the file when the destination is missing or older than the source.

### Copy Files Using Wildcards

```bash
cp *.txt ~/linux-cp-lab/Backups/
```

Copies all matching `.txt` files from the current directory.

### Preserve Directory Attributes

```bash
cp -a project archived_project
```

The `-a` option enables archive mode, preserving attributes and copying directories recursively.

### Create a Backup Before Overwriting

```bash
cp --backup=numbered file.txt copy.txt
```

Creates a numbered backup of an existing destination file before overwriting it.

## 📸 Project Screenshots

Add actual terminal screenshots showing the successful execution of each lab.

Suggested repository structure:

```text
linux-cp-command-project/
├── README.md
├── screenshots/
│   ├── lab01-basic-copy.png
│   ├── lab02-copy-rename.png
│   ├── lab03-copy-directory.png
│   ├── lab04-multiple-files.png
│   ├── lab05-recursive-copy.png
│   ├── lab06-preserve-attributes.png
│   ├── lab07-interactive-copy.png
│   └── lab08-verbose-copy.png
└── scripts/
    └── cp-practice.sh
```

## 📚 Key Takeaways

- `cp` copies files and directories.
- `cp -r` copies directories recursively.
- `cp -p` preserves supported file attributes.
- `cp -i` prompts before overwriting files.
- `cp -v` displays copy operations.
- `cp -u` copies files when the source is newer or the destination is missing.
- `cp -a` is useful for preserving directory structures and file attributes.

## 🚀 Skills Demonstrated

- Linux command-line operations
- File and directory management
- Recursive directory copying
- File backup fundamentals
- Linux permissions and ownership
- Bash command-line proficiency
- Basic system administration

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

**Building practical Linux skills one command at a time.**
