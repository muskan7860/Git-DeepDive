# Git & GitHub Deep Dive
# Complete Beginner to Advanced DevOps Guide

---

# Introduction

Git is one of the most important tools in the DevOps world.

Almost every company uses Git for:
- source code management
- CI/CD pipelines
- Kubernetes manifests
- Infrastructure as Code
- Jenkins pipelines
- automation scripts
- collaboration

Without Git:
- tracking changes becomes difficult
- collaboration becomes risky
- rollback becomes nearly impossible

Git helps engineers:
- store history
- track changes
- collaborate safely
- revert mistakes
- manage versions

---

# What is Git?

Git is a Distributed Version Control System (DVCS).

Git tracks:
- file changes
- code history
- commits
- branches
- collaboration

Git allows multiple engineers to work safely on same project.

---

# What is Version Control?

Version control means:

```text
Managing different versions of files and tracking changes over time.
```

Example:
- Version 1
- Version 2
- Version 3

Git stores all versions internally.

---

# Why Git is Important

Without Git:
- files get overwritten
- no rollback possible
- teamwork becomes dangerous
- history gets lost

Git solves:
- collaboration problems
- rollback problems
- tracking problems
- deployment consistency

---

# What is GitHub?

GitHub is cloud platform used to host Git repositories online.

GitHub provides:
- remote repositories
- collaboration
- pull requests
- issue tracking
- CI/CD integrations
- automation workflows

---

# Difference Between Git and GitHub

| Git | GitHub |
|---|---|
| Local version control tool | Online hosting platform |
| Tracks changes | Stores repositories online |
| Command line tool | Web platform |
| Works offline | Requires internet |

---

# Install Git

Check Git version:

```bash
git --version
```

Example:

```text
git version 2.43.0
```

---

# Configure Git Username

```bash
git config --global user.name "muskan7860"
```

---

# Configure Git Email

```bash
git config --global user.email "muskanpatel914@gmail.com"
```

---

# Verify Configuration

```bash
git config --global --list
```

Output:

```text
user.name=muskan7860
user.email=muskanpatel914@gmail.com
```

---

# What Does --global Mean?

`--global` means:

```text
Apply configuration to all repositories for current user.
```

Configuration stored inside:

```text
~/.gitconfig
```

---

# Create Git Repository

```bash
mkdir git-project
cd git-project
```

---

# Initialize Git

```bash
git init
```

Output:

```text
Initialized empty Git repository
```

---

# What Happens Internally During git init

Git creates hidden directory:

```text
.git
```

Contains:
- commit history
- branches
- configurations
- metadata
- Git objects

---

# View Hidden Files

```bash
ls -la
```

---

# Create README File

```bash
touch README.md
```

---

# Check Git Status

```bash
git status
```

Shows:
- modified files
- staged files
- untracked files
- current branch

---

# Understanding Untracked Files

Example:

```text
Untracked files:
README.md
```

Meaning:

```text
Git sees file but is not tracking it yet.
```

---

# Add Files to Staging Area

```bash
git add .
```

Meaning:

```text
Track all current file changes.
```

---

# What is Staging Area?

Git has 3 major areas:

| Area | Purpose |
|---|---|
| Working Directory | current files |
| Staging Area | prepared changes |
| Repository | committed history |

---

# Commit Changes

```bash
git commit -m "Added README file"
```

---

# What is Commit?

Commit is snapshot of project at specific time.

Commit contains:
- changes
- timestamp
- author
- commit message
- unique ID

---

# Check Commit History

```bash
git log
```

Compact format:

```bash
git log --oneline
```

---

# Create GitHub Repository

Open:

https://github.com

Create repository:
- Git-DeepDive

---

# Add Remote Repository

```bash
git remote add origin https://github.com/muskan7860/Git-DeepDive.git
```

---

# What is origin?

`origin` is nickname for remote repository.

---

# Verify Remote

```bash
git remote -v
```

---

# Understanding Branches

Branch means:

```text
Independent line of development.
```

Default branch commonly:
- main

Older Git versions:
- master

---

# Check Current Branch

```bash
git branch
```

---

# Rename Branch to main

```bash
git branch -M main
```

---

# Push Code to GitHub

```bash
git push -u origin main
```

---

# Meaning of Push Command

| Part | Meaning |
|---|---|
| git push | upload commits |
| -u | set upstream tracking |
| origin | remote repository |
| main | branch name |

---

# Pull Latest Changes

```bash
git pull
```

Downloads latest remote changes.

---

# Difference Between Pull and Push

| Command | Purpose |
|---|---|
| git pull | download changes |
| git push | upload changes |

---

# Clone Repository

```bash
git clone https://github.com/USERNAME/REPO.git
```

---

# Git Credential Configuration

To avoid entering credentials repeatedly:

```bash
git config --global credential.helper store
```

---

# What Happens Internally

Git stores credentials inside:

```text
~/.git-credentials
```

---

# Important GitHub Authentication Understanding

GitHub no longer accepts account password for Git operations.

Instead use:
- Personal Access Token (PAT)

---

# Create GitHub Token

Open:

https://github.com/settings/tokens

Steps:
- Generate token
- Select repo permissions
- Copy token

---

# During Push

Git asks:

```text
Username:
Password:
```

Use:

| Field | Value |
|---|---|
| Username | GitHub username |
| Password | Personal Access Token |

NOT GitHub account password.

---

# Common Errors and Fixes

---

# ERROR 1
# src refspec main does not match any

Error:

```text
error: src refspec main does not match any
```

---

# Cause

Local branch is:
- master

But pushing:
- main

---

# Check Current Branch

```bash
git branch
```

---

# Fix Option 1

Push master:

```bash
git push -u origin master
```

---

# Fix Option 2 (Recommended)

Rename branch:

```bash
git branch -M main
```

Then:

```bash
git push -u origin main
```

---

# ERROR 2
# remote origin already exists

Cause:
- remote already configured

---

# Check Existing Remote

```bash
git remote -v
```

---

# Fix

Remove old remote:

```bash
git remote remove origin
```

Add again:

```bash
git remote add origin REPO_URL
```

---

# ERROR 3
# failed to push some refs

Error:

```text
failed to push some refs
```

---

# Cause

Remote repository contains commits not available locally.

---

# Fix

```bash
git pull origin main --allow-unrelated-histories --no-rebase
```

Then:

```bash
git push
```

---

# ERROR 4
# non-fast-forward

Meaning:

```text
Remote branch ahead of local branch.
```

Git blocks overwrite for safety.

---

# Fix

```bash
git pull
git push
```

---

# ERROR 5
# divergent branches

Meaning:

```text
Local and remote histories differ.
```

---

# Fix

```bash
git pull origin main --allow-unrelated-histories --no-rebase
```

---

# ERROR 6
# Authentication failed

Cause:
- wrong password
- GitHub password used instead of token

---

# Fix

Use:
- Personal Access Token

NOT:
- GitHub account password

---

# ERROR 7
# Permission denied (publickey)

Cause:
- SSH authentication issue

---

# Fix

Either:
- configure SSH keys
OR
- use HTTPS remote URL

---

# ERROR 8
# nothing to commit, working tree clean

Meaning:

```text
No new file changes detected.
```

Not an error.

---

# ERROR 9
# Vim Editor Opens During Merge

Example:

```text
Merge branch 'main'
```

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

---

# Undo Last Commit

Keep changes:

```bash
git reset --soft HEAD~1
```

Delete changes:

```bash
git reset --hard HEAD~1
```

WARNING:

```text
--hard permanently deletes changes.
```

---

# View File Differences

```bash
git diff
```

---

# Real DevOps Usage of Git

Git used for:
- Kubernetes YAML
- Terraform
- Helm charts
- Jenkinsfiles
- Dockerfiles
- CI/CD pipelines
- Shell scripts
- Ansible playbooks

---

# Production Best Practices

- commit frequently
- use meaningful commit messages
- pull before push
- avoid committing secrets
- use branches properly
- review changes before pushing

---

# Security Best Practices

Never commit:
- passwords
- API keys
- private keys
- secrets

Use:
- .gitignore
- vaults
- secret managers

---

# Important Interview Questions

## What is Git?

Distributed version control system.

---

## What is GitHub?

Cloud platform hosting Git repositories.

---

## Difference Between Git and GitHub?

Git:
- version control software

GitHub:
- repository hosting platform

---

## What is Commit?

Snapshot of project at specific point in time.

---

## What is Branch?

Independent line of development.

---

## Difference Between git pull and git fetch?

git fetch:
- downloads changes only

git pull:
- downloads + merges changes

---

## What is Merge Conflict?

When Git cannot automatically combine changes.

---

# Final Understanding

Git is backbone of:
- DevOps
- CI/CD
- Infrastructure as Code
- Cloud Engineering
- Platform Engineering
- Modern Software Development

Strong Git knowledge is mandatory for:
- DevOps engineers
- Linux administrators
- SRE engineers
- Platform engineers
- Cloud engineers
