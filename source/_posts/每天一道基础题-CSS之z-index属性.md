---
title: 每天一道基础题-CSS之z-index属性
comments: true
date: 2018-05-21 21:52:59
tags:
  - css
categories:
  - 每天一道基础题
---

最近在做 Vue 项目时，使用 ElementUI 做页面的 UI 框架，但是在写页面的过程中出现很多奇怪的现象，调试发现一个原因是 ElementUI 框架改变了很多默认的样式，第二个原因是自己页面的 z-index 和 position 使用不恰当，遂决定要彻底弄懂一些 CSS 方面的问题，毕竟前端 CSS 是重要的一环，不能似懂非懂。
<!-- more -->

## 我遇到的问题?

1. 当  #home 的 `position:fixed` 时
<p data-height="265" data-theme-id="dark" data-slug-hash="xjMNBB" data-default-tab="css,result" data-user="linghuam" data-embed-version="2" data-pen-title="z-index2" class="codepen">See the Pen <a href="https://codepen.io/linghuam/pen/xjMNBB/">z-index2</a> by linghuam (<a href="https://codepen.io/linghuam">@linghuam</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

2. 当 #home 的 `position:static/absolute/relative` 时
<p data-height="265" data-theme-id="dark" data-slug-hash="xjMNra" data-default-tab="css,result" data-user="linghuam" data-embed-version="2" data-pen-title="z-index" class="codepen">See the Pen <a href="https://codepen.io/linghuam/pen/xjMNra/">z-index</a> by linghuam (<a href="https://codepen.io/linghuam">@linghuam</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## 问题？
- z-index 值越大的元素一定越靠上吗？
- 为什么不同的 position 值会影响层叠顺序？

## 开始找资料了解 z-index 属性，下面是对一些官方文档和技术大牛博客的总结

`z-index属性`指定两件事：
1. 规定**层叠顺序**
2. 创建**层叠上下文**

**注：**z-index 只在定位元素（position 不为 static 默认值）上起作用

`z-index`取值：
1. auto (默认值，不会创建层叠上下文，层叠顺序与父元素一致)
2. 负数、零、正数（整数）
3. inherit （全局）
4. initial （全局）
5. unset （全局）

### 层叠顺序（Stacking Order）
{% asset_img 01.png %}

### 层叠上下文（Stacking Contexts）
- 每个层叠上下文对应一个根级元素，html 元素是根级层叠上下文
- 层叠上下文的**创建**有三种方式
  1. 文档的根元素（如 html 元素）
  2. 元素的 position 属性值不为 static **且** z-index 值不为 auto （position:relative; z-index:auto;不会创建）
  3. 元素的 opacity 值小于 1
  4. position 值为 fixed 的元素 （**我遇到的问题的答案**）
- 一些其他的 CSS 属性也会创建层叠上下文，如 __transforms__,__filters__,__css-regions__,__paged media__等等。
- 一个通用的规则是：**需要脱离画面外渲染的元素都会创建层叠上下文**

### 同一个层叠上下文元素的层叠顺序（从后往前，从底往上）
- 根元素
- z-index 为负值的定位元素
- 非定位元素（根据在 HTML 中的出现顺序排列）
- z-index 为 auto 的 定位元素
- z-index 为 正值的 定位元素

### 原话引用
> 1. z-index only works on positioned(fixed/relative/absolute but not static) elements
> 2. z-index values can create stacking contexts
> 3. Every stacking context has a single HTML element as its root element

## z-index 最佳实践
1. **谁大谁上：** 同一层叠上下文中，z-index 大者居上
2. **后来居上：** 层叠水平一致、层叠顺序相同的时候，在DOM流中处于后面的元素会覆盖前面的元素

> 1. IE6/IE7浏览器有个bug，就是z-index:auto的定位元素也会创建层叠上下文
> 2. 在过去，position:fixed和relative/absolute在层叠上下文这一块是一路货色，都是需要z-index为数值才行。但是，不知道什么时候起，Chrome等webkit内核浏览器，position:fixed元素天然层叠上下文元素，无需z-index为数值。根据我的测试，目前，IE以及FireFox仍是老套路。

## 例子
### 不改变 html 结构，不改变 z-index 属性，不改变 position 属性的情况下，将红色框置于最底层？
<p data-height="265" data-theme-id="dark" data-slug-hash="WJPqmY" data-default-tab="css,result" data-user="linghuam" data-embed-version="2" data-pen-title="Stacking Order (problem)" class="codepen">See the Pen <a href="https://codepen.io/linghuam/pen/WJPqmY/">Stacking Order (problem)</a> by linghuam (<a href="https://codepen.io/linghuam">@linghuam</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

答案，添加:

```css
/* opacity 小于1 */
div:first-child{
    opacity: 0.99
}
```

## 参考文章
- [深入理解CSS中的层叠上下文和层叠顺序](http://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/)
- [What You May Not Know About the Z-Index Property](https://webdesign.tutsplus.com/articles/what-you-may-not-know-about-the-z-index-property--webdesign-16892?ec_unit=translation-info-language)
- [上篇中文版](https://webdesign.tutsplus.com/zh-hans/articles/what-you-may-not-know-about-the-z-index-property--webdesign-16892)
- [What No One Told You About Z-Index](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)
- [css-tricks z-index](https://css-tricks.com/almanac/properties/z/z-index/)