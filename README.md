# Git & GitHub Complete Troubleshooting Guide

# Beginner to DevOps Engineer Level Documentation

---

# Introduction

Git and GitHub are the backbone of modern DevOps, software development, CI/CD pipelines, and infrastructure automation.

Every DevOps engineer uses Git daily for:

* source code management
* version control
* infrastructure as code
* Kubernetes manifests
* Jenkins pipelines
* automation scripts
* team collaboration

This guide covers:

* Git basics
* GitHub configuration
* authentication setup
* push/pull workflow
* common errors
* troubleshooting
* production-level understanding

Goal:

* Teach absolute beginners
* Explain internal Git behavior
* Build interview-level understanding
* Solve real-world Git issues

---

# What is Git?

Git is a distributed version control system.

Git tracks:

* file changes
* code history
* commits
* collaboration
* versions

Git helps developers:

* revert changes
* collaborate safely
* maintain project history
* prevent data loss

---

# What is GitHub?

GitHub is a cloud platform used to host Git repositories.

GitHub provides:

* remote repository hosting
* collaboration
* CI/CD integrations
* pull requests
* code review
* issue tracking

---

# Difference Between Git and GitHub

| Git                  | GitHub                 |
| -------------------- | ---------------------- |
| Version control tool | Cloud hosting platform |
| Works locally        | Works online           |
| Tracks changes       | Stores repositories    |
| CLI software         | Web platform           |

---

# Install Git

Check Git version:

```bash
git --version
```

Example output:

```text
git version 2.43.0
```

---

# Configure Git Username and Email

## Set Username

```bash
git config --global user.name "muskan7860"
```

---

## Set Email

```bash
git config --global user.email "muskanpatel914@gmail.com"
```

---

## Verify Configuration

```bash
git config --global --list
```

Example output:

```text
user.name=muskan7860
user.email=muskanpatel914@gmail.com
```

---

# What Does --global Mean?

`--global` means:

```text
Apply configuration for all repositories of current user.
```

Configuration stored inside:

```text
~/.gitconfig
```

---

# Create Project Directory

```bash
mkdir shell-scripting
cd shell-scripting
```

---

# Initialize Git Repository

```bash
git init
```

Output:

```text
Initialized empty Git repository
```

---

# What Happens Internally During git init

Git creates hidden folder:

```text
.git
```

This contains:

* commit history
* branches
* objects
* metadata
* configurations

---

# Check Hidden Files

```bash
ls -la
```

---

# Create README File

```bash
touch README.md
```

---

# Add Files to Git Staging Area

```bash
git add .
```

Meaning:

```text
Track all current file changes.
```

---

# What is Staging Area?

Git has 3 areas:

| Area              | Purpose           |
| ----------------- | ----------------- |
| Working Directory | current files     |
| Staging Area      | prepared changes  |
| Repository        | committed history |

---

# Commit Changes

```bash
git commit -m "Added Day 01 notes"
```

---

# What is Commit?

Commit is:

```text
Snapshot of project at specific point in time.
```

Each commit has:

* unique ID
* author
* timestamp
* message

---

# Create GitHub Repository

Open:

[https://github.com](https://github.com)

Create repository:

Example:

```text
DeepDive_Shell_Script
```

---

# Connect Local Repo to GitHub

```bash
git remote add origin https://github.com/muskan7860/DeepDive_Shell_Script.git
```

---

# What is origin?

`origin` is nickname for remote repository.

Check remote:

```bash
git remote -v
```

---

# Push Code to GitHub

```bash
git push -u origin main
```

---

# Meaning of Push Command

| Part     | Meaning               |
| -------- | --------------------- |
| git push | upload commits        |
| -u       | set upstream tracking |
| origin   | remote repository     |
| main     | branch                |

---

# Configure Credential Storage

To avoid entering username/password every time:

```bash
git config --global credential.helper store
```

---

# What Does Credential Helper Do?

Git stores credentials locally.

Stored inside:

```text
~/.git-credentials
```

---

# Important GitHub Authentication Note

GitHub no longer accepts account password for Git operations.

Instead use:

```text
Personal Access Token (PAT)
```

---

# Create GitHub Token

Open:

[https://github.com/settings/tokens](https://github.com/settings/tokens)

Steps:

* Generate new token
* Select repo permission
* Generate token
* Copy token

---

# Use Token as Password

During push:

```text
Username: muskan7860
Password: <paste token>
```

NOT GitHub account password.

---

# Daily Git Workflow

```bash
git pull

git add .

git commit -m "Added Day 02 variables"

git push
```

---

# Common Git Errors and Fixes

---

# ERROR 1

# Permission Denied While Creating Directory

Error:

```text
mkdir: cannot create directory: Permission denied
```

Cause:

Trying to create directory inside protected location.

Example:

```bash
mkdir /home/shell-scripting
```

---

# Fix

Use home directory:

```bash
cd ~
mkdir shell-scripting
```

---

# ERROR 2

# bash: ./script.sh: Permission denied

Cause:

Script lacks execute permission.

---

# Fix

```bash
chmod +x script.sh
```

Then:

```bash
./script.sh
```

---

# Why Execute Permission Needed?

Linux needs execute permission to run file as program.

Without execute permission:

* treated as normal text file

---

# ERROR 3

# command not found in Variables

Example:

```bash
name = Muskan
```

Error:

```text
command not found
```

---

# Cause

Spaces around '='.

Bash interprets:

| Part   | Meaning  |
| ------ | -------- |
| name   | command  |
| =      | argument |
| Muskan | argument |

---

# Fix

Correct syntax:

```bash
name="Muskan"
```

---

# ERROR 4

# Variable Not Printing

Example:

```bash
Last_Name="Patel"
echo $Last_name
```

---

# Cause

Bash variables are case-sensitive.

Different:

```text
Last_Name
Last_name
```

---

# Fix

Use exact variable name:

```bash
echo $Last_Name
```

---

# ERROR 5

# Newline Not Working

Example:

```bash
echo "Hello\nWorld"
```

---

# Cause

Default echo does not interpret escape characters.

---

# Fix

```bash
echo -e "Hello\nWorld"
```

---

# ERROR 6

# Push Rejected (fetch first)

Error:

```text
! [rejected] main -> main (fetch first)
```

---

# Cause

Remote repository contains commits not present locally.

Usually happens when:

* README created on GitHub
* another user pushed changes
* repository histories differ

---

# Fix

```bash
git pull origin main --allow-unrelated-histories --no-rebase
```

Then:

```bash
git push -u origin main
```

---

# ERROR 7

# divergent branches

Error:

```text
Need to specify how to reconcile divergent branches
```

---

# Meaning

Local and remote repositories both contain separate commits.

Git asks:

```text
How should histories be combined?
```

---

# Fix

```bash
git pull origin main --allow-unrelated-histories --no-rebase
```

---

# ERROR 8

# non-fast-forward

Error:

```text
non-fast-forward
```

---

# Meaning

Remote branch is ahead of local branch.

Git blocks push to prevent overwriting remote history.

---

# Fix

First pull latest changes:

```bash
git pull origin main --allow-unrelated-histories --no-rebase
```

Then push:

```bash
git push
```

---

# ERROR 9

# fatal: 'main' does not appear to be a git repository

Cause:

Wrong command:

```bash
git push main
```

Git interprets:

* main as remote repository name

---

# Correct Command

```bash
git push origin main
```

---

# ERROR 10

# Vim Editor Opens During Merge

Example screen:

```text
Merge branch 'main'
```

---

# Why It Happens

Git opens editor for merge commit message.

---

# Fix

Press:

```text
ESC
```

Then type:

```text
:wq
```

Press Enter.

Meaning:

| Command | Meaning    |
| ------- | ---------- |
| w       | write/save |
| q       | quit       |

---

# Git Branch Understanding

Branch means:

```text
Independent line of development.
```

Default branch usually:

```text
main
```

---

# Check Current Branch

```bash
git branch
```

---

# Check Git Status

```bash
git status
```

Very important troubleshooting command.

Shows:

* modified files
* staged files
* untracked files
* branch information

---

# View Commit History

```bash
git log
```

Compact view:

```bash
git log --oneline
```

---

# Undo Last Commit

Keep changes:

```bash
git reset --soft HEAD~1
```

Remove changes:

```bash
git reset --hard HEAD~1
```

WARNING:

```text
--hard permanently deletes changes.
```

---

# Clone Existing Repository

```bash
git clone https://github.com/USERNAME/REPO.git
```

---

# Pull Latest Changes

```bash
git pull
```

Downloads latest remote changes.

---

# Difference Between Pull and Push

| Command  | Purpose          |
| -------- | ---------------- |
| git pull | download changes |
| git push | upload changes   |

---

# Real DevOps Usage of Git

Git used for:

* Kubernetes YAML
* Jenkins pipelines
* Dockerfiles
* Terraform
* Helm charts
* Shell scripts
* CI/CD pipelines

---

# Production Best Practices

* commit frequently
* write meaningful commit messages
* pull before push
* never hardcode secrets
* use branches properly
* review code before merging

---

# Security Best Practices

Never commit:

* passwords
* API keys
* tokens
* private keys

Use:

* .gitignore
* secret managers
* vault systems

---

# Important Interview Questions

## What is Git?

Distributed version control system.

---

## Difference between Git and GitHub?

Git:

* version control tool

GitHub:

* cloud hosting platform for Git repositories

---

## What is Commit?

Snapshot of project at specific time.

---

## What is Branch?

Independent line of development.

---

## Difference Between Pull and Push?

Pull:

* download remote changes

Push:

* upload local changes

---

## What is Merge Conflict?

When Git cannot automatically combine changes.

---

# Final Understanding

Git is not just a tool.

Git is:

* collaboration system
* version tracking engine
* DevOps backbone
* infrastructure management tool
* CI/CD foundation

Strong Git knowledge is mandatory for:

* DevOps engineers
* Linux administrators
* Cloud engineers
* SRE engineers
* Platform engineers
* Software developers

