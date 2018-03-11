---
title: vue源码分析
comments: true
date: 2018-03-05 09:26:06
tags:
  - vue
categories:
  - vue
---

### 响应式原理？
- Observer：观察者，观察数据读写操作
- Watcher：订阅者，数据变化时执行响应操作
- Dep：纽带

### Vue不支持IE8以下版本的浏览器？
因为Vue是基于 Object.defineProperty 来实现数据响应的，而 Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是为什么 Vue 不支持 IE8 以及更低版本浏览器的原因

### vue 的双向绑定机制？

### vue 计算属性与普通属性区别？

### 实现 Vue SSR（服务端渲染）？

### Vue 组件 data 为什么必须是函数？
这个其实不关Vue的事情，这是js本身的一种特性造成的。当两个实例继承同一个对象的时候么当你修改其中一个属性的时候，另外一个实例也会跟着改。

### Vue computed 实现？
https://github.com/youngwind/blog/issues/89


### diff 算法实现？

### Vue complier 实现？

### 另一种方式实现 Vue 的响应式原理？

### vuejs源码里面的类为什么没有用 ES6 的 class 来声明，而还是采用原型继承，看了其他开源库也是这样，用了ES6的其他特性，但很少用class 来声明类，这里面有什么秘密吗？
