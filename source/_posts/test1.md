---
title: test1
date: 2017-12-22 14:10:06
tags: 
- test1
---

# 文件与目录管理

## 目录的基本操作
1. 显示目录和目录列表
```bash
ls
```
2. 创建一个目录
```bash
mkdir
```
3. 删除一个目录
```bash
rmdir
```
4. 切换目录
```bash
cd
cd .. // 返回上层目录
cd ~ or cd // 直接切换到用户根目录下
cd - // 返回进入此目录之前所在的目录
```
5. 显示当前工作目录
```bash
pwd
```

## 文件的基本管理
1. 创建新文件
```bash
touch
```
2. 复制文件
```bash
cp [参数] [源] [目标]
```
3. 移动文件
```bash
mv [参数] [源] [目标]
```
4. 删除文件
```bash
rm
```
5. 查看文件内容
```bash
more // 分屏显示
less
head // 查看前 n 行
tail
od // 指定格式查看
```
6. 文件类型
```bash
ls -l // 列出所有文件信息
file // 识别文件类型
```
7. 查询文件
```bash
find
locate
grep
```
8. 其他管理命令
```bash
cd
man [命令名] // 显示命令的帮助信息
clear // 清屏
```
