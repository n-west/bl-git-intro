
# Initializing repos

## New porject

For new porjects, you can initialize a repository with

```
git init
```

Nothing magic happens, but the repository contents are created in `.git`. You'll still have to
add, commit, and push changes. On Github, you'll have to make a repository before you can push to it.

## Existing project

If there is an existing project you `clone` it with

```
git clone URL
```

For read-only from github you can use https://github.com/USERNAME/REPOSTIRY.

For read/write you should use your ssh key with the URI git@github.com:USERNAME/REPOSITORY


## LFS

Large files that are binary data which we don't want to track **changes** to are often stored with LFS, which
stores a URL to download the whole file from rather than embedding multiple revisions inside the repository. If
you are missing large files in a repository, you probably need to install git-lfs.

To track a file with lfs use

```
git lfs track PATH/TO/FILE
```

Then you will need to commit the `.gitattributes` file

## Submodules

Submodules embed other git repositories inside of your git repository. This can potentially be a long chain, so
operating with the `--recursive` flag is useful. You can initialize submodules in a repository that has them with

```
git submodule update --init --recursive
```

To add a submodule to your repository use

```
git submodule add URI
```

You will then need to add changes to the .gitmodules and commit them
