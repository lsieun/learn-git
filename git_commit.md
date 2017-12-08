# commit相关操作 #

## Git撤销git commit 但是未git push的修改 ##

1. 找到上次git commit的 id
2. 
     git log 
     找到你想撤销的commit_id

2.  git reset --hard commit_id

      完成撤销,同时将代码恢复到前一commit_id 对应的版本。

3. git reset commit_id 
     
	完成Commit命令的撤销，但是不对代码修改进行撤销，可以直接通过git commit 重新提交对本地代码的修改。




