
# Version Control System

## What is a Version Control System (VCS)?

A Version Control System is a tool that helps you:
- Track changes to files over time
- Work on a project with others
- Revert back to an earlier version if something breaks
- See who made what change, and when

---

## ✅ Key Benefits of Git

| Feature        | What it Means                                    |
|----------------|--------------------------------------------------|
| Track Changes  | See what changed in your code over time          |
| Undo Mistakes  | Go back to a working version if something breaks |
| Branching      | Try new features without messing up main code    |
| Collaboration  | Work with others and combine changes smoothly    |
| History        | Know who made what changes and why               |

---

# Basic Commands of Git

| Command             | What it Does                                  |
|---------------------|-----------------------------------------------|
| git init            | Start a Git repo                              |
| git status          | Show changes                                  |
| git add file.txt    | Stage file to commit                          |
| git commit -m "msg" | Save a snapshot with a message                |
| git log             | Show commit history                           |
| git push            | Send your changes to GitHub (remote)          |
| Code .              | Use to open the code in VS Code               |

---

# Centralized and Distributed Version Control

## 1. Centralized Version Control System (CVCS)
**Examples:** SVN (Subversion), Perforce

In a centralized system:
- There is one central server where the entire codebase lives.
- Developers connect to this server to pull code and push changes.
- If the server is down, no one can collaborate or access history.
<img width="1081" height="265" alt="image" src="https://github.com/user-attachments/assets/a3db33e0-1c04-45c3-8ef7-7880a84f2490" />

## 2. Distributed Version Control System (DVCS)
**Examples:** Git, Mercurial

In a distributed system (like Git):
- Every developer has a full copy of the repository, including history.
- You can commit, view logs, branch etc., offline.
- You only need to connect to the central repo (e.g., GitHub) when pushing or pulling.
<img width="1005" height="295" alt="image" src="https://github.com/user-attachments/assets/76124a6a-bf6b-4d1e-8e35-f217a1fd7ecd" />

## Advantages
- Work offline.
- Faster operations (all local).
- No central point of failure.
- More powerful branching and merging.

---

### 🧠 Why Git is Distributed

Git was designed to:
- Be fast
- Support non-linear workflows (branches, merges)
- Allow offline work
- Encourage collaboration without stepping on toes

---

### 🔁 Summary: Centralized vs Distributed Systems

| Feature           | Centralized (CVCS)            | Distributed (DVCS/Git)             |
|-------------------|------------------------------|-------------------------------------|
| Server required?  | Yes                          | No (for most operations)            |
| Offline work?     | ❌ No                        | ✅ Yes                              |
| Full history?     | ❌ No                        | ✅ Yes                              |
| Speed             | Slower                       | Faster                              |
| Risk of failure   | High                         | Low                                 |
| Collaboration     | Limited                      | Flexible                            |

---

# 🛠️ Git vs 🌐 GitHub

| Feature       | Git                                       | GitHub                                      |
|---------------|-------------------------------------------|---------------------------------------------|
| 🧠 What is it?| A tool / command-line program             | A platform / website                        |
| 🔍 Purpose   | Tracks code changes (version control)      | Hosts Git repositories online               |
| 📦 Type      | Installed on your computer                 | Cloud-based service                         |
| 🌍 Online?  | ❌ No (it's local)                          | ✅ Yes (requires internet)                  |
| 📁 Stores Code| Locally (on your system)                  | Remotely (on GitHub's servers)              |
| 👥 Collaboration | Possible, but manual (via email, USB, etc.) | Easy collaboration with pull requests, issues, etc.   |
| 🛡️ Security | You manage access locally                  | GitHub manages users, teams, permissions     |

---

# Git Branching

## 🔀 What is a Git Branch?
A branch in Git is a separate version of your code that allows you to:
- Work on new features
- Fix bugs
- Try experimental ideas without affecting your main code (usually the main or master branch).

---

## ✅ Why Use a Branching Strategy?
A branching strategy is a set of rules or a workflow your team follows to:
- Keep code organized
- Control what gets deployed
- Avoid bugs in production
- Make collaboration easier

---

## 🔧 Common Git Branches in a Team Workflow

| Branch Name   | Purpose                                 |
|---------------|-----------------------------------------|
| main / master | Stable production-ready code            |
| develop       | Ongoing development (integration)       |
| feature/*     | New features under development          |
| release/*     | Preparing for a new production release  |
| hotfix/*      | Emergency fixes for production bugs     |

---

## 🌳 Git Branching Strategy: Git Flow Model

This is a widely-used strategy for managing branches.

**1. main branch (or master)**
- Always contains stable production code
- You don’t develop directly here
- Releases and hotfixes get merged here

**2. develop branch**
- Integrates features before going to production
- All feature branches are merged here
- When you're ready to release, merge into release or main

**3. feature/<name> branches**
- Used for building a new feature
- Created from: develop
- Merged into: develop

**Example:**
git checkout develop
git checkout -b feature/login-page


**4. release/<version> branches**
- Prepares a release version for production
- Final polishing: bug fixes, tests, version bumping
- Created from: develop
- Merged into: main and develop

**Example:**
git checkout develop
git checkout -b release/1.0.0


**5. hotfix/<name> branches**
- For fixing critical bugs in production
- Created from: main
- Merged into: main and develop

**Example:**
git checkout main
git checkout -b hotfix/urgent-crash-fix


---


<img width="1018" height="349" alt="image" src="https://github.com/user-attachments/assets/5aee6d59-31bf-40e1-9fa6-9d623bb425c7" />

## ✅ Summary Table

| Branch    | Created From | Merged Into      | Use Case                       |
|-----------|--------------|------------------|--------------------------------|
| main      | N/A          | hotfix/release   | Production-ready code          |
| develop   | main         | feature/release  | Integration branch             |
| feature   | develop      | develop          | New features                   |
| release   | develop      | main & develop   | Final testing before release   |
| hotfix    | main         | main & develop   | Emergency fixes in production  |

