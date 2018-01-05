---
title: gitignore配置文件
comments: true
date: 2018-01-05 17:31:00
tags:
  - git
categories:
  - config
---

gitignore 文件是用来标记文件是否被纳入版本管理系统的配置文件，一般在 git 仓库的根目录下创建名为 `.gitignore`的文件。下面详细说明它的一些用法。
<!-- more -->

## 规则设计

* gitignore文件中一行代表一个规则

* 空白行不匹配任何文件，可以用它来作为分隔行

* 结尾的空格将被忽略，除非它们通过“\”引用

* 以"#"号开头的行是注释行

* 以星号“*”通配多个字符

* 以问号“?”通配单个字符

* 以方括号“[]”包含单个字符的匹配列表，如 “test[abc]d.txt” 匹配 “testad.txt" "testbd.txt" "testcd.txt"

* 叹号“!”表示不忽略(跟踪)匹配到的文件或目录，如 “test[abc]d.txt !test[c]d.txt” 将不会忽略 “testcd.txt”文件

* 路径包含“/”

> “foo/” 将全局匹配foo路径下的所有文件，如：“foo/a.txt”，“foo/a/b”, "a/foo/b"都将被匹配

> “foo/\*” 或 “foo/\*.html” 将只会匹配跟目录下的文件，如：“foo/*” 会匹配 “foo/a/b” 但不会匹配 “a/b/foo/c"

* 路径不包含“/”

> “foo” 将全局匹配foo路径，效果同 “foo/”


* 头部的“/”匹配根目录下的路径，如："/*.c" matches "cat-file.c" but not "mozilla-sha1/sha1.c"

* 双星号(**)

  * 以 "\*\*" 开头的匹配所有路径。如："\*\*/foo" matches file or directory "foo" anywhere, the same as pattern "foo". "\*\*/foo/bar" matches file or directory "bar" anywhere that is directly under directory "foo".

  * 以 "/\*\*" 结尾的匹配路径下的所有文件。如："abc/\*\*" matches all files inside directory "abc"

  * 以 "/\*\*/" 中部的匹配零个或一个路径。如："a/**/b" matches "a/b", "a/x/b", "a/x/y/b" and so on

  * 其他的模式被认为是无效的

## 注意事项

* gitignore只能将还未被纳入版本控制系统的文件排除出版本控制，如果想把一个已经进入版本控制的文件排除出去，使用如下命令(点号不能忽略)：
```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

* Windows下创建.gitignore文件的常用方法

 * 方法一（最直接）：

   在资源管理创建文件时，文件命名“.gitignore.”，注意结尾有个.号，回车确认时系统会自动存成.gitignore。

 * 方法二：

   打开文本编辑器，保存时文件名输入“.gitignore”，保存类型选“所有文件”、

 * 方法三：

   进入cmd命令行，执行 echo > .gitignore 输入空内容并创建文件，
   或执行 rename somefile .gitignore、copy somefile .gitignore 从已有文件复制、重命名。
   

## 参考文档
* [官方解释](https://git-scm.com/docs/gitignore)

* [gitignore文件模板](https://github.com/github/gitignore)

* [自动生成gitignore文件网站](https://www.gitignore.io/)
