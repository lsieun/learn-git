# config

## Telling Git Who You Are

One of the first things that you need to configure in Git is who you are, in terms of the username and e-mail address. Git expects you to set these two values, regardless of what interface or version of Git you use. This is because Git is a source management system. Because its purpose is to track changes by users over time, it wants to know who is making those changes so that it can record them.

The values can be set via commands:

```bash
git config --global user.name <name>
git config --global user.email <email address>
```

**The e-mail address is not validated** when you set it in Git. In fact, you can enter any e-mail address and Git will be happy. However, there is some advanced functionality in Git that uses this e-mail address. That functionality allows for tasks such as creating and sharing patches and zipped versions of changes. For that functionality, **having a correct e-mail address is important**. Also, there are other tools, such as Gerrit (a code-review tool built on top of Git), that heavily utilize the e-mail address and depend on it being correct.

使用email的时候，可以不用写对。但是，写对了，是有好处的。

## Default Editor

The default editor is primarily used when you need to type in a message while making a `commit` into the repository. If you don't supply the message in the command line when you do the commit, Git will bring up the default editor on your system to allow you to type one in.

If you would rather use a different editor, you can use the following config command to specify which one to use: `git config --global core.editor <editor name or path + name> <optional options for the editor>`.

The `--global` option is not required, but most users want to use the same editor for all of their repositories. Here again, you can break down `core.editor` as the editor value in the core section of the configuration.

If the editor is already in the path that Git knows about, then the path isn't required. Here are some examples of configuring editors:

```bash
## Linux
git config --global core.editor vim
## OS X
git config --global core.editor "nano"
## Windows
git config core.editor "'C:\Program Files\windowsnt\accessories\wordpad.exe'"
## Bash shell on Git for Windows
git config --global core.editor "'C:/Program Files(x86)/Notepad++/notepad++.exe' -multiInst -noSession -notabbar"
```

Note the different uses for **single quotes** and **double quotes** in the respective examples. Also, in the last example, `-multInst`, `-noSession`, and `-notabbar` are all options to Notepad++ to make it simpler to use. (`multInst` tells Notepad++ to allow multiple instances to run; `noSession` tells it not to remember the session state—that is, not to load the last file you were working on; and `notabbar` just avoids displaying
the tabbed selection bar at the top.)

## End of Line Settings

### CRLF

A **carriage return**, sometimes known as a cartridge return and often shortened to `CR`, `<CR>` or `return`, is a control character or mechanism used to reset a device's position to **the beginning of a line of text**.

Newline (frequently called line ending, end of line (EOL), **line feed**, or line break) is a control character or sequence of control characters in a character encoding specification (e.g. ASCII or EBCDIC) that is used to signify **the end of a line of text** and **the start of a new one**.

`CR` and `LF` are control characters, respectively coded `0x0D` (13 decimal) and `0x0A` (10 decimal).

They are used to mark a **line break** in a text file. As we know, Windows uses two characters the `CR LF` sequence; Unix only uses `LF` and the old MacOS ( pre-OSX MacIntosh) used `CR`.

### autocrlf

Now, let's look at one of the key settings users need to manage with Git: handling **end of line** (`EOL`) values. Git manages the **two types of line endings**: **carriage returns/line feeds** (`CRLF`) for Windows and **line feeds** (`LF`) for OS X/Linux.

In the context of Git, there are two options that are controlled by the `EOL` setting<sub>注：在两个地方控制EOL的值</sub>:

- How line endings are stored in content when it is committed into the repository<sub>注：第一个地方，从working directory提交到repository的时候</sub>
- How line endings are updated (or not) when content is checked out of the repository onto a local disk<sub>注：第二个地方，从repository检出到working directory的时候</sub>

The first item refers to **whether or not Git normalizes line endings in the repository**. Normalizing refers to stripping out `CR`s and only storing files with `LF`s.

- normalize
  - to make something or somebody conform to a standard

For the second item, when content is checked out of Git, Git can update line endings in text files. This option allows you to specify **whether or not Git updates line endings in files after checkout**, and, if it does, which type it sets them to.

At a user or repository level, how Git handles these options is controlled by a configuration setting named `core.autocrlf`. As before, the "`.`" is a separator, and you can think of the first part as the section of the configuration, and the second part as the specific value being set in that section. The `crlf` part here obviously stands for **carriage return, line-feed**—meaning the common EOL sequence for files on a Windows environment. The `auto` part refers to automatically inserting `CRLF` sequences in files when they are checked out.

There are **three possible values** for the `core.autocrlf` setting:

- `core.autocrlf=true`. This value tells Git to normalize line endings to just `LF`s when storing files in the repository and to automatically insert `CRLF`s when files are checked out. If users are working on a **Windows** environment, this is **the recommended value**. It allows them to get `CRLF`s in files when checked out from Git, but doesn't store the `CR`s in the repository.

```bash
git config --global core.autocrlf true
```

- `core.autocrlf=input`. This value tells Git to normalize line endings to just `LF`s when storing files in the repository but not to change anything when files are checked out. If users are working in a **Unix** environment, this is the recommended value because Unix expects just `LF`s.

```bash
git config --global core.autocrlf input
```

- `core.autocrlf=false`. This default value tells Git not to change anything when files are being checked in or checked out. **This is the primary value for the setting that can get users into trouble**. Suppose you have two users working on code for the same repository, one in a Windows environment and one in a Unix environment. If both users have specified the `core.autocrlf=false` value in their configurations, then when they commit changes, the files from Windows will have `CRLF`s and those from Unix will have just `LF`s. If the respective users later each check out the other's files, then the files will have the wrong line endings for their system. For this reason, this value should not be used when **mixed** environments are being used in a project.

```bash
git config --global core.autocrlf false
```

In general, it's a best practice to set the `core.autocrlf` setting to one of the values other than `false`, depending on which environment you're working in.

It should also be noted that there are other configuration settings that can contribute to how line endings are handled. However, these settings are more obscure and broader in terms of what they affect. Also, **their default values generally work well** for what most users need to do.
