### git操作手册

#### 克隆
- git clone https://github.com/hxuelun/git-project.git  克隆所有分支
- git clone -b dev https://github.com/hxuelun/git-project.git  克隆一个分支叫dev的远程仓库到本地

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
- git branch 查看本地分支
- git branch -r 查看远程分支
- git branch -a 查看本地分支和远程分支
- git merge dev  合并dev分支   合并之前需要先切回到主分支，然后使用命令用于合并指定分支到当前分支
- git branch -vv 查看本地分支和远程分支的跟踪关系

#### 删除分支
- git branch -d dev  删除本地dev分支  合并完成后，就可以使用git branch -d dev 删除dev分支
- git branch -D dev  强制删除本地dev分支
- git push origin --delete dev  删除远程dev分支
- git push origin :dev  删除远程dev分支，等同于git push origin --delete dev 
- git remote prune origin 删除本地分支存在但是远程分支已经不存在的分支，这条命令只会同步本地和远程有过关联关系的分支，原先在本地从来没有推到远程的分支是不会有任何变化，即不会删除也不会被推送到远程

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
- 1、首先切换到想要合并到的分枝下，运行'git merge’命令 （例如将dev-20180608分支合并到dev-20180622分支的话，进入dev-20180622分支运行git merge dev-20180608命令）
- 2、如果合并之后的代码有冲突，如下图红框中所示，此时需要手动解决冲突后再提交上去。
- 3、解决冲突：如下图所示，两个分支冲突的代码会以”=======”字符串分隔开来，分隔符上面为本分支的代码，分隔符下面为合并过来的分支代 码。此时根据实际情况判断需要保留哪个分支的代码。
- 4、解决冲突之后需要进行提交操作。执行如下命令提交：
Git add .
Git commit –m ‘备注’
Git push origin dev-20180622
如果没有冲突，合并完之后也需要执行git push origin [分支名]的操作。

- 1、创建分支步骤
    - 1、切换分支：新的分支需要从哪个分支切出来就切换到那个分支。
    - 2、执行：git branch branchname 命令创建新分支
    - 3、切换分支：执行git checkout branchname 命令切换到新分支
    - 4、push到服务器：git push origin branchname
    - 5、git pull时会提示如下信息：
      git branch --set-upstream-to=origin/《branch》 dev-20180613  
      修改上面的代码，如下：
      执行：git branch --set-upstream-to=origin/dev-20180613 dev-20180613
      此时就可以正常git pull, 其中origin/dev-20180613是你本地分支对应的远程分支；your_branch是你当前的本地分支。

### git连接远程分支
- git push <远程主机名>  <本地分支名>:<远程分支名>
- git push origin master:master  //如果省略远程分支名，则表示将本地分支推送与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。
- git push origin dev //将本地dev分支推送到远程,这条命令表示，将本地的dev分支推送到origin主机的dev分支。如果后者不存在，则会被新建。
- git push origin :dev  //这条命令省略本地分支名，则表示删除指定的远程dev分支，因为这等同于推送一个空的本地分支到远程分支。git push origin :dev 等同于 git push origin --delete dev

- git checkout --track origin/branch_name 如果远程新建了一个分支，本地没有该分支,可以利用 git checkout --track origin/branch_name ，这时本地会新建一个分支名叫 branch_name ，会自动跟踪远程的同名分支 branch_name
- git checkout -b dev origin/dev //创建远程origin的dev分支到本地
- git checkout -b 本地分支名 origin/远程分支名   // 这个就是上面命令的解释，将远程git仓库里的指定分支拉取到本地（本地不存在的分支）
这个将会自动创建一个新的本地分支，并与指定的远程分支关联起来，例如远程仓库里有个分支dev2,我本地没有该分支，我要把dev2拉到我本地：
git checkout -b dev2 origin/dev2  这条命令若成功，将会在本地创建新分支dev2,并自动切到dev2上。

### 删除远程分支后，本地git branch -a 依然能看到删除的远程分支的解决办法
 - git remote show origin 可以查看remote地址，远程分支，还有本地分支与之相对应关系等信息，此时我们就可以看到那些远程仓库
 已经不存在的分支，根据提示，使用git remote prune origin 命令，这样就可以删除那些远程仓库不存在的分支

### 本地查看不到远程新建的分支的解决方法
- 在github网页上新建了一个新的分支，但是在本地git branch -r 查看不到这个新建的远程分支。
git是分布式的这个设计思想。每个git版本库彼此是独立的，默认是没有通知机制的，任意一个版本库更新了，其他人压根不知道，git也不会主动联网去获取更新——因为Linus大神设计git就是为了避免SVN/CVS必须联网才能使用的诟病。clone之后，每个人得到的都是完整的一份版本库的拷贝，因此就算中央仓库挂掉了，随便找个人的版本库放上去就能恢复了。
因此git同步版本库一定是手工操作的，对应的命令就是fetch(本地同步远程)和push(远程同步本地)。
<font color='red'>所以，你想要看到远程分支，必须使用git fetch获取远程更新之后再看。再继续 git branch -r 就能看到了</font>


### 查看当前的远程库
- git remote  要查看当前配置有哪些远程仓库，可以用 git remote 命令，它会列出每个远程库的简短名字。在克隆完某个项目后，至少可以看到一个名为 origin 的远程库，Git 默认使用这个名字来标识你所克隆的原始仓库,也可以加上 -v 选项（译注：此为 --verbose 的简写，取首字母），显示对应的克隆地址：
  ```
  $ git remote -v 
  origin  git://github.com/schacon/ticgit.git (fetch)
  origin  git://github.com/schacon/ticgit.git (push)
  ```
### 添加远程仓库
- git remote add [shortname] [url]，要添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用，运行 git remote add [shortname] [url]，
  ```
  $ git remote 
  origin
  $ git remote add pb git://github.com/paulboone/ticgit.git
  $ git remote -v
  origin  git://github.com/schacon/ticgit.git
  pb  git://github.com/paulboone/ticgit.git
  ```

### 查看远程仓库信息
- git remote show [remote-name] 我们可以通过命令 git remote show [remote-name] 查看某个远程仓库的详细信息

### 远程仓库的删除和重命名
- git remote rename [修改的名称] [修改后的名称] ,比如想把 pb 改成 paul，可以这么运行：git remote rename pb paul

#### 配置信息
- 配置用户名：git config user.name "testName"
- 配置邮箱 : git config user.email "test@sina.com"
- 查看配置信息: git config --list

#### git生成SSH Key
- ssh-keygen -t rsa -C "347609357@qq.com"     使用这个命令生成SSH Key的时候会有一个地方需要输入SSH Key的安全密码，可以直接按回车键不用设置，当然设置密码也可以，设置了密码自己记住就行
- 然后找到 .ssh文件，里面有几个文件，找到id_rsa和id_rsa.pub，一个是私钥，一个是公钥，把id_rsa.pub文件里面的字符串复制到github中ssh key中添加


### <font color='red'>注意</font>
- 如果在远程代码库创建的分支，直接 git branch -a 是显示不出来远程分支的，需要git pull拉取之后，再git branch -a 才能看到远程分支

test 0410分支
