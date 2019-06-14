### git操作手册

#### 克隆
- git clone https://github.com/hxuelun/git-project.git  克隆所有分支
- git clone -b dev https://github.com/hxuelun/git-project.git  克隆某个分支

#### 初始化本地仓库
- git init 初始化本地仓库
-  git remote add origin git@github.com:hxuelun/git-project.git  关联远程仓库
-  git add ./ 添加这一级目录所有文件到暂存区  或 git add README.md 添加某个文件到暂存区
-  git commit -m 提交暂存区的文件到本地版本库
-  git commit -a -m  添加到暂存区并且提交到本地版本库   相当于git add . 和 git commit -m 命令的合并
-  git push -u origin master  本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程，由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

##### 切换分支
- git branch dev 创建一个dev分支
- git checkout dev 切换分支
- git checkout -b dev  创建dev分支，然后切换到dev分支,git checkout命令加上-b参数表示创建并切换
- git branch 查看分支
- git merge dev  合并dev分支   合并之前需要先切回到主分支，然后使用命令用于合并指定分支到当前分支
- git branch -d dev  删除分支  合并完成后，就可以使用git branch -d dev 删除dev分支

#### 删除文件
- git rm test.txt  从版本库中删除该文件

#### 查看记录
- git log 
- git reflog
- git log --oneline
