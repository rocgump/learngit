Git is a distributed version control system.
Git is free software.


git init 														把当前目录变成 Git 可以管理的仓库
git add <file>	
	git add readme.txt 								把文件添加到仓库
git commit -m <message>	
	git commit -m "wrote a readme file"		把文件提交到仓库，-m后面输入的是本次提交的说明
	
git status	查看当前的仓库状态
git diff <file>	查看修改的文件内容


提交修改和提交新文件是一样的两步，第一步是git add
在执行第二步git commit之前，我们再运行git status查看要提交的修改，确认后再提交