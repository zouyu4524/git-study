# Git 学习笔记

### 创建新的Branch

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
为新的branch添加新的`remote`
```
git remote add [name_of_remote] [name_of_new_branch]
```

### 参考

1. [Create a new branch with git and manage branches](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)