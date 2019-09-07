---
title: WebGIS开发入门
comments: true
date: 2019-08-04 20:28:08
tags:
- webgis
categories:
- gis
---

# WebGIS 开发入门

将技术的原理、业界使用情况、在咱们公司的现状或者结合点、后续趋势都能够阐述出来。

## 什么是 WebGIS

GIS + WWW = Web GIS

Web: 不用解释

GIS: 重点解释GIS

geographic information systems 
geographic information science
地理信息系统（科学）

短视频：https://www.bilibili.com/video/av17091140

交叉学科
![](./WebGIS开发入门/gis相关学科.png)

ersi: what is gis
https://www.esri.com/en-us/what-is-gis/overview#image6

## 关键技术及原理

### 数据

结构化数据（关系表） & 半结构化数据（对象属性不固定） & 非结构化数据（图片、视屏、音频）

数据类型

- 矢量（定位明显，属性隐含）
  * 点
  * 线
  * 面
路网、poi

- 栅格（属性明显，定位隐含）
  * 卫星影像
  * DEM

气象、降雨量。。。
- 相互转化

http://zhihu.esrichina.com.cn/?/article/528

数据描述
矢量：geojson\shp\wkt\wkb\kml
https://geojson.org/
```
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [125.6, 10.1]
  },
  "properties": {
    "name": "Dinagat Islands"
  }
}
```
shp：https://www.cnblogs.com/nygfcn1234/p/3399605.html

栅格：dem

### 坐标系与投影

定位一个要素，必须嵌入一个参照系。

因为 GIS 所描述是位于地球表面的信息，所以根据地球椭球体建立的地理坐标（经
纬网）可以作为所有要素的参照系统。因为地球是一个不规则的球体，为了能够将
其表面的内容显示在平面的显示器或纸面上，必须进行坐标变换。

椭球体
球体

地理坐标系
平面坐标系

坐标变换：平移、旋转、缩放

经度、纬度

聊聊GIS中那些坐标系：
https://www.cnblogs.com/onsummer/p/7451128.html

地理坐标系、大地坐标系与地图投影与重投影详解：
https://www.cnblogs.com/arxive/p/6017260.html

地图地理投影：
https://www.wolfram.com/language/11/geo-computation/cartographic-geo-projections.zh.html

地图投影的科普向：
https://zhuanlan.zhihu.com/p/24981976

地理坐标系、大地坐标系与地图投影与重投影详解
https://blog.csdn.net/angelazy/article/details/44085099

BBC《地图》纪录片
从“我们看到的地图一直都错得离谱”说起：
http://www.3snews.net/column/252000039786.html

墨卡托投影
https://blog.csdn.net/qq_35732147/article/details/83856513


墨卡托投影的地图最大的缺点就是和现实差别太大，变形非常严重。

在墨卡托投影的地图上，变形最严重的就是格陵兰岛了。地图上非洲的大小和格陵兰岛差不多大，但如果计算一下的话：非洲面积约是3020万平方千米，格陵兰岛面积约是217万平方千米，也就是说，非洲的面积是格陵兰岛的14倍！

再比如墨卡托投影的地图上的加拿大，看起来是个瘦瘦的长方形，但实际上，加拿大是个类似正方形的形状。它不仅扭曲得不像样，而且还被放大了好几倍。在地图上加拿大的面积大约是美国的三倍，实际上加拿大比美国大不了多少。

### 常见的地图服务

天地图：
https://service.tianditu.gov.cn/#

OGC:
https://blog.csdn.net/u014177758/article/details/73250749

地图类型：
https://enterprise.arcgis.com/zh-cn/server/latest/create-web-apps/windows/a-framework-for-deploying-web-gis-applications.htm


WMS
WMTS

瓦片原理：
https://blog.csdn.net/ahence/article/details/44057681
https://blog.csdn.net/tmchongye/article/details/63536108
https://blog.csdn.net/wd4java/article/details/44956799

### 技术资源

### 空间分析与可视化


## 应用和展望

## 资料分享

https://cntchen.github.io/2016/05/09/%E5%9B%BD%E5%86%85%E4%B8%BB%E8%A6%81%E5%9C%B0%E5%9B%BE%E7%93%A6%E7%89%87%E5%9D%90%E6%A0%87%E7%B3%BB%E5%AE%9A%E4%B9%89%E5%8F%8A%E8%AE%A1%E7%AE%97%E5%8E%9F%E7%90%86/


https://cntchen.github.io/2016/05/09/%E5%9B%BD%E5%86%85%E4%B8%BB%E8%A6%81%E5%9C%B0%E5%9B%BE%E7%93%A6%E7%89%87%E5%9D%90%E6%A0%87%E7%B3%BB%E5%AE%9A%E4%B9%89%E5%8F%8A%E8%AE%A1%E7%AE%97%E5%8E%9F%E7%90%86/

坐标转化库：（误差在10米左右）
https://github.com/wandergis/coordtransform

瓦片地图原理：
https://segmentfault.com/a/1190000011276788
https://www.maptiler.com/google-maps-coordinates-tile-bounds-projection/

国内主要地图瓦片坐标系定义及计算原理：
https://cntchen.github.io/2016/05/09/%E5%9B%BD%E5%86%85%E4%B8%BB%E8%A6%81%E5%9C%B0%E5%9B%BE%E7%93%A6%E7%89%87%E5%9D%90%E6%A0%87%E7%B3%BB%E5%AE%9A%E4%B9%89%E5%8F%8A%E8%AE%A1%E7%AE%97%E5%8E%9F%E7%90%86/

瓦片地图原理：
https://segmentfault.com/a/1190000011276788


OGC标准
https://www.jianshu.com/p/fa323448bf47

GIS开发者
https://www.giserdqy.com/gis/gisknowledge/

空间关系：
https://malagis.com/gis-spatial-relations.html


从底层谈，WebGIS 原理、设计、实现：
https://www.cnblogs.com/naaoveGIS/category/600559.html

面积和距离测量：

(十七)WebGIS中距离及面积测量的原理和实现以及坐标转换的简单介绍：https://www.cnblogs.com/naaoveGIS/p/4115021.html
"Some Algorithms for Polygons on a Sphere"
https://trs.jpl.nasa.gov/handle/2014/41271
https://trs.jpl.nasa.gov/bitstream/handle/2014/41271/07-0286.pdf?sequence=1&isAllowed=y


距离：
http://www.movable-type.co.uk/scripts/latlong.html
https://en.wikipedia.org/wiki/Haversine_formula
https://www.cnblogs.com/softidea/p/6925673.html
https://www.cnblogs.com/softfair/p/distance_of_two_latitude_and_longitude_points.html