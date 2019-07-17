# config

<!-- TOC -->

- [1. syntax](#1-syntax)
- [2. dissect an example](#2-dissect-an-example)
- [3. Configuration Scope](#3-Configuration-Scope)
  - [3.1. System](#31-System)
  - [3.2. Global](#32-Global)
  - [3.3. Local](#33-Local)
- [Seeing Configuration Values](#Seeing-Configuration-Values)
- [Undoing a Configuration Setting](#Undoing-a-Configuration-Setting)
- [Listing Configuration Settings](#Listing-Configuration-Settings)

<!-- /TOC -->

## 1. syntax

To set configuration values in Git, you use the `config` command. Here's the syntax:

```bash
git config [<file-option>] [type] [-z|--null] name [value [value_regex]]
git config [<file-option>] [type] --add name value
git config [<file-option>] [type] --replace-all name value [value_regex]
git config [<file-option>] [type] [-z|--null] --get name [value_regex]
git config [<file-option>] [type] [-z|--null] --get-all name [value_regex]
git config [<file-option>] [type] [-z|--null] --get-regexp name_regex [value_regex]
git config [<file-option>] --unset name [value_regex]
git config [<file-option>] --unset-all name [value_regex]
git config [<file-option>] --rename-section old_name new_name
git config [<file-option>] --remove-section name
git config [<file-option>] [-z|--null] -l | --list
git config [<file-option>] --get-color name [default]
git config [<file-option>] --get-colorbool name [stdout-is-tty]
git config [<file-option>] -e | --edit

```

## 2. dissect an example

Now here's an example of the most common syntax:

```bash
git config --global user.name "Joe Gituser"
```

Let's dissect the various parts of this command.

- `git config`: The first two pieces are simply issuing the `config` command from `git`. 
- `--global`: After that is an **option**, `global`, (preceded by **two hyphens** because you are spelling it out).
- `user.name`: Next comes the configuration setting that you're updating: `user.name`. Git uses a "`.`" notation to separate out the two pieces of a configuration setting—in this case, `user` and `name`. Think of this as setting the name value of the user section in the configuration.
- `"Joe Gituser"`: And finally, you have the actual value that you're setting this configuration setting to. Notice that because you have spaces in the value, you need to enclose the entire string in quotes.

Here's another example:

```bash
git config --global user.email Joe.Gituser@mailhost.com
```

One additional note: Git configuration settings are stored in text files. It is possible to change these settings by editing the associated text files, but this is highly discouraged because it's easy to make a mistake and also to accidentally modify other settings.

## 3. Configuration Scope

Recall that the Git model is designed for many, smaller repositories instead of fewer, monolithic ones. Because users may normally be working with multiple repositories, it would be inconvenient and subject to error to have to configure the same settings in each repository. As a result, Git provides options to simplify choosing **the scope for configuration values**.

这段的意思是：

- （1） Git适合于many, smaller repositories，而并非fewer, monolithic repositories。
- （2） Git在配置（Configuration）的范围方面来满足多样性。

There are **three levels** available for configuration: `system`, `global`, and `local`.

### 3.1. System

Configuration at the system level means that a configuration value applies to all repositories on a given system (machine) unless it's overridden at a lower level. These settings apply regardless of the particular user.

To ensure that a configuration value applies at the system level, you specify the `--system` option for the `config` command, as in `git config --system core.autocrlf true`.

These settings are usually stored in a `gitconfig` file in either `/usr/etc` or `/usr/local/etc`. On a Windows system, if you're using Git for Windows, the system file is in `C:\ProgramData\Git\config`. In other systems, look in the directory where Git was installed.

存储位置：在CentOS 7上， Git版本是1.8.3.1，配置文件是在`/etc/gitconfig`。但是，没有验证在其他操作系统上的位置是在哪里。

### 3.2. Global

Configuration at the global level implies that a configuration value applies to all of the repositories for a particular user, unless overridden at the local level. Unless you need repository-specific settings, this is the most common level for users to work with because it saves the effort of having to set values for each repository.

An example of setting values at the global level would be the configuration for `user.name` and `user.email` where the `--global` option was incorporated. These settings are stored in a file named `.gitconfig` in each user's home directory.

存储位置：`~/.gitconfig`

### 3.3. Local

Setting a configuration value at the local level means that the setting only applies in the context of that one repository. This can be useful in cases where you need to specify unique settings that are particular to one repository. It can also be useful if you need to temporarily override a higher-level setting.

An example could be overriding the global end of line settings because content in a repository is targeted for a different platform. To update settings at this level, you can specify the `--local` option or just omit any of the local, global, or system options for the configuration.

应用场景：换行的标志

As an example of this last point, the following two commands are equivalent: `git config --local core.autocrlf true` and `git config core.autocrlf true`.

The local repository's configuration is stored within the local Git repository, in `.git/config`.

存储位置：`<git repository>/.git/config`

## Seeing Configuration Values

To see what value a particular configuration setting has, you can use `git <setting>` as in `git config user.name`.

## Undoing a Configuration Setting

Occasionally, you may need to remove a user setting at a particular level. Git provides the `unset` option for this, and it's pretty straightforward:

```bash
git config --unset <other options> <value to remove>
```

Other options here would generally refer to one of the scope options

```bash
git config --unset --global user.name
git config --global user.name
```

## Listing Configuration Settings

Another option related to viewing configuration values is `--list`. Supplying the `list` option to `git config` results in a list of all configuration settings being dumped. By default, this list includes local, global, and system settings without qualification. So, if you have both a local and global value for the same setting, you will see both.

```bash
git config --list
```

If the settings have the same values, this can be confusing (and potentially misleading) if you're not aware of the reasons behind it. To work around seeing these multiple values, you can refine the list by specifying one of the scope options.

```bash
git config --local --list
```

