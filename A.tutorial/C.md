# C

<!-- TOC -->

- [1. git help](#1-git-help)
- [2. git config](#2-git-config)
  - [2.1. git config command](#21-git-config-command)
  - [2.2. git config concept](#22-git-config-concept)
  - [2.3. git config internals](#23-git-config-internals)
- [3. git init](#3-git-init)
  - [3.1. `.git` subdirectory](#31-git-subdirectory)
- [4. git add](#4-git-add)
  - [4.1. git add internals](#41-git-add-internals)
- [5. git commit](#5-git-commit)
  - [5.1. git commit concept](#51-git-commit-concept)
  - [5.2. git commit internals](#52-git-commit-internals)
  - [blob](#blob)
  - [tree](#tree)
  - [commit](#commit)
  - [parent commit](#parent-commit)
  - [tag](#tag)

<!-- /TOC -->

```txt
how to use Git wisely = use case 如何合理的使用它，这里是如何使用好
--------------------------------
git command(命令)=与外界交互的手段，这里是如何使用
porcelain command | plumbing command
--------------------------------
git concept（概念，抽象的东西）=软件所提供了“知识域”
--------------------------------
git internal（物理文件，具体的东西）=承载“知识域”的具体实现
object store(tag/commit/tree/blob), index, ref(HEAD/branch/tag)
```


```txt
HEAD
----------------
tag, branch(动态的tag), ORIGIN_HEAD
----------------
commit
----------------
tree
----------------
blob
```


```bash
## 第一组命令
git config --global user.name "Tom Cat"
git config --global user.email "tom@example.com"
git init
git add hello.txt
```

## 1. git help

查看git的命令帮助，可以使用`git help <subcommand>`或`git <subcommand> --help`：

```bash
# 第一种方式
$ git help init
# 第二种方式
$ git init --help
```

## 2. git config

### 2.1. git config command

也可以使用命令进行查看：

```bash
$ git config --global user.name
Tom Cat
$ git config --global user.email
tom@example.com
```

### 2.2. git config concept

### 2.3. git config internals

配置的`name`和`email`信息，保存在`~/.gitconfig`文件中。

```bash
$ cat ~/.gitconfig
[user]
    name = Tom Cat
    email = tom@example.com
```

## 3. git init

### 3.1. `.git` subdirectory

Let’s view the contents of the new Git repository by changing to the directory containing the Git repository and running the `find` command.

```bash
$ cd ~/GitInPractice/.git/ && tree
.
├── branches
├── config    # the configuration of the local repository
├── description    # a file that describes the repository
├── HEAD    # HEAD pointer
├── hooks    # event hook samples (scripts that run on defined events)
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   └── update.sample
├── info
│   └── exclude    # contains files that should be excluded from the repository
├── objects
│   ├── info    # object information
│   └── pack    # pack files
└── refs
    ├── heads    # branch pointers
    └── tags    # tag pointers

9 directories, 13 files
```

## 4. git add

### 4.1. git add internals

The `index` is **a temporary and dynamic binary file** that describes **the directory structure of the entire repository**. More specifically, the `index` captures a version of the project’s overall structure at some moment in time. The project’s state could be represented by a commit and a tree from any point in the project’s history, or it could be a future state toward which you are actively developing.

关于index:

- （1） 存储位置： `.git/index`
- （2） 存储格式： a temporary and dynamic binary file
- （3） 存储内容： the directory structure of the entire repository

One of the key, distinguishing features of Git is that it enables you to alter the contents of the index in methodical, well-defined steps. The `index` allows a separation between **incremental development steps** and **the committal of those changes**.

## 5. git commit

### 5.1. git commit concept

```txt
staging area --> repository
```

```txt
index --> object store
```

Git is a version control system built on top of an **object store**. Git creates and stores a collection of objects when you commit.

The main Git objects we’re concerned with: `commit`s, `blob`s, and `tree`s. There’s also a `tag` object.

### 5.2. git commit internals

At the heart of Git’s repository implementation is the **object store**. It contains your original data files and all the log messages, author information, dates, and other information required to rebuild any version or branch of the project.

Git places only **four types of objects** in the **object store**: the `blobs`, `trees`, `commits`, and `tags`. These four atomic objects form the foundation of Git’s higher level data structures.

- `Blobs`: Each version of a file is represented as a blob. Blob, a contraction of “binary large object,” is a term that’s commonly used in computing to refer to some variable or file that can contain any data and whose internal structure is ignored by the program. A blob is treated as being opaque. A blob holds a file’s data but does not contain any metadata about the file or even its name.
- `Trees`: A tree object represents one level of directory information. It records blob identifiers, path names, and a bit of metadata for all the files in one directory. It can also recursively reference other (sub)tree objects and thus build a complete hierarchy of files and subdirectories.
- `Commits`: A commit object holds metadata for each change introduced into the repository, including the author, committer, commit date, and log message. Each commit points to a tree object that captures, in one complete snapshot, the state of the repository at the time the commit was performed. The initial commit, or root commit, has no parent. Most commits have one commit parent, although in some situations a commit can reference more than one parent.
- `Tags`: A tag object assigns an arbitrary yet presumably human readable name to a specific object, usually a commit. Although 9da581d910c9c4ac93557ca4859e767f5caf5169 refers to an exact and well-defined commit, a more familiar tag name like `Ver-1.0-Alpha` might make more sense!

| Git Concepts      | Git Internals                |
| ----------------- | ---------------------------- |
| repository        | `<repo>/.git/objects/`       |
| staging area      | `<repo>/.git/index`          |
| working directory | `<repo>`，排除`<repo>/.git/` |

### blob

```bash

```

### tree

### commit

### parent commit

Every `commit` object points to its **parent commit**. The **parent commit** in a linear, branchless history is the one that immediately preceded it. The only commit that lacks a parent commit is the initial commit: the first commit in the repository. By following the parent commit, its parent, its parent, and so on, you can always get back from the current commit to the initial commit.

### tag





