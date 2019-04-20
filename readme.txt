Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
Creating a new branch is quick and simple.


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
git push origin master #向远程仓库推送本地更新

git clone git@github.com:rocgump/gitskills.git

5.分支管理
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建 + 切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
禁用Fast forward合并分支 git merge --no-ff -m "merge with no-ff" dev
删除分支：git branch -d <name>

6.解决冲突
git merge <branch name>提示有冲突，需要手动合并
查看冲突文件，Git 用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
修改后再提交，即可合并
查看分支的合并情况 git log --graph --pretty=oneline --abbrev-commit
合并后即可以删除分支

7.Bug 分支
git stash			保存工作区
git stash list 		查看stash list 

修复Bug后切换回工作分支
工作现场还在，Git 把 stash 内容存在某个地方了，但是需要恢复一下，有两个办法：
一是用git stash apply恢复，但是恢复后，stash 内容并不删除，你需要用git stash drop来删除；
另一种方式是用git stash pop，恢复的同时把 stash 内容也删了，再用git stash list查看，就看不到任何 stash 内容了
你可以多次 stash，恢复的时候，先用git stash list查看，然后恢复指定的 stash，用命令：git stash apply stash@{0}

8.多人协作
git remote	# 查看远程仓库名称
git remote -v# 远程仓库名称和地址，如果没有推送权限，就看不到 push 的地址
git push origin master # 将本地分支推送到远程库对应的远程分支上：
git checkout -b dev origin/dev	# 克隆并切换到dev分支
git pull oragin dev	# 从远程拉取dev分支
git branch --set-upstream-to=origin/dev dev # 建立本地分支和远程分支的关联
git branch -a   # 查看所有分支
git branch -r   # 查看远程分支


因此，多人协作的工作模式通常是这样：

1.首先，可以试图用git push origin <branch-name>推送自己的修改；
2.如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3.如果合并有冲突，则解决冲突，并在本地提交；
4.没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
这就是多人协作的工作模式，一旦熟悉了，就非常简单。

小结
查看远程库信息，使用git remote -v；
本地新建的分支如果不推送到远程，对其他人就是不可见的；
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

9.标签
git tag <tagname> <commit id> 	# 用于新建一个标签，默认为HEAD，也可以指定一个 commit id；
git tag -a <tagname> -m "comments"  # 可以指定标签信息；
git tag		# 可以查看所有标签。
git show <tagname>	# 查看标签
git tag -d <tagname> # 删除标签
git push origin <tagname>  # 推送某个标签到远程库
git push origin --tags 	#一次性推送全部尚未推送到远程的本地标签
git push origin :refs/tags/<tagname> # 删除远程标签，需要本地先删除

10.忽略特殊文件
新建.gitignore文件,然后把要忽略的文件名填进去，Git 就会自动忽略这些文件。

11.配置命令别名
git config --global alias.last 'log -1'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
配置 Git 的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。
配置文件放哪了？每个仓库的 Git 配置文件都放在.git/config文件中：
别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。
而当前用户的 Git 配置文件放在用户主目录下的一个隐藏文件.gitconfig中：









