# Git-study
0.Git官网
  https://git-scm.com/book/zh/v2（下载电子书最佳）
1.安装（腾讯Ubuntu）
  sudo apt-get install git
  git --version
2.配置（最小）
  //global 最常用，local、system不常用
  git config --global user.name "chenjinxin"
  git config --global user.email 1067446576@qq.com

  git config --global --list  //查看配置信息
3.优先级：local > global > system
$ git config --local
$ git config --global
$ git config --system
  显示 config 的配置
  $ git config --list --local
  $ git config --list --global
  $ git config --list --system
  清除，--unset
  $ git config --unset --local user.name
  $ git config --unset --global user.name
  $ git config --unset --system user.name
  $ git log
  查看 commit 信息，Author 的 name 和 email

git diff : 默认查看工作区和暂存区的区别
git diff --cached : 查看暂存区和HEAD的区别
git diff --文件名1 文件名2 : 查看文件1和文件2的变化

变更工作区使用：checkout；变更暂存区使用：reset
把暂存区恢复成和HEAD一样：git reset HEAD
把工作区恢复成和暂存区一样：git checkout --文件名
取消暂存区部分文件的更改：git reset HEAD --文件1路径 文件2路径

git reset 的三个参数
--soft 这个只是把 HEAD 指向的 commit 恢复到你指定的 commit，暂存区 工作区不变
--hard 这个是 把 HEAD， 暂存区， 工作区 都修改为 你指定的 commit 的时候的文件状态
--mixed 这个是不加时候的默认参数，把 HEAD，暂存区 修改为 你指定的 commit 的时候的文件状态，工作区保持不变

消除最近的几次提交：git reset --hard commit指针

查看不同提交的指定文件的差异：
  分支之间：
    git diff 分支1 分支2 -- 文件路径
  commit之间：
    git diff commit1的ID号 commit2的ID号 -- 文件路径

正确删除文件的方法：
  git rm 文件路径

git stash：
  把工作空间文件放入栈中
    git stash apply：把栈中的文件恢复，栈内容不变
    git stash pop：把栈中文件弹出
  git stash list：查看stash内容

指定不需要Git管理的文件：
  vi .gitignore
  指定不需要管理的文件名的正则表达式（*.class|*.exe|*.jar|doc/|）
    doc：不管理doc文件名的文件（文件、文件名、文件夹及其子文件）
    doc/：不管理doc文件夹下的文件，但是管理doc文件夹
    *.doc：不管理以doc结尾的文件

git branch -av：查看分支

#GitHub
配置公私密钥
ls -al ~/.ssh ：查看是否已存在秘钥
创建密钥：
  ssh-keygen -t rsa -b 4096 -C "your_email"
  一路回车
  ls -al ~/.ssh
    id_rsa.pub 公钥
      复制到远端
创建项目：
  new repository
    Owner：个人（仅个人可以管理）/组织（共同管理）
    Add .gitignore:选择语言，可以智能创建拦截文件
    Add a license:MIT License 分享
把本地仓库同步到GitHub
  把本地git仓库同步到GitHub
    git remote add github GitHub仓库地址
      github表示给GitHub仓库起得名称
    git remote -v
      查看连接的仓库
    git push github --all
      将暂存区的内容推送到远程仓库，有一些有冲突的分支或文件会push失败（![rejected]）
    gitk --all
      git可视化
    git fetch github master
      将 github 的 master 分支拉取下来
      gitk
        拉取下来的内容会独立成一个分支
    git branch -v
      显示本地的分支
    git branch -va
      显示所有的分支
    git merge --allow-unrelated-histories github/master
      合并无关分支
    git push github master
      推送到本地名为 github 的远程仓库的 master 分支

不同人修改了同一个分支的不同文件（非线性结构）
  git clone SSH链接 本地文件名
    本地文件名不写则默认新建远端仓库名的文件夹作为工作区，写上则以本地文件名新建文件夹作为本地工作区
  第一个人push成功
  第二个人push失败
    git branch -av
      显示所有分支
    显示当前分支 [ahead 1, behind 1] ...
    git merge 分支路径（github/feature/add_git_commands）

不同人修改了同分支同文件的不同区域
  git branch -av
    ... [behind 2] ...
      有两个文件更新
  git pull
    使本地工作区与远端同步
  两人修改文件
  第一个人push成功
  第二个人push失败
    ！[rejected]
  git fetch
  git branch -av
    [ahead 1,behind 1]
  git merge origin/feature/add_git_commands
不同人修改了同一个分支的相同文件
  第二个人push失败
  git pull
    CONFLICT（merge 失败，文件内容有冲突）
  vi index.html
    git 会做一些标记，如下
  <<<HEAD
      别人改动的内容
  ===
      本人改动的内容
  >>> ***
    自己手动决定如何修改
  git status
    UNmerged paths.
      ...
  git commit -am'****'
同时变更了文件名和文件内容
  git pull
  person1 修改了文件名并commit push
  person2 在原文件修改了内容，commit，push失败
  person2 git pull
  本地文件名与远端同步了，并且本地修改的内容也保存下来了
    git可以智能地处理更改文件名的提交
把同一文件改成了不同的文件名
  git pull
  git rm 原文件
  git add 要保留的文件
  git rm 删除两个更改文件中不要的那个
  git commit -am'****'
  gitk --all
  git branch -av
  git push
  
