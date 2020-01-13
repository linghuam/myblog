## 切图原理？

http://www.cnblogs.com/naaoveGIS/p/3898607.html
http://www.cnblogs.com/naaoveGIS/p/3899821.html
http://blog.csdn.net/qingyafan/article/details/53367204

## 屏幕坐标和地图坐标转换原理？
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

## 插值算法实现原理？
- 已知条件：一系列离散点；要插的值序列，如：[3,5,7,9]
- 网格化。采用 IDW 算法将离散点网格化。
- 取一个待插值数 p0，将每个网格的顶点数值与之相减，结果大于零则标记为'+'，结果小于零则标记为'-'
- 这样就得到一个顶点要么是正，要么是负的网格。
- 逐一的处理每个网格，取网格各个边的中点，然后找到将正负分开的连线将中点相连接
- 重复上诉过程，插另一个值

http://blog.csdn.net/silangquan/article/details/47054309

https://en.wikipedia.org/wiki/Marching_squares
