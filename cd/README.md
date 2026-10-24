🐧 **Linux Project 02: Mastering the `cd` Command**

Continuing my hands-on Linux learning journey!

In this project, I explored 8 practical ways to use the `cd` command, including navigating directories, switching between folders, using absolute and relative paths, and working with directory shortcuts.

💻 Building essential Linux skills for System Administration, IT Support, and Cybersecurity.

🔗 GitHub: https://github.com/farhan115

#Linux #LinuxCommands #Bash #RHCSA #SystemAdministration #Cybersecurity #HandsOnLearning

# 🐧 Linux Project 02: Mastering the `cd` Command

## 📌 Project Overview

This hands-on Linux project demonstrates how to use the `cd` (Change Directory) command to navigate the Linux filesystem efficiently.

The project covers 8 practical directory navigation techniques commonly used in Linux System Administration, IT Support, Cybersecurity, and Cloud Computing.

## 🎯 Project Objectives

- Navigate between Linux directories.
- Understand absolute and relative paths.
- Access home, parent, and root directories.
- Switch between previously visited directories.
- Navigate nested directory structures.
- Practice essential Linux command-line skills.

## 🛠️ Lab Environment

- **Operating System:** Linux (Ubuntu/RHEL or equivalent)
- **Interface:** Bash Terminal
- **Commands:** `cd`, `pwd`, `mkdir`, `ls`

## 💻 Hands-On Labs

### Lab 1: Navigate to a Specific Directory

```bash
cd Documents
pwd
```

**Purpose:** Move into the Documents directory and verify the current working directory.

### Lab 2: Navigate to the Home Directory

```bash
cd
pwd
```

**Purpose:** Return directly to the current user's home directory.

### Lab 3: Navigate to the Parent Directory

```bash
cd ..
pwd
```

**Purpose:** Move one directory level up.

### Lab 4: Navigate to the Root Directory

```bash
cd /
pwd
```

**Purpose:** Navigate to the root directory of the Linux filesystem.

### Lab 5: Return to the Previous Directory

```bash
cd /var
cd -
```

**Purpose:** Switch back to the previously visited working directory.

### Lab 6: Navigate to a Subdirectory

```bash
cd ~/Documents/Projects
pwd
```

**Purpose:** Navigate to a nested directory using a path relative to the home directory.

### Lab 7: Navigate Using an Absolute Path

```bash
cd /etc
pwd
```

**Purpose:** Navigate directly to a directory using its full filesystem path.

### Lab 8: Practice Directory Shortcuts

```bash
cd ~
cd ..
cd -
```

**Purpose:** Practice Linux directory navigation shortcuts.

## 🧪 Practice Environment Setup

Create a sample directory structure before completing the labs:

```bash
cd ~
mkdir -p Documents/Projects
mkdir -p Linux-Labs/Project02
ls
```

## 📸 Project Screenshots

Add terminal screenshots demonstrating the execution of each command.

Suggested screenshot structure:

```text
screenshots/
├── lab01-specific-directory.png
├── lab02-home-directory.png
├── lab03-parent-directory.png
├── lab04-root-directory.png
├── lab05-previous-directory.png
├── lab06-subdirectory.png
├── lab07-absolute-path.png
└── lab08-shortcuts.png
```

## 📚 Key Takeaways

- `cd` changes the current working directory.
- `cd ~` navigates to the home directory.
- `cd ..` moves to the parent directory.
- `cd /` navigates to the filesystem root.
- `cd -` returns to the previous working directory.
- Absolute paths start with `/`.
- Relative paths are interpreted from the current directory.

## 🚀 Skills Demonstrated

- Linux filesystem navigation
- Bash command-line proficiency
- Directory management
- Absolute and relative path navigation
- Linux administration fundamentals
- Terminal-based troubleshooting

## 🎓 Career Relevance

These skills provide a foundation for:

- Linux System Administrator
- IT Support Specialist
- Cybersecurity Analyst
- Cloud Support Engineer
- Identity and Access Management (IAM) Engineer

## 👨‍💻 Author

**Farhan Muntasir**

GitHub: https://github.com/farhan115

*Learning | Practicing | Documenting Linux Administration*

---

**Linux Project Series — Building practical Linux skills one command at a time.**
