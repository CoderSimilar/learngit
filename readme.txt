Git is a distributed version control systeam.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
# Git学习

* 初始化Git仓库

    git init

* 添加文件到git仓库

    git add <file> 

    git commit -m <massage>

* 查看工作区状态

    git status

* 查看文件修改内容

    git diff

* 回退到之前的版本

    git reset --hard commit_id

    HEAD指当前版本，上一个版本是HEAD^,上上一个版本是HEAD^^,上100个版本是HEAD~100

* 查看提交历史，以便确认回退到哪个版本

    git log

* 重返未来，查看命令历史，确定回到未来的哪个版本

    git reflog

* git 暂存区

    ![image-20230114154351337](C:\Users\similar\AppData\Roaming\Typora\typora-user-images\image-20230114154351337.png)

* git跟踪记录的是修改，每次修改如果不用git add到暂存区，那么就不会加入到commit中

* 直接丢弃工作区的修改

    git checkout -- <filename>

* 撤销添加到暂存区的文件修改

    1，git reset HEAD <filename>

    2，git checkout -- <filename>

* 已经提交到版本库的修改想要撤销，使用版本回退，前提是没有推送到远程仓库

* 删除文件

    git rm

    如果一个文件已经被提交到版本库，那么不用担心误删，但是只能恢复到最新版本，将会丢失最近一次提交后修改的内容

* 关联远程库

    git remote add origin git@sever_name:path/repo_name.git

    关联远程库必须指定用名，origin是习惯默认用名

    关联后，使用git push -u origin master第一次推送master分支的所有内容

    此后，每次本地提交以后，有必要的话就可以使用命令

    ​	git push origin master推送最新修改

* 克隆仓库

    使用git clone进行仓库的克隆

    git支持多种协议，包括https，但是ssh协议速度最快。

* 查看分支

    git branch

* 创建分支

    git branch <name>

* 切换分支

    git checkout<name> 或者 git switch <name>

* 创建+切换分治

    git checkout -b <name> 或者 git switch -c <name>

* 合并分支到当前分支

    git merge <name>

    当git无法自动合并分支时，必须首先解决冲突，再提交。

    解决冲突就是把Git合并失败的内容手动编辑为我们希望的内容再提交。

* 查看分支合并图

    git log --graph

* 删除分支

    git branch -d <name>

* 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除。

* 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

    在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

    开发一个新feature，最好新建一个分支；

    如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

* 多人协作的工作模式：

    1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
    2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
    3. 如果合并有冲突，则解决冲突，并在本地提交；
    4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

    如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

    这就是多人协作的工作模式，一旦熟悉了，就非常简单。

* 查看远程库信息

    git remote -v

* 本地新建的分支如果不推送到远程，对其他人不可见。

* 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；

* 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致

* 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。
