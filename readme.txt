Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.

1.创建版本库
git init 								把当前目录变成 Git 可以管理的仓库
git add <file>							把文件添加到仓库
git commit -m <message>					把文件提交到仓库，-m后面输入的是本次提交的说明
git status								查看当前的仓库状态
git diff <file>							比较修改的文件内容

提交修改和提交新文件是一样的两步，第一步是git add
在执行第二步git commit之前，我们再运行git status查看要提交的修改，确认后再提交


2.版本回退
git log 查看仓库提交日志	单行显示使用git log --pretty=oneline
在 Git 中，用HEAD表示当前版本，也就是最新的提交（注意我的提交 ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上 100 个版本写 100 个^比较容易数不过来，所以写成HEAD~100。
把当前版本回退到上一个版本，就可以使用git reset
git reset --hard HEAD^	回退到上一版本
git reset --hard 1094a	回退到指定ID的版本
git reflog用来记录你的每一次命令,可以查看操作记录和版本ID

HEAD指向的版本就是当前版本，因此，Git 允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。


3.撤销修改
git checkout -- readme.txt
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。

git reset HEAD <file>	
该命令可以把暂存区的修改撤销掉（unstage），重新放回工作区。


