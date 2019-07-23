# Git 学习笔记

### 创建新的Branch

**Branch管理原则**<sup>[1]</sup>: 

> In your github fork, you need to keep your master branch clean, by clean I mean without any changes, like that you can create at any time a branch from your master. Each time that you want to commit a bug or a feature, you need to create a branch for it, which will be a copy of your master branch.

将远程的repo（origin/master）同步至本地
```
git pull
```
然后, 以此创建新的branch
```
git checkout -b [name_of_new_branch]
```
将新的branch推送至远程repo
```
git push origin [name_of_new_branch]
```
在新创建的branch上进行修改, 所有的commit在该branch上开展, 直至达到阶段性的进展再考虑将其同步至master branch。  

在新的branch上commit前务必确认当前处于新的branch, 如下命令查看当前branch
```
git branch --list
```
当前branch将会用`*`标注。  

如果当前branch中的修改到达一个阶段, 可以将其合并至master branch中, 操作如下
```
git checkout master
git merge origin/[name_of_new_branch]
```
首先切换回master branch, 再执行`merge`命令, 将修改发生的branch合并至master branch中。

### 参考

1. [Create a new branch with git and manage branches](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)