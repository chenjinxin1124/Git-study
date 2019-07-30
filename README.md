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
