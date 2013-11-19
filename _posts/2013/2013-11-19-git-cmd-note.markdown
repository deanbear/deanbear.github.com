---
layout: post
title: Git命令学习笔记
date: 2013-11-19 15:50:48
categories:
- 笔记
tags:
- Git
- 笔记
---

岗位变动后，真正要在工作上接触Git了。读[git community book](http://gitbook.liuhui998.com/)的笔记，一些高级技能如submodule以及复杂操作暂未掌握，后续实战用到时补上。

一句话评价Git：太强大，强大到不想用，我想念svn！

p.s. 我又忘记切换成繁体字了。

===

复制仓库	
	
	git clone repo

本地新建初始化仓库
	
	git init

=== 

添加未受版本控制的文件进入待提交索引

	git add file1 file2 file3

查看目录当前情况

	git status

提交变更（加-a参数可以直接提交除新增外的所有修改不需先add）

	git commit
	
===

本地创建新分支

	git branch branch_name

查看本地分支(git branch)，查看所有分支加参数-a

切换当前工作分支

	git checkout branch_name

合并分支

	git merge branch_name

合并后重置回上一个提交/合并后重置回上个提交保留待提交索引/合并后重置回上个提交索引退回工作区

	git reset --hard HEAD~1

	git reset --soft HEAD~1

	git reset --mixed HEAD~1
	
还原一个文件到上次提交状态

	git checkout -- file
	
拉取远程仓库并合并

	git pull

更新远程仓库分支情况

	git fetch
	
推送本地内容至远程仓库

	git push
	
删除已合并分支/强制删除分支

	git branch -d branch_name

	git branch -D branch_name

===

查看提交记录

	git log (--pretty=raw | short | oneline)

比较内容修改

	git diff (--stat | branch_name | --cached )

===

生成轻量级tag

	git tag alias_name SHA1

生成标签对象

	git tag -a alias_name SHA1

===

分支重建

	git rebase orig_branch

中断解决冲突继续
	
	git rebase --continue

取消重建
	
	git rebase --rebort

===

交互式新增/重建

	git add -i
	
	git rebase -i
	
===

暂存工作

	git stash ""

恢复暂存

	git stash apply
	
查看队列

	git stash list

===

二分查找出问题分支

	git bisect	start | reset

问责

	git blame file

查询

	git grep
	
===









