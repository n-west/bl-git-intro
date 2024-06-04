
# More advanced and/or rare situations

## rebase

Rebase is a potentially dangerous operation with git. This "reapplies" commits
as if they were sets of diffs you were adding then committing all over again. This is useful
in two (probably more) scenarios:

First, you have a branch and want to keep a **linear history** on top of another branch people
have worked on. In this case you'll have your own local branch and a remote branch.

You can use

```
git rebase REMOTE BRANCH
```

and your changes will be replayed on top of the remote branch as if that was your starting point.
It is possible that some **conflict**s will occur if you and the remote development changed the same
or similar lines of code. Resolving conflicts is outside of our scope, but there are several ways to
handle it and don't be afraid to ask for help if this occurs.

Second, you have your local repository and branch and would like to change history. This is common
when you have a bunch of not useful commits of work in progress, you want to change a commit message,
or you want to change the order of commits. You can use

```
git rebase -i
```

This is a dangerous but powerful command. Try to avoid using it until you've pushed your code somewhere safe
or work on a toy repository. You can **squash** commits which will merge them in to a single commit in history
and allow you to change the message. You can **fixup** which will just merge commits to a single commit. You
can reorder commits my moving lines in the interactive dialog around. You can **edit** commits which allows you
to remove or add specific changes inside the commit. You can **ammend** a commit which allows you to change the
message.



