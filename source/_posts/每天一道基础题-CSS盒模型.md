---
title: 每天一道基础题-CSS盒模型
comments: true
date: 2018-04-23 23:00:36
tags:
  - css
categories:
  - 每天一道基础题
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### 什么是盒模型？
在 CSS 中，所有的 HTML 元素都可以被看做一个个”矩形盒子“，它由 content + padding + border + margin 组成。

### 标准盒模型(W3C)和IE(\<IE6)盒模型？
{% asset_img 1.png %}

### box-sizing?
- content-box（标准盒模型）
  - width = 内容的宽度
  - height = 内容的高度
- border-box（怪异盒模型）
  - width = border + padding + 内容的宽度
  - height = border + padding + 内容的高度

### 视觉格式化模型(visual formatting model)
[display属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display)<br>
最常见的三种：block, inline, and inline-block

### 外边距塌陷?
> 所谓的塌陷其实是两个BFC的相邻盒或者父子盒相互作用时产生的。
> 在形成BFC的两个盒子会取两个盒子相邻边的最大margin作为相邻边的共用maring。

### 块级格式化上下文 BFC(Block Formatting Context)？
- [Understanding CSS Layout And The Block Formatting Context](https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/)

### 行内格式化上下文 IFC(Inline Formatting Context)？
-[When does a box establish an inline formatting context?](https://stackoverflow.com/questions/16936297/when-does-a-box-establish-an-inline-formatting-context)

### 参考文档
- [Understanding CSS Layout And The Block Formatting Context](https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/)
- [Visual formatting model](https://www.w3.org/TR/CSS2/visuren.html)
- [BFC and IFC](https://www.w3.org/TR/CSS21/visuren.html#block-formatting)
- [你真的了解盒模型吗](https://rainey.space/2016/07/02/Ni_Zhen_De_Liao_Jie_He_Mo_Xing_Ma/)
