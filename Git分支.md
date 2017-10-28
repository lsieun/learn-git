# branch + conflict + stash #

## 1. branch ##

### 1.1 local branch ###

local branch支持“增、删、改、查”操作，支持“切换 和 合并”操作。

#### 查 ####

查看分支

	git branch
	git branch -v # 其中-v表示查看branch的细节

查看已经（未）合并的分支
	git branch --merged
	git branch --no-merged

#### 增 ####

添加分支

	git branch <branch_name>

#### 改 ####

修改分支的名字

	git branch -m <old_name> <new_name>
	git branch -M <old_name> <new_name>

#### 删 ####

删除分支（-d就是如果在此分支上做了修改，则不能删除；-D强制删除）

	git branch -d <branch_name>
	git branch -D <branch_name>	

#### 切换 ####

切换分支

	git checkout <branch_name>

创建分支,并同时切换到该分支（一步到位）

	git checkout -b <branch_name>

#### 合并 ####

合并分支（将<branch_name>分支合并到当前分支）

	git merge <branch_name>

合并分支，拒绝fast forword，产生合并commit

	git merge --no-ff

### 1.2 remote branch ###

	#列出远程分支
	git branch -r

	#列出远程合并的分支
	git brach -r --merged

	#取出远程分支
	git checkout -t origin/<branch_name>

	#删除远程分支
	git push origin <space>:<remote_branch>
	git fetch -p

## 2.conflict ##

冲突解决要点：

1. 在同一仓库，不同分支上，修改同一文件
2. 在同一仓库，同一分支上，不同的人，修改了同一文件
3. 不同的仓库，修改了同一文件
4. 冲突只在合并分支的时候才会发生
5. 发生冲突并不可怕，冲突的代码不会丢失
6. 解决冲突，重新提交，commit时不要给message
7. 冲突信息的格式



## 3. git stash ##

保存进度

	git stash

弹出进度

	git stash pop

查看stash列表

	git stash list

删除stash列表

	git stash clear



