---
title: 前端基础-CSS层叠与继承
comments: true
date: 2018-04-18 22:27:59
tags:
categories:
- 前端基础
- CSS
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### 层叠？

**CSS层叠规则：（按权重由高到低排序）**
1. 重要性（!important 强于非 !important）
2. 特殊性 (内联：1000，id：0100，class/属性/伪类：0010，元素/伪元素：0001；结合符、通配符、继承无特殊性)
3. 源代码顺序（后申明的覆盖前面的）

>注意: 通用选择器 (*), 复合选择器 (+, >, ~, ' ') 和否定伪类 (:not) 在特殊性中无影响。

### 继承？

**可继承属性：（列举常用的）**
- font
- color
- cursor
- letter-spacing
- line-height
- list-style
- text-align
- visibility
- [w3c](https://www.w3.org/TR/CSS21/propidx.html)
- [stackoverflow](https://stackoverflow.com/questions/5612302/which-css-properties-are-inherited)

**不可继承属性：**
- 大多数框模型(position、z-index、margin、padding、border、background）

**控制继承：**
- `inherit`：选定元素属性值设置为和父元素一样
- `initial`：选定元素属性值设置为和浏览器默认样式一样
- `unset`：将属性重置为自然值。即若是自然继承的，表现像 inherit；否则，表现像 initial
- `revert`：属性值被设置成自定义样式所定义的属性（如果被设置）， 否则属性值被设置成用户代理的默认样式

>注意: initial 和 unset 不被IE支持。
