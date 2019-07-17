# learn-git

:cherry_blossom:  学习Git笔记

学习网站：

- GitHub Help: https://help.github.com/
- Writing on GitHub: https://help.github.com/categories/writing-on-github/
- dotfiles: http://dotfiles.github.io/

Repository是一个“生态环境”

Working Directory 和 `.git/`

就好像河北和北京的关系

The higher level porcelain command

the plumbing command git apply

## Local Repository and OS

- git init

- rm -rf .git/

## Local Repository and Remote Repository

### repo

- git remote --verbose
- git clone URL
- git remote add remote_name URL

### branches

- git branch --list
- git branch --all
- git branch --remotes

- git checkout --track remote_name/branch
- git push --set-upstream remote_name branch_local branch_remote
- git push
- git push --delete remote_name branch_remote


## Local Repository -- branch

- git branch --list
- git checkout branch
- git checkout -b branch branch_parent
- git merge branch

## Branch

- git status
- git log
- git log --oneline

### tag （黄金圣斗士）

- `git tag`: List all tags
- `git show <tag_name>`

### commit area (in repo) （青铜圣斗士）

- git commit --amend
- git show commit
- `git tag <tag_name> <commit_id>`

### staging area (out of repo) （竞技场）

- git commit -m "message"
- git reset HEAD filename

### working directory （普通人）

- git add --all
- git add filename(s)
- git add --patch filename

## JGit

- [JGit](https://www.eclipse.org/jgit/)
- [JGit - Tutorial](https://www.vogella.com/tutorials/JGit/article.html)
- [jgit-cookbook](https://github.com/centic9/jgit-cookbook/)
- [eclipse/jgit](https://github.com/eclipse/jgit)


- the history of branches
  - rewrite commit data
  - make lots of small commits into a single commit
  - make commit messages contain more information
- jargon
- Git’s internals
- command: detail the large number of options for Git’s commands

纲举目张

纲举目张是一个汉语成语，读音为gāng jǔ mù zhāng，意思是提起鱼网上的大绳一抛，一个个网眼就都张开了。比喻文章条理分明，也指抓住事物的关键，带动其他环节。也形容文章条理分明。出自战国·吕不韦《吕氏春秋·用民》：“壹引其纲，万目皆张。”

There's an old saying that "when all you have is a hammer, everything looks like a nail."
