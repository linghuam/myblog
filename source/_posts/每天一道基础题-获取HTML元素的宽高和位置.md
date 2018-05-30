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

### Extensions to the **[Window](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-window-interface)** Interface

{% asset_img window.png %}

**图片纠错：** scrollX = pageXOffset：表示滚动条在X轴方向上滚动的距离；scrollY = pageYOffset：表示滚动条在Y轴方向上滚动的距离

{% asset_img window-chart2.png %}

The *Screen* Interface

{% asset_img screen.png %}

{% asset_img screen-chart.png %}

### Extensions to the **[Document](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-document-interface)** Interface

{% asset_img document.png %}

### Extensions to the **[Element](https://www.w3.org/TR/cssom-view-1/#extension-to-the-element-interface)** Interface

{% asset_img element.png %}

{% asset_img element-chart.png %}

{% asset_img scrollheight.png %}

### Extensions to the **[HTMLElement](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-htmlelement-interface)** Interface

{% asset_img htmlelement.png %}

{% asset_img htmlelement-chart.png %}

### Extensions to the **[HTMLImageElement](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-htmlimageelement-interface)** Interface

{% asset_img htmlimgelement.png %}

###  Extensions to the **[Range](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-range-interface)** Interface

{% asset_img rang.png %}

### Extensions to the **[MouseEvent](https://www.w3.org/TR/cssom-view-1/#extensions-to-the-mouseevent-interface)** Interface

{% asset_img mouseevent.png %}

{% asset_img mouseevent-chart.png %}


## 参考
- [CSSOM View Module](https://www.w3.org/TR/cssom-view-1/)
- [CSSOM视图模式(CSSOM View Module)相关整理](http://www.zhangxinxu.com/wordpress/2011/09/cssom%E8%A7%86%E5%9B%BE%E6%A8%A1%E5%BC%8Fcssom-view-module%E7%9B%B8%E5%85%B3%E6%95%B4%E7%90%86%E4%B8%8E%E4%BB%8B%E7%BB%8D/)
- [W3C DOM Core](https://www.w3.org/TR/DOM-Level-2-Core/core.html#ID-87CD092)
- [UIEvent](https://developer.mozilla.org/zh-CN/docs/Web/API/UIEvent)
- [一张图彻底掌握scrollTop, offsetTop, scrollLeft, offsetLeft......](https://github.com/pramper/Blog/issues/10)
- [MDN:HTMLElement.offsetParent](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/offsetParent)
- [深入理解定位父级offsetParent及偏移大小](http://www.cnblogs.com/xiaohuochai/p/5828369.html)
- [offsetParent算法分析](http://www.cnblogs.com/rubylouvre/archive/2012/10/30/2746751.html)