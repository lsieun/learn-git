# After Install

## name and email

```bash
## 配置name和email信息
$ git config --global user.name "Tom Cat"
$ git config --global user.email "tom@example.com"
```

## Enabling Auto-complete If You Don't Have It

第一种方案

The shortest way to activate the bash auto-completion for Git on Debian is to add

```bash
source /etc/bash_completion.d/git
```

to the `~/.bashrc` (and restart the terminal).

第二种方案

You need to `source /etc/bash_completion.d/git` to enable **git auto-completion**.

In my `.bashrc` it's done with:

```bash
for file in /etc/bash_completion.d/* ; do
    source "$file"
done
```

第三种方案

Auto-complete is already enabled in Git for Windows and some other distributions. For other versions (Linux, OS X) where it is not enabled, you can download scripts that implement this feature for different shells from

```url
https://github.com/git/git/tree/master/contrib/completion
```

An alternate approach, a simple way is just to click the desired script and then find the button labeled `Raw` on that page. Click that button to go to a web page with just the contents of that file. Then, you can download that script to your local system (through the browser) and add it into the appropriate init file in your home directory or into the appropriate directory for auto-completion for all users if your shell supports that.

Here's the direct link for the raw version:

```txt
https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
```

After getting the raw version of the file, you can download that page as the file `git-completion.bash` to your local system. Once the script is downloaded, you add a line like the following into your `.bashrc` file (create the file if needed):

```bash
source ~/git-completion.bash
```

To extend this functionality for all users, you'll need to find out where your particular OS stores and expects to find **auto-completion scripts** and put the downloaded file there. For most bash systems, there is a `/etc/bash_completion.d` directory where scripts like this can be stored to be loaded. If you're not sure where the location is, try searching for completion on your file system, or consult Google.

