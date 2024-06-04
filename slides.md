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
* This repository contains images tracked with `git-lfs`. 