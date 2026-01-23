# Git Initialization and First Commit
# Git, Shell Scripting, Docker & Streamlit

This repository contains **hands-on assignments** for mastering foundational DevOps tools:

- Git (Version Control)
- Shell Scripting
- Docker
- Streamlit + Docker + Git Capstone Project

Each section contains **definitions, objectives, commands, and examples** for practical understanding.

---

## 1. Git Learning Assignments

### 1.1 Foundational Concepts

#### Initialize and Commit

**Objective:** Learn to start a Git repository, track files, and commit changes.

**Steps & Commands:**

1. Create a new project directory:
mkdir MyProject
cd MyProject

2. Initialize Git repository:
git init

3. Create a README file:

nano README.md
# Assignment
This is my first Git assignment.

4.Check repository status:
git status

5. Stage the file for commit:
git add README.md
Definition: git add moves files from the working directory to the staging area.

6. Commit the changes:
git commit -m "Initial commit with README"
Definition: git commit creates a snapshot of staged changes in the repository.

# Branching and Merging

# Objective: Learn feature isolation and integration.

# Steps & Commands:

@Create a new feature branch:
git checkout -b feature-update


@Modify README.md:
echo "Added feature section" >> README.md
git add README.md
git commit -m "Updated README with feature section"


@Switch back to main branch:
git checkout main


@Merge feature branch:
git merge feature-update


@(Optional) Delete merged branch:

git branch -d feature-update

# Working with Remotes

# Objective: Sync local repo with GitHub.

# Steps & Commands:

# Create empty repo on GitHub (skip adding README).

@Add remote:
git remote add origin <remote_url>

@Push commits to remote:
git push -u origin main

@Pull changes made on GitHub:

git pull origin main

1.2 Intermediate Assignments
Handling Merge Conflicts

Scenario: Modify same line in two branches. Merge produces conflict.

Resolution Example:

git merge feature-conflict

# Conflict markers appear in README.md
# Resolve manually, then
git add README.md
git commit -m "Resolved merge conflict"

# Undoing Changes

Discard local changes in working directory:

git checkout -- README.md

Undo last commit but keep changes staged:

git reset --soft HEAD~1

Revert a commit already pushed:

git revert <commit_hash>

# Interactive Rebasing

Clean commit history before push:

git rebase -i HEAD~3


# Options:

pick → keep commit

squash → combine commits

reword → rename commit message

# 2. Shell Scripting Assignments
# Module 1: Getting Started with the Shell
pwd               # Print working directory
ls -l             # List files in current directory
mkdir demo        # Create directory
rm -rf demo       # Remove directory and files
cd ..             # Move up one directory

# Module 2: First Scripts

Hello World Script

#!/bin/bash
echo "Hello World"


Save as hello.sh and run:

chmod +x hello.sh
./hello.sh


System Info Script

#!/bin/bash
echo "Current Date: $(date)"
echo "Current User: $(whoami)"
echo "Hostname: $(hostname)"

# Module 3: Variables and User Input
#!/bin/bash
read -p "Enter your name: " name
echo "Hello, $name!"
read -p "Enter first number: " a
read -p "Enter second number: " b
echo "Sum: $((a + b))"

# Module 4: Conditional Statements
#!/bin/bash
file="README.md"
if [[ -f "$file" && -r "$file" ]]; then
    echo "$file exists and is readable"
else
    echo "$file missing or not readable"
fi

# Module 5: Loops

Count files in directory

#!/bin/bash
for f in *; do
    echo $f
done
Countdown

#!/bin/bash
for ((i=10; i>=1; i--)); do
    echo $i
done

# Module 6: Functions
#!/bin/bash
function sum() {
    echo "Sum: $(($1 + $2))"
}
sum 5 7

# Module 7: Text Processing
grep "ERROR" logfile.txt
awk '{print $1}' logfile.txt
sed 's/old/new/g' logfile.txt

# Module 8: Arrays
servers=("server1" "server2" "server3")
for server in "${servers[@]}"; do
    echo "Pinging $server..."
done

# Module 9: Error Handling & Debugging
#!/bin/bash
set -e  # exit on error
if ! ping -c 1 google.com; then
    echo "Network unreachable"
    exit 1
fi

# 3. Docker Assignments
# Docker Basics

# Definition: Docker is a containerization platform that allows apps to run in isolated environments. Unlike VMs, containers share the host OS kernel and are lightweight.

Commands:

docker --version
docker pull python:3.11
docker run -it python:3.11 /bin/bash
docker stop <container_id>
docker rm <container_id>


Dockerfile Example for Python App

FROM python:3.11
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]


Build and Run

docker build -t myapp .
docker run -p 8501:8501 myapp

# 4. Capstone Project: Streamlit + Docker + Git

Steps:

Create Git repo and initialize.

Build app.py:

import streamlit as st

st.title("Hello World App")
name = st.text_input("Enter your name")
if name:
    st.write(f"Hello {name}!")


Create requirements.txt:

streamlit


Dockerfile:

FROM python:3.11
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8501
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]


Build and run container:

docker build -t streamlit-app .
docker run -p 8501:8501 streamlit-app


Git Workflow:

git checkout -b dev
# make changes
git add .
git commit -m "Added interactive widget"
git checkout main
git merge dev
git tag v1.0
git push origin main --tags 
