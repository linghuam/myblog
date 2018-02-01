---
title: 前端面试-webgis
comments: true
date: 2018-01-30 23:42:01
tags:
  - webgis
categories:
  - 前端面试
---

## leaflet、mapbox、webGIS
<!-- more -->

### 切图原理？

http://www.cnblogs.com/naaoveGIS/p/3898607.html
http://www.cnblogs.com/naaoveGIS/p/3899821.html
http://blog.csdn.net/qingyafan/article/details/53367204

### 屏幕坐标和地图坐标转换原理？
- 首先获取地图的中心点和比例尺级别，屏幕DPI
- 计算 Resolution，屏幕上一像素代表的实际距离。
- 计算屏幕范围对应的地理范围，得到屏幕左上角坐标对应的地理坐标
```js
var topleftx = mapx - (containerWidth * resolution) / 2;
var toplefty = mapy - (containerHeight * resolution) / 2;
```
- 用户点击屏幕上的一个点 (x,y)计算地理坐标点
```js
var mapx = topleftx + x * resolution;
var mapy = toplefty + y * resolution;
```
https://www.cnblogs.com/naaoveGIS/p/3930603.html
https://www.jianshu.com/p/b5dbdbd5cd8c
http://blog.csdn.net/yht_roy/article/details/39346235

### 插值算法实现原理？
http://www.cnblogs.com/naaoveGIS/p/6142226.html
https://en.wikipedia.org/wiki/Bilinear_interpolation
