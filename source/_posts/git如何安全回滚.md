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

## 远程回滚

**方法一：** 可以在本地回滚后，用 `git push -f origin branch`强制回滚远程仓库，但不安全。

## 不小心提交了大文件导致 git push 不了，怎么解决？

github 限制单个文件提交体积不超过 100M。

```bash
# 1、先查找到提交大文件的记录
git log
# 2、依次撤销commit（包含过要删除的大文件的 commit 必须都给撤销了，要不然会报错）
git reset commitid
# 3、上面的撤销只是对 commit 命令的撤销，不会对你修改过的代码撤销的，他们还是在的。
# 4、删除掉本地的大文件（或者修改 gitignore 忽略掉）
# 5、重新进行提交
```


## 总结

* 公共分支上回滚不要用 `git reset`。

* 回滚出错，可用 `git reflog` 恢复，但要费一番功夫。

## 参考：

* [Git工具-重置揭密](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86)

* [Git三大特色之Stage(暂存区)](https://blog.csdn.net/qq_32452623/article/details/78417609)

* [如何回滚一次错误的合并？](https://zhuanlan.zhihu.com/p/40220954)

* [Git-少年，你想学回滚吗？想撤销文件修改吗？](https://juejin.im/post/5b3f05175188251aaa2d0e88)

* [git-reset](https://git-scm.com/docs/git-reset)

* [git-revert](https://git-scm.com/docs/git-revert)

* [git-checkout](https://git-scm.com/docs/git-checkout)
