---
title: testdraft
comments: true
categories:
- mobile
tags:
- testdraft
date: 2017-12-25 09:46:17
---


# 移动端知识

# 问题
* 为什么retina屏的图片要设计成普通屏的两倍？
* 在做移动端开发时，尺寸单位有哪些？用哪个合适？
* 移动端字体和图标设计格式和尺寸？

## 名词解释

**像素：** 一个像素就是计算机屏幕所能显示一种特定颜色的最小区域。

在web前端开发领域，像素有以下两层含义：

1、设备像素(Device independent pixels)：设备屏幕的物理像素，对于任何设备来讲物理像素的数量是固定的。

2、CSS像素(CSS pixels)：又称为逻辑像素，是为web开发者创造的。在css和JavaScript中使用的像素都是逻辑像素。

**物理分辨率(设备像素) ：** 硬件支持的分辨率。

屏幕在硬件层面划分的格网数，设备被制造出来后，物理分辨率就固定了，无法改变。

**逻辑分辨率(CSS像素) ：** 软件可以达到的分辨率。

css中设置的px像素就是逻辑分辨率，如iphone4的物理分辨率是640\*960，逻辑分辨率是 320*480px,那么 1px 就需要物理上2个格网来渲染。

**分辨率:**  一般指的是物理分辨率，指设备被划分的格网数，如 iphone8 4.7英寸版的分辨率是：1334*750。

 注：不能带px单位，px指的是逻辑分辨率。

 注：分辨率的值越大不一定代表显示越精细，显示的精细程度由ppi大小决定。
 一般经常说的分辨率高低都是在ppi和尺寸一致时才能代表屏幕精细程度。

**屏幕像素密度(PPI=DPI):** 每英寸（1英寸=2.54厘米）所包含的物理像素数。衡量屏幕精细程度的绝对标准。

**设备像素比(DPR):** 设备像素比DPR(devicePixelRatio)是默认缩放为100%的情况下，物理像素与逻辑像素的比值。

dpr = 物理像素 / 逻辑像素。（前提条件：缩放比例为1）
js获取方式：window.devicePixelRatio。

**屏幕尺寸：** 屏幕对角线的长度，单位为英寸(in)。如 iphone 屏幕有 4.7英寸 和 5.5英寸。

  屏幕尺寸 = Math.sqrt(Math.pow(devicePixelX,2) +  Math.pow(devicePixelY,2)) / ppi。

**Retina屏幕：** 所谓“Retina”是一种显示技术，可以把更多的像素点压缩至一块屏幕里，从而达到更高的分辨率并提高屏幕显示的细腻程度。由摩托罗拉公司研发。最初该技术是用于Moto Aura上。这种分辨率在正常观看距离下足以使人肉眼无法分辨其中的单独像素。也被称为视网膜显示屏。
retina屏幕在苹果设备上应用较多。在开发中retina屏指dpr为2的屏幕。

## 移动端三个视口
* 元素的宽度都是相对于父元素的，body元素的默认宽度是html元素宽度的100%，而html元素的宽度是基于视口的。
* 在PC端，视口只有一个（浏览器的可视区域，不包括菜单栏），并且视口的宽度 = 浏览器窗口的宽度。
* 布局视口：移动端CSS布局的依据视口，即CSS布局会根据布局视口来计算。
* chrome开发者工具里面表示的尺寸是理想视口大小。
* JS获取布局视口宽度和高度
```js
document.documentElement.clientWidth
document.documentElement.clientHeight
```
* 视觉视口：用户看到的网站部分。
* 理想视口：下面那段代码告诉浏览器：将布局视口的宽度设为理想视口。
```HTML
<meta name="viewport" content="width=device-width" />
```
* 总结
```
1、在PC端，布局视口就是浏览器窗口(视觉视口)
2、在移动端，视口被分为两个：布局视口、视觉视口。
3、移动端还有一个理想视口，它是布局视口的理想尺寸，即理想的布局视口。（注：理想视口的尺寸因设备和浏览器的不同而不同，但这对于我们来说无所谓）
4、可以将布局视口的宽度设为理想视口
```

## 缩放
缩放：缩小放大的是 CSS像素。

## HTML5中meta标签
meta视口标签存在的主要目的是为了让布局视口和理想视口的宽度匹配，meta视口标签应该放在HTML文档的head标签内，语法如下：
[meta文档](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta)
```HTML
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
1、width：设置布局视口的宽度，device-width：是理想视口的宽度
2、init-scale：设置页面的初始缩放程度
3、minimum-scale：设置了页面最小缩放程度
4、maximum-scale：设置了页面最大缩放程度
5、user-scalable：是否允许用户对页面进行缩放操作
上面代码的意思是，让布局视口的宽度等于理想视口的宽度，页面的初始缩放比例以及最大缩放比例都为1，且不允许用户对页面进行缩放操作。
```

## CSS3中媒体查询
媒体查询是响应式设计的基础，他有以下三点作用：
```
1、检测媒体的类型，比如 screen，tv等
2、检测布局视口的特性，比如视口的宽高分辨率等
3、特性相关查询，比如检测浏览器是否支持某某特性（这一点不讨论，因为它被目前浏览器支持的功能对于web开发来讲很无用）
```

[css中使用媒体查询的语法](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)
```
@media 媒体类型 and (视口特性阀值){
    // 满足条件的css样式代码

}
```

下面是一段在css中使用媒体查询的示例:
```
@media all and (min-width: 321px) and (max-width: 400px){
    .box{
        background: red;
    }
}
```

## 设计图PSD
* psd尺寸是按照设备像素设计的
* 将缩放值设置为【设备像素比的倒数】，那么css一个像素对应设备上一个像素。
```js
// 下面的代码最终能保证一个问题，那就是无论任何设备，布局视口的宽度总是等于设备像素。
// 问题：设备像素变了，图形大小不会变，跨设备时不能等比缩放。
var scale = 1 / window.devicePixelRatio;
document.querySelector('meta[name="viewport"]')
.setAttribute('content',
'width=device-width,initial-scale=' +
scale +
', maximum-scale=' +
scale +
', minimum-scale=' +
scale +
', user-scalable=no');
```

## rem
rem 是相对尺寸单位，相对于 **html** 标签字体大小的单位。
例：如果 html 的 font-size = 18px;那么 1rem = 18px。

### 方法一
手机淘宝的方法。
有一个缺点，就是转化rem单位的时候，需要除以font-size的值，淘宝用的是iPhone6的设计图，所以淘宝转换尺寸的时候要除以75，这个值可不好算，所以还要借用计算器来完成，影响开发效率，另外，在转还rem单位时遇到除不尽的数时我们会采用很长的近似值比如上面的2.6666667rem，这样可能会使页面元素的尺寸有偏差。
```js
// 1.将布局视口大小设为设备像素尺寸
var scale = 1 / window.devicePixelRatio;
document.querySelector('meta[name="viewport"]').setAttribute('content','width=device-width,initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
// 2.动态设置html字体大小
document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + 'px';
// 3.将设计图中的尺寸换算成rem
// 元素的rem尺寸 = 元素的psd稿测量的像素尺寸 / 动态设置的html标签的font-size值
```
html模板
```html
<html>
<head>
    <title></title>
    <meta charset="utf-8" />
    <meta name="viewport" content="" />
</head>
<body>
    <script>
    var scale = 1 / window.devicePixelRatio;
    document.querySelector('meta[name="viewport"]').setAttribute('content','width=device-width,initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');

    document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + 'px';
    </script>
</body>
</html>
```

### 方法二
网易方法。由于这种做法在开发中换算rem单位的时候只需要将测量的尺寸除以100即可，所以不需要使用计算器我们就可以很快的完成计算转换，所以这也会提升开发效率。
```js
// 1、拿到设计图，计算出页面的总宽，为了好计算，取100px的font-size，如果设计图是iPhone6的那么计算出的就是7.5rem，如果页面是iPhone5的那么计算出的结果就是6.4rem。
// 2、动态设置html标签的font-size值
 document.documentElement.style.fontSize = document.documentElement.clientWidth / 以rem为单位的页面总宽 + 'px';
//如iPhone6的设计图就是：
document.documentElement.style.fontSize = document.documentElement.clientWidth / 7.5 + 'px';
//如iPhone5的设计图就是：
document.documentElement.style.fontSize = document.documentElement.clientWidth / 6.4 + 'px';
// 3、做页面是测量设计图的px尺寸除以100得到rem尺寸。
// 4、和淘宝的做法一样，文字字体大小不要使用rem换算。
```
下面是这种做法的html模板：
```html
<html>
<head>
    <title></title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" />
</head>
<body>
    <script>
    document.documentElement.style.fontSize = document.documentElement.clientWidth / 7.5 + 'px';
    </script>
</body>
</html>
```

### 文字字体大小是不要换算成rem做单位的


## 解决方案/最佳实现
* [手淘可伸缩布局方案库](https://github.com/amfe/lib-flexible)

## 参考文档
* [手淘可伸缩布局方案库](https://github.com/amfe/lib-flexible)
* [一篇真正教会你开发移动端页面的文章(一)](http://hcysun.me/2015/10/16/%E4%B8%80%E7%AF%87%E7%9C%9F%E6%AD%A3%E6%95%99%E4%BC%9A%E4%BD%A0%E5%BC%80%E5%8F%91%E7%A7%BB%E5%8A%A8%E7%AB%AF%E9%A1%B5%E9%9D%A2%E7%9A%84%E6%96%87%E7%AB%A0(%E4%B8%80)/)
* [一篇真正教会你开发移动端页面的文章(二)](http://hcysun.me/2015/10/19/%E4%B8%80%E7%AF%87%E7%9C%9F%E6%AD%A3%E6%95%99%E4%BC%9A%E4%BD%A0%E5%BC%80%E5%8F%91%E7%A7%BB%E5%8A%A8%E7%AB%AF%E9%A1%B5%E9%9D%A2%E7%9A%84%E6%96%87%E7%AB%A0-%E4%BA%8C/)
* [使用Flexible实现手淘H5页面的终端适配](https://www.w3cplus.com/mobile/lib-flexible-for-html5-layout.html)
* [移动端页面开发资源总结](http://hcysun.me/2015/09/25/%E7%A7%BB%E5%8A%A8%E7%AB%AF%E9%A1%B5%E9%9D%A2%E5%BC%80%E5%8F%91%E8%B5%84%E6%BA%90%E6%80%BB%E7%BB%93/)
