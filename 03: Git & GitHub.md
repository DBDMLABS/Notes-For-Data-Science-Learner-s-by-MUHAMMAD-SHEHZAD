# Git and GitHub

---

Used by developers to **control versions** and collaborate on the same project.

## Table of Contents

* [Git Commands](#git-commands)
* [Setup](#setup)
* [Git 3-Stage Workflow](#git-3-stage-workflow)
* [Initialize Repository](#initialize-repository)
* [See Changes & History](#see-changes--history)
* [.gitignore & .gitkeep](#gitignore--gitkeep)
* [Unstaging & Restore](#unstaging--restore)
* [Undo Commits](#undo-commits)
* [Revert Commit](#revert-commit)
* [Branching](#branching)
* [Merging Branches](#merging-branches)
* [Merge Conflicts](#merge-conflicts)
* [Remote Repository](#remote-repository)
* [Clone Repository](#clone-repository)
* [Push & Pull](#push--pull)
* [Fetch](#fetch)
* [Stash](#stash)
* [Tags](#tags)
* [Basic GitHub Workflow](#basic-github-workflow)

---

## Git Commands

### Setup

> Check Git version:

```bash
git --version
```

### Configure User Details

```bash
git config --global user.name "User Name"
git config --global user.email "user@email.com"
```

> Check configuration:

```bash
git config --list
```

---

## Git 3-Stage Workflow

**Working Directory → Staging Area → Repository**

> Check status:

```bash
git status
```

### Add to Staging

> Specific file:

```bash
git add file_name.txt
```

> All files:

```bash
git add .
```

> Multiple files:

```bash
git add file1.txt file2.txt
```

> Check status again:

```bash
git status
```

### Commit

> Specific staged changes:

```bash
git commit -m "Your message"
```

---

## Initialize Repository

> Create folder:

```bash
mkdir dbdm-project
```

> Enter folder:

```bash
cd dbdm-project
```

> Initialize Git:

```bash
git init
```

---

## See Changes & History

> See changes:

```bash
git diff
```

> Commit history:

```bash
git log
```

> Compact history:

```bash
git log --oneline
```

> See branches with commits:

```bash
git log --oneline --all --graph
```

---

## .gitignore & .gitkeep

### .gitignore

> Create a file named:

```text
.gitignore
```

> Examples:

```text
file_name.txt
folder/
*.log
temp*
!important.log
```

> Add `.gitignore`:

```bash
git add .gitignore
```

### .gitkeep

> `.gitkeep` is used to keep an empty folder in Git.

```bash
mkdir uploads
touch uploads/.gitkeep
git add uploads/.gitkeep
```

---

## Unstaging & Restore

> Remove specific file from staging:

```bash
git restore --staged file_name.txt
```

> Remove all files from staging:

```bash
git restore --staged .
```

> Discard changes in a file and restore last committed version:

```bash
git restore file_name.txt
```

> **Warning:** This permanently discards the uncommitted changes in that file.

---

## Undo Commits

### Soft Reset

> Undo last commit and keep changes **staged**:

```bash
git reset --soft HEAD~1
```

### Mixed Reset

> Undo last commit and keep changes **unstaged**:

```bash
git reset HEAD~1
```

### Hard Reset

> Undo last commit and delete uncommitted changes:

```bash
git reset --hard HEAD~1
```

> Hard reset can permanently delete work.

---

## Revert Commit

> Safely undo a specific commit by creating a new commit:

```bash
git revert commit_code
```

> To see commit code:

```bash
git log --oneline
```

---

## Branching

> Create branch:

```bash
git branch branch_name
```

> Switch branch:

```bash
git switch branch_name
```

> Create + switch:

```bash
git switch -c branch_name
```

> Check branches:

```bash
git branch
```

> Switch to main:

```bash
git switch main
```

> Delete branch:

```bash
git branch -d branch_name
```

> Force delete:

```bash
git branch -D branch_name
```
---

## Merging Branches

> Switch to the branch that will receive changes:

```bash
git switch main
```

> Merge another branch:

```bash
git merge branch_name
```

### Fast-Forward Merge

> Main has no new commit since the branch was created.

```text
main ───────────────►
       \
        feature ────►
```
> Practice

``` bash
# Step 1: Create and switch to feature branch
git switch -c feature

# Step 2: Create a new file and commit
echo "Feature Code" > feature.txt
git add .
git commit -m "added feature file"

# Step 3: Switch back to main
git switch main

# Step 4: Merge
git merge feature
```
### Three-Way Merge

> Both branches have new commits.

```text
        feature ───►
       /
main ──●───────────►
       \
        changes ───►
```

> Practice

``` bash
# Step 1: Create login-feature branch
git switch -c login-feature

# Step 2: Add a file on the feature branch
echo "Login Feature" > login.txt
git add .
git commit -m "added login"

# Step 3: Switch back to main and add a different file
git switch main
echo "Main Update" > main.txt
git add .
git commit -m "main updated"

# Step 4: Merge with -m to avoid Vim editor
git merge login-feature -m "three way merge completed"
```

> Git creates a **merge commit**.

### Squash Merge

> Combines feature commits into one commit.

```bash
Feature branch before squash:

ui-feature:   A --- B --- C --- D --- E
                    (navbar) (footer) (sidebar)

After squash merge onto main:

main:         A --- B --- F
                          |
                    (UI Feature Complete)
                    All 3 commits combined into one
```
> Practice
```bash
# Step 1: Create ui-feature branch
git switch -c ui-feature

# Step 2: Make multiple commits
echo "Navbar" > navbar.txt
git add .
git commit -m "navbar added"

echo "Footer" > footer.txt
git add .
git commit -m "footer added"

echo "Sidebar" > sidebar.txt
git add .
git commit -m "sidebar added"

# Step 3: Switch to main
git switch main

# Step 4: Squash merge (stages all changes but does NOT commit yet)
git merge --squash ui-feature
```
### Octopus Merge

> Merges multiple branches at once.

```bash
Before octopus merge:

feature-a:   A --- X
feature-b:   A --- Y
feature-c:   A --- Z

After octopus merge:

             X
            / \
main:  A---+   M  (one merge commit, 3 parents)
            \ /|
             Y |
              \|
               Z
```
>Practice
```bash
# Branch 1: feature-a
git switch -c feature-a
echo "A Feature" > a.txt
git add .
git commit -m "feature a"

# Branch 2: feature-b
git switch main
git switch -c feature-b
echo "B Feature" > b.txt
git add .
git commit -m "feature b"

# Branch 3: feature-c
git switch main
git switch -c feature-c
echo "C Feature" > c.txt
git add .
git commit -m "feature c"

# Switch to main and merge all three at once
git switch main
git merge feature-a feature-b feature-c -m "octopus merge all features"
```
---

## Merge Conflicts

> Check conflict:

```bash
git status
```

> Open the conflicted file and choose the required changes.

```text
<<<<<<< HEAD
Current branch
=======
Incoming branch
>>>>>>> branch_name
```

> After fixing:

```bash
git add .
git commit -m "Resolve merge conflict"
```

> Abort merge:

```bash
git merge --abort
```

---

## Remote Repository

> Add GitHub remote:

```bash
git remote add origin https://github.com/username/repository.git
```

> Check remote:

```bash
git remote -v
```

> Rename remote:

```bash
git remote rename origin upstream
```

> Remove remote:

```bash
git remote remove origin
```

---

## Clone Repository

> Download an existing GitHub repository:

```bash
git clone https://github.com/username/repository.git
```

> Enter repository:

```bash
cd repository
```

---

## Push & Pull

### Push

> Upload local commits to GitHub:

```bash
git push origin main
```

> First push + set upstream:

```bash
git push -u origin main
```

### Pull

> Download and merge latest changes:

```bash
git pull origin main
```

---

## Fetch

> Download remote changes without merging:

```bash
git fetch
```

> Fetch from origin:

```bash
git fetch origin
```

> **fetch** = download changes
> **pull** = fetch + merge

Woekflow
```bash
# 1. Always start by downloading latest code
git pull

# 2. Make your changes in text editor...

# 3. Check what changed
git status

# 4. Stage all changes
git add .

# 5. Commit with a message
git commit -m "Describe what you changed"

# 6. Upload to GitHub
git push
```
---

## Remote Branches
> Pushing a Branch to GitHub
```bash
# Nobita creates a feature branch locally
git checkout -b feature-login
# Makes changes and commits
git add login.txt
git commit -m "Add login page"
# Push branch to GitHub
git push -u origin feature-login
```

> View all branches
```bash
# See local branches only
git branch
# See all branches (local + remote)
git branch -a
```

> Checking Out Remote Branches
```bash
# Suneo wants to see Nobita's feature branch
git fetch origin
git checkout feature-login
```

> Deleting Remote Branches
```bash
# Delete branch from GitHub
git push origin --delete feature-login
# Delete local branch
git branch -d feature-login
```
## Fork
### Fork a Repository

> Go to the original GitHub repository → click Fork.

```bash
Gian's Repo
      ↓
    Fork
      ↓
Nobita's GitHub Repo
```
### Clone Your Fork

> Clone your fork, not the original repository.

```bash
git clone git@github.com:nobita-nobi/school-project.git
cd school-project
```
> Check the remote:

```bash
git remote -v
origin  → Your fork
```
### Add Original Repo as Upstream

> Add the original repository as upstream.

```bash
git remote add upstream git@github.com:gian-doraemon/school-project.git
```
> Check:

```bash
git remote -v
origin    → Your fork
upstream  → Original repository
origin vs upstream
Remote	Meaning
origin	Your fork
upstream	Original repository
```
> Remember:

origin   = YOU
upstream = ORIGINAL OWNER
### Create a Branch

> Always create a separate branch for your changes.

```bash
git switch -c fix-homepage

Make your changes, then:

git add homepage.txt
git commit -m "Fix homepage title"
```

### Push to Your Fork

> Push your branch to origin.

```bash
git push origin fix-homepage
Your branch
     |
     ↓
  origin
     |
     ↓
Your GitHub Fork
```
### Create a Pull Request

> On your GitHub fork:
> Compare and pull request → Create pull request

> Make sure:

> base repository:
> gian-doraemon/school-project

> base branch:
> main

← Pull Request ←

> your fork:
> nobita-nobi/school-project

> branch:
```bash
fix-homepage
Pull Request Flow
Your Fork
fix-homepage
      |
      | Pull Request
      ↓
Original Repo
main
      |
      ↓
Review → Approve → Merge
```

### Review & Merge

> The original owner reviews your Pull Request.

```bash
Review Code
     ↓
Comments / Changes
     ↓
Approve
     ↓
Merge Pull Request

After merging, your changes become part of the original repository.
```

### Sync Fork with Upstream

> After the original repository changes:

```bash
git switch main
git pull upstream main
git push origin main
```
> Flow:

```bash
Original Repo
     ↓
upstream
     ↓
Local main
     ↓
origin
     ↓
Your Fork

Now your fork is up to date.

Working with Remote Branches

Suppose Suneo has a remote branch:

origin/feature-database
```
### Fetch Remote Branches
```bash
git fetch origin
```

> View remote branches:
```bash
git branch -r

Example:

origin/main
origin/feature-database
origin/fix-homepage
```

### Create Local Branch from Remote Branch
```bash
git switch -c feature-database origin/feature-database
```

> Now you have a local copy of the remote branch.
```bash
Remote Branch
origin/feature-database
          ↓
Local Branch
feature-database
```

### Make Changes & Push

Edit the files, then:
```bash
git add database.txt
git commit -m "Fix database connection string"
git push origin feature-database
```
> The changes are pushed back to the same remote branch.

### Another Developer Pulls the Changes

> Suneo can update his local branch:
```bash
git switch feature-database
git pull origin feature-database
```

### Complete Fork Workflow
```bash
FORK
  ↓
CLONE
  ↓
ADD UPSTREAM
  ↓
CREATE BRANCH
  ↓
MAKE CHANGES
  ↓
COMMIT
  ↓
PUSH → ORIGIN
  ↓
PULL REQUEST
  ↓
REVIEW
  ↓
MERGE
  ↓
SYNC WITH UPSTREAM
```



## Stash

> Temporarily save uncommitted changes:

```bash
git stash
```

> See stashes:

```bash
git stash list
```

> Restore latest stash:

```bash
git stash pop
```

> Apply stash without removing it:

```bash
git stash apply
```

> Delete latest stash:

```bash
git stash drop
```

---
## Git Rebase
> Rebase vs Merge
```bash
MERGE:
main:    A --- B --- C --- M (merge commit)
              \           /
feature:       D ------- E

REBASE:
main:    A --- B --- C
                         \
feature:                  D' --- E'
(commits moved to end of main)
```
> Never rebase commits that have been pushed to GitHub and shared with others. Only rebase local commits.
```bash
# Nobita's feature branch is behind main
git checkout feature-login

# Update with latest main
git rebase main

# Now feature branch has latest main changes
# And commits are in a clean line
```
## Tags

> Create tag:

```bash
git tag v1.0
```

> List tags:

```bash
git tag
```

> Push tag:

```bash
git push origin v1.0
```

> Push all tags:

```bash
git push origin --tags
```
---

## Basic GitHub Workflow

```bash
git clone repository-url
cd repository

git switch -c feature-name

# Make changes

git status
git add .
git commit -m "Add feature"

git push -u origin feature-name
```

> Then create a **Pull Request** on GitHub.

---

## Quick Git Workflow

```bash
git status
git add .
git commit -m "message"
git push
```

> **Edit → Add → Commit → Push**
---

### Author

**MUHAMMAD SHEHZAD**
GitHub: https://github.com/dbdmlabs

---
