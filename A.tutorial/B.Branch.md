# Branch

In version control, branches are a way of separating different ideas. They are used in a
lot of different ways. You can use branches to denote different versions of software.
You might use very short-term branches to work on a bug fix, or you might use a
longer-term branch to test out a new idea.

## Listing Branches

To get a list of all branches, you can use either the `branch` command on its own, or add the parameter `--list`.

```bash
# Listing local branches
$ git branch --list
```

By default, the `master` branch is copied into your local repository and you can begin working directly on it. In addition to this branch, you have also **downloaded all other branches** that were available in **the remote repository**. They are available for reference purposes, but they are not available to be worked on until you have set up **a working copy of the remote branch**. To list all branches in your repository, use the parameter `--all`.

```bash
# List all branches
$ git branch --all
```

To get a usable list of the names of the remote branches, use the parame‐
ter `--remotes` (or `-r` for short) instead.

```bash
# List remote branches
$ git branch --remotes
```

These branches are all accessible to you, although you’ll need to make your own copy before committing changes to them.

## Updating the List of Remote Branches

The list of remote branches does not stay up to date automatically, so the list will become out of date over time. To update the list, use the command `fetch`.

```bash
# Fetch a revised list and the contents of all remote branches
$ git fetch
```

## Using a Different Branch

```bash
# Switching branches with the command checkout
$ git checkout --track origin/video-lessons
```

## Creating New Branches

Creating a new development branch

```bash
# First checkout the branch you want to use as the starting point:
$ git checkout master
# Next, create a new branch:
$ git branch 1-process_notes
# Finally, check out the new branch:
$ git checkout 1-process_notes
```

或者

```bash
# Creating a new development branch from the master branch
$ git checkout -b 1-process_notes master
```



```bash
# 

```

















