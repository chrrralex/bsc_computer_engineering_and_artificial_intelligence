# 0B. Git Basics

## 0B.01. What is a version control system?

A VCS (Version Control System) tracks changes in files over time.

Why it is useful?
- Keep history of changes.
- Restore old versions.
- Collaborate with others.
- Avoid overwriting work.

Common examples of VSC programs/tools are Git, Subversion and Mercurial. In this chapter we're going to analyze Git, based on the Unix operating system. Git is the most widely VCS, cause it's a free and open source project.

## 0B.02. What are Git and GitHub?

Git is a distributed version control system that you can run locally on your computer, in one, or more repositories. You can use directly, once installed, directly in a CLI (Command-Line Interface), tipically represented by a shell (like zsh, csh, bash, or fish).

GitHub is a cloud platform that hosts Git repositories and handles collaboration tools (issues, pull requests, content integration, content delivery, boards, and so on). Another examples of commons cloud platforms are GitLab and Bitbucket.

## 0B.03. What is a repository?

A repository (also called repo) is a project folder tracked by Git.

A repository contains:

- The project files.
- The change history.
- The branches.

You can create a git repository by the following command, that creates a hidden folder called  `.git` where all configurations and so other things about git are stored:

```bash
git init
```

If you create a repository in a cloud platform like GitHub, you can clone an existing repository with the `git clone` command:

```bash
git clone <repositoryUrl>
```

where tipically `<repositoryUrl>` is an SSH, or HTTP URL you can copy directly from the cloud platform.

You can clone a repository in a custom folder by specifying a relative, or absolute path after `<repositoryUrl>`, like this:

```bash
git clone <repositoryUrl> <path>
```

If you want to see some informations about the inited repo, you can use `cat`:

```bash
cat .git/config
```

An example of its output is:

```txt
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[remote "origin"]
        url = <repositoryUrl>
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main
        vscode-merge-base = origin/main
```

## 0B.04. Git version

To check if a specific version of git is installed on your local machine, you can use the option `--version`, often contracted in `-v`:

```bash
git --version
# or
git -v
```

An example of output is:

```bash
git version 2.43.0
```

This is very useful to verify if git is installed, or its compatibility with your system.

## 0B.05. Git configuration

If you have a GitHub account (or any other cloud platform account that is compatible with git), you can set your username and email (required for many git operations in a repo) with the `git config` command:

```bash
git config --global user.name "Mario Rossi"
git config --global user.email "mario@email.com"
```

You can see your configurations with the parameter `--list`:

```bash
git config --list
```

## 0B.06. Git branches

A branch is an independent line of development. A repo can have one, two, or more collaborators (developers, managers, stakeholders, or other people). So, each member of the project can develop in a different and independent branch.

You can list teh branches of the current repository with the `git branch` command:

```bash
git branch
```

Or you can create a branch by specifying its name:

```bash
git branch <branchName>
```

To change the branch you're working on, you can use the `git checkout` command in the following way:

```bash
git checkout <branchName>
```

To create a branch and switch in only one command, you must use the `-b` option: 

```bash
git checkout -b <branchName>
```

To delete a branch, the `-b` option must be used before the branch name:

```bash
git branch -d <branchName>
```

Pay attention with the deletion commands: once you use the previous command, the branch is removed permanently.

You can force a deletion with the uppercase `-D` option:

```bash
git branch -D <branchName>
```

## 0B.07. Git commit

A commit saves a snapshot of changes. It's the smallest unit if the git history and it can have own properties, of which the most important is the message: it's a small description about the changes made.

First of all, you can add a specific file to the next comment you want to create with the `git add` command:

```bash
git add <fileName>
```

To add any files, you can use the dot (`.`) instead of `<fileName>`:

```bash
git add .
```

You can create a commit with a message by the `git commit` command and the `-m` option (the message is required for a commit):

```bash
git commit -m "<messageHere>"
```

To create an inline message, use `-am` instead of `-m`:

```bash
git commit -am "<inlineMessageHere>"
```

You can update the message of your last commit by using the `--amend` option:

```bash
git commit --amend
```

You can see the history of commits by using the `git log` command:

```bash
git log
```

A compact output of the previous command can be botained with the `--oneline` option:

```bash
git log --oneline
```

Instead, to see a detailed graph view as output you can use `--all`, `--graph` and `--oneline` options:

```bash
git log --graph --oneline --all
```

## 0B.08. Git pull

`git pull` command allows you to download and merge changes from a remote repository.

The most basic syntaxt of this command is:

```bash
git pull
```

You can specify the remote branch in this way:

```bash
git pull <repository> <branchName>
```

Often, `<repository>` has the value `origin`: it means you refer  the current repository.

Instead, the following command (with `--rebase` option):

```bash
git pull --rebase origin main
```

is equivalent to these commands:

```bash
git fetch
git merge origin/main
```

## 0B.09. Git push

`git push` command allows you to uploads local commits to a remote repository.

The basic syntaxt is:

```bash
git push
```

If you want to push your changes in a specific branch, you can specify it in this way:

```bash
git push <repository> <branchName>
```

If you've created a new branch in a local machine (without using GitHub) and you want to push not only the changes, but the branch iteself also, you can use the `-u` option in this way:

```bash
git push -u <repository> <branchName>
```

You can force a push with `--force` option:

```bash
git push --force
```

A safer force push with `--force-with-lease` option:

```bash
git push --force-with-lease
```

## 0B.10. Git reset

`git reset` moves the current branch to another commit.

A soft reset keeps staged changes (your local changes). You can make a soft reset by the `git reset` command with the `--soft` command: 

```bash
git reset --soft HEAD~1
```

An hard reset delete all local changes and it can be obtained with `git reset` command with the `--hard` option:

```bash
git reset --hard HEAD~1
```

You can reset only a specific file by specifying it in this way:

```bash
git reset <fileName>
```

In git, each commit has the own hash. You can specify this hash immediately after `git reset --hard` to return to a specific commit, without your local changes. Here's an example:
Reset to specific commit:

```bash
git reset --hard <commitHash>
```

Normally, git can recognize the commit you are referring to by specifying the first 8-10 characters (each commit has a unique hash, so it is different from all the others).

## 0B.11. Git collaboration

Typical collaboration workflow:

1.  Clone repository

```bash
git clone https://github.com/org/project.git
```

2.  Create branch

```bash
git checkout -b feature-auth
```

3.  Work and commit

```bash
git add .
git commit -m "Add authentication"
```

4.  Push branch

```bash
git push origin feature-auth
```

5.  Open Pull Request on GitHub

6.  After review → merge into `main`

Update local repository:

```bash
git pull origin main
```

### 0B.12. Command Summary

Here is a quick command summary:

```bash
----------------------- ------------------------
Command                 Purpose
----------------------- ------------------------
git init                create repository
git clone               copy remote repository
git add                 stage changes
git commit              save snapshot
git push                upload commits
git pull                download changes
git branch              manage branches
git checkout            change branch
git reset               undo commits
git log                 show history
----------------------- ------------------------
```
