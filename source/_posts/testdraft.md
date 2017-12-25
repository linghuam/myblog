---
title: testdraft
date: 2017-12-22 14:22:57
excerpt: true
categories:
- git
tags:
- testdraft
---


## git教程

* [廖雪峰-git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
* [高级教程-Pro Git](http://git.oschina.net/progit/)
* [官网-GitBook](https://git-scm.com/book/zh/v2)


## git常用命令

### 配置

 * 用户信息
```
 $ git config --global user.name "John Doe"
 $ git config --global user.email johndoe@example.com
 $ git config core.ignorecase false  //对文件名大小写敏感
 $ git config --global credential.helper store //记住密码
 $ git config --global gui.encoding utf-8 //git乱码问题
```
 * 文本编辑器
```
 $ git config --global core.editor emacs
```
 * 差异分析工具
```
 $ git config --global merge.tool vimdiff
 ```
 * 记住密码
 ```
 git config --global credential.helper store
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
### 克隆远程库

```
git clone http://git.oschina.net/iOceanPlus/XGSWebProject

在本地新建了一个版本库，默认建一个本地master分支。
用origin/master(远程跟踪分支，用户只读)表示远程库的master分支
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
## 常见问题

* 乱码 git config --global gui.encoding utf-8
