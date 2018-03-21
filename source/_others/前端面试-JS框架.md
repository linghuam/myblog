---
title: 前端面试-JS框架
comments: true
date: 2018-01-30 23:39:24
tags:
  - JS框架
categories:
  - 前端面试
---

## vuejs、angularjs、reactjs
<!-- more -->

### vue 综合

http://www.bslxx.com/p/3187.html

### vue 响应式原理。

https://www.imooc.com/article/14466

vue 是 **MVVM** 框架。M 代表数据，V 代表视图。

- M的实现：通过 observer 对数据进行监听，并且通过发布-订阅模式监测数据变化。
  * 用户在 Vue 组件的定义中返回 data 对象
  * vue 内部在 initData 方法里面干了两件事
     1. 通过 proxy 方法将 data 的属性代理到 Object.defineProperty 的 getter 和 setter上；
     2. 通过 observe 方法来添加对 data 的监听。Observer 主要作用就是将对象属性添加 getter、setter，
        以及收集依赖和对数据更新作分发。

- V的实现：compile 编译模板、解析 Directive
  * 通过 compiler 来编译模板、解析指令，将模板编译成一段 documentfragment

- 响应式的实现：Watcher类，解析 expression，收集依赖，当 expression 变化时触发回调，更新视图。


模型通过Observer、Dep、Watcher、Directive等一系列对象的关联，最终和视图建立起关系。归纳起来，Vue.js在这里主要做了三件事：

- 通过 Observer 对 data 做监听，并且提供了订阅某个数据项变化的能力。
- 把 template 编译成一段 document fragment，然后解析其中的 Directive，得到每一个 Directive 所依赖的数据项和update方法。
- 通过Watcher把上述两部分结合起来，即把Directive中的数据依赖通过Watcher订阅在对应数据的 Observer 的 Dep 上。当数据变化时，就会触发 Observer 的 Dep 上的 notify 方法通知对应的 Watcher 的 update，进而触发 Directive 的 update 方法来更新 DOM 视图，最后达到模型和视图关联起来。


### vue数据绑定原理？ [详情](https://segmentfault.com/a/1190000006599500)

vue是通过**数据劫持**的方式来做数据绑定的，其中最核心的方法便是通过`Object.defineProperty()`来实现对属性的劫持，
达到监听数据变动的目的。

答：vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

具体步骤：

第一步：需要observe的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter和getter
这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化

第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:
1、在自身实例化时往属性订阅器(dep)里面添加自己
2、自身必须有一个update()方法
3、待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。

第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。


### Vue生命周期？
1. beforeCrate: 实例刚被创建，初始化事件、进行数据观测，data计算前。
2. created： 实例创建完成，属性已绑定，但DOM还未生成。data初始化，$el还不存在。
3. beforeMount：挂载前，完成 data 和 el 初始化。
4. mounted： 挂载后
5. beforeUpdate：更新前
6. updated：更新后
7. beforeDestory：销毁前，实例仍存在。
8. destoryed啊：销毁后，移除所有事件监听，销毁所有子实例。

### Vue组件数据通信？vue如何实现父子组件通信，以及非父子组件通信？
1. 父到子：props down； 子组件中 this.$parent
2. 子到父：events up；this.$ref
3. 兄弟组件：中专站， new Vue()
4. vuex

### Vue是如何实现虚拟 DOM 的？
http://www.jb51.net/article/112811.htm

Virtual Dom可以看做一棵模拟了DOM树的JavaScript树，其主要是通过vnode,实现一个无状态的组件，当组件状态发生更新时，然后触发Virtual Dom数据的变化，然后通过Virtual Dom和真实DOM的比对（DOM diff 算法），再对真实DOM更新。可以简单认为Virtual Dom是真实DOM的缓存。

状态变化先反馈到Virtual Dom上，Virtual Dom在找到最小更新视图，最后批量更新到真实DOM上，从而达到性能的提升。

snabbdom 实现虚拟DOM
- vnode：相当于树的节点，首先会解析template构造节点树。
- patch：将 Virtual DOM 渲染成真实 DOM。
  patch 实现了 Diff 算法，diff 算法的核心是比较只会在同层级进行, 不会跨层级比较。
- hook：钩子方法中可以执行扩展模块，attribute、props、eventlistener等可以通过扩展模块实现。

### vuex原理？

[详情](https://tech.meituan.com/vuex-code-analysis.html)


### Vue脏检查？

在 angular中，他没有办法判断你的数据是否做了更改， 所以它设置了一些条件，当你触发了这些条件之后，它就执行一个检测来遍历所有的数据，对比你更改了地方，然后执行变化。这个检查很不科学。而且效率不高，有很多多余的地方，所以官方称为脏检查。

Vue.js 则根本没有这个问题，因为它使用基于依赖追踪的观察系统并且异步列队更新，所有的数据变化都是独立地触发，除非它们之间有明确的依赖关系。唯一需要做的优化是在 v-for 上使用 track-by。


### MVC、MVVM了解么，数据双向绑定和单向绑定实现方式？

vue 和 angular 实现双向绑定，React 是单向数据流。

单向绑定的优点是相应的可以带来单向数据流，这样做的好处是所有状态变化都可以被记录、跟踪，状态变化通过手动调用通知，源头易追溯，没有“暗箱操作”。同时组件数据只有唯一的入口和出口，使得程序更直观更容易理解，有利于应用的可维护性。缺点则是代码量会相应的上升，数据的流转过程变长，从而出现很多类似的样板代码。同时由于对应用状态独立管理的严格要求(单一的全局store)，在处理局部状态较多的场景时(如用户输入交互较多的“富表单型”应用)，会显得啰嗦及繁琐。

基本上双向绑定的优缺点就是单向绑定的镜像了。优点是在表单交互较多的场景下，会简化大量业务无关的代码。缺点就是由于都是“暗箱操作”，我们无法追踪局部状态的变化(虽然大部分情况下我们并不关心)，潜在的行为太多也增加了出错时 debug 的难度。同时由于组件数据变化来源入口变得可能不止一个，新手玩家很容易将数据流转方向弄得紊乱，如果再缺乏一些“管制”手段，最后就很容易因为一处错误操作造成应用雪崩。


### 前端路由原理？

[详情](https://segmentfault.com/a/1190000007238999)
history API 和 Hash

### vue-router实现原理？


### 说一下Vue实现双向数据绑定的原理，以及vue.js和react.js异同点，如果让你选框架，你怎么怎么权衡这两个框架，分析一下？

主要是发布订阅的设计模式，还有就是ES5的Object.defineProperty的getter和setter机制，然后顺便扯了一下Angular的脏检测


### 比如Vue，问问数据绑定怎么做的，如何解决getter/setter不能监听数组变异方法，监听的回调和事件怎么解耦的，watcher去重怎么做的，DOM批更新怎么做的？

**如何解决getter/setter不能监听数组变异方法:**
Vue的方法是，改写数组的push、pop等8个方法，让他们在执行之后通知我数组更新了（这种方法带来的后果就是你不能直接修改数组的长度或者通过下标去修改数组。参见官网）。这样改进之后我就不需要对数组元素进行响应式处理，只是遇到数组的时候把数组的方法变异即可。于是在用户使用数组的push、pop等方法会改变数组本身的方法时，可以监听到数组变动。


### 为什么要选vue？与其它框架对比的优势和劣势？

### js 设计模式
https://www.cnblogs.com/xianyulaodi/p/5827821.html
http://www.cnblogs.com/tugenhua0707/p/5198407.html

### requireJS的基本原理？
requireJS是使用创建script元素，通过指定script元素的src属性来实现加载模块的。但这里有几个基本问题需要解决：

1、模块依赖加载之后，如何调用回调函数？

使用script来加载这些模块依赖，并且**监听load**函数，且每个script元素都会有一个自定义的属性，用来指明模块名的。

触发'已定义'这个事件。

2、加载依赖之后，如何将接口暴露给回调函数？

当执行回调函数的时候，会使用**apply**将模块定义中的接口，传递给回调函数。这个时候，模块依赖的接口便会作为参数传递给回调函数。

3、如何解决循环依赖的问题？

在模块加载依赖的时候，先检查模块依赖中是否存在正在注册的模块，如果存在的话，则先将模块依赖数量减一。
通过这种方法用来解决循环依赖的问题。

4、如何解决重复加载的问题？

将已定义的模块保存在一个对象中，当加载模块依赖的时候，如果在这个对象中存在的话，则直接返回这个模块。
否则的话，则再走一遍加载的模块的流程。

参考：
* http://blog.csdn.net/cde7070/article/details/65935888
* https://www.cnblogs.com/axl234/p/5295307.html
