# git常规用法
---

## windows下配置git和Github:  
1. 注册Github账号，安装 Git for windows客户端；
2. Git bash下输入以下命令：  
	`ssh-keygen -t rsa -C "your_email_address_registerd_on_github"`，在当前路径下生成`.ssh`文件夹，复制目录下的公钥`id_rsa.pub`,回到Github上，点击*Add SSH Key*,添加title和刚才复制过来的key；
3. 本地验证是否认证成功，在Git bash下输入`ssh -T git@github.com`, 认证通过后会提示成功；
4. 配置本地用户名和邮件：  
```
$ git config --global user.name "your name"
$ git config --global user.email "your_email_address"
```

## Git基本命令:

1. __git remote__
	* 进入要上传的仓库，右键git bash
	* 输入：`git remote add origin git@github.com:your_github_name/your_repo.git`
2. __git clone__
	* `git clone /path/to/local_repository`：克隆本地仓库到当前目录； 
	* `git clone git@github.com:github_usename/repo_name.git`：克隆远程服务器上的仓库。
3. __workflow__
	* 本地仓库的三种状态：_working dir_, _Index(stage)_, _HEAD_,即“工作目录”，“缓存区域”，“已提交状态”。  
	* 正常提交流程：
		1. `git status`：本地改动之后，查看改动详情；
		2. `git add filename`：提交单个文件,或者提交所有`git add *`到暂缓区域；
		3. `git commit -m "your comment for this commit"`：最终提交；
		4. `git push`：推送到远端仓库。
4. __git branch__
	* `git branch`：查看当前所有的分支；
	* `git checkout -b your_new_branch_name`：切换分支，如果没有则新建分支；
	* `git checkout master`：回到主分支；
	* `git branch -d branch_name_you_will_delete`:删除分支，__主分支上才能操作__
	* `git push origin <branch>`:除非你将分支推送到远程仓库，不然该本地分支不会被他人看见。
5. __merge and pull__
	* `git pull`:获取远程更新；
	* `git merge <branch>`:合并其他分支到当前分支；
	* `git diff <source_branch> <target_branch>`:预览差异。
6. __tag：__`git log`查看本地的提交信息
7. __undo__
	* `git checkout -- <filename>`:该命令会将HEAD中的最新内容替换掉你工作目录中的文件，已添加到暂缓区的改动和新文件不会受到影响；
	* `git fetch origin`:获取远端仓库的最新版本；
	* `git reset --hard origin/master`:丢弃本地的所有改动与提交，并将本地分支指向它。
8. __GUI__
	* `git config color.ui true`:彩色的git输出；
	* `git config format.pretty oneline`:显示历史纪录是，每个提交的信息只显示一行；
	* `git add -i`:交互式添加文件到暂缓区。
9. __git reference__
	* [《Pro Git》](https://git-scm.com/book/en/v2)
	* [图解Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
	* [git-简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
	* [如何高效利用Github](http://www.yangzhiping.com/tech/github.html)
