# Git Configuration

## Configuration Files

Git’s configuration files are all simple text files in the style of `.ini` files.

Like many tools, Git supports a hierarchy of configuration files. In decreasing precedence they are:

- `.git/config`: Repository-specific configuration settings manipulated with the `--file` option or by default. These settings have the highest precedence.
- `~/.gitconfig`: User-specific configuration settings manipulated with the `--global` option.
- `/etc/gitconfig`: System-wide configuration settings manipulated with the `--system` option if you have proper Unix file write permissions on it. These settings have the lowest precedence. Depending on your actual installation, the system settings file might be somewhere else (perhaps in `/usr/local/etc/gitconfig`), or may be entirely absent.

For example, to establish **an author name** and **email address** that will be used on all the commits you make for all of your repositories, configure values for `user.name` and `user.email` in your `$HOME/.gitconfig` file using `git config --global`:

```bash
git config --global user.name "Jon Loeliger"
git config --global user.email "jdl@example.com"
```

Or, to set a repository-specific name and email address that would override a `--global` setting, simply omit the `--global` flag:

```bash
git config user.name "Jon Loeliger"
git config user.email "jdl@special-project.example.org"
```

Use `git config -l` to list the settings of all the variables collectively found in the complete set of configuration files:

```bash
git config -l
```

Use the `--unset` option to remove a setting:

```bash
git config --unset --global user.email
```

Multiple configuration options and environment variables frequently exist for the same purpose. For example, the editor to be used when composing a commit log message follows these steps, in order:

- `GIT_EDITOR` environment variable
- `core.editor` configuration option
- `VISUAL` environment variable
- `EDITOR` environment variable
- the `vi` command

### Configuring an Alias

For starters, here is a tip for setting up command aliases. If there is a common but
complex Git command that you type frequently, consider setting up a simple Git alias
for it.

```bash
git config --global alias.show-graph \
'log --graph --abbrev-commit --pretty=oneline'
```

In this example, I’ve made up the `show-graph` alias and made it available for use in any repository I make. Now when I use the command `git show-graph`, it is just like I had typed that long `git log` command with all those options.
