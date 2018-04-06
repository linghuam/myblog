---
title: js-浅拷贝与深拷贝
comments: true
date: 2018-01-30 17:43:31
tags:
  - javascript
categories:
  - javascript
---

js 中经常用到对象的浅拷贝与深拷贝。下面来对它们作一个探讨。
<!-- more -->

## 什么是拷贝？浅拷贝与深拷贝的区别是什么？

拷贝就是生成对象的一个一模一样的副本，就像文件的复制一样。JavaScript 中的拷贝就是生成跟原对象一模一样的对象。
JavaScript 中的数据类型分为**简单类型**（boolean, string, number, undefined, null）
和**复杂类型**（Function、Array、Object）。简单类型是按值存储的，复杂类型是按引用存储的。

浅拷贝与深拷贝对简单类型的处理是一致的，但对复杂类型有区别，**浅拷贝只拷贝复杂类型的引用**，
拷贝后的对象跟原对象引用同一块内存空间。
**深拷贝则对拷贝的对象重新分配存储空间**，拷贝后的对象跟原对象引用不同的内存空间。


## 浅拷贝实现方法

### Object.assign

```js
Object.assign(target, ...sources);
```

Object.assign 将源对象**自身的**且**可枚举**的属性拷贝到 target。

Object.assign 使用源对象的的`[[get]]`和目标对象的`[[set]]`方式进行拷贝，这意味着
它会触发属性的 getters 和 setters。所以拷贝 get 描述的属性时需只会拷贝值，不会拷贝定义。
通过`Object.getOwnPropertyDescriptor()` 和 `Object.defineProperty()` 来解决。

更多 Object.assign 请参考： https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign

### 简单复制语句

```js
function simpleClone(sourceObj){
  var obj = {};
  for (var i in sourceObj){
    obj[i] = sourceObj[i];
  }
  return obj;
}
```

## 深拷贝实现方法

### 利用 JSON 内置对象

```js
function deepClone (obj){
  return JSON.parse(JSON.stringify(obj));
}
```

**优缺点：**
1. 他无法实现对函数 、RegExp等特殊对象的克隆
2. 会抛弃对象的constructor,所有的构造函数会指向Object
3. 对象有循环引用,会报错

### 递归拷贝

```js
function deepClone (targetObj, srcObj){
  var obj = targetObj || {};
  for (var i in srcObj){
    var prop = srcObj[i];
    // 避免相互引用对象导致死循环
    if(obj === prop){
      continue;
    }
    if (typeof prop === 'object'){
      obj[i] = (prop.constructor === Array) ? [] : {};
      deepClone(obj[i], prop);
    } else {
      obj[i] = prop;
    }
  }
  return obj;
}
```

// 深克隆还有很多坑待解决，上面的还不够 TODO...
