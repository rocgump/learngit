Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.


git init 														把当前目录变成 Git 可以管理的仓库
git add <file>	
	git add readme.txt 								把文件添加到仓库
git commit -m <message>	
	git commit -m "wrote a readme file"		把文件提交到仓库，-m后面输入的是本次提交的说明
	
git status	查看当前的仓库状态
git diff <file>	查看修改的文件内容


提交修改和提交新文件是一样的两步，第一步是git add
在执行第二步git commit之前，我们再运行git status查看要提交的修改，确认后再提交

git log 查看仓库提交日志	单行显示使用git log --pretty=oneline
在 Git 中，用HEAD表示当前版本，也就是最新的提交（注意我的提交 ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上 100 个版本写 100 个^比较容易数不过来，所以写成HEAD~100。
把当前版本回退到上一个版本，就可以使用git reset
git reset --hard HEAD^	回退到上一版本
git reset --hard 1094a	回退到指定ID的版本
git reflog用来记录你的每一次命令,可以查看操作记录和版本ID

HEAD指向的版本就是当前版本，因此，Git 允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。