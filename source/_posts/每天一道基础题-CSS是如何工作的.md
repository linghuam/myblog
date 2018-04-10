---
title: 每天一道基础题-CSS是如何工作的
comments: true
date: 2018-04-10 21:42:04
tags:
  - css
categories:
  - 每天一道基础题
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### CSS 工作原理？
- 首先下载和解析 html 并最终形成 DOM(Document Object Model)
- 当 html 还在解析时，下载和解析 CSS 并最终形成 CSSOM(CSS Object Model)
- 浏览器根据 DOM 和 CSSOM 绘制渲染最终页面
<br>
{% asset_img 01.png CSS工作原理图 %}

### CSS 作用于 HTML 的几种方式？
1. 通过 link 标签导入单独的 css 文件
2. 通过 style 标签插入 css 代码
3. 通过 element 的 style 属性写入样式

### 参考
- [Episode 32: How CSS works and what we aim for with CSS](https://hackernoon.com/episode-32-how-css-works-and-what-we-aim-for-with-css-ecf2304904a9)
