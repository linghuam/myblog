---
title: 每天一道基础题-CSS中vertical-align属性
comments: true
date: 2018-05-23 22:45:10
tags:
  - css
categories:
  - 每天一道基础题
---

在刚刚接触 CSS 的同学中，经常使用到 vertical-align 来实现垂直对齐，但经常会困惑的是它并没有起到什么效果，下面就一起来探讨一下它到底是个什么鬼。
<!-- more -->

## 我遇到的问题

```HTML
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>vertical-align</title>
</head>

<body>
    <div class="container">
        <input id="input1" type="checkbox">
        <label for="input1">
            选项一
        </label>
        <input id="input2" type="checkbox">
        <label for="input2">
            选项二
        </label>
        <input id="input3" type="checkbox">
        <label for="input3">
            选项三
        </label>
    </div>
</body>

</html>
```
{% asset_img 1.png%}
我们要将复选框跟文字垂直居中对齐，这时要用到 vertical-align
方法：
```css
label{
    vertical-align: middle;
}
```

## 基本概念
- 该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐
- 初始值： baseline
- 可取值： baseline | sub | super | text-top | text-bottom | middle | top | bottom | <percentage> | <length>
- 适用元素：inline、inline-block、table-cell、::first-letter、::first-line
- 继承性：无
- 百分比值：参照元素自身的 line-height 值
{% asset_img 2.png %}

## 最佳实践

> 1. 只有一个元素属于 `inline`或是`inline-block`（table-cell也可以理解为inline-block水平）水平，其身上的 vertical-align 属性才会起作用
> 2. vertical-align:middle属性的表现与否，仅仅与其父标签有关，至于我们通常看到的与后面的文字垂直居中显示那都是假象
> 3. vertical-align的本质上是个独立的个体，与后面的inline水平的元素是不存在直接的关系的。两者没有必然的联系，这是一个需要认识清楚的重要的东西。

## 例子
[demo](http://www.zhangxinxu.com/study/201005/verticle-align-test-demo.html)

## 参考
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/vertical-align)
- [line-height](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height)
- [text-align](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-align)
- [我对CSS vertical-align的一些理解与认识（一）](http://www.zhangxinxu.com/wordpress/2010/05/%E6%88%91%E5%AF%B9css-vertical-align%E7%9A%84%E4%B8%80%E4%BA%9B%E7%90%86%E8%A7%A3%E4%B8%8E%E8%AE%A4%E8%AF%86%EF%BC%88%E4%B8%80%EF%BC%89/)
- [CSS vertical-align的深入理解(二)之text-top篇](http://www.zhangxinxu.com/wordpress/2010/06/css-vertical-align%E7%9A%84%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%EF%BC%88%E4%BA%8C%EF%BC%89%E4%B9%8Btext-top%E7%AF%87/)
- [CSS深入理解vertical-align和line-height的基友关系](http://www.zhangxinxu.com/wordpress/2015/08/css-deep-understand-vertical-align-and-line-height/)
- [Vertical-Align: All You Need To Know](http://christopheraue.net/design/vertical-align)
