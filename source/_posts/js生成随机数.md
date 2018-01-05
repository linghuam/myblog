---
title: js生成随机数
comments: true
date: 2018-01-05 14:49:07
tags:
  - javascript
categories:
  - javascript
---

在 javascript 中，想要得到一个随机数，通常使用 `Math.random()` 函数，它将得到一个从0到1（包含0不包含1）之间的一个浮点数。
然而随机数的使用并不像这么简单，下面一起来探讨一下js中的随机数。

<!-- more -->

## `Math.random()`生成特定范围内的随机数

* 生成0-1随机小数【0<= r < 1】
```js
function getRandom() {
  return Math.random();
}
```

* 生成一定范围的随机数【min<= r < max】
```js
function getRandomArbitrary(min, max) {
  return Math.floor(Math.random() * (max - min)) + min;
}
```

* 生成一定范围的随机整数【min<= r < max】
```js
function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min)) + min;
}
```

* 生成包含最大最小值的随机整数【min <= r <= max】
```js
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

## window.crypto.getRandomValues API

`Math.random()`只是用来创建一个随机数字，但是用它来生成随机安全密码是不行的。

如果要实现这种功能，可以使用getRandomValues API。

**首先**创建一个typedArray数组用来存储随机结果，数组的元素类型可以是`Int8Array`,`Uint8Array`,
`Int16Array`,`Uint16Array`,`Int32Array`,`Uint32Array`。

```js
var array = new Uint32Array(10); //表示创建一个长度为10的无符号32位整型数组
```

**然后**调用API，填充随机数值。

```js
window.cryto.getRandomValues(array);
```

## 参考文档
* MDN-Math.random()：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random
* MDN-getRandomValues：https://developer.mozilla.org/en-US/docs/Web/API/RandomSource/getRandomValues
* JavaScript中的随机数：https://www.w3cplus.com/javascript/rounding-recipes.html
