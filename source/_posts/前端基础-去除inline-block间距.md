---
title: 前端基础-去除inline-block间距
comments: true
date: 2018-06-24 21:53:07
tags:
categories:
- 前端基础
- CSS
---
面试时面试官问了我一个问题，就是做一个菜单的时候，菜单项中间空出的空白是怎么引起的，如何去除？自己一下就蒙了，没遇到过这种情况，后来上网搜了搜，发现确实有这个问题，于是总结了一番。
<!--more-->

[demo](https://github.com/linghuam/test/tree/master/css/28.html)

下面是根据张鑫旭博客的整理

## 方法一: 移除空格

```HTML
<div class="menu">
    <a href="#">
    menuitem1</a><a href="#">
    menuitem2</a><a href="#">
    menuitem3</a><a href="#">
    menuitem4</a><a href="#">menuitem5</a>
</div>
```
或
```HTML
<div class="menu">
    <a href="#">menuitem1</a
    ><a href="#">menuitem2</a
    ><a href="#">menuitem3</a
    ><a href="#">menuitem4</a
    ><a href="#">menuitem5</a>
</div>
```
或
```HTML
<div class="menu">
    <a href="#">menuitem1</a><!--
    --><a href="#">menuitem2</a><!--    
    --><a href="#">menuitem3</a><!--                
    --><a href="#">menuitem4</a><!--
    --><a href="#">menuitem5</a>
</div>
```

## 方法二：省略闭合标签或只写最后一个闭合标签

兼容性写法：

```HTML
<div class="menu">
        <a href="#">menuitem1
        <a href="#">menuitem2
        <a href="#">menuitem3
        <a href="#">menuitem4
        <a href="#">menuitem5</a>
</div>
```

HTML5写法：

```HTML
<div class="menu">
        <a href="#">menuitem1
        <a href="#">menuitem2
        <a href="#">menuitem3
        <a href="#">menuitem4
        <a href="#">menuitem5
</div>
```

## 方法三：font-size:0

```HTML
<style>
    .menu{
        font-size: 0;
        /*兼容*/
        -webkit-text-size-adjust:none;
    }
    .menu a {
        font-size: 16px;
    }
</style>
<div class="menu"> 
        <a href="#">menuitem1</a>
        <a href="#">menuitem2</a>
        <a href="#">menuitem3</a>
        <a href="#">menuitem4</a>
        <a href="#">menuitem5</a>
</div>
```

## 方法四：letter-spacing 或 word-spacing

```HTML
<!--display: inline-table or table;处理Chrome兼容性问题-->
<div class="menu" style="letter-spacing: -3px;display: inline-table;"> 
        <a href="#" style="letter-spacing: 0;">menuitem1</a>
        <a href="#" style="letter-spacing: 0;">menuitem2</a>
        <a href="#" style="letter-spacing: 0;">menuitem3</a>
        <a href="#" style="letter-spacing: 0;">menuitem4</a>
        <a href="#" style="letter-spacing: 0;">menuitem5</a>
</div>
<!--或-->
<div class="menu" style="word-spacing: -6px;display: inline-table;"> 
        <a href="#" style="word-spacing: 0;">menuitem1</a>
        <a href="#" style="word-spacing: 0;">menuitem2</a>
        <a href="#" style="word-spacing: 0;">menuitem3</a>
        <a href="#" style="word-spacing: 0;">menuitem4</a>
        <a href="#" style="word-spacing: 0;">menuitem5</a>
</div>
```

##  其他方法

1.使用浮动：不推荐，会造成一些奇怪[问题](https://codepen.io/chriscoyier/pen/blExo)

2.使用flex布局

3.other

YUI:
```css
.yui3-g {
    letter-spacing: -0.31em; /* webkit */
    *letter-spacing: normal; /* IE < 8 重置 */
    word-spacing: -0.43em; /* IE < 8 && gecko */
}

.yui3-u {
    display: inline-block;
    zoom: 1; *display: inline; /* IE < 8: 伪造 inline-block */
    letter-spacing: normal;
    word-spacing: normal;
    vertical-align: top;
}
```
or 

```css
li {
    display:inline-block;
    background: orange;
    padding:10px;
    word-spacing:0;
    }
ul {
    width:100%;
    display:table;  /* 调教webkit*/
    word-spacing:-1em;
}

.nav li { *display:inline;}
```

## 参考
-[去除inline-block元素间间距的N种方法](https://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-%E5%8E%BB%E9%99%A4%E9%97%B4%E8%B7%9D/)
-[Fighting the Space Between Inline Block Elements](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)