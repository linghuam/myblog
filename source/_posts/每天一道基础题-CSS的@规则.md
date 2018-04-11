---
title: 每天一道基础题-CSS的@规则
comments: true
date: 2018-04-11 23:07:20
tags:
  - css
categories:
  - 每天一道基础题
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### @ 作用？
@ 用于传递**元数据**、**条件信息** 或其他 **描述性信息**的。

### 常规 @ 规则？
@ + 规则名称 + 规则内容 + 分号
- [@charset](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@charset)
，定义样式表使用的字符集
- [@import](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@import)，告诉 CSS 引擎引入一个外部样式表
- [@namespace](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@namespace)，告诉 CSS 引擎必须考虑 XML 命名空间

### 嵌套 @ 规则？
@ + 规则名称 + 嵌套内容
- [@media](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@media)，条件规则，媒体查询
- [@page](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@page)，描述打印文档时布局的变化
- [@font-face](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face)，描述下载的外部字体
- [@keyframes](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes)，描述 CSS 动画关键帧
- [@supports](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@supports)，如果满足给定条件则条件规则组里的规则生效
- [@document](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@document)，如果文档样式表满足给定条件则条件规则组里的规则生效
