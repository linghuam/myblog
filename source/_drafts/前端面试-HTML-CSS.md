---
title: 前端面试-HTML&CSS
comments: true
date: 2018-01-30 23:36:58
tags:
  - html
  - css
categories:
  - 前端面试
---

## HTML & CSS
<!-- more -->

### css常用布局？

- 流动模型

  默认布局方式。典型特征是块状元素上下分布，行内元素左右分布。

- 浮动模型

  float：none | left | right

  clear: left | right | both | none

  元素默认不能浮动，设置 float 使其浮动。

  浮动元素的包含块是其最近的块级祖先元素，浮动元素会生成一个块级框，即使它是行内元素。

  浮动元素的边界不能超出包含块。左右不能互超。

  行内框与一个浮动元素重叠时，其边框、背景和内容都在该浮动元素‘之上’显示；

  块框与一个浮动元素重叠时，其边框和背景在该浮动元素'之下'显示，而内容在浮动元素之上显示。

  虽然从正常文档流中删除了，但还是会影响布局，其周围元素会环绕，并且外边距不能合并。

- 定位模型（层模型）

  position: static | relative | absolute | fixed | sticky

- flex

   **容器属性：**

   两轴：水平主轴 和 垂直交叉轴

   flex-direction: 决定轴向。四种：水平左端、水平右端、垂直上沿、垂直下沿；

   flex-wrap: 元素默认按一个轴排列，规定元素排不下时的方向。三种：不换行、换行第一行上、换行第一行下；

   flex-flow: flex-direction 和 flex-wrap 简写形式

   justify-content: 定义项目在水平轴对齐方向。 五种：左、右、居中、两端、均匀分布。

   align-itmes: 定义项目在垂直轴对齐方向。五种：上、中、下、第一行文字基线、占满。

   align-content: 定义了多根轴线的对齐方式。六种：交叉轴起点、交叉轴终点、交叉中中点、两端、均匀、占满。

   **元素属性：**

   order：定义排列顺序， 取值0，1，2...越小越靠前；

   flex-grow: 定义元素放大比例，取值0，1，2...有剩余空间时，0表示不放大；

   flex-shrink: 定义元素缩小比例，取值1，0, 2...空间不足时如何缩小；

   flex-basis: 在分配多余空间之前，项目占据的主轴空间。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间；

   flex: flex-grow、flex-shrink、flex-basis简写；

   align-self: 定义与其他元素不一样的对齐方式，可覆盖 align-items属性。

   参考1：http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html

   参考2：http://www.ruanyifeng.com/blog/2015/07/flex-examples.html

- grid

  flex是一个维度的，而grid是两个维度的网格式布局。

- 常用布局：三行布局（max-width自适应）；两栏布局（一边定宽，一边自适应）；三栏布局（圣杯、双飞翼）

- 圣杯与双飞翼区别：

   - 圣杯采用的是padding，而双飞翼采用的margin，解决了圣杯布局main的最小宽度不能小于左侧栏的缺点。
   - 双飞翼布局不用设置相对布局，以及对应的left和right值。
   - 通过引入相对布局，可以实现三栏布局的各种组合，例如对右侧栏设置position: relative; left: 190px; ,可以实现sub+extra+main的布局。

### css盒模型？

**定义：**content + padding + border + margin

**怪异盒模型：**IE, 即： width = content + padding + border；（IE6一下或IE7、8的怪异模式）

**标准盒模型：**即： width = content；

**box-sizing属性: **设置 `box-sizing: content-box | border-box` 统一盒模型种类；

**外边距合并：** 普通文档流块级框的垂直外边距会合并，行内、浮动、绝对定位元素之间的外边距不合并。设置 `*{padding:0;margin:0;}` 清除默认值；

**margin越界：**（第一个子元素的margin-top和最后一个子元素margin-bottom的值加在父元素上）应该给父元素加前置内容。

**盒模型画三角形：**
```css
{width:0;height:0;border:100px solid transparent;border-top:100px solid red;}
```

### css 居中？

- 水平居中

  子元素为行内元素：`text-align:center`；

  定宽块级元素：`margin:0 auto`；

  多个块级元素：`display:inline-block;` 或 `display:flex;`

- 垂直居中

  行内元素(要求父元素定高)：`padding-top = padding-bottom`
  或 `line-height: ***`
  或 `display:table-cell;vertical-align:middle`
  或 `display:flex;justify-content:center;flex-direction:colum;`

  行内元素(父元素不定高)：设置伪元素的高等于父容器的高，然后添加 `vertical-align:middle`

  块级元素（已知高度，父元素相对定位）：`position:absolute;height:100px;top:50%;margin-top:-50px;`

  块级元素（未知高度，父元素相对定位）：`position:absolute;top:50%;transform:translateY(-50%);`
   或 `display:flex;flex-direction:colum;justify-content:center;`

- 水平且垂直

  宽高固定：`width:300px;height:100px;padding:20px;position:absolute;top:50%;left:50%;margin: -70px 0 0 -170px`

  高宽不固定：`position:absolute;top:50%;left:50%;transform:translate(-50%, -50%);`
    或 `display:flex;justify-content:center;align-items:center;`

### CSS 选择器优先级怎么计算？
css 优先级由高到低顺序：!important > 内联样式 > id选择器 > 类 > 标签|属性|伪类 > *。

精确的计算是根据**特殊性值**来计算的，如果特殊性值相同，那么后定义的覆盖前面的。

内联、id、class、标签 赋予的权重分别是 1000、100、10、1，根据权重取舍元素css属性。

### css 动画的理解？

**transition**过渡是通过初始和结束两个状态的平滑过渡来实现简单动画。
包含四个属性：参与过渡的属性、持续时间、动画类型、延迟时间。

**animation**通过关键帧来实现更为复杂的动画。
包含属性：动画名、持续时间、过渡类型、延迟时间、循环、反向。


### css 动画 与 js 动画的比较？

webkit 内核浏览器的渲染线程分为主线程和 compositor 线程，js动画在主线程中完成，而css动画在修改以下属性时`仅触发composite，不触发layout、repaint`，这些属性有：`transform、
opacity、perspective`。

jQuery动画慢的原因：1、布局颠簸，复杂操作导致过多的重绘和重排；2、消耗内存，阻碍线程。

CSS3动画好的原因：1、优化DOM操作；2、开启3D加速，但会消耗内存。

总之：js动画灵活兼容性好，css动画则简单、某些情况下性能好，但缺乏灵活性和兼容性。

requestAnimationFrame：会把每一帧中的所有DOM操作集中起来，在一次重绘或重排中完成，并且时间间隔紧随浏览器的刷新频率，每秒60帧。在隐藏或不可见元素中，requestAnimationFrame将不会进行重绘或重排。
setTimeout 存在时间不准确和丢帧问题。

### BFC?

css中盒模型布局的css渲染模式。布局方式属于常规文档流。
元素对其；外边距折叠；包含浮动；防止文字环绕；多列布局。


### px/em/rem 的区别?

  都是相对长度。

  px 相对屏幕分辨率而言；

  em 值不固定，会继承父级元素的字体大小；

  rem 相对的只是HTML根元素大小。

### css 预处理器？ // TODO...
sass、less、postcss

### link 和 @import 区别？

- link 是 html 标签，@import 是 css 提供；

- link 在页面加载时加载，@import 引用的 css 会在页面加载完才开始加载；

- link 优先级高于 @import；

- @import 兼容性不好 IE5以上；

### position的值？应用场景？
- static: 默认，正常文档流。top、right、left、bottom、z-index属性无效。
- relative: 相对布局，相对自身正常位置，自身位置仍然保留。
- absolute: 绝对布局，相对于第一个包含块（position不为static），脱离文档流，自身位置不保留，形成新层。
- fixed: 固定布局，相对于视口坐标，脱离文档流，自身位置不保留，不随滚动条改变位置。
- sticky: 粘性定位，正常情况下按照正常文档流定位。当滚动到该元素的位置时，元素的定位（相对于包含块）发生改变。

### css选择器？可以继承的属性？优先级算法？css3新增伪类元素？

**选择器：**id、class、标签、相邻（h1 + p）、子选择器(ul > li)、后代、通配符、属性、伪类；

**可继承：**font-size font-family color ul li dl dd dt；

**不可继承：**border padding margin width height；

**优先级：** !important > id > 类 > 其他； 内联样式大于css文件样式；文件后面样式大于前面样式；

### doctype 作用？严格模式与混杂模式？

 **doctype** 声明在文档最前面，告知浏览器用什么文档类型和规范来解析这个文档；

 **严格模式**是以浏览器支持的最高规格和标准来运行；

 **混杂模式**是以向后兼容方式呈现；

 doctype不存在或格式不正确会导致浏览器以混杂模式呈现。

### 行内元素？块级元素？空元素？

css 规范规定，每个元素都 `display` 属性，确定该元素类型，每个元素都有默认的 display 值，如 div 默认是 block 为块级元素，span 默认 inline 为行内元素。

**块级元素：**独占一行；可以设置 width,height, margin, padding, border;

**行内元素：**和其他元素在同一行；不能设置宽高，可以设置 margin-left 、 margin-right，不能设置 margin-top,margin-bottom；

**行内元素有：**a b span img input select strong

**块级元素有：**div p ul ol li h1 h2 h3 h4 dl dt p

**空元素（替换元素）：**img input link meta  少见的：area base col ...

### iframe缺点？

- 阻塞主页面的 onload 事件。

- iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以影响页面并行加载。

- 如果需要使用 iframe，最好用 js 动态给其加 src 属性。
