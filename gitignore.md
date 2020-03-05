# gitignore

输入`git help gitignore`查看gitignore的帮助文档


从字符的角度去理解：#   \    /  *  **  []  ! 

*.txt
*.[ao]

从目录或文件的角度：“文件”和“目录”


A `gitignore` file specifies intentionally untracked files that Git should ignore. Files already tracked by Git are not affected.

> gitignore文件用于明确的指定哪些文件不需要track，而已经track的文件不受gitignore的影响。


The purpose of gitignore files is to ensure that certain files not tracked by Git remain untracked.

To stop tracking a file that is currently tracked, use `git rm --cached`.

如果没有指定目录，就表示任意目录

a.txt
*.txt

## Java

```txt
# IDEA

.idea/
*.iml
*.kotlin_module
target/
lib/
build/
dist/
.*
!.gitignore
```
