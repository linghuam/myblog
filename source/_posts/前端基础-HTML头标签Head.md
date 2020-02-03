---
title: 前端基础-HTML头标签Head
comments: true
date: 2018-03-25 21:02:57
tags:
categories:
- 前端基础
- HTML
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### Head 的作用是什么？
头部的主要作用是用来定义整个页面一些**元数据**（如标题、编码、作者、样式资源、脚本资源等）的，不用于显示内容。

### Head 里面可以有哪些内容?

#### Title 标签
定义文档的标题，显示在浏览器的标题栏或标签页上。

它只可以包含文本，若是包含有标签，则包含的任何标签都不会被解释。

一个 head 元素只能包含一个 title 元素

同时需要开标签和闭标签。注意：遗漏 title 标签会导致浏览器忽略掉页面的剩余部分

```HTML
<head>
<title>我是 title</title>
</head>
```

#### Meta 标签
用于为文档添加_元数据_，利于 SEO 优化，防止安全问题。

[meta 标签使用](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)

```HTML
<head>
<!--指定文档编码-->
<meta charset="utf-8">
<meta name="author" content="linghuam">
<meta name="description" content="this is a learning example">
<!-- Redirect page after 3 seconds -->
<meta http-equiv="refresh" content="3;url=http://www.mozilla.org/">
</head>
```

#### Link 标签
指定了外部资源与当前文档的关系，通常用于链接 css 资源。

[link 标签使用](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link)

**为站点添加图标的两种方式：**
1. 将其保存在与网站的索引页面相同的目录中，以 .ico 格式保存。
2. `<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">`

```HTML
<link rel="stylesheet" href="my-css-file.css">
```

#### Style 标签
为文档添加样式。

元数据内容，如果声明了 scoped 属性，变为流内容。

既可以在 head 中，又可以在 body 中。

[style 标签使用](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style)

```HTML
<head>
<style type="text/css">
body{
  color:red;
}
</style>
</head>
```

#### Script 标签
嵌入或引用可执行脚本。

既可以在 head 中，又可以在 body 中。

[script 标签使用](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script)

```HTML
<head>
<script src="a.js"></script>
</head>
```
