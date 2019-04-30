---
title: Javascript模块规范:CommonJS和AMD
date: 2017-06-20 16:49:47
tags: [JavaScript,CommonJS,AMD]
categories: Note
---
目前，通行的Javascript模块规范有两种：CommonJS和AMD。
<div align=center>
![“封面”](/images/bg/0010.jpg)
</div>
<!--more-->
## CommonJS
> 在浏览器环境下，没有模块也不是特别大的问题，毕竟网页程序的复杂性有限；但是在服务器端，一定要有模块，与操作系统和其他应用程序互动，否则根本没法编程。node.js的模块系统，就是参照CommonJS规范实现的。在CommonJS中，有一个全局性方法require()，用于加载模块。

假定有一个数学模块math.js，就可以像下面这样加载。
```js [math.js]
var math = require('math');
math.add(2,3); // 5 ,调用模块提供的方法
```
CommonJS规范不适用于浏览器环境。第二行math.add(2, 3)，在第一行require('math')之后运行，因此必须等math.js加载完成。浏览器端的模块，不能采用"同步加载"（synchronous），只能采用"异步加载"（asynchronous）。这就是AMD规范诞生的背景。
##　AMD规范
> 全称：Asynchronous Module Definition（异步模块定义）
> 它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

AMD也采用require()语句加载模块，但是不同于CommonJS，它要求两个参数：
`require([module], callback);`
上述的例子：
```js
　　require(['math'], function (math) {
　　　　math.add(2, 3);
　　});
```
math.add()与math模块加载不是同步的，浏览器不会发生假死。所以很显然，AMD比较适合浏览器环境。