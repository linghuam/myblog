---
title: macos使用技巧
comments: true
categories:
  - 开发工具
date: 2018-04-23 23:30:40
tags:
---


收集 mac 使用技巧
<!-- more -->

# macos使用技巧

## 软件安装

- mac 文件类型：dmg、pkg、zip、tar
- windows 文件类型：exe、msi
- 安装包：pkg
- 打包格式：dmg、zip、tar
- pkg = app文件 + 脚本文件
- dmg 打包 app 文件；打包 pkg 文件

- istat menus 电脑使用状况查看软件
- cleanmymac 清理软件
- moom 分屏软件

- dash：开发文档
- home brew： macOS 缺失的软件包的管理器
- iterm2 ：命令行工具

## 技巧

- 长按最大化按钮分屏；软件moom
- 快速查看：选中文件按空格键
- 文件改名：选中文件按回车
- 查看文件信息：cmd + i
- 切换输入法：ctrl + space (按住不动手选)
- 搜索： cmd + space ; cmd + F
- 删除光标右侧字符：fn + delete
- 删除光标左侧所有字符：cmd + delete
- cmd + 方向键 将光标移动到最边边
- `Command + Shift + .`显示隐藏文件(夹)，再按一次恢复。
- finder下 `Command + Shift + G`前往任意文件夹

## 命令行

```bash
# 文件列表
ls
ls -la

# 定位
cd filename or dirname
cd ..

# 创建文件夹
mkdir dirname

# 创建文件
touch filename

# 删除文件夹
rm -rf dirname

# 删除文件
rm filename

# 移动文件
mv sourceFile target
# example
mv a.html ../test
mv a.txt b.html ../test
mv * ../test
mv *.js ../../

# 复制文件
cp sourceFile target
# example
cp a.html test/a.html

# 退出并保存
esc + :wq
```

## 快捷键

- 清除光标之前的所有内容：Ctrl + U
- 光标跳到起始位置：Ctrl + A
- 光标调到末尾位置：Ctrl + E
- 搜索命令：Ctrl + R

## 配置环境变量

1. /etc/profile （建议不修改这个文件 ）
全局（公有）配置，不管是哪个用户，登录时都会读取该文件。

2. /etc/bashrc （一般在这个文件中添加系统级环境变量）
全局（公有）配置，bash shell执行时，不管是何种方式，都会读取此文件。

3. ~/.bash_profile （一般在这个文件中添加用户级环境变量）
每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!
但是有时在.bash_profile 文件中的环境变量并没有起到作用
这时可以查看使用的Mac OS X是什么样的Shell

```bash
➜  ~ echo $SHELL
/bin/zsh
```

4. 当mac上安装了zsh后，修改环境变量就需要在~/.zshrc中修改，比如加入代理：

```bash
export http_prox=http://10.199.75.12:8080
export https_proxy=http://10.199.75.12:8080
```
如果想要修改立即生效，需要执行

```bash
source ~/.zshrc
```

## 参考

- [MAC OS 小白入门视频](https://www.youtube.com/watch?v=pMmuk9bthUE)
