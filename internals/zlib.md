# zlib

Git compresses content using `zlib` compression.

## pigz

```bash
sudo yum install pigz
```

```bash
## （1）初始化Git Repository
$ git init

## （2）添加新文件hello.txt
$ echo "hello world" > hello.txt
$ git hash-object hello.txt
3b18e512dba79e4c8300dd08aeb37f8e728b8dad

## （3）添加hello.txt到staging area
$ git add hello.txt
$ find .git/objects/
.git/objects/
.git/objects/pack
.git/objects/info
.git/objects/3b
.git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad

## 查看blob的内容：对比git cat-file和unpigz之间的区别
$ git cat-file -p 3b18e51
hello world
$ unpigz -c .git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad
blob 12hello world


## （4）将hello.txt从staging area提交到repository
$ git commit -m "First Commit"
[master (root-commit) ff33b2d] First Commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt
$ git rev-parse ff33b2d
ff33b2d27aec54af36b0c2559573e62365a9e045

$ find .git/objects/
.git/objects/
.git/objects/pack
.git/objects/info
.git/objects/3b
.git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad
.git/objects/68
.git/objects/68/aba62e560c0ebc3396e8ae9335232cd93a3f60
.git/objects/ff
.git/objects/ff/33b2d27aec54af36b0c2559573e62365a9e045

## 查看commit的内容：对比git cat-file和unpigz之间的区别
$ git cat-file -p ff33b2d
tree 68aba62e560c0ebc3396e8ae9335232cd93a3f60
author Tom Cat <tom@example.com> 1563349934 -0400
committer Tom Cat <tom@example.com> 1563349934 -0400

First Commit
$ unpigz -c .git/objects/ff/33b2d27aec54af36b0c2559573e62365a9e045
commit 163tree 68aba62e560c0ebc3396e8ae9335232cd93a3f60
author Tom Cat <tom@example.com> 1563349934 -0400
committer Tom Cat <tom@example.com> 1563349934 -0400

First Commit

## 查看tree的内容：对比git cat-file和unpigz之间的区别
$ git cat-file -p 68aba62
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    hello.txt
$ unpigz -c .git/objects/68/aba62e560c0ebc3396e8ae9335232cd93a3f60
tree 37100644 hello.txt;�ۧ�L����r���
```

