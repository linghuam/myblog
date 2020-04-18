## 点击td排序表格

## css 单位：vm、vh

## https加密算法？为什么对称和非对称？

## 块级元素和行内元素有什么区别，举例常用的块级和行内元素，行内元素有padding／margin吗？

- 块级元素独占一行，内部可嵌套块级或行内元素；有：div、p、h1-h6、ul等
- 行内元素在一行内布局，按行排列，超出自动折行；有：a、span、img、input、label、button等；
- 行内**非替换**元素设置 width、height无效，可设置line-height；【img 和 canvas 可设置宽高】；替换元素都可以设置，如img。
- 行内**非替换**元素设置 padding、margin只有左右生效，上下无效；替换元素都可以设置，如img。

## call,apply,bind的区别，并举例使用的场景？
- call：fn.call(this,param1,param2,param3); 返回fn执行后的返回值
- apply：fn.apply(this,[param1,param2,param3]); 返回fn执行后的返回值
- bind：fn.bind(this,arguments); 返回一个新的fn

```js
Function.prototype.bind = function(context) {
  var slice = Array.prototype.slice;
  var args = slice.apply(arguments, 1);
  return function() {
    return this.apply(context, slice(arguments, 0).concat(args));
  }
}
```

## 画出一个正方形，并且自适应，列出的方法越多越好？

```html
<!-- https://www.cnblogs.com/dantis/p/6846611.html -->
<!-- https://segmentfault.com/a/1190000009476303 -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>画自适应正方形</title>
    <style media="screen">
      /* 法一 */
      .box{
        width:50%;
        padding-top:50%;
        background-color: red;
      }

      /* 法二 */
      .box2{
        width:50%;
        overflow: hidden;
        background-color: red;
      }
      .margin{
        margin-top: 100%;
      }

      /* 法三 */
      .box3{
        width:100%;
        height:80vh;
        background-color: red;
      }

      /* 法四 */
      .box4{
        width:100%;
        overflow: hidden;
        background-color: red;
      }
      .box4:after{
        content: '';
        display: block;
        margin-top: 100%;
      }
    </style>
  </head>
  <body>

    <div class="box">
    </div>

    <div class="box2">
      <div class="margin">

      </div>
    </div>

    <div class="box3">

    </div>

    <div class="box4">

    </div>
  </body>
</html>
```

## css基础？

```html
/* 窗口大小500*500，img大小1000*800  */
  <p>
    <a><img></img></a>
  <p>
```
- 问a，p宽高
  a: auto auto
  p: 500 500
- 给img加了绝对定位，a，p的宽高
  a: auto auto
  p: 500 0
- 给p加relative，img加 margin-top：30%，margin-left：30%
  a: auto auto
  p: 500 0
- 变成top：30%，left：30%
  a: auto auto
  p: 500 0

## 父级元素下面无固定宽高的块元素，实现水平垂直居中?
高宽不固定：`position:absolute;top:50%;left:50%;transform:translate(-50%, -50%);`
    或 `display:flex;justify-content:center;align-items:center;`

## arguments 是数组吗？不是的话，怎么变成数组?
不是，是类数组对象

Array.prototype.slice.call(arguments);
[...arguments]

## 写出下面会输出的值？
```js
if([]==false){console.log(1)};
if({}==false){console.log(2)};
if([]){console.log(3)}
if([1]==[1]){console.log(4)}

// 只输出1,3
```
if([])直接调用blooean()方法

考察 js == 与 === 的区别？
1. 对于string,number等基础类型，==和===是有区别的
   * 不同类型间比较，==之比较“转化成同一类型后的值”看“值”是否相等，===如果类型不同，其结果就是不等
   * 同类型比较，直接进行“值”比较，两者结果一样
2. 对于Array,Object等高级类型，==和===是没有区别的
   * 进行“指针地址”比较
3. 基础类型与高级类型，==和===是有区别的
   * 对于==，将高级转化为基础类型，进行“值”比较
   * 因为类型不同，===结果为false

总的来说，== 会引起类型转换，比较的是值； === 不会引起类型转换，比较的是内存地址。

绝大多数场合应该使用 === ，只有检测 null/undefined 的时候可以使用 x == null。

## 修改错误，可以使用es6?

```js
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000 * i);
} // 使得其输出为0，1，2，3，4
```

法一： var 改成 let
法二：闭包
```js
for (var i = 0; i < 5; i++){
  (function (index){
    setTimeout(function (){
      console.log(index);
    }, 1000 * index);
  })(i);
}
```

## instanceof 原理？

```js
function Person(name, age){
    this.name = name;
    this.age = age;
}

function Student(score){
    this.score = score;
}

Student.prototype = new Person('李明',22);
var s = new Student(99);

console.log(s instanceof Student);  //true
console.log(s instanceof Person);  //true
console.log(s instanceof Object);  //true
```

检测对象A是不是另一个对象B的实例的原理是：
查看对象B的prototype属性指向的原型对象是否在对象A的原型链上，若在则返回true，若不在则返回false。

## 判断数组？
if(Object.prototype.toString.call(arr)==='[object array]')

或

Array.isArray(arr)

## session、cookie、sessionStorage、localStorage等区别?
详见：http://www.jb51.net/article/122101.htm

Cookie/Session机制详解：http://blog.csdn.net/fangaoxin/article/details/6952954

cookie存储在客户端，session存储在服务端，通过 session id 来识别客户端， session id存储在cookie中或url中。

移动端不支持 cookie，可通过将 session id 写入 URL 来记录用户状态。

当客户端第一次请求session对象时，服务端生成一个id并发送给客户端，客户端在下次请求时，再将这个id发送给服务端。

cookie安全性不好，session安全，但服务端压力大。

**存储大小：**
- cookie 数据大小不能超过4k。
- sessionStorage 和 localStorage 虽然也有存储大小的限制，但比 cookie 大得多，可以达到5M或更大。
**有期时间：**
- localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
- sessionStorage  数据在当前浏览器窗口关闭后自动删除。
- cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
**作用域不同:**
- sessionStorage 不在不同的浏览器窗口中共享，即使是同一个页面；
- localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。

## Cookie 组成？ 

http://www.xuebuyuan.com/889016.html
Cookie格式如下:

Set－Cookie: NAME=VALUE；Expires=DATE；Path=PATH；Domain=DOMAIN_NAME；SECURE

Secure：在Cookie中标记该变量，表明只有当浏览器和Web Server之间的通信协议为加密认证协议时，浏览器才向服务器提交相应的Cookie。当前这种协议只有一种，即为HTTPS。


## 浏览器发送cookie时会发送哪几个部分?

```
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: name=value; expires=失效时间; domain=域名
```

## Cookie 是否会被覆盖，localStorage是否会被覆盖?
Cookie是可以覆盖的，如果重复写入同名的Cookie，那么将会覆盖之前的Cookie

如果要删除某个Cookie，只需要新建一个同名的Cookie，并将maxAge设置为0，并添加到response中覆盖原来的Cookie。注意是0而不是负数。负数代表Cookie只保存在内存中，浏览器关闭即消失。

localStorage存储在一个对象中，如果重复写入同名的 key，也会覆盖之前的 key。


## http？[详解](https://www.jianshu.com/p/6aa2fda4d4a1)

**协议分层：** http应用层 ——> TCP传输层 ——> IP网络层 ——> 链路层（网络接口）——> 物理层（网卡）

**封装：**发送端在层与层传输数据时，每经过一层必定会打上改成所属的首部信息；接收端在层与层传输数据
时，每经过一层会把对应的首部消去。

## http 请求方法？

HTTP1.0定义了三种请求方法：GET, POST 和 HEAD方法。

HTTP1.1新增了五种请求方法：PUT, DELETE, OPTIONS, TRACE 和 CONNECT 方法。

1. | GET | 请求指定的页面信息，并返回实体主体。
2. | HEAD | 类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头。
3. | POST | 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。
4. | PUT | 从客户端向服务器传送的数据取代指定的文档的内容。
5. | DELETE | 	请求服务器删除指定的页面。
6. | CONNECT | HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
7. | OPTIONS | 询问的请求，如CORS的预检请求。允许客户端查看服务器的性能。
8. | TRACE | 回显服务器收到的请求，主要用于测试或诊断。


## https？

加密处理防止窃听。可通过SSL（Secure Socket Layer，安全套接层）或TLS（Transport Layer Security，安全传输协议）的组合使用，加密通信。与SSL组合使用的HTTP叫HTTPS。

## post、get区别？
1. 本质都是 TCP 连接，并无区别，只是贴上不同的标签，便于处理
2. get 只产生一个 TCP 数据包， post 产生两个 TCP数据包
3. get 在一次请求中将 header 和 data 发送给服务器，服务器返回 200
4. post 先发送 header 再 发送 data

5. get请求一般用于向服务器查询某些信息, post请求通常用于向服务器发送应该被保存的数据
6. get请求可以将查询字符串参数追加到url的末尾; post请求应该把数据作为请求的主体提交
7. 因为get请求提交的数据直接加载url末尾,所以其大小有限制; 理论来讲, post是没有大小限制的
8. post安全性比get要高
9. get可以缓存，post不能缓存
10. get对搜索引擎友好
11. 对于get方式, 服务器端用Request.QueryString获取变量的值, 对于post方式, 服务器端用Request.Form获取提交的数据

## 缓存？

浏览器缓存知识小结及应用：http://www.cnblogs.com/lyzg/p/5125934.html

- 200 ok ：当浏览器没有缓存，或用户强制刷新，浏览器直接获取最新数据。
- 304：由 last-modified/etag 控制。先发送请求到服务器，如果没有变化，返回304。
- 200 from cache：由 expires/cache-control 控制。

策略：[详情](http://www.cnblogs.com/skynet/archive/2012/11/28/2792503.html)
- Expires 缺点:绝对时间
- Cache-Control 相对时间 max-age 控制缓存在时间
- Last-Modified/If-Modified-Since
- Etag/If-None-Match

## 强缓存和协商缓存的命中和管理？
1）浏览器在加载资源时，先根据这个资源的一些 http header 判断它是否命中强缓存，强缓存如果命中，浏览器直接从自己的缓存中读取资源，不会发请求到服务器。

2）当强缓存没有命中的时候，浏览器一定会发送一个请求到服务器，通过服务器端依据资源的另外一些http header验证这个资源是否命中协商缓存，如果协商缓存命中，服务器会将这个请求返回，但是不会返回这个资源的数据，而是告诉客户端可以直接从缓存中加载这个资源，于是浏览器就又会从自己的缓存中去加载这个资源。

3）强缓存与协商缓存的共同点是：如果命中，都是从客户端缓存中加载资源，而不是从服务器加载资源数据；区别是：强缓存不发请求到服务器，协商缓存会发请求到服务器。

4）当协商缓存也没有命中的时候，浏览器直接从服务器加载资源数据。

## 强缓存？

1. 当浏览器对某个资源的请求命中了强缓存时，返回的 http 状态为 200，在 chrome 的开发者工具的 network 里面 size会显示为 from cache。

2. 强缓存是利用 **Expires** 或者 **Cache-Control** 这两个 http response header 实现的，它们都用来表示资源在客户端缓存的有效期。

 **Expires:** 是 http1.0 提出的一个表示资源过期时间的 header，它描述的是一个**绝对时间**，由服务器返回，用 GMT 格式的字符串表示，如：Expires:Thu, 31 Dec 2037 23:55:55 GMT。

 **Cache-Control:** Expires 是较老的强缓存管理 header，由于它是服务器返回的一个绝对时间，在服务器时间与客户端时间相差较大时，缓存管理容易出现问题，比如随意修改下客户端时间，就能影响缓存命中的结果。所以在 http1.1 的时候，提出了一个新的 header，就是 Cache-Control，这是一个**相对时间**，在配置缓存的时候，以秒为单位，用数值表示，如：Cache-Control:max-age=315360000。

3. Cache-Control 描述的是一个相对时间，在进行缓存命中的时候，都是利用客户端时间进行判断，所以相比较 Expires，Cache-Control 的缓存管理更有效，安全一些。
4. 这两个 header 可以只启用一个，也可以同时启用，当 response header 中，Expires 和 Cache-Control 同时存在时，Cache-Control 优先级高于 Expires。

## 协商缓存？
1. 当浏览器对某个资源的请求没有命中强缓存，就会发一个请求到服务器，验证协商缓存是否命中，如果协商缓存命中，请求响应返回的http状态为304并且会显示一个Not Modified的字符串。
2. 协商缓存是利用的是**【Last-Modified，If-Modified-Since】** 和 **【ETag、If-None-Match】**这两对Header来管理的。

## 浏览器行为对缓存的影响?
1. 如果资源已经被浏览器缓存下来，在缓存失效之前，再次请求时，默认会**先检查是否命中强缓存**，如果强缓存命中则直接读取缓存，**如果强缓存没有命中则发请求到服务器检查是否命中协商缓存**，如果协商缓存命中，则告诉浏览器还是可以从缓存读取，否则才从服务器返回最新的资源。这是默认的处理方式。
2. 以下行为可能改变缓存的默认处理方式
 - 当`ctrl+f5`强制刷新网页时，直接从服务器加载，跳过强缓存和协商缓存；
 - 当`f5`刷新网页时，跳过强缓存，但是会检查协商缓存。

## 请列举三种禁止浏览器缓存的头字段, 并写出相应的设置值？
1. Expires: 告诉浏览器把回送的资源缓存多长时间  -1或0则是不缓存
2. Cache-Control: no-cache
3. Pragma: no-cache

## 永久登录？
只在登录时查询一次数据库，以后访问验证登录信息时不再查询数据库。

实现方式是把账号按照一定的规则加密后，连同账号一块保存到Cookie中。下次访问时只需要判断账号的加密规则是否正确即可。

本例把账号保存到名为account的Cookie中，把账号连同密钥用MD1算法加密后保存到名为ssid的Cookie中。验证时验证Cookie中的账号与密钥加密后是否与Cookie中的ssid相等。

提示：该加密机制中最重要的部分为算法与密钥。由于MD1算法的不可逆性，即使用户知道了账号与加密后的字符串，也不可能解密得到密钥。因此，只要保管好密钥与算法，该机制就是安全的。

## 三次握手，四次挥手？
建立TCP连接需要三次握手，而断开连接需要执行四次挥手。

**三次握手：**
* 第一步: 客户机的TCP先向服务器的TCP**发送一个连接请求报文**. 这个特殊的报文中不含应用层数据, 其首部中的**SYN标志位被置1**. 另外, 客户机会随机选择一个起始序号**seq=x**(连接请求报文不携带数据,但要消耗掉一个序号)
* 第二步: 服务器端的TCP收到连接请求报文后, 若同意建立连接, 就向客户机发送请求, 并为该TCP连接**分配TCP缓存和变量**. 在确认报文中,**SYN和ACK位都被置为1**, 确认号字段的值为**x+1**, 并且服务器随机产生起始序号**seq=y**(确认报文不携带数据, 但也要消耗掉一个序号). 确认报文同样不包含应用层数据.
* 第三步: 当客户机收到确认报文后, 还要向服务器给出确认, 并且也要给该连接**分配缓存和变量**. 这个报文的**ACK标志位被置为1**, 序号字段为**x+1**, 确认号字段为**y+1**

**四次挥手：**
* 第一步: 客户机打算关闭连接,就向其TCP发送一个**连接释放报文**,并停止再发送数据,**主动关闭TCP连接**, 该报文的**FIN标志位被置1, seq=u**，它等于前面已经传送过的数据的最后一个字节的序号加1(FIN报文即使不携带数据,也要消耗掉一个序号)
* 第二步: 服务器接收连接释放报文后即发出确认, 确认号是**ack=u+1**, 这个**报文自己的序号是v**, 等于它前面已传送过的数据的最后一个自己的序号加1. 此时, 从客户机到服务器这个方向的连接就释放了, TCP连接处于**半关闭状态**. 但服务器若发送数据, 客户机仍要接收, 即从服务器到客户机的连接仍未关闭.
* 第三步: 若服务器已经没有了要向客户机发送的数据, 就**通知TCP释放连接**, 此时其发出**FIN=1**的连接释放报文
* 第四步: 客户机收到连接释放报文后, 必须发出确认. 在确认报文中, **ACK字段被置为1**, 确认号**ack=w+1, 序号seq=u+1**. 此时, TCP连接还没有释放掉, 必须经过等待计时器设置的时间2MSL后, A才进入到连接关闭状态.

## http常见状态码？
- 1开头 （信息性状态码）接收的请求正在处理
- 2开头 （成功状态码）表示成功处理了请求的状态代码
  * 200 Ok：请求被正确处理
  * 204 No Content：请求被成功处理，但服务器不返回任何实体，用于只需向服务器发送信息而不需要服务器返回信息的场景
  * 206 Partial Content：范围请求，响应报文包含有content-range描述的范围实体。
- 3开头 （重定向状态码）表示要完成请求，需要进一步操作。 通常，这些状态代码用来重定向
  * 301 Moved Permanently：永久性重定向，请求的资源已被分配了新的URI
  * 302 Found：临时性重定向
  * 303 See Other：请求资源存在另一个URI，应使用GET方法获取资源
  * 304 Not Modified：协商缓存，表示请求资源没有修改可，以直接使用浏览器缓存
  * 307 Temporary Redirect：临时性重定向，不会将 POST 变成 GET
- 4开头 （客户端错误状态码）服务器无法处理请求，请求有误
  * 400 Bad Request：请求报文包含语法错误
  * 401 Unauthorized：请求需要 http 认证信息
  * 403 Forbidden：请求被服务器拒绝
  * 404 Not Found：服务器无法找到请求的资源
- 5开头（服务器错误状态码）服务器处理请求出错，服务器本身有误
  * 500 Internal Server Error：服务器在执行请求时出错
  * 503 Service Unavailable：服务器处于超负载或停机维护状态

## http 报文结构？
HTTP请求报文解剖：https://yq.aliyun.com/articles/44672

1. 请求报文
 - 请求行：请求方法、URI、http版本。如 `POST /rest/ HTTP/1.1`
 - 首部字段：Accept、Accept-Encoding、Accept-Language、UserAgent、Content-Length、Content-Type、Referer、Origin、Connection、Host...
 - 请求主体：key=value & key=value

2. 响应报文
 - 状态行：http版本、状态码。如 `HTTP/1.1 200 OK`
 - 首部字段：Date、Content-Length、Content-Type、Accept-Ranges、Server
 - 响应主体：xml、html、json...

## http请求和响应头？
1. HTTP请求头

  accept：浏览器通过这个头告诉服务器，它所支持的数据类型。如：text/html, image/jpeg。

  accept-Charset：浏览器通过这个头告诉服务器，它支持哪种字符集。

  accept-encoding：浏览器通过这个头告诉服务器，它支持哪种压缩格式。

  accept-language：浏览器通过这个头告诉服务器，它的语言环境。

  host：浏览器通过这个头告诉服务器，它想访问哪台主机。

  if-modified-since：浏览器通过这个头告诉服务器，缓存数据的时间。

  referer：浏览器通过这个头告诉服

2. HTTP响应头

  location：服务器通过这个头告诉浏览器跳到哪里。

  server：服务器通过这个头告诉浏览器服务器的型号。

  content-encoding：服务器通过这个头告诉浏览器数据的压缩格式。

  content-length：服务器通过这个头告诉浏览器回送数据的长度。

  content-language：服务器通过这个头告诉浏览器语言环境。

  content-type：服务器通过这个头告诉浏览器回送数据的类型。

  refresh：服务器通过这个头告诉浏览器定时刷新。

  content-disposition：服务器通过这个头告诉浏览器以下载方式打开数据。

  transfer-encoding：服务器通过这个头告诉浏览器数据是以分块方式回送的务器，客户机是哪个页面来的(防盗链)。

  Connection：浏览器通过这个头告诉服务器，请求完后是断开链接还是维持链接。

## WebSocket 原理？
WebSocket：5分钟从入门到精通: https://juejin.im/post/5a4e6a43f265da3e303c4787

## 浏览器内核？常见兼容性问题？常用hack技巧？

[详情](https://zhuanlan.zhihu.com/p/27447843)

IE：Trident

Mozilla: Gecko

Goole: webkit

Opera: Presto

浏览器默认margin、padding不同。解决办法是加一个全局的。

## gzip压缩？

GZIP，即网页压缩，是由WEB服务器和浏览器之间共同遵守的协议，也就是说WEB服务器和浏览器都必须支持该技术，而现在主流的浏览器都是支持的，包括IE、FireFox、谷歌浏览器、Opera 等。常见的WEB服务器有Apache 和IIS 等。双方的协商过程如下：

1、首先浏览器请求某个URL 地址，并在请求的头 (head) 中设置属性accept-encoding值为gzip、deflate，表明浏览器支持gzip和deflate这两种压缩方式。

（注：gzip是一种数据压缩格式，默认且目前仅使用deflate算法压缩data部分；deflate是一种压缩算法,是huffman编码的一种加强。）

2、WEB服务器接收到请求后判断浏览器是否支持压缩，如果支持就传送压缩后的响应内容，否则传送不经过压缩的内容；

3、浏览器获取响应内容后，判断内容是否被压缩，如果是则解压缩，然后显示响应页面的内容。（IE5.5以上才支持gzip）

GZIP压缩的比率往往在3到10倍，也就是本来90k大小的页面，采用压缩后实际传输的内容大小只有28至30K大小，这可以大大节省服务器的网络带宽，同时如果应用程序的响应足够快时，网站的速度瓶颈就转到了网络的传输速度上，因此内容压缩后就可以大大的提升页面的浏览速度。

**web服务器处理http压缩的过程：**
1. Web服务器接收到浏览器的HTTP请求后，检查浏览器是否支持HTTP压缩（Accept-Encoding 信息）；

2. 如果浏览器支持HTTP压缩，Web服务器检查请求文件的后缀名；

3. 如果请求文件是HTML、CSS等静态文件，Web服务器到压缩缓冲目录中检查是否已经存在请求文件的最新压缩文件；

4. 如果请求文件的压缩文件不存在，Web服务器向浏览器返回未压缩的请求文件，并在压缩缓冲目录中存放请求文件的压缩文件；

5. 如果请求文件的最新压缩文件已经存在，则直接返回请求文件的压缩文件；

6. 如果请求文件是动态文件，Web服务器动态压缩内容并返回浏览器，压缩内容不存放到压缩缓存目录中。

在HTTP1.1开始，Web客户端可以通过**Acceppt-Encoding**请求头来标识对压缩的支持。服务端响应头标识**content-encoding:gzip**采用的压缩方法。

## XSS是什么，攻击原理，怎么预防？
http://blog.csdn.net/qq_21956483/article/details/54377947

**定义：**

XSS攻击是Web攻击中最常见的攻击方法之一，它是通过对网页注入可执行代码且成功地被浏览器
执行，达到攻击的目的，形成了一次有效XSS攻击，一旦攻击成功，它可以获取用户的联系人列
表，然后向联系人发送虚假诈骗信息，可以删除用户的日志等等，有时候还和其他攻击方式同时实
施比如SQL注入攻击服务器和数据库、Click劫持、相对链接劫持等实施钓鱼，它带来的危害是巨
大的，是web安全的头号大敌。

**攻击条件：**
1. 向web页面注入恶意代码；
2. 这些恶意代码能够被浏览器成功的执行。

**攻击类型：**
1. XSS**反射型**攻击，恶意代码并没有保存在目标网站，通过引诱用户点击一个链接到目标网站的恶意链接来实施攻击的。
2. XSS**存储型**攻击，恶意代码被保存到目标网站的服务器中，这种攻击具有较强的稳定性和持久性，比较常见场景是在博客，论坛等社交网站上，但OA系统，和CRM系统上也能看到它身影，比如：某CRM系统的客户投诉功能上存在XSS存储型漏洞，黑客提交了恶意攻击代码，当系统管理员查看投诉信息时恶意代码执行，窃取了客户的资料，然而管理员毫不知情，这就是典型的XSS存储型攻击。

**解决办法：**
1. 在表单提交或url参数传递前对参数进行过滤。如：过滤html字符，过滤非法js和css，url参数编码等
2. 过滤用户输入的字符，检查用户输入的内容中是否有非法内容。如<>（尖括号）、”（引号）、 ‘（单引号）、%（百分比符号）、;（分号）、()（括号）、&（& 符号）、+（加号）等。严格控制输出。
3. 不要进入不安全的网站、不要提交敏感信息。

## CRSF:跨站请求伪造？
**定义：**
CSRF（Cross-site request forgery）跨站请求伪造，也被称为“One Click Attack”或者Session Riding，通常缩写为CSRF或者XSRF，是一种对网站的恶意利用。尽管听起来像跨站脚本（XSS），但它与XSS非常不同，XSS利用站点内的信任用户，而CSRF则通过伪装来自受信任用户的请求来利用受信任的网站。与XSS攻击相比，CSRF攻击往往不大流行（因此对其进行防范的资源也相当稀少）和难以防范，所以被认为比XSS更具危险性。

**CSRF的常见特性：**
- 依靠用户标识危害网站
- 利用网站对用户标识的信任
- 欺骗用户的浏览器发送HTTP请求给目标站点
- 另外可以通过IMG标签会触发一个GET请求，可以利用它来实现CSRF攻击。

**CSRF攻击依赖下面的假定：**
- 攻击者了解受害者所在的站点
- 攻击者的目标站点具有持久化授权cookie或者受害者具有当前会话cookie
- 目标站点没有对用户在网站行为的第二授权

**解决办法：**
利用Token。

Token，就是令牌，最大的特点就是随机性，不可预测。一般黑客或软件无法猜测出来。

Token一般用在两个地方:

1)防止表单重复提交、

2)anti csrf攻击（跨站点请求伪造）。

两者在原理上都是通过session token来实现的。当客户端请求页面时，服务器会生成一个随机数Token，并且将Token放置到session当中，然后将Token发给客户端（一般通过构造hidden表单）。下次客户端提交请求时，Token会随着表单一起提交到服务器端。

然后，如果应用于“anti csrf攻击”，则服务器端会对Token值进行验证，判断是否和session中的Token值相等，若相等，则可以证明请求有效，不是伪造的。

不过，如果应用于“防止表单重复提交”，服务器端第一次验证相同过后，会将session中的Token值更新下，若用户重复提交，第二次的验证判断将失败，因为用户提交的表单中的Token没变，但服务器端session中Token已经改变了。


## css盒模型？

**定义：**content + padding + border + margin

**怪异盒模型：**IE, 即： width = content + padding + border；（IE6一下或IE7、8的怪异模式）

**标准盒模型：**即： width = content；

**box-sizing属性: **设置 `box-sizing: content-box（W3C） | border-box（IE6）` 统一盒模型种类；

**外边距合并：** 普通文档流块级框的垂直外边距会合并，行内、浮动、绝对定位元素之间的外边距不合并。设置 `*{padding:0;margin:0;}` 清除默认值；

**margin越界：**（第一个子元素的margin-top和最后一个子元素margin-bottom的值加在父元素上）应该给父元素加前置内容。

**盒模型画三角形：**
```css
{width:0;height:0;border:100px solid transparent;border-top:100px solid red;}
```

## CSS 选择器优先级怎么计算？
css 优先级由高到低顺序：!important（ie6不支持） > 内联样式 > id选择器 > 类 > 标签|属性|伪类 > *。

精确的计算是根据**特殊性值**来计算的，如果特殊性值相同，那么后定义的覆盖前面的。

内联、id、class、标签 赋予的权重分别是 1000、100、10、1，根据权重取舍元素css属性。

## position的值？应用场景？
- static: 默认，正常文档流。top、right、left、bottom、z-index属性无效。
- relative: 相对布局，相对自身正常位置，自身位置仍然保留。
- absolute: 绝对布局，相对于第一个包含块（position不为static），脱离文档流，自身位置不保留，形成新层。
- fixed: 固定布局，相对于视口坐标，脱离文档流，自身位置不保留，不随滚动条改变位置。
- sticky: 粘性定位，正常情况下按照正常文档流定位。当滚动到该元素的位置时，元素的定位（相对于包含块）发生改变。

应用场景：广告漂浮层，底部按钮，右上角的小数字图标

## 三次握手？
在TCP/IP协议中,TCP协议提供可靠的连接服务,采用三次握手建立一个连接.

第一次握手：建立连接时,客户端发送syn包(syn=j)到服务器,并进入SYN_SEND状态,等待服务器确认；
SYN：同步序列编号(Synchronize Sequence Numbers)

第二次握手：服务器收到syn包,必须确认客户的SYN（ack=j+1）,同时自己也发送一个SYN包（syn=k）,即SYN+ACK包,此时服务器进入SYN_RECV状态；

第三次握手：客户端收到服务器的SYN＋ACK包,向服务器发送确认包ACK(ack=k+1),此包发送完毕,客户端和服务器进入ESTABLISHED状态,完成三次握手.

完成三次握手,客户端与服务器开始传送数据

## Http、Https 区别？
- http效率更高，https更安全
- http采用明文传输，https是经过SSL加密的
- http采用 80 端口，https采用 443 端口
- https协议需要到ca申请证书，一般免费证书较少，因而需要一定费用
- http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全

## XSS是什么，攻击原理，怎么预防？
http://blog.csdn.net/qq_21956483/article/details/54377947

**定义：**

XSS攻击是Web攻击中最常见的攻击方法之一，它是通过对网页注入可执行代码且成功地被浏览器
执行，达到攻击的目的，形成了一次有效XSS攻击，一旦攻击成功，它可以获取用户的联系人列
表，然后向联系人发送虚假诈骗信息，可以删除用户的日志等等，有时候还和其他攻击方式同时实
施比如SQL注入攻击服务器和数据库、Click劫持、相对链接劫持等实施钓鱼，它带来的危害是巨
大的，是web安全的头号大敌。

**攻击条件：**
1. 向web页面注入恶意代码；
2. 这些恶意代码能够被浏览器成功的执行。

**攻击类型：**
1. XSS**反射型**攻击，恶意代码并没有保存在目标网站，通过引诱用户点击一个链接到目标网站的恶意链接来实施攻击的。
2. XSS**存储型**攻击，恶意代码被保存到目标网站的服务器中，这种攻击具有较强的稳定性和持久性，比较常见场景是在博客，论坛等社交网站上，但OA系统，和CRM系统上也能看到它身影，比如：某CRM系统的客户投诉功能上存在XSS存储型漏洞，黑客提交了恶意攻击代码，当系统管理员查看投诉信息时恶意代码执行，窃取了客户的资料，然而管理员毫不知情，这就是典型的XSS存储型攻击。

**解决办法：**
1. 在表单提交或url参数传递前对参数进行过滤。如：过滤html字符，过滤非法js和css，url参数编码等
2. 过滤用户输入的字符，检查用户输入的内容中是否有非法内容。如<>（尖括号）、”（引号）、 ‘（单引号）、%（百分比符号）、;（分号）、()（括号）、&（& 符号）、+（加号）等。严格控制输出。
3. 不要进入不安全的网站、不要提交敏感信息。

**防御手段:**
1. 在输出html时，加上Content Security Policy的Http Header
（作用：可以防止页面被XSS攻击时，嵌入第三方的脚本文件等）
（缺陷：IE或低版本的浏览器可能不支持）
2. 在设置Cookie时，加上HttpOnly参数
（作用：可以防止页面被XSS攻击时，Cookie信息被盗取，可兼容至IE6）
（缺陷：网站本身的JS代码也无法操作Cookie，而且作用有限，只能保证Cookie的安全）
3. 在开发API时，检验请求的Referer参数
（作用：可以在一定程度上防止CSRF攻击）
（缺陷：IE或低版本的浏览器中，Referer参数可以被伪造）


## 写一个函数每次调用输出会自增 1？
```js
var func = (function (){
  'use strict';
  var count = 0;
  return function (){
    return count ++;
  };
})();
func();
```
## JavaScript 数据类型？哪些存储在堆里哪些在栈里？你刚才说到栈后进先出，哪种数据结构先进先出？
**JavaScript 数据类型：**字符串，数字，布尔，Null，Undefined，数组，对象

JavaScript的数据类型分为两大种：

**基本类型：**Undefined、Null、Boolean、Number 和 String，这5中基本数据类型可以直接访问，他们是按照值进行分配的，存放在栈(stack)内存中的简单数据段，数据大小确定，内存空间大小可以分配。

**引用类型：**即存放在堆(heap)内存中的对象，变量实际保存的是一个指针，这个指针指向另一个位置。

**堆：**队列优先,先进先出；

**栈：**先进后出；


## JavaScript 作用域？
详解JavaScript作用域:http://blog.csdn.net/liuyan19891230/article/details/50417235
- 全局作用域
- 函数作用域
- let块级作用域
- 嵌套函数形成作用域链，由内向外查找，作用域链执行前就已经形成


## 事件流，事件代理，点击一个 div 里面的一系列 li 弹出它的 innerHTML 怎么做？ li 里面还有子元素，比如 span 怎么处理？
**DOM2事件流：** 捕获阶段 -> 目标阶段 -> 冒泡阶段
事件委托
```js
var list = divEle.querySelectorAll('ul li');
divEle.addEventListener('click',function (e){
  var ev = e || window.event;
  var target = ev.target || ev.srcElement;
  for (let i = 0, len = list.length; i < len; i++){
    if (list[i] == target){
      alert(target.innerHTML);
    }
  }
});
```
闭包
```js
var myul = document.getElementsByTagName("ul")[0];
var list = myul.getElementsByTagName("li");

function foo(){
    for(var i = 0, len = list.length; i < len; i++){
        var that = list[i];
        list[i].onclick = (function(k){
            var info = that.innerHTML;
            return function(){
                alert(k + "----" + info);
            };
        })(i);
    }
}
foo();
```

## 从哪些方面提高网站的渲染速度？ 你刚才提到 GZip，具体怎么做？
1. 内容方面
 - 减少http请求
 - 代码压缩
 - js代码写在</body>之前
 - 浏览器缓存（cookie/sessionStorage/localStorage）
 - 将静态资源放置在子域名下，实现并行下载数目增加
 - 缓存ajax结果
 - 减少DOM节点数

2. 服务器方面
 - cdn加速
 - gzip压缩

3. js
 - 引用压缩过的库（.min）
 - 减少操作DOM节点，必要时将节点缓存起来（离线更新）；
 - 少用递归或者用尾递归优化
 - 减少全局变量
 - 懒加载
 - 预加载

4. css
 - 精简css代码的编写，减少嵌套层次
 - 使用sprite图
 - 尽量采用简写
 - 用link代替@import
 - 动画要用在脱离文档流的元素上

5. 图片处理
 - 图片一般要压缩到小于200k（banner等）
 - 可将资源放至子域名下
 - 用iconfont代替小图标

## 301 和 302 区别？ 304 含义？304 原理？501 和 502 区别？
- 301：永久性重定向，302：临时性重定向
- 304：命中协商缓存
- 501：服务器不具备完成请求的功能。例如，服务器无法识别请求方法时可能会返回此代码
- 502：服务器暂时不可用，有时是为了防止发生系统过载

## git 用过是吧，git pull 和 git fetch 区别？哪个命令可以重命名分支？
- git fetch只会将本地库所关联的远程库的commit id更新至最新
- git pull会将本地库更新至远程库的最新状态
- 重命名分支： git branch (-m | -M) <oldbranch> <newbranch>：

## 前端打包工具都用过哪些，除了 webpack 呢？webpack 和 gulp有什么不同？
- gulp强调的是前端开发的工作流程，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。简单说就一个Task Runner。
- webpack是一个前端模块化方案，更侧重模块打包，我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。

## 原生的 DOM 操作都有什么？增删改查都是哪些命令？
原生DOM操作方法小结：https://www.cnblogs.com/springJournal/p/5736984.html
JavaScript常见原生DOM操作API总结：https://www.cnblogs.com/liuxianan/p/javascript-dom-api.html
```
Document.createElement() // 创建元素

Element.removeAttribute() // 从元素中删除指定的属性

Element.removeChild(）// 删除子元素

Element.innerHTML // 设置或获取描述元素后代的HTML语句

Document.getElementById() // 返回对拥有指定 id 的第一个对象的引用
Document.getElementsByTagName() // 返回带有指定标签名的对象集合
Document.getElementsByName() // 返回带有指定名称的对象集合
Document.getElementsByClassName() // 返回一个节点列表（数组），包含了所有拥有指定 class 的子元素
attribute.getAttribute()
```

## 说一下闭包。闭包有什么缺点？
* 背景
 - 局部变量不能共享和长久保存，全局变量会造成全局污染，而闭包避免了这两个问题。
 - js 作用域是函数作用域。
 - 闭包就是一个函数引用另外一个函数的变量。


* 使用场景 http://blog.csdn.net/yanghua_kobe/article/details/6780181
 - setTimeout 调用。setTimeout 的第一个参数为函数，如果要向这个函数传参数，可以定义一个有参数函数并
 返回一个无参函数。
 - 将函数关联到对象的实例方法，一个 javascript 对象被封装用来参与一个特定 DOM 元素的交互，将对象和方法名作为
 参数传递给一个函数，它返回一个函数，在这个函数内部执行并返回对象的该方法，其实就是事件绑定。
 - 封装相关的功能集，多个函数共享一个变量，为了避免全局污染，可用闭包声明一个自执行函数。


## tcp 与 udp 区别？
http://blog.csdn.net/li_ning_/article/details/52117463


## promise原理？
https://mengera88.github.io/2017/05/15/promise%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/
https://mengera88.github.io/2017/05/18/Promise%E5%8E%9F%E7%90%86%E8%A7%A3%E6%9E%90/
https://segmentfault.com/a/1190000009478377

主要使用了设计模式中的观察者模式：

* 通过Promise.prototype.then和Promise.prototype.catch方法将观察者方法注册到被观察者Promise对象中，同时返回一个新的Promise对象，以便可以链式调用。

* 被观察者管理内部pending、fulfilled和rejected的状态转变，同时通过构造函数中传递的resolve和reject方法以主动触发状态转变和通知观察者。

## JS中bind方法与函数柯里化？
```js
function bind(fn,context){
  return function (){
    return fn.apply(context,arguments);
  }
}
```

## css 清除浮动与bfc，两列布局?
CSS清除浮动大全共8种方法: http://www.jb51.net/css/173023.html

如何去除浮动？

方法一：使用一个空的div

方法二：overflow:hidden

方法三： display:inline-block;

方法四： position:absolute;

方法五：float:left;

方法六： zoom:1

方法七：after伪类+content方式

BFC:一个容器，提供了布局，里面与外面无关。
https://www.cnblogs.com/nujufoul/p/7092520.html
https://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html
bfc的特性：
     内部的Box会在垂直方向上一个接一个的放置。
     垂直方向上的距离由margin决定
     bfc的区域不会与float的元素区域重叠。
     计算bfc的高度时，浮动元素也参与计算
     bfc就是页面上的一个独立容器，容器里面的子元素不会影响外面元素。
触发bfc的元素：
      根元素
      float的值不为none
      overflow的值不为visible
      display的值为inline-block、table-cell、table-caption
      position的值为absolute或fixed。

## 数组方法map和reducer区别？
- arr.map(callback[,thisArg])：处理每个元素，不改变原数组，返回新数组。
```js
arr.map((x) => x*2);
```
- arr.reduce(callback[,initialValue])：对数组元素进行累积运算，返回元素运算后的结果，不改变原数组。
```js
// 求和
[1,2,3,4,5].reduce(function (accumulate, value, index, arr){
  return accumulate + value;
}, 0);
```

## 进程与线程的区别？
终于有个我会的了，这个显然想问你js的运行机制。先介绍了下进程与线程。

一个浏览器是一个进程，虽然js是单线程的，但是浏览器是多线程的，v8引擎也是多线程的，比如有渲染线程，有处理请求的线程。

然后说说任务队列，eventloop。没有理解很深也不敢往下说。

事件循环可以看下这个 https://github.com/ccforward/cc/issues/47

## geohash基本原理？
https://www.cnblogs.com/tgzhu/p/6204173.html

## 怎么实现登录时"记住我"的功能？
cookie

## 一个浮动的div后面又跟了一个div，在页面上是怎么布局的？
重叠覆盖。
解决：清除浮动或设置包围盒高度。


## 获取页面元素位置与宽高？
- element.clientWidth = content + padding
- element.clientHeight = content + padding
- element.getBoundingClientRect() 返回值情况
  * left:包围盒左边 border 以外的边缘距页面左边的距离
  * right:包围盒右边 border 以外的边缘距页面左边的距离
  * top:包围盒上边 border 以外的边缘距页面顶部的距离
  * bottom:包围盒下边 border 以外的便于距页面顶部的距离
  * width: content + padding + border
  * height: content + padding + border
  * 注意，设置外边距时外边距合并的情况

## requestAnimationFrame 原理？是同步还是异步？
异步，传入的函数在重绘之前调用

- 页面是否可见
   当页面被最小化或者被切换成后台标签页时，页面为不可见，浏览器会触发一个 visibilitychange事件,并设置document.hidden属性为true；切换到显示状态时，页面为可见，也同样触发一个 visibilitychange事件，设置document.hidden属性为false。

- 动画帧请求回调函数列表
  每个Document都有一个动画帧请求回调函数列表，该列表可以看成是由< handle, callback>元组组成的集合。其中handle是一个整数，唯一地标识了元组在列表中的位置；callback回掉函数，形参为一个时间值的函数（该时间值为动画函数每次开始执行距离第一次执行的毫秒数）。

```
requestAnimationFrame方法，总结起来，每次调用这个方法时会简单的发生两件事（浏览器处理过程）如下：

   1.首先要判断document.hidden属性是否为true,就是浏览器开着才会执行。

   2.浏览器会清空上一轮的动画函数，这个怎么理解呢？就是说Handle=requestanimatonframerequest(函数名);这一句话调用一次后就被浏览器吃掉了。

   3.这个方法返回的handle值会和动画函数，以这样的方式:< handle, callback>  进入到----动画帧请求回调函数列；

   4.浏览器会遍历动画帧请求回调函数列表，根据handel的值大小，依次去执行相应的动画函数；

所以，正确的requestanimatonframerequest其实应该是不断的递归
```

- http://web.jobbole.com/91578/
- https://my.oschina.net/bghead/blog/850692
- http://www.zhangxinxu.com/wordpress/2013/09/css3-animation-requestanimationframe-tween-%E5%8A%A8%E7%94%BB%E7%AE%97%E6%B3%95/


## requestAnimationFrame 与 setTimeout 比较？
setTimeout缺点：
- setTimeout 时间不准确
- setTimeout 容易丢帧，造成动画卡顿

requestAnimationFrame优点：
- requestAnimationFrame 由系统来决定回调函数的执行时机，步伐跟着系统的刷新步伐走。它能保证回调函数在屏幕每一次的刷新间隔中只被执行一次，这样就不会引起丢帧现象，也不会导致动画出现卡顿的问题。
- CPU节能：页面不可见时 requestAnimationFrame 会暂停，而 setTimeout 会执行，浪费系统资源
- 函数节流：在高频率事件(resize,scroll等)中，为了防止在一个刷新间隔内发生多次函数执行，使用requestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销。


## js事件机制？点击屏幕上一个按钮，事件是如何传播的？（存疑）
捕获 -> 冒泡

## 下面代码输出结果？为什么？

```js
Function.prototype.a = 'a';
Object.prototype.b = 'b';
function Person(){};
var p = new Person();
console.log('p.a: '+ p.a); // p.a: undefined
console.log('p.b: '+ p.b); // p.b: b
```

## 下面代码输出结果？为什么？

```js
const person = {
  mingzi: 'menglinghua',
  say: function (){
    return function (){
      console.log(this.mingzi);
    };
  }
};
person.say()(); // undefined
```

```js
const person = {
  mingzi: 'menglinghua',
  say: function (){
    return () => {
      console.log(this.mingzi);
    };
  }
};
person.say()(); // menglinghua
```

## 下面代码输出结果？为什么？

```js
setTimeout(() => console.log('a'), 0);
var p = new Promise((resolve) => {
  console.log('b');
  resolve();
});
p.then(() => console.log('c'));
p.then(() => console.log('d'));
console.log('e');
// 结果：b e c d a
// 任务队列优先级：promise.Trick()>promise的回调>setTimeout>setImmediate
```
```js （存疑）
async function async1() {
    console.log("a");
    await  async2(); //执行这一句后，await会让出当前线程，将后面的代码加到任务队列中，然后继续执行函数后面的同步代码
    console.log("b");

}
async function async2() {
   console.log( 'c');
}
console.log("d");
setTimeout(function () {
    console.log("e");
},0);
async1();
new Promise(function (resolve) {
    console.log("f");
    resolve();
}).then(function () {
    console.log("g");
});
console.log('h');
// 直接在控制台中运行结果：      d a c f h g b e
// 在页面的script标签中运行结果：d a c f h b g e
```

## js bind 实现机制？手写一个 bind 方法？（存疑）
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind
```js
if (typeof Function.prototype.bind === "undefined"){
  Function.prototype.bind = function (thisArgs){
    var fn = this,
        slice = Array.prototype.slice,
        args = slice.call(arguments, 1);
    return function (){
      return fn.apply(thisArgs, args.concat(slice.call(arguments)));
    }
  }
}
```

## 实现 vue 中的 on,emit,off,once，手写代码。

```js
var EventEmiter = function (){
  this._events = {};
};
EventEmiter.prototype.on = function (event, cb){
  if (Array.isArray(event)){
    for (let i = 0, l = event.length; i < l; i++){
      this.on(event[i], cb);
    }
  } else {
    (this._events[event] || (this._events[event] = [])).push(cb);
  }
  return this;
};
EventEmiter.prototype.once = function (event, cb){
  function on () {
    this.off(event, cb);
    cb.apply(this, arguments);
  }
  on.fn = cb;
  this.on(event, on);
  return this;
};
EventEmiter.prototype.off = function (event, cb){
  if (!arguments.length){
    this._events = Object.create(null);
    return this;
  }
  if (Array.isArray(event)){
    for (let i = 0, l = event.length; i < l; i++){
      this.off(event[i],cb);
    }
    return this;
  }
  if (!cb){
    this._events[event] = null;
    return this;
  }
  if (cb){
    let cbs = this._events[event];
    let i = cbs.length;
    while(i--){
      if (cb === cbs[i] || cb === cbs[i].fn){
        cbs.splice(i, 1);
        break;
      }
    }
    return this;
  }
};
EventEmiter.prototype.emit = function (event){
  let cbs = this._events[event];
  let args = Array.prototype.slice.call(arguments, 1);
  if (cbs){
    for (let i = 0, l = cbs.length; i < l; i++){
      cbs[i].apply(this,args);
    }
  }
};
```

## 用 js 实现双链表，手写代码？

## vue 的双向绑定机制？详细介绍。

## 哪些操作会引起浏览器重绘和重排？
- postion:absolute; left:100px;会不会引起？ 不会？
- translateX:100px;会不会引起？ 不会
- getBoundingClientRect会不会引起？
- getClientWidth、getClientHeight会不会引起？

http://caibaojian.com/css-reflow-repaint.html
https://github.com/wangning0/Autumn_Ning_Blog/blob/master/blogs/10-27/reflow&repaint.md

## 页面性能监测？


## js 实现发布订阅模式？

```js
// 由于这些成员对于任何发布者对象都是通用的，故将它们作为独立对象的一个部分来实现是很有意义的。那样我们可将其复制到任何对象中，并将任意给定对象变成一个发布者。
// 如下实现一个通用发布者，定义发布者对象……
let publisher = {
  subscribers: {
    any: []
  },
  subscribe: function (fn, type = `any`) {
    if (typeof this.subscribers[type] === `undefined`) {
      this.subscribers[type] = [];
    }
    this.subscribers[type].push(fn);
  },
  unSubscribe: function (fn, type = `any`) {
    let newSubscribers = [];
    this.subscribers[type].forEach((item, i) => {
      if (item !== fn) {
        newSubscribers.push(fn);
      }
    });
    this.subscribers[type] = newSubscribers;
  },
  publish: function (args, type = `any`) {
    this.subscribers[type].forEach((item, i) => {
      item(args);
    });
  }
};

```

## js 操作 Class?
```js
/*
  Element.classList 只读
  Element.className 可读可写，空格分割的字符串
  Element.setAttribute('class', elm.getAttribute('class'))
 */
function addClass(el, className){
   if(!hasClass(el, className)){
     el.className += ' ' + className;
     console.log(el.className);
   }
}
function removeClass(el, className){
   if (hasClass(el, className)){
     var arr = el.className.split(' ');
     var index = arr.indexOf(className);
     arr.splice(index, 1);
     el.className = arr.join(' ');
     console.log(el.className);
   }
}
function hasClass(el, className){
  var classarr = el.className.split(' ');
  return classarr.indexOf(className) === -1 ? false : true ;
}
```

## 用promise手写ajax？
```js
function myAjax(){
  return new Promise(function (resolve, reject){
    var xhr = new XMLHttpRequest();
    xhr.open('GET', url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
}
```

## 手写 JSONP 实现？
```js
(function (window, document){
  "use strict";
  var jsonp = function (url ,data, callback){
     // 处理 data
     var dataString = url.indexOf('?') === -1 ? '?' : '&';
     for (var key in data ){
       if (data.hasOwnProperty(key)){
         dataString += key + '=' + data[key] + '&';
       }
     }
     // 生成 callbackFn123
     var callbackFnName = 'my_jsonp_cb' + Math.random().toString().replace('.',' ');
     dataString += 'callback=' + callbackFnName;
     // 创建 script 标签
     var scriptEle = document.createElement('script');
     scriptEle.src = url + dataString;
     // 挂载回调函数
     window[callbackFnName] = function (data){
       callback(data);
       // 处理完回调函数的数据之后，删除jsonp的script标签
       document.body.removeChild(scriptEle);
     }
     // append 到页面中
     document.body.appendChild(scriptEle);
  };
  window.jsonp = jsonp;
})(window, document);
```

## 对数组[1,2,3,4,5,'6',7,'8','a','b','z']进行乱序？
```js
[1,2,3,4,5,'6',7,'8','a','b','z'].sort(() => {
  return Math.random() > 0.5;
});
```


## 判断一个数是否是 NaN 类型？

```js
function isNaNFunc (value){
  return value !== value;
}
// 或者
function isNaNFunc (value){
  return Number.isNaN(value);
}
```

## Number.isNaN(value) 与 isNaN(value) 区别？
1. isNaN 会对 value 进行转换，获取 Number(value) 的值，如果返回 NaN，则为 true，否则为 false;
2. Number.isNaN(value) 不会对 value 进行转换，所以只有当 value 为 NaN 时才返回 true，否则返回 false;

```js
Number.isNaN('blabla'); // false
isNaN('blabla'); // true
Number.isNaN(NaN); // true
```

```js
null == null // true
null === null // true
undefined == undefined // true
undefined === undefined // true
NaN == NaN // true
NaN === NaN // true
typeof NaN // "number"
typeof null // "object"
typeof undefined // "undefined"
// NaN 代表一个范围
// null、undefined 代表一个确切的值
```

## Vue 绑定机制？

## Vue 计算属性和普通属性区别？

## 实现 trim ？
```js
// 删除左右两端空格
String.prototype.trim =  function (){
  return this.replace(/(^\s*)|(\s*$)/g, '');
}
// 删除左边空格
String.prototype.trim =  function (){
  return this.replace(/(^\s*)/g, '');
}
// 删除右边空格
String.prototype.trim =  function (){
  return this.replace(/(\s*$)/g, '');
}
```

## 移动端适配计算方法？
屏幕宽度和设计图宽度比值

## 类继承时静态方法会不会继承？
不会，静态方法由类名直接调用。

## jquery attr 和 proper 区别？ jquery 源码？
都是： 获取匹配的元素集合中的第一个元素的属性的值 或 设置每一个匹配元素的一个或多个属性。
- 对于HTML元素本身就带有的固有属性，在处理时，使用prop方法。
- 对于HTML元素我们自己自定义的DOM属性，在处理时，使用attr方法。

## 将一个数划分成逗号相隔的数？

## let、var、const区别？let 会不会提升作用域？
- const：块级作用域；声明时必须初始化，不然报错；值不可变；
- let：块级作用域；不进行变量提升
- var：函数作用域；进行变量提升
```js
function a(){
  age = 1;
  let age;
  console.log(age);
}
function b(){
  age = 1;
  var age;
  console.log(age);
}
a(); // 报错
b(); // 1
```

## 斐波那契数列？

```js
// f(0) = 0;
// f(1) = 1;
// f(n) = f(n-1) + f(n-2)
function fb(n){
  if (n == 0) return 0;
  if (n == 1) return 1;
  return fb(n-1) + fb(n-2);
}
```


## css常用布局？

- 流动模型

  默认布局方式。典型特征是块状元素上下分布，行内元素左右分布。

- 浮动模型

  float：none | left | right

  clear: left | right | both | none

  元素默认不能浮动，设置 float 使其浮动。

  浮动元素的包含块是其最近的块级祖先元素，浮动元素会生成一个块级框，即使它是行内元素。

  浮动元素的边界不能超出包含块。左右不能互超。

  行内框与一个浮动元素重叠时，其边框、背景和内容都在该浮动元素‘之上’显示；

  块框与一个浮动元素重叠时，其边框和背景在该浮动元素'之下'显示，而内容在浮动元素之上显示。

  虽然从正常文档流中删除了，但还是会影响布局，其周围元素会环绕，并且外边距不能合并。

- 定位模型（层模型）

  position: static | relative | absolute | fixed | sticky

- flex

   **容器属性：**

   两轴：水平主轴 和 垂直交叉轴

   flex-direction: 决定轴向。四种：水平左端、水平右端、垂直上沿、垂直下沿；

   flex-wrap: 元素默认按一个轴排列，规定元素排不下时的方向。三种：不换行、换行第一行上、换行第一行下；

   flex-flow: flex-direction 和 flex-wrap 简写形式

   justify-content: 定义项目在水平轴对齐方向。 五种：左、右、居中、两端、均匀分布。

   align-itmes: 定义项目在垂直轴对齐方向。五种：上、中、下、第一行文字基线、占满。

   align-content: 定义了多根轴线的对齐方式。六种：交叉轴起点、交叉轴终点、交叉中中点、两端、均匀、占满。

   **元素属性：**

   order：定义排列顺序， 取值0，1，2...越小越靠前；

   flex-grow: 定义元素放大比例，取值0，1，2...有剩余空间时，0表示不放大；

   flex-shrink: 定义元素缩小比例，取值1，0, 2...空间不足时如何缩小；

   flex-basis: 在分配多余空间之前，项目占据的主轴空间。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间；

   flex: flex-grow、flex-shrink、flex-basis简写；

   align-self: 定义与其他元素不一样的对齐方式，可覆盖 align-items属性。

   参考1：http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html

   参考2：http://www.ruanyifeng.com/blog/2015/07/flex-examples.html

- grid

  flex是一个维度的，而grid是两个维度的网格式布局。

- 常用布局：三行布局（max-width自适应）；两栏布局（一边定宽，一边自适应）；三栏布局（圣杯、双飞翼）

- 圣杯与双飞翼区别：

   - 圣杯采用的是padding，而双飞翼采用的margin，解决了圣杯布局main的最小宽度不能小于左侧栏的缺点。
   - 双飞翼布局不用设置相对布局，以及对应的left和right值。
   - 通过引入相对布局，可以实现三栏布局的各种组合，例如对右侧栏设置position: relative; left: 190px; ,可以实现sub+extra+main的布局。

## css盒模型？

**定义：**content + padding + border + margin

**怪异盒模型：**IE, 即： width = content + padding + border；（IE6一下或IE7、8的怪异模式）

**标准盒模型：**即： width = content；

**box-sizing属性: **设置 `box-sizing: content-box | border-box` 统一盒模型种类；

**外边距合并：** 普通文档流块级框的垂直外边距会合并，行内、浮动、绝对定位元素之间的外边距不合并。设置 `*{padding:0;margin:0;}` 清除默认值；

**margin越界：**（第一个子元素的margin-top和最后一个子元素margin-bottom的值加在父元素上）应该给父元素加前置内容。

**盒模型画三角形：**
```css
{width:0;height:0;border:100px solid transparent;border-top:100px solid red;}
```

## css 居中？

- 水平居中

  子元素为行内元素：`text-align:center`；

  定宽块级元素：`margin:0 auto`；

  多个块级元素：`display:inline-block;` 或 `display:flex;`

- 垂直居中

  行内元素(要求父元素定高)：`padding-top = padding-bottom`
  或 `line-height: ***`
  或 `display:table-cell;vertical-align:middle`
  或 `display:flex;justify-content:center;flex-direction:colum;`

  行内元素(父元素不定高)：设置伪元素的高等于父容器的高，然后添加 `vertical-align:middle`

  块级元素（已知高度，父元素相对定位）：`position:absolute;height:100px;top:50%;margin-top:-50px;`

  块级元素（未知高度，父元素相对定位）：`position:absolute;top:50%;transform:translateY(-50%);`
   或 `display:flex;flex-direction:colum;justify-content:center;`

- 水平且垂直

  宽高固定：`width:300px;height:100px;padding:20px;position:absolute;top:50%;left:50%;margin: -70px 0 0 -170px`

  高宽不固定：`position:absolute;top:50%;left:50%;transform:translate(-50%, -50%);`
    或 `display:flex;justify-content:center;align-items:center;`

## CSS 选择器优先级怎么计算？
css 优先级由高到低顺序：!important > 内联样式 > id选择器 > 类 > 标签|属性|伪类 > *。

精确的计算是根据**特殊性值**来计算的，如果特殊性值相同，那么后定义的覆盖前面的。

内联、id、class、标签 赋予的权重分别是 1000、100、10、1，根据权重取舍元素css属性。

## css 动画的理解？

**transition**过渡是通过初始和结束两个状态的平滑过渡来实现简单动画。
包含四个属性：参与过渡的属性、持续时间、动画类型、延迟时间。

**animation**通过关键帧来实现更为复杂的动画。
包含属性：动画名、持续时间、过渡类型、延迟时间、循环、反向。


## css 动画 与 js 动画的比较？

webkit 内核浏览器的渲染线程分为主线程和 compositor 线程，js动画在主线程中完成，而css动画在修改以下属性时`仅触发composite，不触发layout、repaint`，这些属性有：`transform、
opacity、perspective`。

jQuery动画慢的原因：1、布局颠簸，复杂操作导致过多的重绘和重排；2、消耗内存，阻碍线程。

CSS3动画好的原因：1、优化DOM操作；2、开启3D加速，但会消耗内存。

总之：js动画灵活兼容性好，css动画则简单、某些情况下性能好，但缺乏灵活性和兼容性。

requestAnimationFrame：会把每一帧中的所有DOM操作集中起来，在一次重绘或重排中完成，并且时间间隔紧随浏览器的刷新频率，每秒60帧。在隐藏或不可见元素中，requestAnimationFrame将不会进行重绘或重排。
setTimeout 存在时间不准确和丢帧问题。

## BFC?

css中盒模型布局的css渲染模式。布局方式属于常规文档流。
元素对其；外边距折叠；包含浮动；防止文字环绕；多列布局。

https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context

https://segmentfault.com/a/1190000006740129

http://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html

http://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/

## px/em/rem 的区别?

  都是相对长度。

  px 相对屏幕分辨率而言；

  em 值不固定，会继承父级元素的字体大小；

  rem 相对的只是HTML根元素大小。

## css 预处理器？ // TODO...
sass、less、postcss

## link 和 @import 区别？

- link 是 html 标签，@import 是 css 提供；

- link 在页面加载时加载，@import 引用的 css 会在页面加载完才开始加载；

- link 优先级高于 @import；

- @import 兼容性不好 IE5以上；

## position的值？应用场景？
- static: 默认，正常文档流。top、right、left、bottom、z-index属性无效。
- relative: 相对布局，相对自身正常位置，自身位置仍然保留。
- absolute: 绝对布局，相对于第一个包含块（position不为static），脱离文档流，自身位置不保留，形成新层。
- fixed: 固定布局，相对于视口坐标，脱离文档流，自身位置不保留，不随滚动条改变位置。
- sticky: 粘性定位，正常情况下按照正常文档流定位。当滚动到该元素的位置时，元素的定位（相对于包含块）发生改变。

## css选择器？可以继承的属性？优先级算法？css3新增伪类元素？

**选择器：**id、class、标签、相邻（h1 + p）、子选择器(ul > li)、后代、通配符、属性、伪类；

**可继承：**font-size font-family color ul li dl dd dt；

**不可继承：**border padding margin width height；

**优先级：** !important > id > 类 > 其他； 内联样式大于css文件样式；文件后面样式大于前面样式；

## doctype 作用？严格模式与混杂模式？

 **doctype** 声明在文档最前面，告知浏览器用什么文档类型和规范来解析这个文档；

 **严格模式**是以浏览器支持的最高规格和标准来运行；

 **混杂模式**是以向后兼容方式呈现；

 doctype不存在或格式不正确会导致浏览器以混杂模式呈现。

## 行内元素？块级元素？空元素？

css 规范规定，每个元素都 `display` 属性，确定该元素类型，每个元素都有默认的 display 值，如 div 默认是 block 为块级元素，span 默认 inline 为行内元素。

**块级元素：**独占一行；可以设置 width,height, margin, padding, border;

**行内元素：**和其他元素在同一行；不能设置宽高，可以设置 margin-left 、 margin-right，不能设置 margin-top,margin-bottom；

**行内元素有：**a b span img input select strong

**块级元素有：**div p ul ol li h1 h2 h3 h4 dl dt p

**空元素（替换元素）：**img input link meta  少见的：area base col ...

## iframe缺点？

- 阻塞主页面的 onload 事件。

- iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以影响页面并行加载。

- 如果需要使用 iframe，最好用 js 动态给其加 src 属性。

## 去除inline-block元素间间距的N种方法？
http://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-%E5%8E%BB%E9%99%A4%E9%97%B4%E8%B7%9D/


## JavaScript 数据类型分哪些？

**基本类型：** Number、String、Boolean、Undefined、Null、Symbol(ES6)、Object

**派生类型：** Function、Array、Map、Set


## JavaScript 内置对象？

Date、Array、Math、Number、Boolean、String、RegExp、Function、Map、Set、WeakMap、WeakSet


## typeof 操作符结果？

**可能的值：** "undefined" | "boolean" | "string" | "number" | "object" | "function" | "symbol"

```js
  typeof null === 'object'；

  typeof Array === 'object';

  typeof {} === 'object';

  typeof new Person() === 'object';

  typeof new Function() ==== 'function';

  typeof Object === 'function'；

  typeof Function === 'function'；
```

## 原型和原型链?

js中一切皆对象，分为普通对象和函数对象。

js中每个对象（函数、数组、数字...）都有 `__proto__` 属性，但只有函数对象才有 `prototype` 属性。

Person.prototype 就是原型对象。

js创建(new)对象时，将 `person.__proto__ = Person.prototype`。

原型和原型链是JS实现继承的一种模型。

原型链的形成是真正是靠`__proto__ `而非 `prototype`。


## 闭包及常用的场景、作用域、单例模式?

* 背景
 - 局部变量不能共享和长久保存，全局变量会造成全局污染，而闭包避免了这两个问题。
 - js 作用域是函数作用域。
 - 闭包就是一个函数引用另外一个函数的变量。


* 使用场景 http://blog.csdn.net/yanghua_kobe/article/details/6780181
 - setTimeout 调用。setTimeout 的第一个参数为函数，如果要向这个函数传参数，可以定义一个有参数函数并
 返回一个无参函数。
 - 将函数关联到对象的实例方法，一个 javascript 对象被封装用来参与一个特定 DOM 元素的交互，将对象和方法名作为
 参数传递给一个函数，它返回一个函数，在这个函数内部执行并返回对象的该方法，其实就是事件绑定。
 - 封装相关的功能集，多个函数共享一个变量，为了避免全局污染，可用闭包声明一个自执行函数。


* 注意事项
因为变量被引用，所以不会被垃圾回收，闭包占用内存、消耗性能，使用要小心。

## js 异步的理解？

js异步编程的4种方法：http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html

js异步的理解：http://blog.csdn.net/ebay/article/details/50952294


js运行是采用单线程的。决定 JavaScript 是否多线程执⾏行是 Runtime。JavaScript 的 Runtime 有如chrome 中V8、Node.js 等。

为什么会单线程执行，有些理由还是很有道理的：设计GUI 框架，多线程的方式抢占资源是很容易造成死锁的，特别是在操作 DOM 上，如果两个线程同时执行，一个执行删除元素，一个执行添加元素，页面就会造成混乱，作为和人直接接触的图形界面，如果出现这种现象，基本上就算是反常识了。

JavaScript 的 Runtime 将不耗时的计算指令在指定的一个主线程中不间断执行，其它耗时的任务，Runtime 会利用回调交给浏览器，由浏览器另行开辟线程来执行，最后将结果集返回给主线程就可以了。

js通过**事件循环**和**消息队列**来执行异步操作的。

js中常用的异步有：
- 凡是带有回调函数作为参数的 API 都是异步的，如 DOM事件、 setTimeOut、Ajax请求等
- 发布/订阅模式
- promise
- generator（ES6）
- async/await(ES7)

**回调和异步不等价**，没有回调，JavaScript 仍然可以是异步，有回调，也可能是同步的！以promise为证，promise 本质是为了解决回调嵌套的问题，优化代码结构，若它本身没有继承并实例化一个异步API，它并不会异步执行。

JavaScript 实现非阻塞运行的方式是异步，异步则使用到浏览器的线程来执行比较耗时的API，而JavaScript 本身仍是单线程。


## JS继承的实现方式?
- 构造函数继承、原型继承、拷贝继承、组合继承...
- 寄生组合继承：通过寄生方式，砍掉父类的实例属性，这样，在两次调用父类构造的时候，不会构造两次，避免了组合继承的问题

  ```js
    function Cat (name){
       Animal.call(this);
       this.name = name || 'tom';
    }
    (
    function (){
      // 创建一个没有实例方法的类
      var Super = function (){};
      Super.prototype = Animal.prototype;
      // 将实例作为子类的原型
      Cat.prototype = new Super();
    }
    )();
  ```

  单继承：
  ```js
  function Animal (){

  }
  function Cat (){
    Animal.call(this);
  }
  Cat.prototype = Object.create(Animal.prototype);
  Cat.prototype.constructor = Cat;
  ```
  多继承：
  ```js
  function  MyClass(){
    SuperClass.call(this);
    OtherSuperClass.call(this);
  }
  MyClass.prototype = Object.create(SuperClass.prototype);
  Object.assign(MyClass.prototype, OtherSuperClass.prototype);
  MyClass.prototype.constructor = MyClass;
  ```

## JavaScript的节流和防抖?

**函数节流**是指一定时间内js方法只跑一次。比如人的眨眼睛，就是一定时间内眨一次。这是函数节流最形象的解释。

**函数防抖**是指频繁触发的情况下，只有足够的空闲时间，才执行代码一次。如生活中的坐公交，就是一定时间内，如果有人陆续刷卡上车，司机就不会开车。只有别人没刷卡了，司机才开车。

 对于频繁的事件、频繁的ajax请求通过设置 setTimeout 来实现节流和防抖。


## JavaScript的事件?

js 是通过消息队列来处理事件的。

**事件类型：** 捕获型事件、冒泡型事件、DOM事件流（同时支持前两种事件模型，默认冒泡，通过设置第三个参数为true设置捕获型）。

**DOM2事件流：** 捕获阶段 -> 目标阶段 -> 冒泡阶段。事件先从 document 往下流，在冒泡时触发目标事件，然后事件继续冒泡到跟节点。

**事件处理程序：**
- DOM0 级事件处理程序

```html
<input type="button" value="ok" onclick="alert('clicked！')"></input>
```

或

```js
var btn = document.getElementById('btn');
btn.onclick = function (e){
  alert(this.id);
}
```

- DOM2 级事件处理程序
```
DOM2级事件定义了两个方法用于处理制定和删除事件处理程序的操作：addEventListener 和 removeEventListener。
所有的DOM节点都包含这两个方法，并且都接收三个参数：事件类名、事件处理方法、一个布尔值。
布尔参数true表示在捕获阶段调用事件处理程序；false表示在事件冒泡阶段处理。
```

- IE 事件处理程序
```
实现了 DOM 两个类似的方法 attachEvent 和 detachEvent，这两个方法都接收两个相同的参数，事件处理程序名称和事件处理程序方法。
由于 IE 只支持事件冒泡，所以添加的程序会被添加到冒泡阶段。
```

- 跨浏览器的事件处理程序
```
跨浏览器的事件处理程序就是创建一个对象，存放用于添加、删除事件处理程序的方法。
方法接收三个参数：要操作的元素、事件名称、事件处理程序函数。
```

**事件对象：**`event.stopPropagation`阻止事件传播；`event.preventDefault`阻止默认行为；`event.target` 事件源;
`event.currentTarget` 当前绑定事件的元素。

**事件委托：** 将子元素的事件绑定到父元素上。优点：减少事件注册，节省内存；动态增加和修改子元素；


## ajax请求方式?

1. 创建请求对象(考虑__兼容性__)，`xhr = new XMLHttpRequest()` 或 `xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");`

2. 发送请求；
  - get：`xhr.open('GET','url?params',isAsync); xhr.send()`;
  - post：`xhr.open('POST','url',isAsync); xhr.send(data)`;
  - 在无法使用缓存、或更新服务器上的文件或数据、或传输大量数据时，用post。否则用get。

3. 获取服务器响应：`xhr.responseText` 和 `xhr.responseXML`;

4. 监听响应状态：`xhr.onreadystatechange` 事件。

   xhr.readyState 对象状态值:

     - 0（未初始化状态）对象已建立或已被 abort() 方法重置，尚未调用 open 方法。
     - 1（初始化状态）服务器连接已建立，open() 方法已经调用，但是 send() 方法未调用。请求还没有被发送。
     - 2（发送数据）send() 方法已调用,HTTP请求已发送到Web服务器。未接收到响应。
     - 3（数据传送中）所有响应头部都已经接收到。响应体开始接受但未完成。
     - 4（完成加载）HTTP响应已经完全接收。

   xhr.status 状态:
     - 200：‘ok’
     - 404: '未找到'


## js判断数据类型的方法?
 - `typeof`: 返回字符串形式，可以判断`function`类型，但判断数组、对象、null时都返回`object`，通过 `Object.prototype.toString`来解决。
 - `instanceof`: 判断已知对象类型， instanceof 后面必须为对象。适用于一些条件选择或分支。
 - `constructor`: 在类继承时会出错。
 - `prototype`: `Object.prototype.toString` 通用方法。
 - `$.type()`: 返回null、undefined、object、对象或类名。

## this指向的问题?
 - 一般情况下，this 在**定义时**是不能确定指向的，最终指向是**执行时**所在的对象。
 - 默认情况下，没有调用对象，this 指向 window；严格模式下，this 指向 undefined。
 - new 操作符、fn.call、fn.apply、fn.bind 可以改变 this 指向。
 - 箭头函数，this 指向是定义时所在的对象，而不是使用时所在的对象。


## new干了什么？

 创建一个空对象，this 变量引用该对象同时还继承了该函数的原型；

 属性和方法被加入到 this 引用的对象中；

 新创建的对象有 this 引用，并最后隐式返回 this;


## 跨域？JSONP原理和实现？CORS设置?

同源策略（同协议、域名、端口号）限制了 Ajax 请求。

- JSONP

  利用 JavaScript 标签的跨域能力

- CORS

  全称是"跨域资源共享"（Cross-origin resource sharing）。是 W3C 标准。
  CORS需要浏览器和服务器同时支持。整个CORS通信过程，都是浏览器自动完成，不需要用户参与。

  **简单请求：**一次请求，请求头包含`Origin`，请求成功，响应头包含`Access-Control-Allow-Origin`，否则，请求失败。
  `get head post`都是简单请求。

  **非简单请求**两次请求，先发送一次‘预检’请求（请求方法是OPTIONS，表示这个请求是用来询问的），头信息包含`Origin\Access-Control-Request-Method\Access-Control-Request-Headers`字段，预检请求成功，响应头包含`Access-Control-Allow-Origin`，否则失败。一旦预检请求成功，以后每次请求跟简单请求一样。

> CORS与JSONP的使用目的相同，但是比JSONP更强大。JSONP只支持GET请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。

- postMessage

  `targetWindow.postMessage(message, targetOrigin, [transfer]);`
   适用于通过`window.open` 或 `iframe` 建立的窗口间的通信。

- WebSocket
- document.domain + iframe
- 代理服务器


## 浅拷贝与深拷贝？

浅拷贝是改变引用，深拷贝递归进行，改变内存。

浅拷贝实现：
- Object.assign
- 简单复制语句

深拷贝实现：
- JSON.stringify 和 JSON.parse 实现。缺点是非json标准的无法拷贝，兼容性问题。
- 递归拷贝


## 数组去重?

- ES6实现：`[...new Set([1,2,3,1,'a',1,'a'])]`

- ES5实现：
```js
  [1,2,3,1,'a',1,'a'].filter(function(ele,index,array){
      return index === array.indexOf(ele)
  })
```
- 利用对象属性不能重复
- 利用 indexOf 以及 forEach

## js 常用的数组和对象操作属性和方法？

**数组方法：**

**创建：**
- `new Array(element0,element1,...)`或 `new Array(len)`
```js
var arr1 = new Array(7);
var arr2 = Array(7);
```
- Array.from(arrayLike, mapFn, thisArg)

  从一个类数组创建一个数组，注意` Array.from('foo') == ['f','o','o'];`

- Array.of(el0[,el1...])：根据传入参数创建一个数组
  ```js
  Array.of(7);// [7]
  Array.of(1,2,3);// [1,2,3]
  Array(7);// [,,,,,,,]
  Array(1,2,3); // [1,2,3]
  ```

**拷贝：**
- arr.slice([begin[,end]])：数组切片，包括 begin 不包括 end，不改变原数组，返回切片后的新数组，不传参数返回整个数组。

**查找：**
- arr.find(callback[,thisArg])：返回数组中**第一个**符合条件的元素的**值**。
- arr.findIndex(callback[,thisArg])：返回数组中**第一个**符合条件的元素的**索引**。
- arr.indexOf(searchElement[,fromIndex])：返回查找到的**第一个元素**的**索引**，从数组头部开始查找。
- arr.lastIndexOf(searchElement[,fromIndex])：返回查找到的**第一个元素**的**索引**，从数组尾部开始查找。

**遍历：**
- arr.forEach(callback[,thisArg])：遍历数组，返回 undefined。不会改变原数组。不能
停止 forEach 遍历（除非抛出异常）。可以用 for...of 来实现停止。

**修改原数组：**
- arr.push(element1,element2,...)：往数组**尾部**添加元素，返回数组的新长度
- arr.pop()：移除数组最后一个元素，并返回该元素
- arr.unshift(element1,element2,...)：往数组**头部**添加元素，返回数组的新长度
- arr.shift()：移除数组头部第一个元素，并返回该元素
- arr.reverse()：将数组倒转，返回新数组，改变原数组
- arr.sort([compareFunction])：对数组排序，并返回排序后的数组，原数组也被改变。

  compareFunction 用于指定排序规则，不指定则默认按 Unicode（字符串） 顺序。
  ```js
  //comparse 形式
  function compare(a,b){
    if (a > b) return 1;
    if (a < b) return -1;
    return 0;
  }
  // 例子
  function compareNumbers(a,b){
    return a - b;
  }
  ```
- arr.splice(start[,deleteCount[,item1,item2...]])：移除并添加新元素，修改原数组，返回
  被删除元素组成的数组。
  ```js
  // 插入是在 start 之前插入
  // 删除是从 start 开始删除，包括 start
  ```

**处理返回新结果：**
- arr.concat()：数组连接，不改变原数组
  ```js
  var arr1 = [1,2,3];
  var arr2 = [4,5,6];
  var arr3 = [7,8,9];
  var narr1 = arr1.concat(arr2); // narr1[1,2,3,4,5,6]
  var narr2 = arr1.concat(arr2,arr3); // narr2[1,2,3,4,5,6,7,8,9]
 ```
- arr.filter(callback[,thisArg])：过滤出符合条件的元素，不改变原数组，返回新数组。
- arr.join([separator])：将数组元素按分隔符拼接成字符串返回，默认分隔符为逗号。
- arr.map(callback[,thisArg])：处理每个元素，不改变原数组，返回新数组。
```js
arr.map((x) => x*2);
```
- arr.reduce(callback[,initialValue])：对数组元素进行累积运算，返回元素运算后的结果，不改变原数组。
```js
// 求和
[1,2,3,4,5].reduce(function (accumulate, value, index, arr){
  return accumulate + value;
}, 0);
```
- arr.reduceRight(callback[,initialValue]): arr.reduce 的逆操作

**判断：**
- Array.isArray(obj)：判断是否是数组，返回 true 或 false
- arr.includes(searchElement[,fromIndex])：数组是否包含给定元素，返回 true or false。
- arr.every(callback[,thisArg])：检测是否**所有元素**满足条件，返回 true or false。
- arr.some(callback[,thisArg])：检测**至少有一个**满足条件，返回 true or false。

**字符串方法：**
- str.charAt(index): 得到索引为 index 处的字符。index 默认为零，范围 0 到 len -1，超出返回空。
- str.charCodeAt(index): 返回指定位置的字符的 Unicode 编码。这个返回值是 0 - 65535 之间的整数。
- str.concat(string2[, string3, ..., stringN]): 连接字符串，返回连接后的新字符串。
- str.includes(searchString[, position]): 字符串是否包含某个子串，返回 true or false。
- str.indexOf(searchValue[, fromIndex]): 返回字符串中某个子串的位置，从前往后找，无则返回 -1。
- str.lastIndexOf(searchValue[, fromIndex]): 返回字符串中某个子串的位置，从后往前找，无则返回 -1。
- str.replace(regexp|substr, newSubstr|function): 字符串替换。
- str.slice(beginIndex[, endIndex]): 字符串切片。
- str.split([separator[, limit]]): 字符串分割。
- str.substr(start[, length]): 子串。
- str.substring(indexStart[, indexEnd]): 子串。
- str.trim(): 去除字符串首尾空格。


**对象方法：**

**对象属性描述符：**
- configurable：可配置性。默认值为`false`，设为`true`表示可以修改属性描述也可以通过 `delete` 删除属性。
- enumerable：可枚举性。默认值为`false`，设为`true`表示可以通过 `for..in` 循环访问到。
- value：属性的值。默认值为`undefined`，可设置为任何 js 类型，如 number、object、function。
- writable：是否可写。默认值为`false`，设为`true`则可以改变属性值。
- get：getter函数。默认值为`undefined`，如果定义，它的返回值将作为属性值。
- set：setter函数。默认值为`undefined`，如果定义，传入的值将用于计算属性值。

**创建对象：**
- 对象字面量
- new Object()
- Object.create()

**静态属性或方法：**
- Object.assign(target, ...sources)：浅复制，返回 target obj。
- Object.create(proto[, propertiesObject])：通过指定原型和属性创建一个新对象，并返回它。
  常用于继承。
- Object.defineProperties(obj, props)：新增或修改一个对象的多个属性，并返回这个对象，原始对象也被修改。
- Object.defineProperty(obj, prop, descriptor)：新增或修改对象的某个属性，并返回这个对象，原始对象也被修改。
- Object.freeze(obj)：冻结一个对象，这个对象的所有属性包括原型属性都不可更改。
- Object.getOwnPropertyDescriptor(obj, prop)：返回对象某个属性的描述符。
- Object.getOwnPropertyDescriptors(obj)：返回对象所有属性的描述符。
- Object.getOwnPropertyNames(obj)：返回对象自有属性名数组。（包括不可枚举属性，不包括 Symbol，不包括 prototype）。
- Object.getOwnPropertySymbols(obj)：返回对象自有的symbol属性名数组。
- Object.getPrototypeOf(obj)：返回对象的 prototype 对象。
- Object.is(value1,value2)：比较对象是否相等

```js
Object.is(undefined,undefined);// true
undefined == undefined;// true
undefined === undefined;// true

Object.is(null,null);// true
null == null;// true
null === null;// true

Object.is(true,true);Object.is(false,false);// true
true == true; false == false;// true
true === true; false === false;// true

Object.is('string','string'); // true
'string' == 'string';// true
'string' === 'string';// true

Object.is({},{});// false
{} == {};// false
{} === {};// false

Object.is(+0,+0); // true
+0 == +0;// true
+0 === +0;// true

Object.is(-0,-0); // true
-0 == -0;// true
-0 === -0;// true

Object.is(+0,-0); // false
+0 == -0;// true
+0 === -0;// true

Object.is(NaN,NaN); // true
NaN == NaN;// false
NaN === NaN;// false
```
- Object.seal(obj)：密封一个对象，不可新增和删除属性，但可修改属性。
- Object.setPrototypeOf(obj,prototype)：修改一个对象的原型属性。
- Object.keys();
- Object.values();

**实例属性或方法：**
- Object.prototype.hasOwnProperty(prop)：判断属性是否是对象自有属性，而不是继承的。
- Object.prototype.isPrototypeOf(object)：判读对象是否存在于另一个对象的原型中。
- Object.prototype.\_\_defineGetter\_\_()：在对象实例上改变 getter 访问函数。
- Object.prototype.\_\_defineSetter\_\_()：在对象实例上改变 setter 访问函数。
- Object.prototype.\_\_lookupGetter\_\_()：获得 getter 访问函数的引用。
- Object.prototype.\_\_lookupSetter\_\_()：获得 setter 访问函数的引用。

## 怎样添加、移除、移动、复制、创建和查找节点？

- 创建新节点： createDocumentFragment() createElement() createTextNode()
- 添加、移除、替换、插入：appendChild() removeChild() replaceChild() insertBefore()
- 查找：querySelect() querySelectAll() getElementById() getElementsByName() getElementsByTagName()

## es6-promise?

用于处理js中的一些异步过程。

1.初始化一个Promise对象，构造函数中有’resolve'和‘reject’参数，分别在成功和失败时执行。

2.一个Promise有以下状态：
    - pending:初始状态，既不是成功，也不是失败；
    - fulfilled:操作成功；
    - rejected:操作失败；

3.Promise实例有then和catch方法。


## es6-generator?

可以返回多次的函数。

用`*`号声明，函数内用 `yield` 关键字。

每调用一次next，则执行一次yield语句。

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen(); // "Generator { }"
g.next(); // {value:1,done:false}
g.next(); // {value:2,done:false}
```

## es6-fetch?

fetch接收两个参数，URL和请求options；

返回promise对象，可以通过 then 和 catch 分别处理成功和失败；

与ajax比较：
1. fetch不能停止；
2. 默认不带cookie；需配置credentials：’inclue'；
3. 服务器返回400、500 时并不会reject；
4. 不能获取状态；
5. 没有defer；

## JS模块化Commonjs,UMD,CMD规范的了解，以及ES6的模块化跟其他几种的区别，以及出现的意义？

- CommonJS：服务端加载，同步，Nodejs
- AMD：前端加载，RequireJs，异步加载，预加载（加载与执行同时发生）
- CMD：前端加载，Seajs，懒加载（先加载，需要时执行）
- UMD：AMD 和 CommonJS的糅合，解决跨平台；运行时
- ES6 Import、Export：通用；静态确定关系；（一个模块只加载一次，只执行一次，下次需要就从内存取，一个模块就是一个单例）

## 函数柯里化？以及说一下JS的API有哪些应用到了函数柯里化的实现？

这个我就说了一下函数柯里化一些了解，以及在函数式编程的应用，最后说了一下JS中bind函数和数组的reduce方法用到了函数柯里化。

## js 将数组排序并筛选出满足条件的元素组成新数组？
```js
var arr = [1,2,3,4,5,6];
var newarr = arr.sort((a,b) => a-b).filter((value) => value % 2 === 0);
```
