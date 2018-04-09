---
title: 每天一道基础题-HTML嵌入资源之Img图片
comments: true
date: 2018-04-09 21:32:29
tags:
  - html
categories:
  - 每天一道基础题
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### Img 语义化？
向网页中添加图片有三种方式：
1. HTML 方式，通过 img 标签添加图片（更具语义化）
2. CSS 方式，通过 background-image 设置背景图（只具有装饰意义）
3. JS 方式，通过 js 操作 canvas 绘制图形 （灵活，适用于一些精细化操作）

以下做法会使 img 标签更好的支持 SEO：
1. 给图片资源起一个更具语义化的名字
2. src 属性的路径使用相对路径，一是提高效率，减少 DNS 查询；二是更好的 SEO
3. alt 属性赋值，便于机器识别、关闭图片节省带宽、兼容性

### 为图片搭配说明文字？
传统做法：
```HTML
<div class="figure">
  <img src="images/dinosaur.jpg"
       alt="The head and torso of a dinosaur skeleton;
            it has a large head with long sharp teeth"
       width="400"
       height="341">

  <p>A T-Rex on display in the Manchester University Museum.</p>
</div>
```

HTML5 做法：
```HTML
<figure>
  <img src="images/dinosaur.jpg"
       alt="The head and torso of a dinosaur skeleton;
            it has a large head with long sharp teeth"
       width="400"
       height="341">

  <figcaption>A T-Rex on display in the Manchester University Museum.</figcaption>
</figure>
```

注意：figure 可以是几张图片、一段代码、音视频、方程、表格或别的。

### 创建响应式图片？
1. 通过 img 标签的 srcset 和 sizes 两个新属性
2. 使用 picture、source 标签
3. 使用 css 媒体查询

经典好文：
1. [响应式图片 MDN 文档](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)
2. [Responsive Images: If you’re just changing resolutions, use srcset](https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/)
3. [Responsive Images 101](https://cloudfour.com/thinks/responsive-images-101-definitions/#responsive-images-101-series)

### 其他？
- [盗链与防盗链](http://www.cnblogs.com/mumuxinfei/p/5256209.html)
- [8种网站防止盗链的方法](http://developer.51cto.com/art/201105/263526.htm)
