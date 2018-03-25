---
title: 每天一道基础题-HTML概述
comments: true
date: 2018-03-21 19:59:47
tags:
  - html
categories:
  - 每天一道基础题
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### 核心？
- 标记语言
- 语义化

*html 就像搭积木玩具中的一个个积木，用不同的积木来表示不同的元素*

### HTML 元素？

标签名 + 内容 + 属性 + 事件

#### 元素结构
{% asset_img 01.png html元素结构%}

*大多数是这种结构，还有一种是无内容的结构，如`<img src="a.png">`*

#### 元素属性
- 一般属性：属性名=属性值
- bool 属性：属性名和属性值相同，可简写为属性名，如 disabled
{% asset_img 02.png HTML属性%}

#### 元素分类
- 块级元素
- 内联元素
- HTML5 分类标准：https://html.spec.whatwg.org/multipage/indices.html#element-content-categories
{% asset_img 03.png 新分类标准 %}


### 为什么？

#### HTML 与其他标记语言的区别？如 XML。
主要区别在于 XML 是一种存储数据的格式，焦点在数据持久化上。而 HTML 是集数据以及表现、行为于一体，焦点在展现和交互上。

#### 怎么理解 HTML 语义化？为什么要语义化？
利于理解文档结构、利于SEO、利于爬虫、利于屏幕阅读器

#### 块级元素与内联元素区别？
- [博文1](http://www.cnblogs.com/ruxpinsp1/archive/2008/07/03/quicky-block-vs-inline.html)
- [博文2](http://www.cnblogs.com/iceflorence/p/6626187.html)

#### 哪些公共属性？哪些特有属性？
- [文档1](https://html.spec.whatwg.org/multipage/indices.html#elements-3)


### 参考
- [MDN HTML 文档](https://developer.mozilla.org/zh-CN/docs/learn/HTML)
