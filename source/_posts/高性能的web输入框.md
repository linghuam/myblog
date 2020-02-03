---
title: 高性能的web输入框
comments: true
date: 2019-08-12 23:36:39
tags:
categories:
- 专题
- 性能优化
---

# High-performance input handling on the web

[推酷地址](https://www.tuicool.com/articles/ZfaURvZ)

[原文链接](https://nolanlawson.com/2019/08/11/high-performance-input-handling-on-the-web/?utm_source=tuicool&utm_medium=referral)

```js
function throttleRAF () {
    let queuedCallback
    return callback => {
        if (!queuedCallback) {
            requestAnimationFrame(() => {
                const cb = queuedCallback
                queuedCallback = null
                cb()
            })
        }
        queuedCallback = callback
    }
}
```

[A simple method to invoke a function after the browser has rendered & painted a frame](https://github.com/andrewiggins/afterframe)

[fastdom](https://github.com/wilsonpage/fastdom)