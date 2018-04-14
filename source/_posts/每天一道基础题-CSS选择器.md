---
title: 每天一道基础题-CSS选择器
comments: true
date: 2018-04-12 21:50:27
tags:
  - css
categories:
  - 每天一道基础题
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### 选择器原理？
浏览器的样式系统是从最右边的选择符开始向左进行匹配的
> The style system matches a rule by starting with the rightmost selector and moving to the left through the rule’s selectors. As long as your little subtree continues to check out, the style system will continue moving to the left until it either matches the rule or bails out because of a mismatch.

### 选择器分类？
- **简单选择器(Simple selectors)：** tagName、id、class、*
- **属性选择器(Attribute selectors)：**属性/属性值，[了解更多...](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Introduction_to_CSS/Attribute_selectors)
- **伪类(Pseudo-classes)：** [了解更多...](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
- **伪元素(Pseudo-elements)：**[了解更多...](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
- **组合器(Combinators)：** [了解更多...](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Introduction_to_CSS/Combinators_and_multiple_selectors)
- **多用选择器(Mutiple selectors)：**将以逗号分隔开的多个选择器放在一个CSS规则下面， 以将一组声明应用于由这些选择器选择的所有元素。

### 选择器优先级？
为了内容完整性添加此标题，此处不作详细介绍，将在 CSS 层叠规则处介绍

### 关于 CSS 选择器性能问题？
《高性能网站建设指南》的作者 [Steve Souders](http://stevesouders.com/) 结论：

- 对于绝大部分网站，优化 CSS 选择器对网站整体性能的影响很小，不值得这么做。
- 更应该关注某些类型的 CSS 选择器以及与 JavaScript 交互的部分，这才是影响性能的关键。

作者从选择器的原理的角度进一步探索了哪些 CSS 选择器真正的影响性能，他的结论是：

- 影响性能的决定因素是**最右边的选择器**选择的范围大小。

并给出了一些例子：
```CSS
a.class007 * {}  /* 最右边的通配符会选择所有元素，对性能有较大影响*/
a.class007 div {}
#id0007 > a{}
.class007 [href]{}
div:first-child{}
```

下面摘自作者的原话：
>For most web sites, the possible performance gains from optimizing CSS selectors will be small, and are not worth the costs. There are some types of CSS rules and interactions with JavaScript that can make a page noticeably slower. This is where the focus should be.

>  For 70% or more of today’s users, improving these CSS selectors would only make a 20 ms improvement.

> The key to optimizing CSS selectors is to focus on the rightmost selector.

> Not all CSS selectors hurt performance, even those that might look expensive. The key is focusing on CSS selectors with a wide-matching key selector.

### 参考
- [Performance Impact of CSS Selectors](https://www.stevesouders.com/blog/2009/03/10/performance-impact-of-css-selectors/)
- [Simplifying CSS Selectors](https://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/)
