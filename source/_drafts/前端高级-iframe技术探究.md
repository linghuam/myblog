---
title: 前端高级-iframe技术探究
comments: true
date: 2020-05-26 10:41:03
tags:
categories:
- 前端高级
---


跨域的 iframe 互相访问受限，可通过 postMessage 通信

iframe 上的事件冒泡只能到达 iframe 内部，无法到达 parent 中

跨域的 iframe 无法监听 iframe.contentWindow 上的事件，同域的可以监听

火狐及chorme都不支持onerror事件，而且，不管iframe加载是否成功，都会触发onload事件。

