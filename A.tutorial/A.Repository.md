# Repository

学一样东西（例如“Git”），重要的是理解其中涉及的“概念体系”。这个概念体系，应该是一点点展开的。每展开一个概念，同时又有相应的实际操作命令。

Git最核心的两点：

（1）保持“数据的逻辑一致性”。（静）
（2）从“时间维度”展开。（动）

保持“数据的逻辑一致性”。从公司的角度来说，程序代码是由开发人员（Developer）编写的，它的作用就是为了完成一定的业务功能。当然，对于不同的公司来说，代码需要完成的业务功能是不一样的。从Git的角度来说，

代码-业务-公司（精神，抽象）
代码-数据-Git（肉体，具体）

“文以载道”的意思是说“文”像车，“道”像车上所载之货物，通过车的运载，可以达到目的地。文学也就是传播儒家之“道”的手段和工具。这样的文学观念偏于文学的教化目的。

这个道理，其实大家都潜移默化的知道它，只是很少有人会从这个角度来阐述它。

OS/Linux/Windows
Directory

Git
Repository

有那么五分钟，说明我们要解决什么问题，如果你已经听懂了，那么之后的内容可以直接跳过。

有选择性的去学，有一个nivagate去做说明要从哪儿去学？

When you create a new repository in Git, you generally begin from one of three starting points:

- From a clone of an existing repository
- From an existing folder of untracked files
- From an empty directory

## Cloning an Existing Project

To download a copy of a project, you will use the command `clone`.

Unlike *downloading a zipped set of files*, **creating a clone of a project** will download a copy of all the files in the repository—along with **the commit history** —and it will remember where you downloaded the code from by setting up **the remote code hosting server** as **a tracked repository**. Don’t worry, it doesn’t keep a persistent connection, but rather it bookmarks the location in case you want to check for updates and download them to your local repository at a later date.

```bash
# git clone <url>
$ git clone https://gitlab.com/gitforteams/gitforteams.git
```

## Converting an Existing Project to Git

You can start with any folder of files and create a Git repository from it using the initialization command `init`. Git will be aware of all files in this directory, including subfolders, so make sure you run the command `init` from the root folder for your project.

```bash
# Initialize a directory for version control
$ git init
```

You should get into the habit of using the command `status` as frequently as you would. This command lets you know what’s happening at this moment in your repository—and knowing what’s happening is key to understanding Git. Go ahead and check the status of your repository now.

```bash
# Check the status of your repository
$ git status
```

**Getting your files into Git** is **a two-step process**. Although it feels a little tedious when you’re first getting started, this is a feature because it allows you to make **multiple unrelated changes** at once in your working directory. **Changes** can be **staged** into **groups of commits** in the index—each group getting a different commit message.

We want to add everything that is in our working directory because this is the initial import of files.

```bash
# Add all files to the staging area of your repository
$ git add --all
```

staging area

Now that your files are added, you can save their current state into the repository with the command `commit`.

```bash
# Commit all staged files to your repository
$ git commit -m "Initial import of all project files."
```

## Initializing an Empty Project

When we teach Git, it’s generally easiest to start with a completely empty directory, void of any files.

```bash
# 1. Create a new, empty folder:
$ mkdir empty-repository
# 2. Change into your new folder:
$ cd empty-repository
# 3. Run the Git initialization command:
$ git init
# 4. Verify the hidden repository folder was added:
$ ls -al
```

If you see a new hidden folder, `.git`, your repository has been created. This folder will contain the record of all the changes to your repository. There’s nothing scary contained in this folder, but if you remove it, your project will no longer be tracked. This means you will not be able to recover previous versions of any of the files in your repository, you will lose all commit messages for your repository, and whatever state the files are currently in will be immutable.

### Reviewing History

Once you have made your first commit into a repository, you are ready to start reviewing history.

To review the changes that have been made in a repository, use the command `log`. By default, this command allows you to review the commit message and author information for every commit in the branch that is currently checked out of your local repository.

```bash
# Reviewing a repository’s history with log
$ git log
```

The command `log` will output a full history of your repository’s commit messages in **reverse chronological order**.

If, however, you are working with a more established code base, there will be a lot of messages. This can be quite overwhelming and difficult to scan. You can shorten the messages to just the first line of the message by adding the parameter `--oneline`. To exit, press `q`.

```bash
# Viewing a condensed history of your project
$ git log --oneline
```


```bash
# 

```

Other branches will have different commits, and different copies of
the repository will have commits made by different developers. It’s
basically anarchy, but limited to each little repository. The conven‐
tions we establish as software teams are **what bring order to the
chaos** and allow us to share our work in a sane manner. (Remem‐
ber **the branching strategies** we learned in Chapter 3? They’ll **keep
the work sorted into logical thought streams**. Remember the **per‐
mission strategies** from Chapter 2? They’ll keep people locked into
the right place, and unable to make changes to the “blessed” reposi‐
tory without the community gatekeeper’s consent.)




