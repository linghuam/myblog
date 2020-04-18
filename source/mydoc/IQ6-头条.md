
### 描述一下JS的`new`操作符具体做了什么?

（1）创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
（2）属性和方法被加入到 this 引用的对象中。
（3）新创建的对象由 this 所引用，并且最后隐式的返回 this 。

```js
var obj = {};
this = obj;
obj.__proto__ = fn.prototype;
return obj;
```

### JS编程实现简单模板引擎变量替换？

### 封装一个ajax请求库实现get和post方法？

```js
// https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started
// https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest
var ajax = (function(){
  function getQueryString(data) {
    return Object.keys(data).map(key => {
      return `${key}=${encodeURIComponent(data[key])}`;
    }).join('&');
  }
  
  const objAssign = Object.assign ? Object.assign : function objAssign(target, args) {
    if (target == null) {
      throw new TypeError('Cannot convert undefined or null to object!');
    }
    for(let i = 1; i < arguments.length; i++) {
      let nextSource = arguments[i];
      if (nextSource != null) {
        for (let nextKey in nextSource) {
          if (Object.prototype.hasOwnProperty.call(nextSource, nextKey)) {
            target[nextKey] = nextSource[nextKey];
          }
        }
      }
    }
    return target;
  }
  
  function ajax(options) {
    options = objAssign({}, options, {
      dataType: "json"
    });
    const xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
      // 请求是否完成
      if (xhr.readyState === XMLHttpRequest.DONE) {
        // 请求返回的状态码，200表示成功
        if (xhr.status === 200) {
          /*获取数据
          1. xhr.responseText - 以文本字符串形式返回服务器响应
          2. xhr.responseXML - 以 XMLDocument 对象形式返回
          */
          let res = xhr.responseText;
          if (options.dataType === 'json') {
            res = JSON.parse(res);
          }
          if (typeof options.success === 'function') {
            options.success.call(null, res);
          }
        } else {
          if (typeof options.fail === 'function') {
            options.fail.call(null, xhr.status);
          }
        }
      }
    };
    let url = options.url;
    if (options.type === 'GET') {
      url += '?' + getQueryString(options.data);
      xhr.open('GET', url);
      xhr.send();
    } else if (options.type === 'POST') {
      xhr.open('POST', url);
      xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
      const formdata = getQueryString(options.data);
      xhr.send(formdata);
    }
  }

  return ajax;
}());
```

### 节流(trottle)与防抖(debounce)？


### 求二叉树是否存在和值为N的路径？

### 100 * 100 的 Canvas 占内存多大？
https://juejin.im/post/5bdeb357e51d4536140fc7df

### 算法能力如何？ 给一个数组如：[[“a”,”b”,”c”],[“d”,”e”],…..]得到[ad,ae,bd,be,cd,ce]，手写实现的方法？（要求js实现）
### 如何将上面的改成函数式编程风格？
### 如果数组中出现[[“a”,”b”,”c”],[“a”,”d”]]要求去掉”aa”这种情况（即两组所取的元素不能有相同的）？不能用filter…
### 跳台阶问题？m阶楼梯，一次最多可跳4次，有多少种可能？（本来问n次，然后直接举例说4次）手写实现代码？
### 死锁的条件是什么？
### js单线程？setTimeout(,100)是否会100ms后执行，原因是？EventLoop？
### 谈谈你对reactjs的理解？为什么项目中选用reactjs？与其他框架的区别？双向绑定是ng1还是ng2？vuejs1还是vuejs2？
### 项目中有使用flux或者redux等么？
### reactjs中虚拟dom要这样实现的原因是什么？（不是问如何实现的=_=）

https://blog.csdn.net/tzcccy/article/details/79246811
（1）、请简述一下DNS。
（2）、有听过HTTPDNS吗？
（3）、有哪些方法能加快网络连接速度
（4）、如何维持长链接
（5）、如何发送心跳包
（6）、自动布局（设置约束）和手动布局（设置frame）的优缺点，哪个效率高，为什么？
（7）、一道简单dp题，求两个字符串最长连续公共序列

 (1）、用户产生一个下拉刷新动作，请详细描述网络如何传输
（2）、简述tcp连接时的握手过程，不要第三次握手行不行？
（3）、讲讲拥塞避免算法
（4）、GCD同步与异步
（5）、GCD的使用场景
（6）、NSArray、NSSet、NSDictionary的效率
（7）、只用栈实现一个队列
（8）、内存中堆与栈的区别
（9）、什么时候在栈中什么时候在堆中
（10）、为什么OC不能像下面这样实例一个对象
class A;
A a;
（11）、请简述操作系统内存管理
（12）、一个iOS app，在内存中除了会使用到堆区和栈区，还会使用到什么区
（13）、一个算法题，给定一个字符串（只有小写字母）和m步操作，每一步操作可以把相邻
两个字符交换位置，问最多执行m步操作后，字符串中最长连续相同字符的长度是多少

（1）、算法题，给一组数字，这些数字里面每一个都重复出现了三次，只有一个数字只出现了一个，要求在时间O（n）空间O（1）内解出来。
（2）、说说你做项目过程中印象深刻的地方或者技术难点
（3）、使用自动布局，把三个view横向等宽等间距（与父view边距也相等）排列。


### https://www.imooc.com/article/274197

### https://www.imooc.com/article/33783

### https://q.shanyue.tech/interviews/2018.html#%E8%83%8C%E6%99%AF

### https://ssrshare.github.io/2019/04/15/html-css-js/