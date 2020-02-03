---
title: 前端基础-encodeURIComponent原理
comments: true
date: 2018-06-24 21:55:36
tags:
categories:
- 前端基础
- BOM
---

前端开发中，我们经常在请求路径中带各种参数，但细心的你会发现，在浏览器的路径栏看到的地址跟自己输入的参数不一样，浏览器将自己的输入转换成了一串字符。
这其中涉及到 encodeURI、encodeURIComponent、decodeURI、decodeURIComponent(escape和unescape已被弃用)。
<!--more-->

## encodeURI 和 decodeURI

encodeURI(uri)
- 参数：uri一个包含URI或其他待编码的文本的字符串
- 返回：uri的一个副本，其中某些字符已被替换为十六进制转义序列。

ASCII 字母和数字以及下面的ASCII标点字符将不会编码：-_.!~*'()  ;/?:@&=+$,#

uri中的其他字符将被转换为对应的 **UTF-8** 编码，并将结果的一、二或三个字节编码为一个 `%xx` 格式的十六进制转义序列。在这种编码机制中，ASCII字符将被替换为一个单独的`%xx` 转义序列，编码在 \uoo8o ~ \uo7ff 之间的字符将被替换为两个转义序列，其他所有的十六位的Unicode字符则将被替换为三个转义序列。

使用这个方法来编码URI时，必须确保该URI的组件(如查询字符串)**都不包含**如“?”和“#”等的URI分隔字符。如果这些组件必须包含这类字符，则应该使用encodeURIComponent()来对每个组件进行 **单独编码** 。

decodeURI()是这个方法的逆方法。

## encodeURIComponent 和 decodeURIComponent

encodeURIComponent(s)
- 参数s:一个包含URI一部分或其他待编码文本的字符串。
- 返回：s的一个副本，某些字符已替换为十六进制转义序列。

ASCII字母和数字以及下面这些ASCII标点字符将不会编码：-_.!~*'()，所有其他字符，包括“/”、“:”以及“#”等用于分隔URI的多个组件的标点字符，都将被替换为一个或多个十六进制的转义序列。

## encodeURIComponent() 和 encodeURI() 之间的差别

- encodeURIComponent()假设它的参数是URI的一部分（如协议、主机名、路径或查询字符串）。因此，它将那些用于分隔URI不同部分的标点字符（/:#）也转义了。
- encodeURI方法 **不会** 对下列字符编码：ASCII字母、数字、~!@#$&*()=:/,;?+'
- encodeURIComponent方法 **不会** 对下列字符编码：ASCII字母、数字、~!*()'

## 最佳实践

- 如果需要编码整个 URL，然后需要使用这个 URL，那么用 encodeURI()
- 当你需要编码 URL 中的参数的时候，那么 encodeURIComponent() 是最佳的方法

## 参考

- [URI](https://zh.wikipedia.org/wiki/%E7%BB%9F%E4%B8%80%E8%B5%84%E6%BA%90%E6%A0%87%E5%BF%97%E7%AC%A6)
- [Percent-encoding](https://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_in_a_URI)
- [w3school](http://www.w3school.com.cn/js/jsref_encodeURIComponent.asp)
- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)
- [ZhiHu](https://www.zhihu.com/question/21861899)