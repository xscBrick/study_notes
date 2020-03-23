# GIT 大全

git 是一个先进的分布式版本控制系统
仓库（版本库）：分为本地仓库和远程仓库，简单的理解就是2个文件夹（包含一个 .git(文件夹)），
.git目录（文件夹）：是Git来跟踪管理版本库的，git只能跟踪文本文件的改动
本地仓库与远程仓库：其实就是2个文件夹，分别放着一些东西

workspace：工作区(working Directory)

repository:版本库 工作区有一个隐藏目录 `.git`，这个不算工作区，而是Git的版本库

staging：暂存区（或者叫index）

local repository：本地仓库

remote repository：远程仓库(origin)

![å¨è¿éæå¥å¾çæè¿°](https://img-blog.csdnimg.cn/20190818124505370.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDMwODQwNw==,size_16,color_FFFFFF,t_70)

[TOC]

## 本地仓库操作命令

### git init

初始化一个本地仓库
创建一个空的Git仓库或重新初始化一个现有仓库

### git add

git add <file>

git add .  //添加所有改动文件到暂存区

### git commit

git commit -m "提交改动说明"	//提交到分支

### git branch 

**git branch 一般用于分支得操作，比如创建分支，查看分支**

> git branch //查看本地分子,在当前分支前 有一个*标记
>
> git branch -a // 查看本地及远程所有分支
>
> git branch newbranch //创建新的名为:newbranch 的分支,但是还是在当前分支
>
> git branch -d newbranch //删除分支:newbranch 但是在分支中有一些未merge的提交,会删除失败,可以用 git branch -D newbranch 进行强制删除
>
> git branch -vv	//查看本地对应的远程分支
>
> git branch -m oldBranchName newBranchName	//给分支重命名

### git checkout 

**git checkout 操作分支，操作文件**

> 操作文件
>
> git checkout filename //放弃单个文件的修改
>
> git checkout .	//放弃当前文件下的修改

> 操作分支
>
> git checkout master	//将分支切换到主分支
>
> git checkout -b Dev	//将分支切换到Dev,如果Dev不存在则创建一个Dev分支再切换到Dev

### git status

**用于显示工作目录和暂存区的状态。使用此命令能看到那些修改被暂存到了, 哪些没有, 哪些文件没有被Git tracked到。`git status`不显示已经`commit`到项目历史中去的信息,看项目历史的信息要使用`git log`**

### git diff

**查看区别（不同）**

> git diff HEAD -- readme.txt

### git reset 

**既可以回退版本，也可以把暂存区的修改回退到工作区**

> git reset --hard HEAD^	//回退到上个一个版本
>
> git reset --hard 101bc5		//回退到101bc5

> git reset HEAD readme.txt  //把暂存区的修改撤销掉（unstage），重新放回工作区

> git checkout -- reademe,txt  //丢弃工作区的修改

### git log

显示从最近到最远的提交日志

> git log
>
> git log --pretty=oneline

### git reflog

记录你的每一次命令

### git rm

删除文件

> git rm test.php
>
> git add .
>
> git commit - m "remove test.php"
>
> git checkout -- test.txt //恢复被删除的内容，实际是用版本库里的版本替换工作区的版本
>
> 





### 

## 远程仓库管理

## 基于github

##### 1. 创建SSH key：

在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```

id_rsa :私钥

id_rsa.pub：公钥

登陆github,打开Account settings

##### 2.登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

### git clone

git clone 远程仓库地址



### git push

> git push -u origin master //第一次推送到远程分支，加了参数 -u ，不仅会把本地的master 分支推送到远程分支上，还会把本地的master 分支和远程的master 分支关联起来
>
> git push origin master

# 把本地分支推送到远程指定分支

git push origin local_branch:remote_branch

### git remote add origin 远程仓库地址

git push -u origin master

git push origin master



## 分支管理

### git checkout

> 创建分支
>
> git checkout -b dev
>
> 切换分支
>
> git checkout master

### git branch 

> 创建分支
>
> git branch dev	//创建分支
>
> git branch  //查看当前分支
>
> git branch -a //查看本地及远程所有分支
>
> git branch -d dev //删除dev分支（-D强制删除）

### git merge

合并指定分支到当前分支

> 把 dev 内容合并到master
>
> git checkout master 
>
> git merge dev	//

### git log --graph 查看分支合并图

### git pull

### git fetch

## 

### git branch

### git checkout

### git stash

## 





