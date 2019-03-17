---
title: git
date: 2017-09-22 8:07:33
tags: git
categories: command
---
## 前言

话不多数，先祭上这张常用命令表

![](https://s10.mogucdn.com/mlcdn/c45406/190316_7h08hall9hk30k08e552j820494g9_2076x1466.png)

<div><!-- more--></div>

## git介绍

svn与git,都是版本控制工具，
svn采用集成式管理方式(集成式，通过中央服务器的获取代码，没连接中央服务器无法进行操作，有很大的风险)
git采用分布是管理方式(每个开发人员都有版本控制库，每个人都可单独的做版本的操作，一系列的操作，都ok，不需要连接中央服务器都可以进行代码开发)
 
## 上传仓库信息

建立一个仓库=>仓库建立完成=>复制git上传地址

初始化数据仓库:git clone [url]			//将项目拉下来

设置贡献者

name
email
git config --global user.name	"XXX"
git config --global user.email 	"XX@XX.com"
git config --list				显示所有的
	>> 查看所有配置项


## git的三个工作区

1.工作区
工作区可以称为在使用git将项目拉取下来之后，
拉区上传文件的区域，可以对项目进行编写的区域
称之为工作区，可以对项目进行编写。不可以直接
提交到版本库，必须先将项目存放到暂存区上，然后
将暂存区的文件提交到版本库中



2.暂存区
- 作为过渡层
- 避免误操作
- 保护工作区和版本区
- 分支处理


3.版本区(库)

master,
我们开发的很多个版本都会记录在上面,版本呢，就是通过版本库来控制提交的


## Git命令

## 与远程仓库建立连接

建立连接
git remote  add origin url

修改链接
git remote set-url origin url

与远程仓库建立连接
git push -u origin master

同步远程仓库代码
git fetch origin

### 状态转换查看

git status 		
	>>可以查看当前库中文件的状态，查看当前文件有哪些还没有上传的文件，
git add 
	>>表示添加要上传的文件，添加完成之后使用上传命令，会将添加的文件上传到仓库里面,添加完成之后的文件就在暂存区中了,将文件的状态变成暂存状态了

git commit 
	>>将项目从暂存区=>到版本库的一个过程。会进入提交说明文件中，在这跟文件中，可以添加上传文件的说明，进入文件之后，按i进入编辑模式，输入要添加的内容，添加完成之后，按esc,光标回到底部输入:wq+enter退出编辑,
	>>git commit -m "change",可以直接将注释添加到文件中去
	>>git commit -a -m "注释" 表示将文件添加到暂存区，然后在将文件上传到版本区，操作连在一起了
	
git log 
	>>用于查看上传的状态，日志文件调用

git log --graph --pretty=oneline --abbrev-commit
    >> 查看合并分支关系
    
    
git reflog
    用来记录你的每一次命令
    
### 对比

git diff
	>>工作区和暂存区之间文件代码不同的对比
	>git diff --cached/staged用于查看暂存区和版本区的内容不同
	>git diff master(分支)用于对比工作区与版本库之间的对比

撤销:	
git reset HEAD drag.js
	>>从暂存区，撤销回工作区，将添加到暂存区的文件，撤销回工作区

git checkout (commit.id) <filename/>  回复指定版本，的指定文件
git reset <commit.id>    还原到指定版本
git reset --hard<commit.id>回到指定版本


git reset --hard HEAD^    回到上一个版本
git reset --hard HEAD~(num)    回到前第几个版本

git checkout
	>>将工作区，撤回版本区的最新状态。
548e73470288bc2a0e4f2fbed5486c24c3656e05
git commit --amend
	>>将暂存区的项目提交到版本库中，并且将版本库栈顶位置的项目替换掉

git reset  --hard (commit的哈希值) 可以退回到对应的commit中去

### 删除

git rm	<file.name>			会把对应暂存区的文件删除(必须是在工作区文件被删除之后的情况下才可以进行文件的删除操作)
git rm	-f <file.name>		会把暂存区和工作区的文件一起删除掉,
git rm --cached <file.name>	会删除暂存区的文件


## 将文件同步到远程仓库

第一次推送代码到远程仓库时，使用:
git push -u origin master(分之名) 后续只需要使用git push命令即可

git push origin master (分支名)    可以将当前版本信息提交到远程仓库中
git push origin test:master         // 提交本地test分支作为远程的master分支 //好像只写这一句，远程的github就会自动创建一个test分支
git push origin test:test              // 提交本地test分支作为远程的test分支
git push origin test:master -f 强推
git merge --no-ff -m"和并分支"

多人协作解决冲突

git fetch(把代码拉去过来之后，查看区别之后，在考虑怎么去合并)
git diff rebuild origin/zhouxiao    (查看rebuild分支和zhouxiao分支的内容区别)
git merge origin/zhouxiao            (将当前分支和zhouxiao进行合并)
git pull(直接进行了合并,直接将代码拉去过来，覆盖自己的代码)


### 上传到远程

git push <远程主机名> <本地分支名>:<远程分支名>

1.git add.
2.git commit -m
3.git status -s
4.git log -5
5.git push origin xf		//推到云端
6.git checkout dev		//切换到开发环境
7.git pull			//把代码拉下来
8.git merge --no-ff -m"" xf	//将远程代码
9.git push			//推到云端上		
10.git checkout xf
11.git rebase dev	//合并分支
12.git push


## git分支切换，创建

### 本地仓库操作

git branch <filename>	//创建分支
git branch 				//查看本地分支
git remote  -v  		//可以查看当前git地址是什么


git push origin <branchName> 	//将内容推送到对应的分支
git chackout <branchName>		//切换到对应的分支

git branch -d <branchName>		//删除对应本地的分支

git checkout -b <name>			//创建+切换分支

git merge <name>				//合并某分支到当前分支


### 远程仓库操作

git branch -a			//查看远程仓库分支
git push origin	:<branchName>	//删除对应的远程分支


### 分支操作

切换分支:git checkout name
撤销修改:git checkout -- file
删除文件:git rm file
查看状态:git status
添加记录:git add file 或 git add .
添加描述:git commit -m "miao shu nei rong"
同步数据:git pull
提交数据:git push origin name
分支操作
查看分支:git branch
创建分支:git branch name
切换分支:git checkout name
创建+切换分支:git checkout -b name
合并某分支到当前分支:git merge name
删除分支:git branch -d name
删除远程分支:git push origin :name
合并分支并生成合并记录:git merge --no-ff  name

## 暂存文件不提交commit


Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作:

git stash
命令将当前暂存区的文件存储在空间内，

工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看:
git stash list
命令将当前暂时存区域的文件列表出来，

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了:



## 显示合并log

`git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit`


`git log --graph --pretty=oneline --abbrev-commit`


合并分支后，rebase之前分支


git merge –no-ff 可以保存你之前的分支历史。能够更好的查看 merge历史，以及branch 状态。

git merge 则不会显示 feature，只保留单条分支记录。

git rebase --abort

--no-ff指的是强行关闭fast-forward方式。

fast-forward方式就是当条件允许的时候，git直接把HEAD指针指向合并分支的头，完成合并。属于“快进方式”，不过这种情况如果删除分支，则会丢失分支信息。因为在这个过程中没有创建commit



git merge --squash 是用来把一些不必要commit进行压缩，比如说，你的feature在开发的时候写的commit很乱，那么我们合并的时候不希望把这些历史commit带过来，于是使用--squash进行合并，此时文件已经同合并后一样了，但不移动HEAD，不提交。需要进行一次额外的commit来“总结”一下，然后完成最终的合并。

总结:
--no-ff:不使用fast-forward方式合并，保留分支的commit历史
--squash:使用squash方式合并，把多次分支commit历史压缩为一次



## 标签

> 添加标签

Git tag -a v1.3 -m "新增分期乐外 投统计"

> 推送标签

git push origin  v1.3

