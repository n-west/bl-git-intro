
# Git Intro for Breakthrough Listen

This is meant as a practical introduction to git for the Breakthrough Listen
interns 2024 summer class. This repository will eventually contain most of the
contents of the primer and cheatsheets for the most commonly expected commands.


## New projects

The first thing to do when creating a **new** project is to initialize a repository:

```bash
git init
```

This is a relatively inconsequential command that should print out something
like "Initialized empty Git repository in .../.git/". That's a hidden folder
that you can look in. It should have contents like this:

```
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── push-to-checkout.sample
│   ├── sendemail-validate.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

10 directories, 18 files
```

As you work on your repository these contents will change. You should probably
never need to actually look in this folder, but it's useful to know that every
git command you use is interacting with these contents. The practical
implication here is that to interact with your git repository you'll need to be
inside this directory, otherwise git (the command line utility) won't know
which git repository you want to interact with.


## Existing projects

You should *clone* the repository you're interested in to make a local copy of
it. Cloning will also give you a copy of the entire history of this repository.

```bash
git clone $REMOTE_URL
```

This repository is hosted at `https://github.com/n-west/bl-git-intro` so you can
insert that in place of `$REMOTE_URL` to get this tutorial and its history.

## Remainder of tutorial

Now that you have a repository, the remainder of the tutorial will focus on interacting
with it through git actions.
