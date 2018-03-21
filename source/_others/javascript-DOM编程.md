---
title: javascript-DOM编程
tags:
  - dom
categories:
  - javascript
---

javascript是一门宿主语言，它可以运行在不同的宿主环境中，如动态网页是在浏览器环境下运行的js, NodeJS是在服务器环境下运行的js。
不同的环境为javascript提供了不同的编程接口，这篇文章主要介绍在DOM环境中的javascript，即 **JavaScript DOM 编程**。

<!-- more -->

## 什么是 DOM
DOM 的全称是 `Document Object Model`, 即文档对象模型。

DOM 是 W3C 的推荐标准。 它与平台、语言无关。

DOM 定义了访问诸如 XML 和 XHTML 文档的标准。

W3C DOM 被分为 3 个不同的部分/级别：

* 核心 DOM

 用于任何结构化文档的标准模型

* XML DOM

 用于 XML 文档的标准模型

* HTML DOM

 用于 HTML 文档的标准模型

本文主要讲解 `HTML DOM`。

## JavaScript 与 DOM

从 javascript 的角度出发，它用 **_对象_** 来表示网页中的各个 DOM 部分。
比如，整个页面可以用 `Document` 对象来表示，页面的各个元素(html, head, body, div...)用
`Element` 对象表示。 整个页面结构是一个**树状结构**，`Document` 对象则代表根节点。

## 一切皆 Node




## js如何创建 DOM 元素

## js如何获取 DOM 元素

## js如何修改 DOM 元素

## 参考文档
