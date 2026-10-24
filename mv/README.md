# 🐧 Linux Project 07: Mastering the `mv` Command

## 📌 Project Overview

This hands-on Linux project demonstrates how to use the `mv` (Move) command to move, rename, and organize files and directories in Linux.

The project includes **8 practical labs** covering file management, directory operations, safe overwriting, and backup techniques.

**Project Goal:** Develop practical Linux command-line skills applicable to System Administration, IT Support, Cybersecurity, Cloud Computing, and Automation.

## 🎯 Project Objectives

- Move files between directories.
- Rename files using the Linux terminal.
- Move multiple files simultaneously.
- Move directories and their contents.
- Prevent accidental file overwriting.
- Create backups before replacing existing files.
- Understand interactive and verbose command options.

## 🛠️ Lab Environment

- **Operating System:** Ubuntu Linux / Red Hat Enterprise Linux
- **Terminal:** Bash
- **Commands:** `mv`, `ls`, `mkdir`, `touch`, `echo`
- **Skill Level:** Beginner

## 🧪 Lab Setup

Create a practice environment before starting the exercises.

```bash
mkdir -p ~/linux-mv-lab/{Documents,Backups,Archives,Projects}
cd ~/linux-mv-lab

echo "Linux Project" > file.txt
echo "Original File" > old.txt
echo "First File" > file1.txt
echo "Second File" > file2.txt
echo "Existing Backup" > backup.txt

ls -l
```

**Note:** Some labs move or rename the original files. Recreate the necessary files before each lab if you are completing the exercises sequentially.

## 💻 Hands-On Labs

### Lab 1: Move a File

**Objective:** Move a file from the current directory to another directory.

```bash
mv file.txt Documents/
ls Documents/
```

Expected output:

```text
file.txt
```

**Explanation:** The `mv` command moves `file.txt` into the Documents directory. The file no longer exists in its original location.

### Lab 2: Rename a File

**Objective:** Rename a file without changing its directory.

```bash
mv old.txt new.txt
ls -l new.txt
```

**Explanation:** The file `old.txt` is renamed to `new.txt`.

### Lab 3: Move Multiple Files

**Objective:** Move multiple files into one destination directory.

```bash
mv file1.txt file2.txt Backups/
ls Backups/
```

Expected output:

```text
file1.txt  file2.txt
```

**Explanation:** Both files are moved into the Backups directory.

### Lab 4: Move a Directory

**Objective:** Move an entire directory and its contents.

```bash
touch Projects/project.txt
mv Projects/ Archives/
ls Archives/
ls Archives/Projects/
```

Expected output from the final command:

```text
project.txt
```

**Explanation:** The Projects directory, including its contents, is moved inside Archives.

Unlike `cp`, the `mv` command does not require the `-r` option to move directories.

### Lab 5: Interactive Move — Prevent Accidental Overwriting

**Objective:** Request confirmation before replacing an existing file.

```bash
echo "Updated File" > file.txt
mv -i file.txt backup.txt
```

Example prompt:

```text
mv: overwrite 'backup.txt'?
```

Enter `y` to overwrite or `n` to cancel.

**Explanation:** The `-i` option requests confirmation before overwriting an existing destination file.

### Lab 6: Move Without Overwriting

**Objective:** Protect an existing destination file.

```bash
echo "New Data" > file.txt
mv -n file.txt backup.txt
ls -l file.txt backup.txt
```

**Explanation:** The `-n` option prevents overwriting an existing destination file.

If `backup.txt` already exists, the move is skipped and both files remain.

### Lab 7: Verbose Move — Display Operation Details

**Objective:** Display information about the move operation.

```bash
mv -v file.txt Documents/
```

Example output:

```text
renamed 'file.txt' -> 'Documents/file.txt'
```

**Explanation:** The `-v` option displays the source and destination of the move operation.

### Lab 8: Create a Backup Before Overwriting

**Objective:** Back up an existing destination file before replacing it.

```bash
echo "New Version" > file.txt
mv -b file.txt backup.txt
ls -l backup.txt*
```

Expected files:

```text
backup.txt
backup.txt~
```

**Explanation:** On GNU/Linux, `mv -b` creates a backup of the existing destination before overwriting it. By default, the backup filename uses a `~` suffix.

## 🔬 Additional Practice

### Move Only When the Source Is Newer

```bash
mv -u file.txt backup.txt
```

Moves the source when the destination is missing or older, using the standard GNU `mv -u` behavior.

### Move Files Using Wildcards

```bash
mv *.txt Documents/
```

Moves all matching `.txt` files from the current directory into Documents.

### Create Numbered Backups

```bash
mv --backup=numbered file.txt backup.txt
```

Creates numbered backups when an existing destination must be replaced.

### Rename a Directory

```bash
mkdir OldFolder
mv OldFolder NewFolder
```

Renames `OldFolder` to `NewFolder` when `NewFolder` does not already exist.

## 📸 Project Screenshots

Add actual screenshots of the completed terminal exercises.

Recommended repository structure:

```text
linux-mv-command-project/
├── README.md
├── screenshots/
│   ├── lab01-move-file.png
│   ├── lab02-rename-file.png
│   ├── lab03-multiple-files.png
│   ├── lab04-move-directory.png
│   ├── lab05-interactive-move.png
│   ├── lab06-no-overwrite.png
│   ├── lab07-verbose-move.png
│   └── lab08-backup-before-overwrite.png
└── scripts/
    └── mv-practice.sh
```

## 📚 Key Takeaways

- `mv` moves and renames files and directories.
- `mv -i` prompts before overwriting existing files.
- `mv -n` prevents overwriting existing destination files.
- `mv -v` displays operation details.
- `mv -b` creates a backup before overwriting.
- `mv -u` supports update-based moves.
- Wildcards allow multiple files to be moved efficiently.
- Moving files may replace existing data, so destination paths should always be verified.

## 🚀 Skills Demonstrated

- Linux command-line proficiency
- File and directory management
- File organization and renaming
- Safe file operations
- Backup management
- Linux filesystem navigation
- Bash command-line fundamentals

## 🎓 Career Relevance

These skills are useful for:

- Linux System Administrator
- IT Support Specialist
- Cybersecurity Analyst
- Cloud Support Engineer
- IAM Engineer
- DevOps Engineer

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

**Building practical Linux skills one command at a time.**
