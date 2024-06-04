---
title: Practical Git Primer
center: true
theme: black
transition: slide
margin: 0.04
revealOptions:
  transition: slide
css:
  - ./css/custom.css
  - customers/git intro/css/custom.css
---

## git

Distributed version control system created by Linus Torvalds (of Linux) to manage linux kernel contributions (likes to name his projects after himself)



Stack Overflow conducts annual developer surveys (in 2022):
* git is used by 97% of developers
* 85% use the command line as an interface for git
* 56% use Github professionally (87% personally); 29% use Gitlab professionally (21% personally).
![[figures/developer-survey.png]]
https://survey.stackoverflow.co/2022/#version-control-version-control-system-prof  <!-- element class="left-aligned" -->


---

## Git concepts

Warning: git often has many ways to accomplish a goal and many commands do multiple very different things.

* You **add** changes to a **staging** area
* You **commit** changes to your repository. You can have *local* history that no one else has
* You **push** your **commits** and **branches** to a **remote**
* You can **pull** other peoples changes from a **remote**

Github is just a **remote** that exists in the cloud and offers convenient sharing.

---

## `--help`

* From the command line, all git commands will be `git X` where `X` is a subcommand
* `git X --help` will bring up a "man page", tend to be high quality and thorough, but sometimes theoretical
* We'll focus on concepts with command-line usage
* Other tools (VS Code, Github App) will reuse the same concepts and it helps to know the command-line version

---

## Get this primer

On github, go to https://github.com/n-west/bl-git-intro and "fork" this repository.

Your Github account now owns a copy. You should be able to **clone** this to your local system (or Berkeley datacenter)

```
git clone git@github.com/$YOURGITHUB/bl-git-intro
```

---

## Submodules

Submodules are a corner case of git, but they are common enough to be worth mentioning.

This repository has a submodule in it. Check out [[submodules-primer]].

Cheat sheet:
```
git submodule --update --init
```


---

## Merkle Trees

Use by bitcoin for blockchain, git for history

* tree structure that uses hash of children to label each node

Notice the "commit" is a **hash** (historically SHA-1, now SHA-256 is available)
![[git commit.png]]

The tree stores all files and **deltas** of files. This is practically important because some files (text files like source code) have easier deltas to store than others (images and other binary data). 
* See https://git-scm.com/book/en/v2/Git-Internals-Git-Objects to nerd out on the tree
---

## Large File Storage

* git-lfs is a way to store large files that are tracked fundamentally different
* Consider it a pointer to a url to download, no changes are tracked
* This repository contains images tracked with `git-lfs`, if you don't see them you'll need to install git-lfs
![[github-lfs.png]]

Use `git lfs track FILENAME` to use LFS on a file

---

## Standard workflow

* Work on some files
* `git add` indicate a group of changes
* `git commit` to record changes to the repository
* `git push` to send those changes to a remote (Github)

---

## How I do it (get ready for a commit):

Look at the current status
```
git status

On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   slides.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	figures/github-lfs.png

```

You see changes to files you've already tracked through git and new files that git is not tracking.

---

## How I do it (add changes)

```
git add -i
           staged     unstaged path
  1:    unchanged       +45/-1 slides.md

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> u
           staged     unstaged path
  1:    unchanged       +54/-1 slides.md
Update>> 1
           staged     unstaged path
* 1:    unchanged       +54/-1 slides.md
Update>> 
updated 1 path

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> a
           staged     unstaged path
  1: figures/github-lfs.png
Add untracked>> 1
           staged     unstaged path
* 1: figures/github-lfs.png
Add untracked>> 
added 1 path

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> 
*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now> q
Bye.
```

* `-i` is "interactive", has a terminal user-interface to indicate **updates**, **add untracked**, and a few other options.
* `u` and `a` to update or add. Enter numbers as range (1-4,6-8,10) to select which files to update or add
* enter to accept and go back up a menu, q to quit

---

## How I do it (write a commit)

```
git commit
```

This should trigger a text editor to open.

* Write commit messages like an email to your future self
* First line is a subject
* Empty line
* Body of email, don't waste time on it but describe any nuances that might be useful when looking at history

If you do this well, `git log` can give you a nearly automated work log for your project

---

## How I do it (push commits)

```
git push origin main 
Uploading LFS objects: 100% (1/1), 70 KB | 0 B/s, done.                                                                         
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 16 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 1.23 KiB | 1.23 MiB/s, done.
Total 5 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:n-west/bl-git-intro.git
   486bd24..e2feeb6  main -> main
```

---

## Look at the history

```
git log
```

![[git-log.png]]

This opens history in a tool called `less`. You can use arrows, pgup, pgdn keys to move up and down, use `/` to search. Hit `q` to exit

---

## Branches

* Branches allow an alternate universe to exist in parallel
* Different branches can have different history, then be **merged**
* Many techniques and opinions on merges!
	* **merge commit**, **fast-forward**, **rebase**

```
git branch branches
git status
On branch main
```

```
git checkout branches
git status
On branch branches
```

```
git checkout -b branches # Create and checkout a new branch named branches
```

---

## Merge a branch

```
git commit -m 'add branches'
[branches 66860ae] add branches
 2 files changed, 92 insertions(+), 2 deletions(-)
```

```
git push origin branches 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 16 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.29 KiB | 1.29 MiB/s, done.
Total 4 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
remote: 
remote: Create a pull request for 'branches' on GitHub by visiting:
remote:      https://github.com/n-west/bl-git-intro/pull/new/branches
remote: 
To github.com:n-west/bl-git-intro.git
 * [new branch]      branches -> branches
```

---

## Merge a branch

![[github-pull-request.png]]

---

## Pull changes

If you want to **pull** changes from a remote in to your branch:

```
git pull REMOTE BRANCH
```

```
git pull origin main 
From github.com:n-west/bl-git-intro
 * branch            main       -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.

```

Many options to reconcile, comes down to preferences and people can get very opinionated.

![[github-tree-after-merge.png]]

---

## Merge options

* fast-forward: replay this branch's commits on top of the other branch (always safe)
* git merge: create a merge commit (safe, but can make odd logs)
* git rebase: good for linear history, requires clean tree, can be tricky

---
## Summary

The git repo history is stored in `.git`

```
git add # specify files individually or use -i
git commit # opens an editor. Save the file will save the commit
git push REMOTE BRANCH # push the given branch to the given remote
```

Nothing special about "origin" or "main" other than default values for new repositories

* Look at history with `git log` (hit q to exit)

```
git checkout -b BRANCH_NAME # create a branch with a separate history
# do work
git status # check the status of your repository
git add # -i to use interactive mode
git commit # type a message like an email
git push ORIGIN BRANCH
# Look at github, managae pull requests, etc
```

