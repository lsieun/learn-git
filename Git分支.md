分支简介
实例演示
冲突解决
分支命令

创建分支
切换分支
删除分支
本地分支
远程分支
全并分支
Stash操作
变基操作

	#添加分支
	git branch <branch_name>

	#查看分支
	git branch

	#切换分支
	git checkout <branch_name>

	#创建分支并同时切换到该分支，一步到位
	git checkout -b <branch_name>

	#查看各个分支所在的提交节点
	git branch -v

	#合并分支（将<branch_name>分支合并到当前分支）
	git merge <branch_name>

	#删除分支
	git branch -d <branch_name>

冲突解决要点：

1. 在同一仓库，不同分支上，修改同一文件
2. 在同一仓库，同一分支上，不同的人，修改了同一文件
3. 不同的仓库，修改了同一文件
4. 冲突只在合并分支的时候才会发生
5. 发生冲突并不可怕，冲突的代码不会丢失
6. 解决冲突，重新提交，commit时不要给message
7. 冲突信息的格式


	git reset <hash> --hard






