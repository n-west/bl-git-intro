
# Submodules primer

Submodules are a way to track another repository as part of your repository. This works by adding a pointer to the other repository at a specific commit in the submodule repository. When you do this, everyone that looks at your repository will know the exact version of the other repository to use.

This can be tricky in practice because you often forget to initialize the submodules or update them over time. Since adding a submodule to your repository will always point to a specific commit of the other repository, you (or a maintainer) will need to manually update the commit that is pointed to when you want to upgrade. This can also be a source of confusion because `git pull` does not automatically update submodule pointers!

To update a submodule pointer:

```
git submodule update --init --recursive
```

Technically, only `git submodule update` is required. You can read `git submodule --help` for the other options, but the gist of it is `--init` will initialize any submodule pointers that are not already initialized, recursive will recursively update and initialize all submodule pointers. Recursive is really important, because your submodule could have its own submodules that need to be kept up to date.

This is always a safe command to run.

## Practice:

This repository has a submodule that points to the (current HEAD of the main branch) of this repository: https://github.com/github/training-kit

Run `git submodule update --init --recursive` and watch it download in to the folder "training-kit". Inside this folder you'll see git-guides which contains a few text files that can help with common git commands. This can be a useful reference for you if you're stuck or just want to review some additional material on your own.

