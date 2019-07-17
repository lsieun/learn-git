# Adding Changes to a Repository

Each time you **make a change** to **your working directory**, you will need to explicitly save **the changes** to **your Git repository**. This is a two-part process.

**Changes** in Git must be **staged**, and then **saved** to the repository

You can add one or more filenames at a time; the filenames do not need to be the same type.

```bash
# Add selected changed files to your Git repository
$ git add README.md process-diagram.png
$ git add branch-naming-rules.png
```

For the most part, I add files to **the staging area** one at a time. I find this prevents me from accidentally adding more than I meant to. At the command line, I can type the first few letters of the filename and then press the `Tab` key, and the remainder of the filename will be automatically typed out (this is known as `tab completion` and it’s one of my favorite things to use). If, however, you have a lot of files you need to add, and they’re all contained in the same directory, you may want to **use a wildcard to match files** with a subdirectory, or that all have a similar name.

```bash
# Add all files, recursively, from a given path
$ git add <directory_name>/*
```

```bash
# Add all files with the file extension .svg
$ git add *.svg
```

You can also completely **omit the filenames**, and instead **stage files** according to **whether or not they are known to Git**. By using the parameter `--update` you can **stage all files that are known to Git**, and that have been edited (or updated) since the last commit:

```bash
# 
$ git add --update
```

If you want to be even more outrageous, you can stage all changed files in the working directory by adding the parameter `--all`. This will **restage any files that have been modified since they were first staged** (ensuring all new edits are captured in the commit); **stage any files that are known to Git, but not already staged**; and **stage any files that are not currently being tracked by Git**. It is a very greedy command! Before using it, you should check the list of files that will be added:

```bash
# It is a very greedy command!
$ git status
$ git add --all
```

Once a change has been added to the staging area, it must be committed.

You can commit your staged changes to the repository by running `commit`.

## Adding Partial File Changes to a Repository

If you want even more granularity over your commits, you can choose to add partial changes within a saved file by using the parameter `--patch`.

Adding files via the `--patch` process is a multistep approach. You will first initialize the procedure, and then choose from a list of options on how you want to create your patches. You will be prompted to add the change to the staging area (`y`), or leave this hunk unchanged (`n`). Changed lines will begin either with a `-` (line removed) or a `+` (line added). If a line has been changed, it will display as both removed and added.

## Removing a File from the Stage

If you accidentally add too many files from the staging area, and want to break your changes into smaller commits, you can unstage your proposed changes. Removing a file from the stage doesn’t mean you’ll be undoing the edits you’ve made; it notifies Git that you’re not ready for these changes to be committed to the repository yet.

```bash
# Remove proposed file changes from the staging area
$ git status
$ git reset HEAD ch05.asciidoc
```

## Writing Extended Commit Messages

Your **commit messages** should always include **the rationale for why you made a change**, as well as **a quick summary of the changes you made**. In order to write **a detailed commit message**, you will need more than one line the one line short message style you have been using up to now. I typically write my commit messages with a two-step procedure:

1. Use a terse, one-line message to commit the changes to the repository.
2. Amend the commit to include a full description of what I was thinking when I made the change.

```bash
# Writing a detailed commit message
$ git add --all
$ git commit -m "CH05: Adding technical edits."
$ git commit --amend
```

You don’t need to do this two-step process; you can jump straight into the message editor by omitting the parameter `-m` when first making your commit:

```bash
# 
$ git commit
```

Your default editor will open, and you will be prompted to add a new commit message. The first line of the message will be used for the `--oneline` display, and all lines beginning with `#` will be removed from the final message. Once you’ve crafted your commit message, you will need to save it and then quit the editor to complete the commit.

## Ignoring Files

If you know that your favorite text editor, or IDE, creates temporary files, which are not project specific, you should create a global setting to ignore these files.

First, run the following command to let Git know which file you would like to store your list of “ignored” files in:

```bash
# 
$ git config --global core.excludesfile ~/.gitignore
```

You can now update this file using **one filename per line**. You can use **exact filenames**, or **wildcards** (for example: `*.swp` will match any file ending in `.swp`). For a useful starting point of files to ignore, check out [gitignore.io](https://www.gitignore.io/).

Additionally, you may want specific repositories to ignore specific files or file extensions. In this case, your best option is to add an extra `.gitignore` file to the repository. This has the added benefit of ensuring your teammates don’t accidentally sneak in their build files.

Complete the following steps to customize which files should be ignored for a specific repository:

1. Create a file in the root level of your project named .gitignore.
2. Using one filename per line, add all of the files you never want Git to add to the repository. You can use exact filenames, or wildcards (for example, *.swp).
3. Add the file `.gitignore` to your repository by using the commands `add` and `commit`.

Files with these extensions will no longer be added to your repository, even if you are using the parameter `--all`.

## Working with Tags

Tags are used to pinpoint specific commits. You can think of them like a bookmark. I don’t use tags nearly as much as I should. As a result, I rely on my commit messages to find specific points in the repository. You may find working with tags is a good habit to get into because they will allow you to easily reference points in your time line.

Tags can only be added to specific commits. To know which commit you want to add your tag to, you’ll probably want to use a combination of `log` and `show`. The command `log` will give you a list of all commits in your repository, and the command `show` will display the detailed information for any single commit.

```bash
# Quick list of recent commits
$ git log --oneline
```

Once you think you have found a commit that you would like to investigate a little further, you can get the detailed commit message beginning at that commit by adding the commit ID. To limit the output to only that commit, add the optional parameter `--max-count=` along with the number of log entries you would like to show.

```bash
# Log details for a single commit
$ git log fa04c30 --max-count=1
```

If you want even more details about the commit object, you can use the command `show` to list the changes that happened in that commit as text (of course, this will be less useful for binary files, such as images).

```bash
# Use show to display the log message and textual diff for a single commit
$ git show fa04c30
```

Once you have identified a commit that you want to bookmark, you can do so by using the command `tag`.

```bash
# Adding a new tag, v1.0.0, to a commit object
$ git tag v1.0.0 fa04c30
```

You can now list the available tags by using the command `tag` without any parameters.

```bash
# Listing all tags
$ git tag
```

Once a tag is made, you can investigate the commit where the tag was added.

```bash
# Reviewing a tagged commit
$ git show v1.0.0
```






```bash
# 

```
