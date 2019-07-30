### git操作手册

#### 克隆
- git clone https://github.com/hxuelun/git-project.git  克隆所有分支
- git clone -b dev https://github.com/hxuelun/git-project.git  克隆某个分支

#### 初始化本地仓库
- git init 初始化本地仓库
- git remote add origin git@github.com:hxuelun/git-project.git  关联远程仓库
- git add ./ 添加这一级目录所有文件到暂存区  或 git add README.md 添加某个文件到暂存区
- git add .  批量把当前目录下所有修改过的文件添加到暂存区
- git commit -m 提交暂存区的文件到本地版本库
- git commit -a -m  添加到暂存区并且提交到本地版本库   相当于git add . 和 git commit -m 命令的合并
- git push -u origin master  本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程，由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令,使用git push 命令推送。

##### 切换分支
- git branch dev 创建一个dev分支
- git checkout dev 切换分支
- git checkout -b dev  创建dev分支，然后切换到dev分支,git checkout命令加上-b参数表示创建并切换
- git branch 查看分支
- git merge dev  合并dev分支   合并之前需要先切回到主分支，然后使用命令用于合并指定分支到当前分支

#### 删除分支
- git branch -d dev  删除分支  合并完成后，就可以使用git branch -d dev 删除dev分支

#### 删除文件
- git rm test.txt  从版本库中删除该文件  然后在使用 git commit -m "删除了test.txt文件" 命令提交，文件就从版本库中删除了

#### 查看状态
- git status  查看文件状态   文件状态的简写（M - 修改， A - 添加， D - 删除， R - 重命名，?? - 未追踪）

#### 查看记录
- git log   可以查看详细的提交历史，以便确定要回退到哪个版本
- git log --oneline  可以查看简洁的提交历史，以便确定要回退到哪个版本
- git reflog  用git reflog查看命令历史，以便确定要回到未来的哪个版本

#### 撤销修改
- git checkout -- readme.txt  命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态
- git reset HEAD readme.txt  如果已经把修改的文件添加到了暂存区，可以使用 git reset HEAD readme.txt把暂存区的修改撤销掉（unstage），重新放回工作区，然后用 git checkout -- readme.txt 命令丢弃或撤销工作区的修改

#### 版本回退
- git reset --hard commit_id

#### git创建分支及合并分支代码

#### 配置信息
- 配置用户名：git config user.name "testName"
- 配置邮箱 : git config user.email "test@sina.com"
- 查看配置信息: git config --list

#### git生成SSH Key
- ssh-keygen -t rsa -C "347609357@qq.com"     使用这个命令生成SSH Key的时候会有一个地方需要输入SSH Key的安全密码，可以直接按回车键不用设置，当然设置密码也可以，设置了密码自己记住就行
- 然后找到 .ssh文件，里面有几个文件，找到id_rsa和id_rsa.pub，一个是私钥，一个是公钥，把id_rsa.pub文件里面的字符串复制到github中ssh key中添加

