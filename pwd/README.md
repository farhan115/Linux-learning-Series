# 🐧 Linux Project 03: Mastering the `pwd` Command

## 📌 Project Overview

This hands-on Linux project explores the `pwd` (Print Working Directory) command, which displays the absolute path of the current working directory.

The project demonstrates 8 practical exercises covering directory navigation, logical and physical paths, environment variables, and filesystem troubleshooting.

**Project Goal:** Build foundational Linux command-line skills for System Administration, IT Support, Cybersecurity, and Cloud Computing.

## 🎯 Project Objectives

- Understand the purpose of the `pwd` command.
- Display and verify the current working directory.
- Navigate directories using `cd` and `pwd`.
- Understand logical versus physical directory paths.
- Explore the `$PWD` environment variable.
- Resolve absolute filesystem paths.

## 🛠️ Lab Environment

- **Operating System:** Ubuntu Linux / Red Hat Enterprise Linux
- **Terminal:** Bash
- **Commands:** `pwd`, `cd`, `mkdir`, `echo`, `readlink`

## 💻 Hands-On Labs

### Lab 1: Basic `pwd` Command

**Objective:** Display the current working directory.

```bash
pwd
```

Example output:

```text
/home/farhan
```

**Explanation:** The command prints the absolute path of the current directory.

### Lab 2: Verify Directory Changes

**Objective:** Confirm the current directory after navigation.

```bash
cd /etc
pwd
```

Expected output:

```text
/etc
```

**Explanation:** `pwd` confirms that the current working directory has changed to `/etc`.

### Lab 3: Display the Home Directory Path

**Objective:** Navigate to the home directory and verify its location.

```bash
cd ~
pwd
```

Example output:

```text
/home/farhan
```

**Explanation:** `cd ~` moves to the user's home directory, and `pwd` displays its absolute path.

### Lab 4: Display the Parent Directory Path

**Objective:** Navigate one directory level up.

```bash
cd ~/Documents
cd ..
pwd
```

Example output:

```text
/home/farhan
```

**Explanation:** `cd ..` navigates to the parent directory.

### Lab 5: Display the Logical Directory Path

**Objective:** Understand logical filesystem paths.

```bash
pwd -L
```

Example output:

```text
/home/farhan/Projects
```

**Explanation:** `pwd -L` displays the logical path, which can preserve symbolic-link components.

### Lab 6: Display the Physical Directory Path

**Objective:** Resolve symbolic links in the current directory path.

```bash
pwd -P
```

Example output:

```text
/home/farhan/projects
```

**Explanation:** `pwd -P` displays the physical directory path with symbolic links resolved.

**Note:** The output of `pwd -L` and `pwd -P` may be identical when the directory path contains no symbolic links.

### Lab 7: Display the `$PWD` Environment Variable

**Objective:** Retrieve the current working directory using an environment variable.

```bash
echo "$PWD"
```

Example output:

```text
/home/farhan
```

**Explanation:** Bash maintains the `PWD` variable to track the current working directory.

### Lab 8: Resolve the Full Physical Path

**Objective:** Determine the canonical path of the current directory.

```bash
readlink -f .
```

Example output:

```text
/home/farhan
```

**Explanation:** `readlink -f .` resolves symbolic links and prints the canonical absolute path on Linux systems with GNU `readlink`.

## 🧪 Additional Practice: Logical vs. Physical Paths

Create a symbolic link to demonstrate the difference between `pwd -L` and `pwd -P`.

```bash
cd ~
mkdir -p linux-lab/projects
ln -sfn "$HOME/linux-lab/projects" "$HOME/project-link"

cd ~/project-link

pwd -L
pwd -P
```

Example output:

```text
/home/farhan/project-link
/home/farhan/linux-lab/projects
```

This exercise demonstrates how Linux handles symbolic links during directory navigation.

## 📸 Project Screenshots

Suggested repository structure:

```text
linux-pwd-command-project/
├── README.md
└── screenshots/
    ├── lab01-basic-pwd.png
    ├── lab02-directory-change.png
    ├── lab03-home-directory.png
    ├── lab04-parent-directory.png
    ├── lab05-logical-path.png
    ├── lab06-physical-path.png
    ├── lab07-pwd-variable.png
    └── lab08-readlink.png
```

Add your actual terminal screenshots to document each completed lab.

## 📚 Key Takeaways

- `pwd` displays the current working directory.
- `pwd -L` displays the logical directory path.
- `pwd -P` displays the physical directory path.
- `$PWD` stores the current working directory in Bash.
- `readlink -f .` resolves the canonical directory path.
- Combining `pwd` with `cd` improves filesystem navigation and troubleshooting.

## 🚀 Skills Demonstrated

- Linux command-line proficiency
- Filesystem navigation
- Absolute and relative path understanding
- Symbolic-link troubleshooting
- Bash environment variables
- Linux system administration fundamentals

## 🎓 Career Relevance

These skills are useful for:

- Linux System Administrator
- IT Support Specialist
- Cybersecurity Analyst
- Cloud Support Engineer
- IAM Engineer

## 👨‍💻 Author

**Farhan Muntasir**

GitHub: https://github.com/farhan115

*Linux Administration | IT Support | Cybersecurity | IAM*

---

**Linux Project Series**

- Project 01: `ls` — Listing Files and Directories
- Project 02: `cd` — Directory Navigation
- Project 03: `pwd` — Print Working Directory

*Building practical Linux skills one command at a time.*
