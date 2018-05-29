```js
function $$ (selector, context){
    context = context || document
    var elements = context.querySelectorAll(selector)
    return Array.prototype.slice.call(elements)
}
```

w3c公开邮件： http://lists.w3.org/Archives/Public/www-style
w3c会以记录： http://irc.w3.org/

# 规范的阶段（生命周期）：
- 编辑草案（ ED）
- 首个公开工作草案（ FPWD）
- 工作草案（ WD）
- 候选推荐规范（ CR）
- 提名推荐规范（ PR）
- 正式推荐规范（ REC）

# css3的模块

那些延续 CSS 2.1 已有特性的模块
会升级到 3 这个版本号
 - CSS 语法（ http://w3.org/TR/css-syntax-3）
 - CSS 层叠与继承（ http://w3.org/TR/css-cascade-3）
 - CSS 颜色（ http://w3.org/TR/css3-color）
 - 选择符（ http://w3.org/TR/selectors）
 - CSS 背景与边框（ http://w3.org/TR/css3-background）
 - CSS 值与单位（ http://w3.org/TR/css-values-3）
 - CSS 文本排版（ http://w3.org/TR/css-text-3）
 - CSS 文本装饰效果（ http://w3.org/TR/css-text-decor-3）
 - CSS 字体（ http://w3.org/TR/css3-fonts）
 - CSS 基本 UI 特性（ http://w3.org/TR/css3-ui）
此外， 如果某个模块是前所未有的新概念， 那它的版本号将从 1 开始。
比如下面这些：
 - CSS 变形（ http://w3.org/TR/css-transforms-1）
 - 图像混合效果（ http://w3.org/TR/compositing-1）
 - 滤镜效果（ http://w3.org/TR/filter-effects-1）
 - CSS 遮罩（ http://w3.org/TR/css-masking-1）
 - CSS 伸缩盒布局（ http://w3.org/TR/css-flexbox-1）
 - CSS 网格布局（ http://w3.org/TR/css-grid-1）
