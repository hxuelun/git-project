### git操作手册
- git init 初始化本地仓库
-  git remote add origin git@github.com:hxuelun/git-project.git  关联远程仓库
-  git add ./ 添加这一级目录所有文件到暂存区  或 git add README.md 添加某个文件到暂存区
-  git commit -a -m 提交暂存区的文件到本地版本库
-  git push -u origin master  本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程，由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
