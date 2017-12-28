---
title: editorconfig配置文件详解
comments: true
date: 2017-12-28 13:46:18
tags:
  - config
categories:
  - config
---

EditorConfig可以帮助开发者在不同的编辑器和IDE之间定义和维护一致的代码风格。

官方网站： http://editorconfig.org/
<!--more-->

# Usage

**step1：** 在项目根目录下创建一个`.editorconfig`文件

**step2：** 安装对应编辑器的[插件](http://editorconfig.org/#download)

**step3：** 填写配置文件

**规则如下:**

通配符 | 说明
----------- | -----------
\* | 匹配除/之外的任意字符串
\*\* | 匹配任意字符串
? | 匹配任意单个字符
[name] | 匹配name字符
[!name] | 匹配非name字符
{s1,s3,s3} | 匹配任意给定的字符串（0.11.0起支持）
{num1..num2} | 匹配任意在 num1 与 num2 之间的整数

特殊字符可以用\转义，以使其不被认为是通配符。

**支持属性：**

注：不是所有属性插件都支持，完整版见[complete list of properties](https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties)

* **root：** 设置为 "true" ,编辑器根据此属性停止查找。
* **charset：** 一般设置为 "utf-8" , 可选值有 latin1, utf-8, utf-8-bom, utf-16be or utf-16le。
* **indent_style：**缩进类型 , "space" 或 "tab"
* **indent_size：**缩进数量 , 一般 "2" 或 "4", 可选 "tab"
* **tab_width：**设置整数用于指定替代tab的列数。默认值就是indent_size的值，一般无需指定。
* **end_of_line：**定义换行符，支持lf、cr和crlf。
* **trim_trailing_whitespace：**是否删除行尾的空格， "true" or "false"
* **insert_final_newline：**是否在文件的最后插入一个空行，"true" or "false"

# Example

以下是一个文件示例，用于设置Python和JavaScript代码格式。
```
# EditorConfig is awesome: http://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
end_of_line = lf
insert_final_newline = true

# Matches multiple files with brace expansion notation
# Set default charset
[*.{js,py}]
charset = utf-8

# 4 space indentation
[*.py]
indent_style = space
indent_size = 4

# Tab indentation (no size specified)
[Makefile]
indent_style = tab

# Indentation override for all JS under lib directory
[lib/**.js]
indent_style = space
indent_size = 2

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

# My Config
```
root = true

[*]
charset = utf-8s
indent_style = space
indent_size = 2
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
```

# Recommend

* [EditorConfig介绍1](http://www.jianshu.com/p/712cea0ef70e)
* [EditorConfig介绍2](http://blog.csdn.net/cengjingcanghai123/article/details/43953307)
