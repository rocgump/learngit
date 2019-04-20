Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
Creating a new branch is quick AND simple.

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

4.使用Github
第 1 步，创建 SSH Key，在用户主目录下，看看有没有. ssh 目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。
如果没有，打开 Shell（Windows 下打开 Git Bash），创建 SSH Key：sh-keygen -t rsa -C "youremail@example.com"	
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是 SSH Key 的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
第 2 步：登陆 GitHub，打开 “Account settings”，“SSH Keys” 页面，然后，点 “Add SSH Key”，填上任意 Title，在 Key 文本框里粘贴id_rsa.pub文件的内容
第 3 步,Github 上 Create a new repo,在本地仓库运行命令:git remote add origin git@github.com:rocgump/learngit.git,注意替换用户名
再使用 git push -u origin master 即可把本地库的所有内容推送到远程库上，第一次使用 Git 的clone或者push命令连接 GitHub 时，会得到一个警告，yes确认即可

要关联一个远程库，使用命令 git remote add origin git@server-name:path/repo-name.git；
关联后，使用命令 git push -u origin master第一次推送 master 分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令 git push origin master 推送最新修改；

git clone git@github.com:rocgump/gitskills.git

5.分支管理
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建 + 切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>


