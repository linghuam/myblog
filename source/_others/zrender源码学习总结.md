---
title: zrender源码学习总结
comments: true
date: 2018-02-06 15:13:24
tags:
  - zrender
categories:
  - 可视化
---

## MVC
- M：Storage
- V：Painter
- C：Handler

## 动画

zrender使用的动画库：https://github.com/tweenjs/tween.js

## retina优化 ？？？？
加入retina屏幕的优化：https://github.com/ecomfe/zrender/commit/ba4e11a8b4f9ecff3773a15c6f18c3c1caa21f31


## 文本换行支持
https://github.com/ecomfe/zrender/commit/2a220b77616b4658abb9958520544670e7807b5e

## 修复不设置lineWidth或lineWidth为0时stroke依然默认1像素的问题
https://github.com/ecomfe/zrender/commit/92fd40702036fe9d636a201a63d65fa39b8bb117

##  先fill再stroke

https://github.com/ecomfe/zrender/commit/15dd4a25a079dcfda986fc2b35021607f22f9e7a

## textWidth、textHeight计算缓存
https://github.com/ecomfe/zrender/commit/d5dbe5b7743b64cd3fe01ade2625476e3d826093

## 类继承关系

【src】：
- ZRender：实体类，无继承
- Storage：实体类，无继承
- Painter：实体类，无继承
- Handler：实体类，无继承
- Layer：实体类，无继承
- Element：抽象类，继承自 Transformable、Eventful、Animatable

【src/graphic】：
- Displayable：抽象类，继承自 Element
- Path：实体类，继承自 Displayable
- graphic/shape：所有图形继承自 Path （Shape - Path - Displayable - Element）
- 
