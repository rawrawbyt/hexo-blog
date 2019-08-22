---
title: git常用命令
date: 2018-01-27 14:06:34
tags: [git]
categories: Note
---

git常用命令
<!--more-->

# 入门学习githug

[通关宝典](https://www.jianshu.com/p/482b32716bbe)

# 代码冲突

### 服务器代码合并本地代码

```
$ git stash  //暂存当前正在进行的工作。
$ git pull origin master //拉取服务器的代码
$ git stash pop //合并暂存的代码
```

### 服务器代码覆盖本地代码

```
$git reset --hard  //回滚到上一个版本
$git pull origin master 
```

## 更换git地址
`$ git remote set-url origin`

## 合并一条
`$ git merge --squash another`
`$ git commit –amend –no-edit(git commit –amend -m 'xxxxx')//合并上一次commit`

## git pll 和 git fetch
`git pull = git fetch + git merge`
如果git fetch,`git log -p master..origin/master` //比较本地的master分支和origin/master分支的区别
如果git pull，容易`error: You have not concluded your merge (MERGE_HEAD exists).`
解决方案：
1. 保留本地代码
```
$:git merge --abort //中止合并
$:git reset --merge //重新合并
$:git pull//重新拉取
```
2. 放弃本地代码，保留远端代码
```
$:git fetch --all
$:git reset --hard origin/master
$:git fetch
```

git pull 提示错误,`Your local changes to the following files would be overwritten by merge`
1. 服务器代码合并本地代码
```
$ git stash     //暂存当前正在进行的工作。
$ git pull origin master //拉取服务器的代码
$ git stash pop //合并暂存的代码
```
2. 服务器代码覆盖本地代码
```
$git reset --hard  //回滚到上一个版本
$git pull origin master 
```

## git merge 和 git rebase
git rebase -i 命令来压缩合并两次提交
`git rebase -i HEAD~2`
`?git rebase --onto`
在分支上，执行git rebase master，有冲突就解决冲突，解决后直接git add . 再git rebase --continue，
切换到master分支，执行git merge dev
[看看](https://blog.csdn.net/yuyantai1234/article/details/90072796)

# 一、安装
## git升级
`$ git clone git://git.kernel.org/pub/scm/git/git.git`

# 二、配置
## 查看用户名和邮箱
`$ git config user.name`
`$ git config user.email`

## 修改用户名和邮箱
`$ git config --global user.name`
`$ git config --global user.email`

## 初始化一个版本仓库
`$ git init`

## Clone远程版本库
`$ git clone addr.`

## 添加远程版本库origin
`$ git remote add origin addr.`

## 查看远程仓库
`$ git remote -v `

# 三、提交你的修改

## 添加当前修改的文件到暂存区
`$ git add .`

## 如果你自动追踪文件，包括你已经手动删除的，状态为Deleted的文件
`$ git add -u`

## 提交你的修改
`$ git commit –m &quot;你的注释&quot;`

## 推送你的更新到远程服务器,语法为 git push [远程名] [本地分支]:[远程分支]
`$ git push origin master`

## 查看文件状态
`$ git status`

## 跟踪新文件
`$ git add readme.txt`

## 从当前跟踪列表移除文件，并完全删除
`$ git rm readme.txt`

## 仅在暂存区删除，保留文件在当前目录，不再跟踪
`$ git rm –cached readme.txt`

## 重命名文件
`$ git mv reademe.txt readme`

## 查看当前分支的存在提交历史记录
`$ git log`不包括诸如删除的或被合并的提交

## 查看当前分支所有操作历史
`$ git reflog`诸如历史提交记录，撤销，合并提交等详细历史记录

## 修改最后一次提交注释的，利用–amend参数
`$ git checkout –- readme.txt`

# 四、基本的分支管理

## 创建一个分支
`$ git branch workspace`

## 切换工作目录到workspace
`$ git chekcout workspace`

## 将上面的命令合在一起，创建workspace分支并切换到workspace
`$ git chekcout –b workspace`

## 合并workspace分支，当前工作目录为master
`$ git merge workspace`

## 合并完成后，没有出现冲突，删除workspace分支
`$ git branch –d workspace`

## 拉去远程仓库的数据，语法为 git fetch [remote-name]
`$ git fetch`

## fetch 会拉去最新的远程仓库数据，但不会自动到当前目录下，要自动合并
`$ git pull`

## 查看远程仓库的信息
`$ git remote show origin`

# 五、合并

## 合并的commit的前一个commit节点
`$ git rebase -i （commitHash）`
pick：简写p，启用该commit；
reword：简写r，使用该commit，但是修改提交信息，修改后可以继续编辑后面的提交信息；
edit：简写e，使用commit，停止合并该commit；
squash：简写s，使用该commit，并将该commit并入前一commit；
drop：简写d，移除该commit；

# 六、撤销
## 撤销一个提交的同时会创建一个新的提交
`$ git revert head@{19}`
撤销提交时若多个提交修改了同一文件可能会出现冲突，需要处理冲突后，暂存：`$ git add. ` 
然后继续执行revert操作：`$ git revert --continue `
## 期望撤销的提交是最近独立存在的，并没有发生合并
`$ git reset （commitHash）`