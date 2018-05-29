---
title: 每天一道基础题-获取HTML元素的宽高和位置
comments: true
date: 2018-05-24 19:53:16
tags:
  - css
categories:
  - 每天一道基础题
---

在做一些组件和交互时，常常需要动态获取鼠标点击位置、元素宽高和元素位置信息，网上有很多种方法，但自己没有总结过，不知道各种方法的优缺点和兼容性，在此专门的总结一下。
<!-- more -->

**Note：** 这些关于视觉的内容都被总结在了 W3C 的 [CSSOM View Module](https://www.w3.org/TR/cssom-view-1/) 模块中，里面有详细的接口定义和说明，建议好好研读。

## 阅读 W3C 规范的总结

### Extensions to the *Window* Interface

{% asset_img window.png %}

> **图片纠错：** scrollX = pageXOffset：表示滚动条在X轴方向上滚动的距离；scrollY = pageYOffset：表示滚动条在Y轴方向上滚动的距离

{% asset_img window-chart2.png %}

 The *Screen* Interface
{% asset_img screen.png %}
{% asset_img screen-chart.png %}

### Extensions to the *Document* Interface

{% asset_img document.png %}

### Extensions to the *Element* Interface

{% asset_img element.png %}
{% asset_img element-chart.png %}
{% asset_img scrollheight.png %}




## 元素位置与大小

- Element.clientWidth：**只读属性**，元素内部宽度，包括**内边距**，不包括**垂直滚动条（如果有）、边框、外边距**
> Note：该属性值会被四舍五入为一个**整数**。如果你需要一个小数值，可使用 element.getBoundingClientRect()。

-  Element.clientHeight：**只读属性**，元素内部高度，包含**内边距**，不包括**水平滚动条、边框、外边距**
> Note：内联元素（display:inline）clientWidth、clientHeight都为零，但 display:inline-block 有宽高
- Element.clientLeft：**只读属性**，左边框的宽度，包括滚动条宽度，不包括左外边距和左内边距
- Element.clientTop：**只读属性**，顶部边框的宽度，包括滚动条宽度，不包括顶部外边距和顶内边距

- Element.offsetWidth：**只读属性**，元素的布局宽度，包含**内边距、边框、竖直滚动条**
> Note：该属性值会被四舍五入为一个**整数**。如果你需要一个小数值，可使用 element.getBoundingClientRect()。

- Element.offsetHeight：**只读属性**，元素的像素高度，包含**内边距、边框、水平滚动条**，不包含 :before 或 :after 等伪类元素的高度
> Note: 对于文档的body对象，它包括代替元素的CSS高度线性总含量高。浮动元素的向下延伸内容高度是被忽略的

- Element.offsetLeft：**只读属性**，返回当前元素左上角相对于  HTMLElement.offsetParent 节点的左边界偏移的像素值。
- Element.offsetTop： **只读属性**，返回当前元素相对于其 offsetParent 元素的顶部的距离。
> offsetParent 指的是距该元素最近的 position 不为 static 的祖先元素，如果没有则指向 body 元素。确定了 offsetParent，offsetLeft 指的是元素左侧偏移offsetParent 的距离，同理 offsetTop 指的是上侧偏移的距离。

- Element.offsetParent：是一个只读属性，返回一个指向最近的（closest，指包含层级上的最近）包含该元素的定位元素。如果没有定位的元素，则 offsetParent 为最近的 table, table cell 或根元素（标准模式下为 html；quirks 模式下为 body）。当元素的 style.display 设置为 "none" 时，offsetParent 返回 null。offsetParent 很有用，因为 offsetTop 和 offsetLeft 都是相对于其内边距边界的。
> 在 Webkit 中，如果元素为隐藏的（该元素或其祖先元素的 style.display 为 "none"），或者该元素的 style.position 被设为 "fixed"，则该属性返回 null。
> 在 IE 9 中，如果该元素的 style.position 被设置为 "fixed"，则该属性返回 null。（display:none 无影响。）

- Element.scrollWidth：只读，返回元素的内容宽度，返回四舍五入的整数，返回值包括padding，但不包括margin和border
- Element.scrollHeight： 返回元素的内容高度
- Element.scrollLeft：元素在水平方向滚动的范围
- Element.scrollTop：元素在垂直方向滚动的范围
- window.screen.width： 返回屏幕的宽度
- window.screen.height：返回屏幕的高度
> 该属性返回的宽度值不一定就是浏览器窗口可使用的宽度。当有其他小工具占据了屏幕空间时，浏览器有时不能占用小工具（如任务栏）占据的空间。window.screen.width 和 window.screen.availWidth 两者不同
> 在返回该值时，IE 会考虑缩放设置。只有在缩放比例为 100% 时，IE 才返回真实的屏幕宽度
- window.screen.availWidth：返回浏览器窗口可占用的水平宽度（单位：像素）
- window.screen.availHeight：返回浏览器窗口在屏幕上可占用的垂直空间，即最大高度
> It's the height the browser's window can have if it is maximized, including the browser's bars. So when the window is maximized, screen.availHeight === window.outerHeight
- Element.getBoundingClientRect()： 返回元素的包围盒，小数
>left:包围盒左边 border 以外的边缘距页面左边的距离
 right:包围盒右边 border 以外的边缘距页面左边的距离
 top:包围盒上边 border 以外的边缘距页面顶部的距离
 bottom:包围盒下边 border 以外的便于距页面顶部的距离
 width: content + padding + border
 height: content + padding + border
 注意，设置外边距时外边距合并的情况

{% asset_img 1.png %}
{% asset_img 2.png %}
{% asset_img 3.png %}
http://www.cnblogs.com/youxin/archive/2012/09/21/2697514.html

## 鼠标操作
- MouseEvent.screenX
- MouseEvent.screenY
- MouseEvent.clientX
- MouseEvent.clientY
- MouseEvent.pageX
- MouseEvent.pageY
- MouseEvent.x
- MouseEvent.y
- MouseEvent.offsetX 
- MouseEvent.offsetY
- MouseEvent.movementX
- MouseEvent.movementY
https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent

## 键盘操作
https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent

## 引用
> 1. Document.documentElement 是一个会返回文档对象（document）的根元素的只读属性


## 参考
- [CSSOM View Module](https://www.w3.org/TR/cssom-view-1/)
- [CSSOM视图模式(CSSOM View Module)相关整理](http://www.zhangxinxu.com/wordpress/2011/09/cssom%E8%A7%86%E5%9B%BE%E6%A8%A1%E5%BC%8Fcssom-view-module%E7%9B%B8%E5%85%B3%E6%95%B4%E7%90%86%E4%B8%8E%E4%BB%8B%E7%BB%8D/)
- [W3C DOM Core](https://www.w3.org/TR/DOM-Level-2-Core/core.html#ID-87CD092)
- [UIEvent](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent)
- [一张图彻底掌握scrollTop, offsetTop, scrollLeft, offsetLeft......](https://github.com/pramper/Blog/issues/10)
