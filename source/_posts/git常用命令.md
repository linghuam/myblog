---
title: git常用命令
comments: true
date: 2018-01-05 17:25:28
tags:
categories:
- 开发工具
- git
---

# git常用命令

## git教程

- [廖雪峰-git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
- [高级教程-Pro Git](http://git.oschina.net/progit/)
- [官网-GitBook](https://git-scm.com/book/zh/v2)

<!-- more -->

## 配置

* 配置文件

```bash
# 配置 Git 的时候，加上 --global 是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

# 每个仓库的Git配置文件都放在 .git/config 文件中，通过以下命令查看：
cat .git/config

# 当前用户的Git配置文件放在用户主目录下的一个隐藏文件 .gitconfig 中
cd ~
cat .gitconfig
```

* 用户信息
```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config core.ignorecase false  //对文件名大小写敏感
git config --global credential.helper store //记住密码
git config --global gui.encoding utf-8 //git乱码问题
```

* 命令别名
```bash
git config --global alias.st status
git config --global alias.pl pull
git config --global alias.ps push
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.cfg config
```

* 文本编辑器
```bash
git config --global core.editor emacs
```

* 差异分析工具
```bash
git config --global merge.tool vimdiff
```

* 记住密码
```bash
git config --global credential.helper store
```

* 查看配置信息
```bash
git config --list 或 -l
```

* 获取帮助
```bash
git help <verb>

git help config 或 git config -h
```

* 不忽略空文件夹
```md
在空文件夹下面创建一个`.keep`文件
```

## 新增库

```bash
# 本地
cd [项目目录]
git init

# 远程
git clone <url>
git clone <url> [自定义目录名]

# 项目体积过大时
git clone --depth=1 <url>
```

## 查看状态

```bash
# 查看当前状态
git status
# 简写
# 新添加的未跟踪文件前面有 ?? 标记
# 新添加到暂存区中的文件前面有 A 标记
# 修改过的文件前面有 M 标记
git status -s
# 或
git status --short
```

## 查看提交历史

```bash
# 默认不用任何参数的话，git log 会按提交时间列出所有的更新，最近的更新排在最上面
git log
# 带图形装饰的 log
git log --graph --oneline --decorate
# 一个常用的选项是 -p，用来显示每次提交的内容差异，也可以加上 -2 来仅显示最近两次提交
git log -p -2
# 看到每次提交的简略的统计信息
git log --stat
```

## 修改提交信息

```bash
# 修改最后一次提交信息
$ git commit --amend --no-edit

# 修改前几次提交信息
$ git rebase -i HEAD~3
# HEAD~3 表示修改最近三次
# 其次，将我们想修改的提交的命令由 “pick” 改为 “edit” 。修改完成之后，保存修改。
# 依次使用 “git commit --amend” 和 “git rebase --continue” 修改

# 远程仓库
$ git push -f
```

## 文件操作

git 分区：工作区 -> 暂存区 -> 本地仓库 -> 远程仓库

## 分支操作

### 查看分支

```bash
# 查看本地已有分支
$ git branch

# 查看所有分支，包含远程分支
$ git branch -a

# 查看本地分支与远程分支对应关系
$ git branch -vv
```
### 创建分支

```bash
# 基于本地当前分支创建分支
$ git checkout -b newBranchName
# 同时关联远程分支
$ git checkout -b newBranchName origin/newBranchName

# 基于远程分支创建分支
$ git checkout -b newBranchName origin/branchName
# 或使用 -t 参数，默认在本地建立一个与远端分支同名的分支
$ git checkout -t origin/branchName
```
### 切换分支

```bash
# 工作区没新代码切换分支
$ git checkout newBranch

# 工作区有新代码切换分支
# 工作区间有未提交代码，切换分支自动执行"git merge"操作，故有冲突将无法切换成功；
$ git stash save '存储说明'
$ git checkout B
# 处理完后
$ git checkout A
$ git stash pop

# 如果本来想在A分支上开发， 开发过程中才发现当前处在B分支，想强制将工作区间代码迁到A分支也可以借助“工作现场”完成。
$ git stash save '存储说明'
$ git checkout A
$ git stash pop
# 如有冲突且处理完所有冲突
$ git add -A

# 切换分支异常处理
# 从A分支切换到B分支由于git异常导致虽然切换分支成功，但在当前B分支上留存了大量A分支的代码
# 将所有改动提交到本地仓库
$ git add -A
$ git commit -m '这个commit会被覆盖'
# B 是当前分支名
$ git reset --hard origin/B
```
### 合并分支

```bash
# 合并本地分支代码
$ git merge branchName

# 合并远程分支代码
$ git pull origin branchName

# 合并部分提交
# 如将 A 分支的某几个提交合并到 B 分支，而不是将整个 A 分支合并到 B
# c1 提交必须早于 c2
$ git cherry-pick <c1>..<c2>(左开右闭区间)
# 或
$ git cherry-pick <c1>^..<c2>(闭区间)
# 或
$ git cherry-pick <c1> <c2> <c3> ...(转移多个提交)
# 或
$ git cherry-pick <commitId>(转移某个提交)
# 或
$ git cherry-pick <branchName>(将分支的最近一次提交，转移到当前分支)

# 合并代码减少commit次数("git push"之前，将本地多个commit合并成一个)
$ git rebase -i

# 撤销一个合并
# 如果你觉得你合并后的状态是一团乱麻，想把当前的修改都放弃，你可以用下面的命令回到合并之前的状态：
$ git reset --hard HEAD
```

### 删除分支

```bash
# 删除本地分支
# "-d" 如果该分支代码未合并到其他分支，将无法删除；
# "-D" 强制删除分支，不会出现任何提示；
$ git branch -D xxxx

# 删除远程分支
$ git push origin --delete branchName
```

## 关联远程库

```bash
# 添加远程库
$ git remote add [origin] [git@github.com:nanfei9330/learngit.git]

# 本地新分支推送创建远程分支
$ git push --set-upstream origin <远程分支名>
# 或
$ git push -u origin <远程分支名>

# 关联远程分支
$ git branch --set-upstream-to=origin/<远程分支名> <本地分支名>

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [originName]

# 删除远程仓库
$ git remote rm name

# 修改仓库名
$ git remote rename old_name new_name
```

## 高级

## 保持清洁的Git提交记录

```bash
# 法 1：修改最后一次提交
# 既可以修改我们提交的 message，又可以修改我们提交的文件，最后还会替换最后一个 commit-id
# 修改最后一次提交 message
$ git commit --amend
$ git commit --amend -m "feat: xxx"
# 修改最后一次提交文件
$ git add .
$ git commit --amend --no-edit

# 法 2：善用 git rebase -i（仅在代码未 push 到远程时使用）
$ git rebase -i HEAD~n  # n表示最后几次提交

# 法 3：合并远程分支时避免分叉
# 如果用 merge 命令，就会多处一个 merge 节点，log history 中也会出现拐点，并不是线性的，所以这里我们可以在 feature 分支上使用 rebase 命令
$ git pull origin master --rebase # 将远程分支 master 合并到当前分支
```


## git add

## git checkout
## git reset

```bash
# 可以把暂存区的修改撤销掉（unstage），重新放回工作区
git reset HEAD file
```

## git revert

## git rebase
## git reflog

## ISSUE
- 乱码：git config --global gui.encoding utf-8

## 参考
- [Git push大文件失败解决](https://cloud.tencent.com/developer/article/1466149)