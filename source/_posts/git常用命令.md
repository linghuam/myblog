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

- 用户信息

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config core.ignorecase false  //对文件名大小写敏感
git config --global credential.helper store //记住密码
git config --global gui.encoding utf-8 //git乱码问题
```

* 文本编辑器
```bash
 $ git config --global core.editor emacs
```

* 差异分析工具
```bash
$ git config --global merge.tool vimdiff
```

* 记住密码
```bash
$ git config --global credential.helper store
```

* 查看配置信息
```
 $ git config --list
```

* 获取帮助
```
 $ git help <verb>
 如：$ git help config
```

* 不忽略空文件夹
```
在空文件夹下面创建一个.keep文件
```

## 新增库

```bash
# 本地
git init
# 远程
git clone https://github.com/linghuam/Leaflet.git
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
# 一个常用的选项是 -p，用来显示每次提交的内容差异，也可以加上 -2 来仅显示最近两次提交
git log -p -2
# 看到每次提交的简略的统计信息
git log --stat
```

https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C

## 文件操作

## 分支操作

### 创建分支

```bash
# 基于本地 master 分支创建分支
$ git checkout -b newBranchName

# 基于远程 master 分支创建分支
$ git checkout -b newBranchName origin/branchName
# 使用 -t 参数，默认在本地建立一个与远端分支同名的分支
或 $ git checkout -t origin/branchName

# 查看本地分支与远程分支的对应关系
$ git remote show origin 

# 本地新分支推送创建远程分支
$ git push origin <本地分支名>:<远程分支名>

# 关联远程分支
$ git branch --set-upstream-to=origin/<远程分支名> <本地分支名>
``` 
### 切换分支

```bash
# 工作区没新代码切换分支
$ git checkout newBranch

# 工作区有新代码切换分支
# 工作区间有未提交代码，切换分支自动执行"git merge"操作，故有冲突将无法切换成功；
$ git stash save ‘存储说明’
$ git checkout B
$ 处理完后
$ git checkout A
$ git stash pop

# 如果本来想在A分支上开发， 开发过程中才发现当前处在B分支，想强制将工作区间代码迁到A分支也可以借助“工作现场”完成。
$ git stash save ‘存储说明’
$ git checkout A
$ git stash pop
// 如有冲突且处理完所有冲突
$ git add -A

# 切换分支异常处理
# 从A分支切换到B分支由于git异常导致虽然切换分支成功，但在当前B分支上留存了大量A分支的代码
// 将所有改动提交到本地仓库
$ git add -A
$ git commit -m "这个commit会被覆盖"
//B 是当前分支名
$ git reset --hard origin/B
```
### 合并分支

```bash
# 正常合并分支代码

## 合并本地分支代码
$ git merge branchName

## 合并远程分支代码
$ git pull origin branchName

# 合并代码冲突解决
## 手动解决冲突后
## 告诉git冲突已解决: 
$ git add -A
## 合并完成，提交代码: 
$ git commit -m '说明'
$ git push

# 合并代码异常处理
// 将所有改动提交到本地仓库
$ git add -A
$ git commit -m "这个commit会被覆盖"
//B 是当前分支名
$ git reset --hard origin/B

# 撤销一个合并
如果你觉得你合并后的状态是一团乱麻，想把当前的修改都放弃，你可以用下面的命令回到合并之前的状态：
$ git reset --hard HEAD

# 合并代码减少commit次数（简洁合并）

## 方案一：
$ "git rebase xxx"，如有冲突，"git rebase --abort"，再换用"git merge xxx"。

## 方案二：("git push"之前，将本地多个commit合并成一个)
$ git rebase -i # 进入交互模式，自动打开vim
$ 将后两个“pick”改成 “s”,保存退出(ESC + : + wq）
$ 填写新的commit注释，保存退出
$ 合并完成


# 合并部分提交
# 如将 A 分支的某几个提交合并到 B 分支，而不是将整个 A 分支合并到 B
$ git checkout A
$ git log （查看A的commit id）
$ git checkout B
$ git cherry-pick <c1>..<c2>(左开右闭区间) 或 git cherry-pick <c1>^..<c2>(闭区间)
$ git cherry-pick <commitId>
```

### 删除分支

```bash
# 删除本地分支
# "-d" 如果该分支代码未合并到其他分支，将无法删除；
# "-D" 强制删除分支，不会出现任何提示；
$ git branch -D xxxx 

# 删除远程分支
$ git push origin --delete newBranch
```

### 从某个分支检出单个文件

```bash
$ git checkout [branchName] -- [fileName]
从某个 commit 中取到 文件
$ git checkout [commitId] -- [fileName]
```
 
## 关联远程库

```bash
# 本地库关联远程库，在本地仓库目录运行命令
$ git remote add origin git@github.com:nanfei9330/learngit.git

# 推送master分支的所有内容
$ git push -u origin master
# 第一次使用加上了-u参数，是推送内容并关联分支。
# 推送成功后就可以看到远程和本地的内容一模一样，下次只要本地作了提交，就可以通过命令：
$ git push origin master
#把最新内容推送到Github

# 为推送当前分支并建立与远程上游的跟踪，使用
git push --set-upstream origin master
```

## 回滚操作

```bash
# 修改上次提交，最终只有一个提交
git commit --amend
# 取消暂存文件
git reset HEAD CONTRIBUTING.md
# 撤消对文件的修改
git checkout -- CONTRIBUTING.md
# 清除所有未跟踪的变更
$ git clean -f -d
# 清除所有已经跟踪的变更
$ git checkout .
```

## 其他

```bash
# 查看日志时过滤掉 merge commits
$ git log --oneline --no-merges
# 终极技能
$ git help -g
```









### 分支

* 新建分支
```
 git branch testing  //在当前commit对象上新建一个分支指针
```

* 当前分支
```
head指针指向的分支（git branch 查看所有分支，带*号的为当前分支）
```

* 切换分支
```
git checkout testing
git checkout -b testing
git checkout -b serverfix origin/serverfix //切换到新建的 serverfix 本地分支，其内容同远程分支 origin/serverfix 一致
```

* 合并分支
```
git merge testing //将testing分支与当前分支合并（合并的结果将最为一次新的提交）
// 类型一：Fast forward合并,分支不分叉(c1->c2->c3)
// 类型二：分叉合并，由当前分支的最后一次提交、要合并进来的分支的最后一次提交和两者的共同祖先共同确定。
```

* 删除分支
```
git branch -d testing
```

### 远程操作

* 推送分支
```
 git push (远程仓库名) (分支名) 如：git push origin testing

 git push origin serverfix:serverfix  //上传我本地的 serverfix 分支到远程仓库中去，仍旧称它为 serverfix 分支

 git push origin  new-local-branch-name: new-local-branch-name  //上传新命名的本地分支
```

* 获取远程库所有更新
```
git fetch origin
//来同步远程服务器上的数据到本地该命令首先找到 origin 是哪个服务器,
从上面获取你尚未拥有的数据，更新你本地的数据库，然后把 origin/master 的指针移到它最新的位置上
//并不会将远程分支同步到本地
```

* 合并分支
```
git merge origin/serverfix //将远程分支合并到本地分支
```

* 在远程创建一个与本地 branch_name 同名的分支并跟踪
```
git push --set-upstream origin branch_name
或 
git push -u origin branch_name
```

* 在本地创建一个与 branch_name 同名分支跟踪远程分支
```
git checkout --track origin/branch_name
```

## 获取第三方远程库更新

```bash
git remote add upstream  https://github.com/vuejs/vue.git
git remote -v
git fetch upstream/master
git merge upstream/master
```

## 常见问题

* 乱码 git config --global gui.encoding utf-8



## new

git init

git commit

git log 

git checkout -b test
git checkout -b test origin/aaa

git status

git add .
git add a

// --squash 将多次提交信息合并成一个提交融合进当前仓库
//squash 压缩，压扁
git merge --squash feature1

git log
git log --文件名

git diff 
// 比较分支
git diff 分支1 分支2 // 以分支1为基准
git diff 提交1hash 提交2hash

// 查看谁提交的
git blame a

// 删除远程分支
git push [远程名] :[分支名]
git push origin :test

// 删除本地分支
git branch -d test

// 打补丁
git diff master > a.patch
git apply a.patch

// 把另一个分支的某次提交融到一个分支
// 当分支差异大，无法全部融合的时候，融合某一次提交
git cherry-pick

// 还原
git revert 提交hash // 将修改逆向运行一次，并重新提交

arc diff

## 其他

* [Git push大文件失败解决](https://cloud.tencent.com/developer/article/1466149)