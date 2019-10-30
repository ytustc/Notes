本文参考廖雪峰的git教程，要是哪天忘了就去看廖雪峰的

git分为：

	工作区:
		工作区就是当前的工作目录，
		git init 这是第一步，把当前目录设置为工作区
	版本库（.git）：
		当前目录下有一个.git的隐藏文件夹，这就是版本库
		版本库又可以分为：
			stage（暂存区）
				暂存区放的是从工作区add进来的文件，
				git add filename就是将工作区的文件放到暂存区，暂存区就相当于一个草稿，还没正式提交
			branch（完成分支）
				完成分支是一个链表master，HEAD指向这个链表，每个节点就是每次提交的版本；
				git commit -m "xxx"这就将暂存区的所有文件链接到了完成分支的后面；
				这一步搞定，暂存区就空了，也创造了一个成功的分支；
				后面的就是把这个分支上传到远程仓库GitHub
	远程仓库；
		先在GitHub上创建一个repository，这时候这个仓库是空的，假如我在GitHub上创建了一个新仓库learngit
		现在让本地的版本库和远程的关联起来就用下面这条命令
		git remote add origin git@github.com:ytustc/learngit.git
		origin就是远程库的名字
		
		下面把本地版本库的所有内容推送到远程库上
		git push -u origin master //master是版本库的分支名字
		如果没有前面的关联版本库操作，那么上面这条指令会提示你输入用户名密码
		这是第一次将本地版本库master和远程库master合并，以后要更新远程库，只需要
		git push origin master 即可
		git clone可以下载远程库
		

其它命令：
	版本管理相关：
	git chechout -- readme.c //撤销在工作区对文件的修改
	git status //很重要，查看暂存区文件状态
	git reset HEAD^ readme.c//回退到上一版本，这时候工作区的文件readme.c就变成完成分支下的最近提交的版本
	git diff HEAD -- readme.c //查看工作区的readme.c和版本库的最新版本区别
	git log		//查看版本库的提交记录commit后面一串sha1加密的字符串是版本号
		可以用git reset --hard commitID 用来回退版本的，commitID就是版本号，但不必全部写完，前五个字符就行了
	git reflog  记录每次更新版本的指令，可以用这个找到所有的版本号，回退过去还可以回到现在
	删除文件：
	rm readme.c //删除工作区文件，这时候还没有删掉版本库的文件,需要下面两条指令
		git rm readme 
		git commit -m "删除了这个文件"
		你如果误删了工作区的文件，但是没有删除版本库的，那git chechout -- readme就能回来
	

