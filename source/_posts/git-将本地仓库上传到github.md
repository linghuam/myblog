---
title: git-将本地仓库上传到github
comments: true
date: 2018-01-04 14:29:17
tags:
categories:
- 开发工具
- git
---

在开发中，我们通过`git init`命令在本地创建了一个版本库，但是如何把它上传到 github 上共享呢。

<!-- more -->

其实这个问题再延伸一下，就是如何关联远程仓库和本地仓库。分以下几种情况：

* github有，本地无
* github无，本地有
* github有，本地有

## github有，本地无

即在github上已经创建了一个库A，但本地上没有与之关联的库。

此时只需执行以下命令即可在本地创建一个与之关联的库。
```bash
git clone 远程库地址
// 如： git clone https://github.com/linghuam/weichat.git
```

## github无，本地有

先需要再github上创建一个空的远程库，然后转到[github有，本地有](#t1)


## github有，本地有  <span id="t1"></span>

** 第一步：**
在本地的git bash 中运行命令：

```
git remote add origin 远程库地址

// 如 git remote add origin https://github.com/linghuam/weichat.git
```
这句话的意思是：为本地库添加关联的远程库，远程库的名字是`origin`。

** 第二步：**
将本地内容推送至远程库

```bash
// 1.将本地修改提交到本地库 （若已提交，不必执行）
git add .
git commit -m '注释内容'

// 2.合并远程库内容到本地库 （若远程库为空，不必执行）
// --rebase参数解决分支分叉问题：http://blog.csdn.net/hudashi/article/details/7664631
git pull --rebase origin master

// 3. 将本地库推送到远程库
// 加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令(不加-u)。
git push -u origin master
```

## 参考资料
* git官网：https://git-scm.com/docs
* Pro Git（中文版）：http://git.oschina.net/progit/index.html
* 廖雪峰Git教程：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
