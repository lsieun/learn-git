# Connecting to Remote Repositories

“去中心化”这个概念，要讲清楚，不是没有“中心”。它反对的是“唯一的中心”，提倡的是“多个中心”。

In a centralized version control system, like Subversion, there is one master copy of the repository and all work is written into that copy. When you commit, the information is immediately uploaded to that central repository and available to others. In a decentralized version control system, like Git, there is no single repository that everyone works with. It is merely a convention that declares one copy of the repository to be privileged (and considered to be the official source for the code).


```bash
# 
git remote add origin git@gitlab.com:emmajane/my-git-for-teams.git
git push -u origin master
```


- [ ] origin这个名字要讲清楚

When you add a remote to your repository, you must also assign it a nickname. By default, the nickname is `origin`. You could name it anything you like and Git wouldn’t care. The advantage of using `origin` is that more tutorials online will be as easy as copy and paste; the disadvantage is that `origin` doesn’t really explain very much, especially if your repository actually started locally. In addition to this, `origin` is already in use if you created your repository by cloning it from a remote repository. To connect the project you created to your local repositories, use a nickname `my_gitlab`.

```bash
# Adding a remote to a local repository with a custom name
$ git remote add my_gitlab git@gitlab.com:emmajane/my-git-for-teams.git
```

Confirm the remote was correctly added with the command `remote`.

```bash
# List remote repositories connected to your current repository
$ git remote --verbose
```

## Pushing Your Changes

To upload your changes, you need to have **a connection to the remote repository**, **permission to publish to the repository**, and **the name of the branch to which you want to upload your changes**. The first time you push your branch, you will need to explicitly tell Git where to put things. If you start by using the command `push`, it will tell you what to do next.

```bash
# Upload a branch using the command push
$ git push
```

```bash
# Set the upstream branch while uploading your local branch
$ git push --set-upstream my_gitlab 1-process_notes
```

- [ ] 不同的分支，需要不同的upstream吧

This will upload your branch and set it up for future use. Now whenever you are using this branch, you can issue the much shorter command `git push` to upload your work. By **setting the upstream connection**, you are building a relationship between **your local copy of the branch** and **the remote repository**. This has the same effect as when you used `--track` to check out a remote branch, except in that case you were starting with the remote copy and adding a tracked local copy.

## Branch Maintenance

Once the code has been fully tested, you will want to merge the ticket branch into the `master` branch, and delete the local and remote copies of the ticket branch.

```bash
# Merging a ticket branch into your main branch
$ git checkout master
$ git merge 1-process_notes
```

Now that the changes have been merged into the `master` branch, there’s not a lot of reason to keep the ticket branch open. To keep your repository tidy, you can go ahead and delete the ticket branch now.

```bash
# Delete your local copy of the branch
$ git branch --delete 1-process_notes
```

Finally, you need to do a bit of housekeeping for the remote repository as well. You should also delete remote branches whose changes have been merged into master

```bash
# Delete remote branches that are no longer needed
$ git push --delete my_gitlab 1-process_notes
```

- the name of the branch: megazord
- new branch: `git checkout -b megazord`
- making changes in your branch
- upload your work by adding a new remote to your local repository.
- Housekeeping tasks should be performed

You can do this by merging your ticket branches into your `main` branch, and then deleting the local and remote copies of your branch.

Git time machine

you will learn how to go back in time in the Git time machine to
undo your work and change your commit history.





