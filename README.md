# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
# and the relevant terminal output (e.g., branch listing, merge messages)
```

```bash
lex-alex@DESKTOP-6IB5N3D:~$ sudo apt install git
lex-alex@DESKTOP-6IB5N3D:~$ git config --global user.name "Alexander Schweiger"
lex-alex@DESKTOP-6IB5N3D:~$ git config --global user.email "Alexander.schweiger@stud.thga.de"
lex-alex@DESKTOP-6IB5N3D:~$ mkdir ~/GitPP5
lex-alex@DESKTOP-6IB5N3D:~$ cd ~/GitPP5
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git init
Initialized empty Git repository in /home/lex-alex/GitPP5/.git/
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git checkout -b feature-1
Switched to a new branch 'feature-1'
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ echo "This is my description" >feature.txt
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git add feature.txt
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git commit -m "The textfile feature.txt has been merged"
[feature-1 (root-commit) 2dcab0d] The textfile feature.txt has been merged
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git checkout master
error: pathspec 'master' did not match any file(s) known to git
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git checkout -t -b master
branch 'master' set up to track 'feature-1'.
Switched to a new branch 'master'
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git checkout feature-1
Switched to branch 'feature-1'
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'feature-1'.
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git log
commit 2dcab0dd78082f34eacd777fdf73d8b680d7d395 (HEAD -> master, feature-1)
Author: Alexander Schweiger <Alexander.schweiger@stud.thga.de>
Date:   Wed May 21 22:03:48 2025 +0200

The textfile feature.txt has been merged
```

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs
```
---
```bash

user89@vorlesung:~$ mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare
lex-alex@DESKTOP-6IB5N3D:~$ cd ~/GitPP5
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ cd
lex-alex@DESKTOP-6IB5N3D:~$ ssh user89@128.140.85.215
user89@vorlesung:~$ ls
feature-1  repos
user89@vorlesung:~$ tree -d
.
├── feature-1
└── repos
    └── myproject.git
        ├── branches
        ├── hooks
        ├── info
        ├── objects
        │   ├── info
        │   └── pack
        └── refs
            ├── heads
            └── tags

13 directories
user89@vorlesung:~$ exit
logout
Connection to 128.140.85.215 closed.
lex-alex@DESKTOP-6IB5N3D:~$ cd ~/GitPP5
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git remote add origin-ssh user89@128.140.85.215:~/repos/myproject.git
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git branch
  feature-1
* master
lex-alex@DESKTOP-6IB5N3D:~$ cd ~/GitPP5
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git remote add origin-ssh user89@128.140.85.215:~/repos/myproject.git
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git branch
  feature-1
* master
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git push origin-ssh master
user89@128.140.85.215's password:
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 266 bytes | 266.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To 128.140.85.215:~/repos/myproject.git
 * [new branch]      master -> master
lex-alex@DESKTOP-6IB5N3D:~$ cd ~/GitPP5
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ mkdir git-clone
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ cd git-clone
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git remote add origin-ssh user89@128.140.85.215:~/repos/myproject.git
error: remote origin-ssh already exists.
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git push origin-ssh master
user89@128.140.85.215's password:
Everything up-to-date
lex-alex@DESKTOP-6IB5N3D:~/GitPP5$ git clone user89@128.140.85.215:~/repos/myproject.git
Cloning into 'myproject'...
user89@128.140.85.215's password:
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```
### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs
```

---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
* GitLab MR: *paste URL and a one-sentence summary*

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
