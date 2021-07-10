---
title: git常用命令
toc: true
date: 2015-03-26
tags: tools git 
categories:
- [工具, git]
---



git 常用的命令总结了一下, 不用再每次都去百度了

分支常用命令

```
查看分支：git branch   git branch -a  查看远程分支
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name> 先切换到别的分支


git log 退出   q

```

推拉代码常用命令
```
拉取远程dev  git pull origin dev    
拉取admin     git pull origin admin
git push --set-upstream origin master 设定 push默认分支

关联本地仓库和远程仓库{clone下来无法推送，需要关联 
ssh -T git@gitee.com 查看是否关联成功}

添加远程仓库
git remote add origin git@gitee.com:good_working/teamwork_pracitce.git 
git remote add origin git@github.com:BrianLSH/VueLearning.git

关联了但是还不识别  需要用此命令
git pull origin master --allow-unrelated-histories
第一次本地无代码不用加后缀,如果有需要加上
(https://blog.csdn.net/lindexi_gd/article/details/52554159)
```

撤销修改
```
没有git add的，git checkout -- file可以丢弃工作区的修改：
命令git checkout -- readme.txt意思就是，把readme.txt文件
在工作区的修改全部撤销，这里有两种情况：一种是readme.txt自修改
后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修
改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或
git add时的状态。


git add后的，git reset HEAD <file>可以把暂存区的修改撤销掉（unstage）,  
重新放回工作区：如果再要放弃工作区的修改，接着用git checkout --file
```

文件删除
```
git add/rm <file>   删除文件
git checkout --file 恢复
```




