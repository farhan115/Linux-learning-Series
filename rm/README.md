# 🐧 Linux Project 08: Mastering the `rm` Command

## 📌 Project Overview

This hands-on Linux project demonstrates how to use the `rm` (Remove) command to delete files and directories safely and efficiently.

The project covers **8 practical labs**, including file deletion, recursive directory removal, interactive confirmation, forced deletion, and wildcard-based file management.

**Project Goal:** Develop practical Linux administration skills while understanding safe file deletion and filesystem management.

## 🎯 Project Objectives

- Delete individual files and multiple files.
- Remove directories and their contents.
- Understand recursive file deletion.
- Use interactive confirmation to prevent accidental deletion.
- Display detailed information about deletion operations.
- Understand forced deletion.
- Remove files using wildcard patterns.
- Follow safe Linux file management practices.

## 🛠️ Lab Environment

- **Operating System:** Ubuntu Linux / Red Hat Enterprise Linux
- **Terminal:** Bash
- **Commands:** `rm`, `ls`, `mkdir`, `touch`, `echo`, `pwd`
- **Skill Level:** Beginner

## 🧪 Lab Setup

Create a dedicated practice environment before starting.

```bash
mkdir -p ~/linux-rm-lab/{Documents,Backups,Logs,folder}
cd ~/linux-rm-lab

touch file.txt file1.txt file2.txt
touch Logs/app.log Logs/error.log
touch folder/test.txt

pwd
ls -R
```

**Safety Warning:** The `rm` command normally deletes files permanently without moving them to a recycle bin. Perform these exercises only in your practice directory. Avoid using `sudo` or deleting unfamiliar system files.

Some labs delete the same sample files. Recreate the necessary files before repeating an exercise.

---

## 💻 Hands-On Labs

### Lab 1: Delete a Single File

**Objective:** Remove a file from the current directory.

```bash
rm file.txt
ls
```

**Explanation:** The `rm` command removes the specified file.

**Expected Result:** `file.txt` no longer appears in the directory.

### Lab 2: Delete Multiple Files

**Objective:** Remove multiple files using one command.

```bash
rm file1.txt file2.txt
ls
```

**Explanation:** Multiple filenames can be supplied as arguments to `rm`.

**Expected Result:** Both `file1.txt` and `file2.txt` are deleted.

### Lab 3: Interactive File Deletion

**Objective:** Request confirmation before deleting a file.

```bash
touch file.txt
rm -i file.txt
```

Example prompt:

```text
rm: remove regular empty file 'file.txt'?
```

Enter `y` to confirm or `n` to cancel.

**Explanation:** The `-i` option prompts for confirmation before removal.

### Lab 4: Verbose File Deletion

**Objective:** Display details about the deletion operation.

```bash
touch file.txt
rm -v file.txt
```

Example output:

```text
removed 'file.txt'
```

**Explanation:** The `-v` option displays the names of files as they are removed.

### Lab 5: Delete a Directory Recursively

**Objective:** Remove a directory and everything inside it.

```bash
mkdir -p folder
touch folder/test.txt

rm -r folder/
ls
```

**Explanation:** The `-r` option recursively removes a directory, including its files and subdirectories.

**Expected Result:** The `folder` directory and its contents are removed.

### Lab 6: Interactive Recursive Directory Deletion

**Objective:** Confirm deletions while removing a directory recursively.

```bash
mkdir -p folder
touch folder/test.txt

rm -ri folder/
```

Example prompts:

```text
rm: descend into directory 'folder/'?
rm: remove regular empty file 'folder/test.txt'?
rm: remove directory 'folder/'?
```

**Explanation:** Combining `-r` and `-i` enables recursive deletion with interactive confirmation.

### Lab 7: Force File Deletion

**Objective:** Understand the force option.

```bash
touch file.txt
rm -f file.txt
ls
```

**Explanation:** The `-f` option suppresses confirmation prompts and ignores nonexistent files. It does not override every filesystem permission restriction.

**Important:** Use force deletion carefully because it can remove files without warning.

### Lab 8: Delete Files Using Wildcards

**Objective:** Delete multiple files matching a filename pattern.

```bash
cd ~/linux-rm-lab/Logs

ls *.log
rm -- *.log
ls
```

**Explanation:** The `*.log` pattern matches filenames ending in `.log` in the current directory. The `--` marks the end of command options, protecting against filenames beginning with a hyphen.

**Expected Result:** Matching `.log` files are deleted from the Logs directory.

---

## 🔬 Additional Practice

### Remove an Empty Directory

```bash
mkdir empty-folder
rmdir empty-folder
```

`rmdir` removes empty directories without recursively deleting their contents.

### Confirm Before Removing Every File

```bash
touch example.txt
rm -i example.txt
```

### Preview Files Before Deleting

```bash
ls -l *.log
```

Always review matching files before running a deletion command.

### Remove a Directory Interactively

```bash
mkdir -p test-folder
touch test-folder/sample.txt
rm -ri test-folder/
```

This allows you to review deletion prompts before proceeding.

## 📸 Project Screenshots

Add screenshots of the actual terminal commands and results.

Suggested GitHub repository structure:

```text
linux-rm-command-project/
├── README.md
├── screenshots/
│   ├── lab01-delete-file.png
│   ├── lab02-delete-multiple-files.png
│   ├── lab03-interactive-delete.png
│   ├── lab04-verbose-delete.png
│   ├── lab05-recursive-delete.png
│   ├── lab06-interactive-directory-delete.png
│   ├── lab07-force-delete.png
│   └── lab08-wildcard-delete.png
└── scripts/
    └── rm-practice.sh
```

## 📚 Key Takeaways

- `rm` removes files from the filesystem.
- `rm -i` requests confirmation before deletion.
- `rm -v` displays deletion details.
- `rm -r` removes directories recursively.
- `rm -ri` combines recursive removal with interactive confirmation.
- `rm -f` suppresses prompts and ignores nonexistent files.
- Wildcards allow multiple matching files to be deleted.
- `rmdir` is useful for removing empty directories.
- Always verify paths and filenames before deleting data.

## 🚀 Skills Demonstrated

- Linux command-line proficiency
- File and directory management
- Recursive filesystem operations
- Interactive command execution
- Wildcard pattern matching
- Safe file deletion practices
- Linux administration fundamentals
- Bash terminal operations

## 🎓 Career Relevance

These skills are applicable to:

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
| 08 | `rm` | Removing Files and Directories |

**Building practical Linux skills one command at a time.**
