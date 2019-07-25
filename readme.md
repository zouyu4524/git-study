# Git 学习笔记

<details>
<summary>点击打开目录</summary>
<!-- MarkdownTOC  levels="2,3" autolink="true" -->

- [`origin`](#origin)
- [在Commit前撤销已add的修改](#%E5%9C%A8commit%E5%89%8D%E6%92%A4%E9%94%80%E5%B7%B2add%E7%9A%84%E4%BF%AE%E6%94%B9)
- [在Push前撤销已commit的修改](#%E5%9C%A8push%E5%89%8D%E6%92%A4%E9%94%80%E5%B7%B2commit%E7%9A%84%E4%BF%AE%E6%94%B9)
- [创建新的Branch](#%E5%88%9B%E5%BB%BA%E6%96%B0%E7%9A%84branch)
- [`git remote`](#git-remote)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
</details>

### `origin`

`origin`是remote组中的默认成员, 在`git clone`时自动创建, 其值为远程repo的url（url以`.git`结尾）。

### 在Commit前撤销已add的修改

```
git reset <file>
```
或者如下
```
git reset 
```
撤销所有的已add但未commit的修改。

**注**: 如果repo还没有任何的commit, 也可以通过如下的命令撤销<sup>[2]</sup>
```
git rm [-r] --cached <added_file_to_undo>
```
其中`-r`是可选项, 表示递归式操作, 当需要撤回的文件包含文件夹时需要设置该选项。  
原理在于`git ret`是将`HEAD`撤销至上一次commit状态, 而若还没有任何的commit, 则`HEAD`无法解析。其中[2]给出了很有趣的解释。

### 在Push前撤销已commit的修改

```
git reset <commit_id>
```
将`HEAD`指针☞回`commit_id`所标识的commit, 而查找相应的commit id可以通过`git log <-no.>`完成。其中`no.`为commit的编号, 从新到旧递增, 当前的commit编号为1, 所以可以通过
```
git log -2
```
查看目标commit, 可以进一步比对commit内容确认。明确commit id后, 执行`git reset <commit_id>`即可。  
**注**: 以上操作将完全撤销至上一次commit后的状态, 但不会撤回已经修改的代码。

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
git push -u origin [name_of_new_branch]
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

### `git remote`

`git remote`是管理远程repo的指令, 当每一个项目独立成repo的情况下似乎不需要常使用该指令<sup>[3]</sup>。以下罗列可能的使用场景:

- 检查远程repo与本地的差异
```
git remote [-v | --verbose] update
```
该指令将比对所有remote组中的远程repo各个branch与本地repo相应branch的差异, 一般对个人（现阶段的我）而言, remote组中只有一个成员, 即`origin`。

- 查看远程repo的全部信息
```
git remote -v
```
该指令将罗列出当前git环境下所有的远程repo信息, 以`<remote_name, url>`对的形式显示, 一般而言即显示类似如下内容:
```
origin  https://github.com/zouyu4524/RL-market.git (fetch)
origin  https://github.com/zouyu4524/RL-market.git (push)
```

### 参考

1. [Create a new branch with git and manage branches](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)
2. [How do I undo 'git add' before commit?](https://stackoverflow.com/a/682343/8064227)
3. `git remote --help`