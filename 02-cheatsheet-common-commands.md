
# Commonly used operations

## git status

Show the current status including what files have changed, which files are new and untracked, and the
staging status of any files. Also shows your current branch.

## git add

This is used to **stage** changes to commit.

Every git interface (VS Code, other IDE, command-line) will have some way to add entire files to stage.
GUI tools will have check boxes, etc. On the command line you can use

```
git add path/to/file                        # one file at a time
git add path/to/another-file and-another    # just list as many files as you want
git add -i                                  # interactive adding and updating of files
```

## git commit

Once you have staged changes,

```
git commit
```

will open a text editor for a commit message. You're required to have **something** but it's entirely up
to you what that is. Again, this was originally meant as a primarily e-mail based exchange and it can help
your future self looking through the log to write it as an e-mail to yourself or another knowledgable party.

You can also use a shorthand if your message won't be long:

```
git commit -m '-m stands for --message and will use whatever you put in quotes as the msesage'
```

GUI tools will often put a textbook adjacent to a checkbox for a commit dialog. You select the files to commit
and write your message in the box then hit commit.

## git branch

Branches allow alternate and parallel paths of development. It's always safe to branch and one of the key
features of git is how "cheap" branches are. They are typically merged in to the `main` branch eventually
but they can also be discarded.

In some philosophies of using git for pedantic versioning ("git flow") you have branches that are long-lived
and intended to support older versions. The idea is that features go on new branches and any bug fixes can be
merged or cherry-picked between branches so you truly have paralle l paths of your code.


```
git branch BRANCH_NAME
```

Will create a branch called `BRANCH_NAME`, but not check it out. You still need to use

```
git checkout BRANCH_NAME
```

If you already have a branch you can switch between them with `git checkout`.

There is a shortcut to create a new branch and check it out:

```
git checkout -b BRANCH_NAME
```

## git push

Push a branch and its commits to a remote (like Github)

```
git push REMOTE BRANCH
```

you can have multiple remotes and multiple branches. You **probably** only need to worry about
Github as a remote for the summer. The default when `clone` is used is to call the origin you clone
from `origin`.

If you used `git init`, you may not have a remote by default. If you have a new project in Github they
will provide instructions but you can use the following:

```
git remote add NAME git@github.com:USERNAME/PROJECTNAME.git
```

This styl eof URI uses ssh keys to log in as the git user to github.com

## git pull

This pulls changes from a remote, which can be useful after merging a branch or when someone else
has pushed.

```
git pull REMOTE BRANCH
```


## git log

```
git log
```

Look at the history of commits from the HEAD of your current tree. You will see branch names
and commit messages, hashes, etc. You can also pass branch names or commit SHAs to view the
history from the perspective of that commit
