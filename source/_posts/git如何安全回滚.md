---
title: git如何安全回滚
comments: true
categories:
  - 开发工具
  - git
date: 2020-01-17 19:57:46
tags:
---


项目开发中，如果要上线的代码出现问题，如何快速安全的回滚？本文将介绍 git 的回滚机制。

<!--more-->

## 本地回滚

**方法一：** `git reset`

```bash
// 回滚到上次提交状态，保留本地修改。
git reset HEAD~1
git reset <commit>

// 回滚，但不保留本地修改。
git reset --hard <commit>

// 从暂存区移除特定文件，相当于 unstage 一个文件。
git reset file

// 重置暂存区，相当于 unstage all。
git reset

// 清除掉所有未提交更改。相当于 unstage all + 撤销所有更改。
git reset --hard
```

reset 参数（head 表示当前引用，index 表示暂存区，working 表示工作区）：
* `--mixed`：reset HEAD and index。
* `--soft`：reset only HEAD。
* `--hard`：reset HEAD, index and working tree。
* `--merge`：reset HEAD, index and working tree。
* `--keep`：reset HEAD but keep local changes。

> 使用 reset 命令时应该格外注意，因为如果你拿它来操作提交历史的话，提交历史是无法恢复的。因此它通常被用来撤销缓存区和工作目录的修改。不管是哪种情况，它应该只被用于本地修改（自己本地的缓存区或者尚未 push 到远程分支的提交历史），不要用来重设和他人共享的提交历史。

**方法二：** `git revert`

被用来撤销一个已经提交的快照。生成一个撤消了引入的修改的新提交，然后应用到当前分支，并不会删除原来的历史记录。

**实现上和 reset 是完全不同的：** reset 是直接从历史中移除某个提交，而 revert 是生成一个新提交。`git revert`可以将提交历史中的任何一个提交撤销，而`git reset`会把历史上某个提交及之后所有的提交都移除掉。

```bash
git revert <commit>
```

使用`revert`要解决代码冲突。

{% asset_img reset-vs-revert.png reset和revert区别 %}

**方法三：** `git checkout`

**不带路径**

`git checkout [branch]` 类似于 `git reset --hard [branch]`。
或 `git checkout [commit]`。

> NOTE：两者区别
首先不同于`reset --hard`，`checkout`对工作目录是安全的，它会通过检查来确保将   已更改的文件弄丢。 其实它还更聪明一些。它会在工作目录中先试着简单合并一下样所有 _   还未修改过的_ 文件都会被更新。 而`reset --hard`则会不做检查就全替换所有东西。
第二个重要的区别是如何更新`HEAD`。`reset`会移动`HEAD`指向的分支的指向，不动    `HEAD`，而`checkout`只会移动`HEAD`自身来指向另一个分支。

{% asset_img reset-vs-checkout.png reset和checkout区别 %}

**带路径**

`git checkout file` 撤销对工作区中该文件的所有修改，它也不会移动 HEAD。

## 实际应用

### 本地分支版本回退的方法

```bash
git reflog
git reset --hard [commitId]
```
### 自己的远程分支版本回退的方法

```bash
git reflog
git reset --hard [commitId]
git push -f
```

### 公共远程分支版本回退的问题
使用 `git reset` 需要提醒其他队友手动**用远程分支覆盖本地分支**，否则其他队友可能又会把之前的代码提交上去。

```bash
# 用远程分支覆盖本地分支
git fetch --all
git reset --hard origin/master (这里master要修改为对应的分支名)
git pull
```

**`git revert`撤销某次提交**

```bash
git revert HEAD                     //撤销最近一次提交
git revert HEAD~1                   //撤销上上次的提交，注意：数字从0开始
git revert 0ffaacc                  //撤销0ffaacc这次提交
```

git revert 命令意思是撤销某次提交。它会产生一个新的提交，虽然代码回退了，但是版本依然是向前的，所以，当你用revert回退之后，所有人pull之后，他们的代码也自动的回退了。
但是，要注意以下几点：

> 1、revert 是撤销一次提交，所以后面的commit id是你需要回滚到的版本的前一次提交。
> 2、使用revert HEAD是撤销最近的一次提交，如果你最近一次提交是用revert命令产生的，那么你再执行一次，就相当于撤销了上次的撤销操作，换句话说，你连续执行两次revert HEAD命令，就跟没执行是一样的。
> 3、使用revert HEAD~1 表示撤销最近2次提交，这个数字是从0开始的，如果你之前撤销过产生了commi id，那么也会计算在内的。
> 4、如果使用 revert 撤销的不是最近一次提交，那么一定会有代码冲突，需要你合并代码，合并代码只需要把当前的代码全部去掉，保留之前版本的代码就可以了。

**怎样解决冲突？？**
使用revert命令，如果不是撤销的最近一次提交，那么一定会有冲突。
解决办法：一律使用**传入的更改**，即不使用当前的更改。

git revert 命令的好处就是不会丢掉别人的提交，即使你撤销后覆盖了别人的提交，他更新代码后，可以在本地用 reset 向前回滚，找到自己的代码，然后拉一下分支，再回来合并上去就可以找回被你覆盖的提交了。

## 总结

* 公共分支上回滚不要用 `git reset`。

* 回滚出错，可用 `git reflog` 恢复，但要费一番功夫。

## 参考：

* [远程仓库版本回退方法](https://zhuanlan.zhihu.com/p/56843134)

* [Git工具-重置揭密](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86)

* [Git三大特色之Stage(暂存区)](https://blog.csdn.net/qq_32452623/article/details/78417609)

* [如何回滚一次错误的合并？](https://zhuanlan.zhihu.com/p/40220954)

* [Git-少年，你想学回滚吗？想撤销文件修改吗？](https://juejin.im/post/5b3f05175188251aaa2d0e88)

* [git-reset](https://git-scm.com/docs/git-reset)

* [git-revert](https://git-scm.com/docs/git-revert)

* [git-checkout](https://git-scm.com/docs/git-checkout)

* [如何使用 Git 优雅的回滚](https://juejin.im/post/6854573212341616653?utm_source=gold_browser_extension)