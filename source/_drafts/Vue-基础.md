---
title: Vue-基础
comments: true
date: 2020-07-06 19:06:07
tags:
- vue.js
categories:
- 专题
- Vue
---

对 [vue.js文档](https://cn.vuejs.org/v2/guide/) 的一些总结和剖析。

<!--more-->

## 基础

### 兼容性

原文引用：
> Vue 不支持 IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的 ECMAScript 5 特性。但它支持所有兼容 ECMAScript 5 的浏览器。

原因分析：
vue 利用 `Object.defineProperty` 来监测对象变化，而该接口 IE8 不支持。

### 介绍

[三个框架对比](https://cn.vuejs.org/v2/guide/comparison.html)

### Vue 实例

每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的：

```js
var vm = new Vue({
  // 选项
})
```

### 生命周期

![](lifecycle.png)

## API 剖析（链接源码）

### 全局配置

Vue.config 是一个对象，包含 Vue 的全局配置。可以在启动应用之前修改下列 property：

源码：https://github.com/vuejs/vue/blob/dev/src/core/config.js

#### silent

取消 Vue 所有的日志与警告。

#### optionMergeStrategies

自定义合并策略的选项。

#### 