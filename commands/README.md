# git command README

## git command format

The general form of commands is as follows:

```bash
git <git-options> <command> <command-options> <operands>
```

- [git command format](git_command_01_format.md)

## git command two categories

In Git, there are two categories for the types of commands: **porcelain** and **plumbing**.

- porcelain commands (higher-level commands) (user-friendly commands)
- plumbing commands (low-level commands)

## git command help

```bash
git help <subcommand>
```

示例：

```bash
git help init
```

## Auto-complete

The shortest way to activate the bash auto-completion for Git is to add

```bash
source /etc/bash_completion.d/git
```

to the `~/.bashrc` (and restart the terminal).

Here's an example:

```bash
$ git cl <TAB> <TAB>
clean   clone

$ git config --l <TAB> <TAB>
--list    --local
```

