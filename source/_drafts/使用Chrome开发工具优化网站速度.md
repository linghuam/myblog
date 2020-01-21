---
title: 使用Chrome开发工具优化网站速度
comments: true
date: 2020-01-17 15:00:44
tags:
categories:
- 专题
- 性能优化
---

本文总结 chrome 开发者工具的使用，重点介绍**性能优化**方面的工具。
官方文档参考：https://developers.google.com/web/tools/chrome-devtools/?hl=en。

<!--more-->

## 使用 Chrome DevTools 中的 Coverage 标签查找未使用的 JavaScript 和 CSS 代码

https://developers.google.com/web/tools/chrome-devtools/coverage/


## NetWork

如果您正在寻找提高页面加载性能的方法，不要从 Network 面板开始。有许多类型的负载性能问题与网络活动无关。从审计 Audits 小组开始，因为它给你有针对性的建议如何改善你的页面。参见 [优化网站速度](https://developers.google.com/web/tools/chrome-devtools/speed/get-started)。

**[Timing](https://developers.google.com/web/tools/chrome-devtools/network/reference#timing-explanation) 标签：**

* **Queueing**。浏览器会在以下情况下将某个请求排队：
  * 有更高优先级的请求
  * 在http1.0/1.1协议下，chrome对于同一域名下的并发请求数（连接数）限制为6个。
  * 浏览器正在硬盘的缓存上分配空间

* **Stalled**。请求会因为各种原因的排队被拖延，与请求队列有关系。

* **DNS Lookup**。DNS查询。

* **Proxy negotiation**。浏览器正在与代理服务器协商请求（建立TCP连接的时间）。

* **Request sent**。正在发送请求。
* **ServiceWorker Preparation**。浏览器正在启动Service Worker。
* **Request to ServiceWorker**。正在将请求发送到Service Worker。
* **Waiting (TTFB)**。浏览器正在等待响应的第一个字节。TTFB表示Time To First Byte（至第一字节的时间）。此时间包括1次往返延迟时间及服务器准备响应所用的时间。
* **Content Download**。浏览器正在接收响应。
* **Receiving Push**。浏览器正在通过 HTTP/2 服务器推送接收此响应的数据。
* **Reading Push**。浏览器正在读取之前收到的本地数据。

> 对于某个请求我们能够优化的主要是`Waiting (TTFB)`。它耗费的时间最多。主要从服务器响应和网络传输这两方面来下手。如果只考虑网络传输这个因素，那么压缩传输数据，毕竟网络速度有限，减少传送的数据字节数可以加快传输速度。

## Performance panel




## 参考

* [使用Chrome开发工具优化网站速度](https://developers.google.com/web/tools/chrome-devtools/speed/get-started)