---
title: 前端基础-js数组indexOf方法
comments: true
date: 2018-03-22 15:14:26
tags:
categories:
- 前端基础
- JavaScript
---

每日的基础学习笔记，不求大而全，追求精致和短小，主要从底层技术基础开始，记录一些核心概念、实践应用和原理方法，帮助自己理解前端基础，建立前端知识体系。多问几个**为什么、怎么做**
<!-- more -->

### 数组 indexOf 方法？

#### 定义
```js
arr.indexOf(searchElement,[fromIndex]);
```

#### 参数
- searchElement：被搜索的对象，执行严格比较`===`
- fromIndex：开始搜索的索引
  * 如果没指定，索引为0
  * 如果大于或等于数组长度，直接返回 -1
  * 如果小于0，则从数组尾部开始的第 N 个位置开始索引，但搜索顺序仍然从左至右

#### 返回值
返回找到的第一个元素的索引，若未找到则返回-1


### polyfill

版本1：自己实现

```js
if(!Array.prototype.indexOf){
  Array.prototype.indexOf = function (searchElement, fromIndex){
    if (this == null){
      throw new TypeError('"this" is null or not defined');
    }
    var index = fromIndex,
        len = this.length,
        i;
    if (fromIndex === undefined) index = 0;
    if (fromIndex >= len) return -1;
    if (fromIndex < 0) index = Math.max(len + fromIndex, 0);
    for ( i = index; i < len; i++){
      if (this[i] === searchElement) return i;
    }
    return -1;
  }
}
```

版本2：MDN

```js
if(!Array.prototype.indexOf){
  Array.prototype.indexOf = function (searchElement, fromIndex){
    // 严格模式和非严格模式下this指向不同，严格模式 this 没定义时报错，非严格模式 this 没定义时指向 window 对象
    if (this == null){
       throw new TypeError("Array.prototype.indexOf() - can't convert `" + this + "` to object");
    }
    var index = isFinite(fromIndex) ? Math.floor(fromIndex) : 0,
        that = this instanceOf Object ? this : new Object(this),
        len = isFinite(that.length) ? Math.floor(that.length) : 0;
     if (index >= len) return -1;
     if (index < 0 ) index = Math.max(len + index, 0);
     // 区分 index 不存在时 或 index 存在但值为 undefined 时，that[index] 取值都为 undefined 情况
     if (searchElement === undefined){
        do{
          if (index in that && that[index] === undefined){
            return index;
          }
        }while(++index < len);
     } else {
       do{
         if (that[index] === searchElement){
           return index;
         }
       } while(++index < len);
     }
     return -1;
  }
}
```

版本3：MDN

```js
// Production steps of ECMA-262, Edition 5, 15.4.4.14
// Reference: http://es5.github.io/#x15.4.4.14
if (!Array.prototype.indexOf) {
  Array.prototype.indexOf = function(searchElement, fromIndex) {

    var k;

    // 1. Let o be the result of calling ToObject passing
    //    the this value as the argument.
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    var o = Object(this);

    // 2. Let lenValue be the result of calling the Get
    //    internal method of o with the argument "length".
    // 3. Let len be ToUint32(lenValue).
    var len = o.length >>> 0;

    // 4. If len is 0, return -1.
    if (len === 0) {
      return -1;
    }

    // 5. If argument fromIndex was passed let n be
    //    ToInteger(fromIndex); else let n be 0.
    var n = fromIndex | 0;

    // 6. If n >= len, return -1.
    if (n >= len) {
      return -1;
    }

    // 7. If n >= 0, then Let k be n.
    // 8. Else, n<0, Let k be len - abs(n).
    //    If k is less than 0, then let k be 0.
    k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

    // 9. Repeat, while k < len
    while (k < len) {
      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the
      //    HasProperty internal method of o with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      //    i.  Let elementK be the result of calling the Get
      //        internal method of o with the argument ToString(k).
      //   ii.  Let same be the result of applying the
      //        Strict Equality Comparison Algorithm to
      //        searchElement and elementK.
      //  iii.  If same is true, return k.
      if (k in o && o[k] === searchElement) {
        return k;
      }
      k++;
    }
    return -1;
  };
}
```

### 参考文档
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf
