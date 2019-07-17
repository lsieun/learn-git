# Git Command Format

<!-- TOC -->

- [1. The general form of commands](#1-The-general-form-of-commands)
- [2. Operand Types](#2-Operand-Types)
  - [2.1. two types](#21-two-types)
  - [2.2. why two types](#22-why-two-types)
  - [2.3. the special separation symbol](#23-the-special-separation-symbol)
- [3. Porcelain versus Plumbing Commands](#3-Porcelain-versus-Plumbing-Commands)
  - [3.1. two categories commands](#31-two-categories-commands)
  - [3.2. Porcelain Commands in Git](#32-Porcelain-Commands-in-Git)
  - [3.3. Plumbing Commands in Git](#33-Plumbing-Commands-in-Git)
- [4. Specifying Options](#4-Specifying-Options)

<!-- /TOC -->

## 1. The general form of commands

The general form of commands is as follows:

```bash
git <git-options> <command> <command-options> <operands>
```

Components of a Git Command Line Invocation

| Element             | Description                         | Example                 |
| ------------------- | ----------------------------------- | ----------------------- |
| `git`               | Command to run Git                  |                         |
| `<git-option>`      | Global options for Git itself.      | `git --version`         |
| `<command>`         | Git command to execute              | `git push`              |
| `<command-options>` | Options to the specified command    | `git commit -m "hello"` |
| `<operands>`        | Items for the command to operate on | `git add *.txt`         |

后续内容：

- `<git-option>`
- `<command>`： （2）命令分类（Porcelain versus Plumbing Commands）
- `<command-options>`: （3） 指定命令的选项（Specifying Options）
- `<operands>`： （1）参数类型（Operand Types）

## 2. Operand Types

The general form of commands is as follows:

```bash
git <git-options> <command> <command-options> <operands>
```

这里的重点是`<operands>`那一部分。

### 2.1. two types

Git can take different kinds of operands, which are specifications of objects to operate on. The two most common operands are **the SHA1 value of a commit** (or a named branch or tag that refers to such a commit) and **a path specification to a file or directory on the disk**.

对于operands，可以分成两种类型：

- (1) the SHA1 value of a commit
- (2) a path specification to a file or directory on the disk

For many commands, either or both of these value types may be specified—or neither. When neither operand is specified, the command will operate against all eligible items that it finds in the scope of **the repository**, **staging area**, or **working directory tree**.

对于不同的command来说，它们需要的不同的operands：

- （1）有的需要两种类型的operand
- （2）有的需要其中一种类型的operand
- （3）有的不需要任何类型的operand

### 2.2. why two types

The primary reason to specify both **commit references** and **paths** would be to select **certain paths** that are part of, or in the scope of, **the snapshot** associated with **the commit**. Because Git operates at the granularity of a snapshot (`tree`), you may not always want to do the operation against all items in the snapshot. However, that's what would happen if you just specified the `commit` | `tag` | `branch`. To indicate that the operation should only be done against **certain files or paths** in the scope of the snapshot, you need to add **specific filenames or paths**.

这段的逻辑是这样：为什么要使用commit references和paths这两种类型的operand呢？

- （1）在commit references的内部是含有一个tree的
- （2）而tree，就是在某一时刻整个working directory的snapshot，会包含所有的文件和目录
- （3）综合前两条，操作一个commit reference，就意味着操作在那一时刻所有的文件和目录
- （4）但有些时候，你并不是想操作那个snapshot当中所有的文件和目录，而是其中的几个文件，所以就有了pathes类型的operand

### 2.3. the special separation symbol

When both types are specified, if there is a possibility of Git not being able to tell the difference between a `commit` | `branch` | `tag` and **one or more of the filenames or paths**, then you can separate the two types using the special separation symbol "`--`". Normally, this won't be needed if a commit is expressed as a SHA1 value, but it may be needed if `branch` or `tag` names could be mistaken as **names for files or paths**.

这里就引来了一个问题：这两种类型的operand产生混淆了怎么办呢？

- 回答：加个分隔符号you can separate the two types using the special separation symbol "`--`"

As an example, the command `git <command> a1b2c3d4 file1.txt` might be clear enough, but `git <command> my-tag-name -- my-file-name` could be ambiguous enough when parsed to require the "`--`" separator symbol.

## 3. Porcelain versus Plumbing Commands

The general form of commands is as follows:

```bash
git <git-options> <command> <command-options> <operands>
```

这里的重点是`<command>`那一部分。

### 3.1. two categories commands

In Git, there are two categories for the types of commands: **porcelain** and **plumbing**. Those names may sound strange.

将commands分成两类：

- porcelain commands (higher-level commands) (user-friendly commands) 
- plumbing commands (low-level commands)

The **porcelain commands** are intended to be user-facing, more commonly used, and more convenient. They also typically provide a higher level of functionality.

介绍porcelain commands

The **plumbing commands** function at a lower level and are not expected to be used by the average user. These commands are typically targeted at extracting or modifying content and information more directly from the repository. An example would be the `git cat-file` or `git ls-files` commands that provide a way to look at the contents of a file or directory within the repository if you know how to reference those elements.

介绍plumbing commands

Certain functionality in Git can be accomplished using either **porcelain commands** or **plumbing commands**. However, it would usually take several very specific plumbing commands to accomplish what one porcelain command can do. The **porcelain commands** are based on the **plumbing commands**. They aggregate the functionality of plumbing commands and certain options and sequences in order to make things simpler for the typical Git user.

介绍porcelain commands和plumbing commands两者之间的依赖关系。

In general, you don’t have to view or manipulate the files in `.git`. These “hidden” files are considered part of Git’s plumbing or configuration. Git has a small set of **plumbing commands** to manipulate these hidden files, but you will rarely use them.

- plumbing
  - （建筑物的）管路系统，自来水管道 the system of pipes, etc. that supply water to a building

- plumb
  - 探索；钻研；探究 to try to understand or succeed in understanding sth mysterious

### 3.2. Porcelain Commands in Git

| Command     | Purpose                                                      |
| ----------- | ------------------------------------------------------------ |
| add         | Add file contents to the index.                              |
| bisect      | Find by binary search the change that introduced a bug.      |
| branch      | List, create, or delete branches.                            |
| checkout    | Switch branches or restore working tree files.               |
| cherry      | Find commits yet to be applied to upstream (branch on the remote). |
| cherry-pick | Apply the changes introduced by some existing commits.       |
| clone       | Clone a repository into a new directory.                     |
| commit      | Record changes to the repository.                            |
| config      | Get and set repository or global options.                    |
| diff        | Show changes between commits, commits and working tree, and so on. |
| fetch       | Download objects and refs from another repository.           |
| grep        | Print lines matching a pattern.                              |
| help        | Display help information.                                    |
| log         | Show commit logs.                                            |
| merge       | Join two or more development histories together.             |
| mv          | Move or rename a file, directory, or symlink.                |
| pull        | Fetch from, or integrate with, another repository or a local branch. |
| push        | Update remote refs along with associated objects.            |
| rebase      | Forward-port local commits to the updated upstream head.     |
| rerere      | Reuse recorded resolution for merged conflicts.              |
| reset       | Reset current HEAD to the specified state.                   |
| revert      | Revert some existing commits.                                |
| rm          | Remove files from the working tree and from the index.       |
| show        | Show various types of objects.                               |
| status      | Show the working tree status.                                |
| submodule   | Initialize, update, or inspect submodules.                   |
| subtree     | Merge subtrees and split repositories into subtrees.         |
| tag         | Create, list, delete, or verify a tagged object.             |
| worktree    | Manage multiple working trees.                               |

### 3.3. Plumbing Commands in Git

| Command       | Purpose                                                      |
| ------------- | ------------------------------------------------------------ |
| cat-file      | Provide content or type and size information for repository objects. |
| commit-tree   | Create a new commit object.                                  |
| count-objects | Count an unpacked number of objects and their disk consumption. |
| diff-index    | Compare a tree to the working tree or index.                 |
| for-each-ref  | Output information on each ref.                              |
| hash-object   | Compute object ID and optionally create a blob from a file.  |
| ls-files      | Show information about files in the index and the working tree. |
| merge-base    | Find as good common ancestors as possible for a merge.       |
| read-tree     | Read tree information into the index.                        |
| rev-list      | List commit objects in reverse chronological order.          |
| rev-parse     | Pick out and massage parameters.                             |
| show-ref      | List references in a local repository.                       |
| symbolic-ref  | Read, modify, and delete symbolic refs.                      |
| update-index  | Register file contents in the working tree to the index.     |
| update-ref    | Update the object name stored in a ref safely.               |
| verify-pack   | Validate packed Git archive files.                           |
| write-tree    | Create a tree object from the current index.                 |

假装总结：一个简单且并不靠谱的方法，区分Porcelain Commands和Plumbing Commands：

- Porcelain Commands的形式：`xxx`
- Plumbing Commands的形式：`abc-xyz`

## 4. Specifying Options

The general form of commands is as follows:

```bash
git <git-options> <command> <command-options> <operands>
```

这里的重点主要是`<command-options>`那一部分。

Options supplied either to **Git** or to **Git commands** can be abbreviated as a single letter or spelled out as words. One important note here is that if the option is spelled out, you must precede it with **two hyphens**, as in `--global`.

使用两个hyphen

If the option is abbreviated, **only one hyphen** is required, as in `-a`.

使用一个hyphen

**Abbreviated Options** may be passed together, as in `-am` instead of `-a -m`.

另一种书写方式

When Options are combined in this way, **the ordering is important**. If the first option requires a value, then the second option may be taken as the required value instead of an additional option.

顺序的重要性
