---
title: 前端面试-JavaScript
comments: true
date: 2018-01-30 23:38:11
tags:
  - javascript
categories:
  - 前端面试
---

## JavaScript
<!--more-->

### JavaScript 数据类型分哪些？

**基本类型：** Number、String、Boolean、Undefined、Null、Symbol(ES6)、Object

**派生类型：** Function、Array、Map、Set


### JavaScript 内置对象？

Date、Array、Math、Number、Boolean、String、RegExp、Function、Map、Set、WeakMap、WeakSet


### typeof 操作符结果？

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

### 原型和原型链?

js中一切皆对象，分为普通对象和函数对象。

js中每个对象（函数、数组、数字...）都有 `__proto__` 属性，但只有函数对象才有 `prototype` 属性。

Person.prototype 就是原型对象。

js创建(new)对象时，将 `person.__proto__ = Person.prototype`。

原型和原型链是JS实现继承的一种模型。

原型链的形成是真正是靠`__proto__ `而非 `prototype`。


### 闭包及常用的场景、作用域、单例模式?

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

### js 异步的理解？

js异步编程的4种方法：http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html

js异步的理解：http://blog.csdn.net/ebay/article/details/50952294


js运行是采用单线程的。决定JavaScript 是否多线程执⾏行是Runtime。JavaScript 的Runtime 有如chrome 中V8、Node.js 等。

为什么会单线程执行，有些理由还是很有道理的：设计GUI 框架，多线程的方式抢占资源是很容易造成死锁的，特别是在操作DOM 上，如果两个线程同时执行，一个执行删除元素，一个执行添加元素，页面就会造成混乱，作为和人直接接触的图形界面，如果出现这种现象，基本上就算是反常识了。

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


### JS继承的实现方式?
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

### JavaScript的节流和防抖?

**函数节流**是指一定时间内js方法只跑一次。比如人的眨眼睛，就是一定时间内眨一次。这是函数节流最形象的解释。

**函数防抖**是指频繁触发的情况下，只有足够的空闲时间，才执行代码一次。比如生活中的坐公交，就是一定时间内，如果有人陆续刷卡上车，司机就不会开车。只有别人没刷卡了，司机才开车。

 对于频繁的事件、频繁的ajax请求通过设置 setTimeout 来实现节流和防抖。


### JavaScript的事件?

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


### ajax请求方式?

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


### js判断数据类型的方法?
 - `typeof`: 返回字符串形式，可以判断`function`类型，但判断数组、对象、null时都返回`object`，通过 `Object.prototype.toString`来解决。
 - `instanceof`: 判断已知对象类型， instanceof 后面必须为对象。适用于一些条件选择或分支。
 - `constructor`: 在类继承时会出错。
 - `prototype`: `Object.prototype.toString` 通用方法。
 - `$.type()`: 返回null、undefined、object、对象或类名。

### this指向的问题?
 - 一般情况下，this 在**定义时**是不能确定指向的，最终指向是**执行时**所在的对象。
 - 默认情况下，没有调用对象，this 指向 window；严格模式下，this 指向 undefined。
 - new 操作符、fn.call、fn.apply、fn.bind 可以改变 this 指向。
 - 箭头函数，this 指向是定义时所在的对象，而不是使用时所在的对象。


### new干了什么？

 创建一个空对象，this 变量引用该对象同时还继承了该函数的原型；

 属性和方法被加入到 this 引用的对象中；

 新创建的对象有 this 引用，并最后隐式返回 this;


### 跨域？JSONP原理和实现？CORS设置?

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


### 浅拷贝与深拷贝？

浅拷贝是改变引用，深拷贝递归进行，改变内存。

浅拷贝实现：
- Object.assign
- 简单复制语句

深拷贝实现：
- JSON.stringify 和 JSON.parse 实现。缺点是非json标准的无法拷贝，兼容性问题。
- 递归拷贝


### 数组去重?

- ES6实现：`[...new Set([1,2,3,1,'a',1,'a'])]`

- ES5实现：
```js
  [1,2,3,1,'a',1,'a'].filter(function(ele,index,array){
      return index === array.indexOf(ele)
  })
```
- 利用对象属性不能重复
- 利用 indexOf 以及 forEach

### js 常用的数组和对象操作属性和方法？

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

### 怎样添加、移除、移动、复制、创建和查找节点？

- 创建新节点： createDocumentFragment() createElement() createTextNode()
- 添加、移除、替换、插入：appendChild() removeChild() replaceChild() insertBefore()
- 查找：querySelect() querySelectAll() getElementById() getElementsByName() getElementsByTagName()

### es6-promise?

用于处理js中的一些异步过程。

1.初始化一个Promise对象，构造函数中有’resolve'和‘reject’参数，分别在成功和失败时执行。

2.一个Promise有以下状态：
    - pending:初始状态，既不是成功，也不是失败；
    - fulfilled:操作成功；
    - rejected:操作失败；

3.Promise实例有then和catch方法。


### es6-generator?

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

### es6-fetch?

fetch接收两个参数，URL和请求options；

返回promise对象，可以通过 then 和 catch 分别处理成功和失败；

与ajax比较：
1. fetch不能停止；
2. 默认不带cookie；需配置credentials：’inclue'；
3. 服务器返回400、500 时并不会reject；
4. 不能获取状态；
5. 没有defer；

### JS模块化Commonjs,UMD,CMD规范的了解，以及ES6的模块化跟其他几种的区别，以及出现的意义？

- CommonJS：服务端加载，同步，Nodejs
- AMD：前端加载，RequireJs，异步加载，预加载（加载与执行同时发生）
- CMD：前端加载，Seajs，懒加载（先加载，需要时执行）
- UMD：AMD 和 CommonJS的糅合，解决跨平台；运行时
- ES6 Import、Export：通用；静态确定关系；（一个模块只加载一次，只执行一次，下次需要就从内存取，一个模块就是一个单例）

### 函数柯里化？以及说一下JS的API有哪些应用到了函数柯里化的实现？

这个我就说了一下函数柯里化一些了解，以及在函数式编程的应用，最后说了一下JS中bind函数和数组的reduce方法用到了函数柯里化。

### js 将数组排序并筛选出满足条件的元素组成新数组？
```js
var arr = [1,2,3,4,5,6];
var newarr = arr.sort((a,b) => a-b).filter((value) => value % 2 === 0);
```
