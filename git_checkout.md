# checkout相关操作 #

## 将远程仓库的指定分支检出到本地local当中 ##

克隆远程仓库

	git clone http://192.168.1.78/wangyingbin/allin_site_dynamic.git

查看远程分支

	git branch -r

将远程分支进行检出

	git checkout -b <本地分支名> origin/<远程分支名>
	
	git checkout -b allin_site_dynamic_Ebook origin/allin_site_dynamic_Ebook

查看本地分支与远程分支的对应关系

	git branch -vv


