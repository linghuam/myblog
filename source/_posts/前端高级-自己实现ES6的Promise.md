---
title: 前端高级-自己实现ES6的Promise
comments: true
date: 2018-11-05 09:41:44
tags:
categories:
- 前端高级
---

js-Promise
<!--more-->

```js
/**
 * promise 实现
 * 参考： https://juejin.im/post/5b2f02cd5188252b937548ab
 * 2018-7-5
 */

const STATE = {
    pending: 'pending',
    fulfilled: 'fulfilled',
    rejected: 'rejected'
}

class MyPromise {
    constructor(executor) {
        this.state = STATE.pending
        this.value = ''
        this.reason = ''
        this.onResolveCallbacks = []
        this.onRejectedCallbacks = []
        let resolve = (value) => {
            if (this.state === STATE.pending) {
                this.state = STATE.fulfilled
                this.value = value
                this.onResolveCallbacks.forEach(fn => fn())
            }
        }
        let reject = (reason) => {
            if (this.state === STATE.pending) {
                this.state = STATE.rejected
                this.reason = reason
                this.onRejectedCallbacks.forEach(fn => fn())
            }
        }
        try {
            executor(resolve, reject)
        } catch (err) {
            reject(err)
        }
    }
    then(onFulfilled, onRejected) {
        onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : value => value
        onRejected = typeof onRejected === 'function' ? onRejected : err => {throw err}
        let promise2 = new MyPromise((resolve, reject) => {
            if (this.state === STATE.fulfilled) {
                setTimeout(() => {
                    try {
                        let x = onFulfilled(this.value)
                        resolvePromise(promise2, x, resolve, reject)
                    } catch (e) {
                        reject(e)
                    }
                }, 0)

            }
            if (this.state === STATE.rejected) {
                setTimeout(() => {
                    try {
                        let x = onRejected(this.reason)
                        resolvePromise(promise2, x, resolve, reject)
                    } catch (e) {
                        reject(e)
                    }
                }, 0)

            }
            if (this.state === STATE.pending) {
                this.onResolveCallbacks.push(() => {
                    setTimeout(() => {
                        try {
                            let x = onFulfilled(this.value)
                            resolvePromise(promise2, x, resolve, reject)
                        } catch (e) {
                            reject(e)
                        }
                    }, 0)
                })
                this.onRejectedCallbacks.push(() => {
                    setTimeout(() => {
                        try {
                            let x = onRejected(this.reason)
                            resolvePromise(promise2, x, resolve, reject)
                        } catch (e) {
                            reject(e)
                        }
                    }, 0)
                })
            }
        })
        return promise2
    }
}

function resolvePromise(promise2, x, resolve, reject) {
    if (x === promise2) {
        return reject(new TypeError('Chaining cycle detected for promise'))
    }
    let called
    if (x !== null && (typeof x === 'object' || typeof x === 'function')) {
        try {
            let then = x.then
            if (typeof then === 'function') {
                then.call(x, y => {
                    if (called) return;
                    called = true
                    resolvePromise(promise2, y, resolve, reject)
                }, err => {
                    if (called) return
                    called = true
                    reject(err)
                })
            } else {
                resolve(x)
            }
        } catch(e) {
            if (called) return;
            called = true
            reject(e)
        }
    } else {
        resolve(x)
    }
}

MyPromise.resolve = function (res) {
    return new MyPromise((resolve, reject) => {
        resolve(res)
    })
}

MyPromise.reject = function (err) {
    return new MyPromise((resolve, reject) => {
        reject(err)
    })
}

MyPromise.race = function (promises) {
    return new MyPromise((resolve, reject) => {
        for (let i = 0, len = promises.length; i < len; i++) {
            promises[i].then(resolve, reject)
        }
    })
}

MyPromise.all = function (promises) {
    let arr = []
    let index = 0
    return new MyPromise((resolve, reject) => {
        for (let i = 0, len = promises.length; i < len; i++) {
            promises[i].then(res => {
                arr.push(res)
                index ++
                if (index === len) {
                    resolve(arr)
                }
            }, err => {
                reject(err)
            })
        }
    })
}
```