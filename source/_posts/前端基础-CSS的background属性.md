---
title: 前端基础-CSS的background属性
comments: true
date: 2018-05-25 01:25:44
tags:
categories:
- 前端基础
- CSS
---

每一个 HTML 元素都默认有一个透明（background:transparent）的背景层。background 属性指定元素的背景色和背景图片，以及它们的大小、位置、重复性等。

background 属性是 **非继承** 属性。但是元素的背景默认穿透，因为 `background-color` 的默认值为 `transparent`。

<!--more-->

## 对 W3C 标准的总结和概括

### 多个背景图像的分层

在 **CSS3** 中，一个盒子的背景被分为多个层，分层数取决于 `background-image` 属性值中逗号分隔值的多少。值得注意的是 **none 值也会创建一个层**。

值列表的匹配规则是：
1. 从第一个值开始匹配
2. 超出个数的值被忽略
3. 不足个数的值由前面的值重复补充

**Example1**

对于如下声明:

```css
background-image: url(1.png), url(2.png), url(3.png);
background-position: center center, 20% 80%, top left, bottom right;
background-origin: border-box, content-box;
background-repeat: no-repeat;
```

我们注意到 `background-image` 属性指定了三张图片，首先这三张图片会创建三个层，并且按 **从左到右** 的声明顺序 **从上到下** 依次创建三个层。

其次，根据上文匹配规则，其他属性值列表将分别匹配这三张图片，多删少补。 即背景 `url(1.png)` 将对应 `center center; border-box; no-repeat`，以此类推。

我们注意到 background-position 属性由逗号分隔的值有四个，而背景图片只有三个，因此最后一个值 `bottom right` 无效。
同理，background-origin、background-repeat 的值不足三个，因此要根据前面的值进行补充。

其最终效果等效于:

```css
background-image: url(1.png), url(2.png), url(3.png);
background-position: center center, 20% 80%, top left; /**bttom right **/
background-origin: border-box, content-box, **border-box**;
background-repeat: no-repeat, **no-repeat**, **no-repeat**;
```

第一张图片被渲染在最上层，后面的渲染在下一层，以此类推。并且 `background-color` 层在所有其他层之下。

**注意：** `border-image` 属性定义的图像在背景之上。


### 底色： `background-color` 属性

* 可取值：[color](https://www.w3.org/TR/css3-color/#valuea-def-color) | transparent | inherit
* 默认值：transparent
* 适用性：所有元素
* 继承性：无
* 百分比值：无
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：规定值
* 是否支持动画：是

这个属性设置元素的背景色。背景色绘制在背景图片之下。

背景色会被 `background-clip` 值裁剪。

**例子：**
```css
h1 { background-color: #F00 } /* 设置背景色为红色 */
```

### 图片源：`background-image` 属性

* 可取值：uri | none | inherit
* 默认值：none
* 适用性：所有元素
* 继承性：无
* 百分比值：无
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：绝对路径值 或 none
* 是否支持动画：否

该属性设置元素的背景图片集，多个声明以逗号隔开，背景图片从第一张起 **从上往下** 依次渲染。

**注意：** 
1. 值为 none 或无法加载或格式不支持的图片都将不会被渲染。
2. 当设置 background-image 时务必设置 background-color 以在图片不可用时作为备用。
3. 从 **可访问性** 的角度来说，背景图片只起装饰作用，不应用来传递重要信息。
4. 可避免下载不可见的图片以优化 web 性能。

**例子：**
```css
body { background-image: url(marble.svg) }
p { background-image: none }
div { background-image: url(1.png) url(2.png) }
```

### 重复图片：`background-repeat` 属性

* 可取值：repeat | repeat-x | repeat-y | no-repeat | space | round | inherit
* 默认值：repeat
* 适用性：所有元素
* 继承性：无
* 百分比值：无
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：一个列表，每个条目包含了两个关键字
* 可动画：否

`repeat-x` 计算值为：`repeat no-repeat`

`repeat-y` 计算值为：`no-repeat repeat`

`repeat` 计算值为：`repeat repeat`

`space` 计算值为：`space space`

`round` 计算值为：`round round`

`no-repeat` 计算值为：`no-repeat no-repeat`

若 background-repeat 有两个值，第一表示横向重复，第二个表示纵向重复。

`space`值的含义是：图像会尽可能的重复，但不会被裁剪，第一个和最后一个图像会被固定在元素的相应边上，同时空白会均匀分布在图像之间。

`round`值的含义是：图像会缩放以适应当前尺寸，并且图像之间没有空隙。


```css
body {
    background: white url("pendant.png");
    background-repeat: repeat-y;
    background-position: center;
}
```

### 附着图像：`background-attachment` 属性

* 可取值：scroll | fixed | local | inherit
* 默认值：scroll
* 适用性：所有元素
* 继承性：无
* 百分比值：无
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：特定值
* 可动画：否

当指定了 background-image 时，此属性指定当元素滚动时，图像是随着元素滚动还是相对于视口固定。

当值为 fixed 时，图像摆放位置相对于视口坐标

// 创建一个竖直方向无限滚动的背景
```css
body {
    background: red url("pendant.png");
    background-repeat: repeat-y;
    background-attachment: fixed;
}
```

// 不支持‘fixed’的浏览器
```css
body {
   /* For all UAs: */
   background: white url(paper.png) scroll;
   /* For UAs that do fixed backgrounds: */
   background: white url(ledger.png) fixed;
}
h1 {
   /* For all UAs: */
   background: silver;
   /* For UAs that do fixed backgrounds: */
   background: url(stripe.png) fixed, white url(ledger.png) fixed;
}
```

### 定位图像：`background-position` 属性

* 可取值：[ [ <percentage> | <length> | left | center | right ] [ <percentage> | <length> | top | center | bottom ]? ] | [ [ left | center | right ] || [ top | center | bottom ] ] | inherit
* 默认值：0% 0%
* 适用性：所有元素
* 继承性：无
* 百分比值：相对于自身包围盒
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：列表

当指定了 background-image 时，此属性指定它的初始位置。

如果只指定了一个值，第二个值默认为 ‘center’

如果值不为关键字，第一个值表示横向位置，第二个值表示纵向位置。

负的百分比和长度值是被接受的。

位置计算的标准包围盒是 `padding-box`。

如果 background-attachment 的值为 fixed，则 backgroun-position 相对于视口而不是元素的 padding-box 盒。

```css
The following declarations give the stated (horizontal, vertical) offsets from the top left corner:

background-position: left 10px top 15px;   /* 10px, 15px */
background-position: left      top     ;   /*  0px,  0px */
background-position:      10px     15px;   /* 10px, 15px */
background-position: left          15px;   /*  0px, 15px */
background-position:      10px top     ;   /* 10px,  0px */
background-position: left      top 15px;   /*  0px, 15px */
background-position: left 10px top     ;   /* 10px,  0px */
```
{% asset_img 1.png %}

`<percentage>`
A percentage for the horizontal offset is relative to (width of background positioning area - width of background image). A percentage for the vertical offset is relative to (height of background positioning area - height of background image), where the size of the image is the size given by background-size.

`<length>`
A length value gives a fixed length as the offset. For example, with a value pair of 2cm 1cm, the upper left corner of the image is placed 2cm to the right and 1cm below the upper left corner of the background positioning area.

`top`
Computes to 0% for the vertical position if one or two values are given, otherwise specifies the top edge as the origin for the next offset.

`right`
Computes to 100% for the horizontal position if one or two values are given, otherwise specifies the right edge as the origin for the next offset.

`bottom`
Computes to 100% for the vertical position if one or two values are given, otherwise specifies the bottom edge as the origin for the next offset.

`left`
Computes to 0% for the horizontal position if one or two values are given, otherwise specifies the left edge as the origin for the next offset.

`center`
Computes to 50% (left 50%) for the horizontal position if the horizontal position is not otherwise specified, or 50% (top 50%) for the vertical position if it is.

### 绘制区域：`background-clip` 属性
* 可取值：padding-box | border-box | content-box | inherit
* 默认值：border-box
* 适用性：所有元素
* 继承性：无
* 百分比值：无
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：规定值

Determines the **background painting area**, which determines the area within which the background is painted.


### 定位区域：`background-origin` 属性

* 可取值：padding-box | border-box | content-box | inherit
* 默认值：padding-box
* 适用性：所有元素
* 继承性：无
* 百分比值：无
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：规定值

For elements rendered as a single box, specifies the **background positioning area**.

### 图片尺寸：`background-size` 属性

* 可取值：[ <length-percentage> | auto ]{1,2} | cover | contain
* 默认值：auto
* 适用性：所有元素
* 继承性：无
* 百分比值：see text
* 媒体：[visual](https://www.w3.org/TR/CSS2/media.html#visual-media-group)
* 计算值：规定值

`contain`
Scale the image, while preserving its intrinsic aspect ratio (if any), to the **largest size** such that both its width and its height can **fit inside** the background positioning area.

`cover`
Scale the image, while preserving its intrinsic aspect ratio (if any), to the **smallest size** such that both its width and its height can **completely cover** the background positioning area.

`[<length-percentage> | auto]{1,2}`
The first value gives the width of the corresponding image, the second value its height. If only one value is given the second is assumed to be auto.

A **percentage** is relative to the background positioning area.

An **auto value** for one dimension is resolved by using the image’s intrinsic ratio and the size of the other dimension, or failing that, using the image’s intrinsic size, or failing that, treating it as 100%.

If both values are auto then the intrinsic width and/or height of the image should be used, if any, the missing dimension (if any) behaving as auto as described above. If the image has neither an intrinsic width nor an intrinsic height, its size is determined as for contain.

Negative values are not allowed.


## 参考文档
- [w3c](https://www.w3.org/TR/css-backgrounds-3/#backgrounds)
- [w3school](http://www.w3school.com.cn/cssref/pr_background.asp)
- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/background)
- [css-tricks](https://css-tricks.com/almanac/properties/b/background/)
- [CSS3 Backgrounds相关介绍](https://www.zhangxinxu.com/wordpress/2011/05/%E7%BF%BB%E8%AF%91-css3-backgrounds%E7%9B%B8%E5%85%B3%E4%BB%8B%E7%BB%8D/)
- [《CSS揭秘》第2章](https://book.douban.com/subject/26745943/)
