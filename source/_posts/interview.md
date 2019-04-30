---
title: 面试大宝典
date: 2017-04-12 11:07:57
tags: [面试,summary]
categories: Note
---
<div align=center>
![“封面”](/images/bg/0022.jpeg)
</div>
<!--more-->

# 为什么要学习前端

# 对前端的认识

# 基础知识
## HTML部分
### 1、重绘和回流
 会引起重绘和回流的操作:
 
* 添加、删除元素(回流+重绘)
* 隐藏元素，display:none(回流+重绘)，visibility:hidden(只重绘，不回流)
* 移动元素，比如改变top,left,transform的值，或者移动元素到另外一个父元素中。(重绘+回流)
* 对style的操作(对不同的属性操作，影响不一样)
* 还有一种是用户的操作，比如改变浏览器大小，改变浏览器的字体大小等(回流+重绘)

### 2、浏览器缓存机制
浏览器缓存机制是指通过 HTTP 协议头里的 Cache-Control（或 Expires）和 Last-Modified（或 Etag）等字段来控制文件缓存的机制。
Cache-Control 用于控制文件在本地缓存有效时长。
Last-Modified 是标识文件在服务器上的最新更新时间。如果没有修改，服务器返回304告诉浏览器继续使用缓存；如果有修改，则返回200，同时返回最新的文件。

> 特殊情况：

* 手动刷新页面（F5)，浏览器会直接认为缓存已经过期（可能缓存还没有过期），在请求中加上字段：Cache-Control:max-age=0，发包向服务器查询是否有文件是否有更新。
* 强制刷新页面（Ctrl+F5)，浏览器会直接忽略本地的缓存（有缓存也会认为本地没有缓存），在请求中加上字段：Cache-Control:no-cache（或 Pragma:no-cache），发包向服务重新拉取文件。

### 3、History路由机制
用户访问网页的历史记录通常会被保存在一个类似于栈对象中，即history对象，点击返回就出栈，跳下一页就入栈。

* window.history.back() 返回到上一个页面
* window.history.forward() 进入到下一个页面
* window.history.go([delta]) 跳转到指定页面

> HTML5增强的History Api和时间： 

* pushState是往history对象里添加一个新的历史记录，即压栈。
* replaceState 是替换history对象中的当前历史。
* 当点击浏览器后退按钮或js调用history.back都会触发onpopstate事件（类似的事件: onhashchange）。onpopstate是专门用来监听浏览器前进后退。onhashchange监听浏览器、客户端前进和后退事件

### 4、Canvas和SVG

Canvas 通过Javascript 来绘制 2D 图形。

SVG 是一种使用 XML 描述 2D 图形的语言。

Canvas和SVG相比，canvas更依赖于分辨率，不支持事件处理器，文本渲染能力弱，比较适合密集型游戏，其中的许多对象会被频繁绘制，而svg则比较适用于类似谷歌地图带有大型渲染区域的应用程序。

## CSS部分
### 0、盒子模型
window.top.document.compatMode ？
### 1、选择器
常用选择器：类选择器、标签选择器、ID选择器、后代选择器、群组选择器、伪类选择器(before/after)、兄弟选择器(+~)、属性选择器。
### 2、定位
>relative、absolute、fixed

fixed 在移动端的兼容性问题。
解决方案： absolute+内部滚动
#### 浮动
清浮动方案
### 3、自适应
calc/box
### 4、Flex布局
注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。
### 5、CSS3
> transition、transform、Animation

### 6、Sprite
### 7、iconfont
## JS部分
### 0、基础语法
#### 基础数据类型
>原始类型:Number（数值） String（字符串） Boolean（布尔） Null（空） Undefined（未定义）

>引用类型:Object（对象）

tips:typeof运算符对于null类型返回的是object。


### 1、作用域
每个作用域都有一条对应的作用域链，链头是全局作用域，链尾是当前函数作用域。
作用域链的作用是用于解析标识符，当函数被创建时（不是执行），会将this、arguments、命名参数和该函数中的所有局部变量添加到该当前作用域中，当JavaScript需要查找变量X的时候（这个过程称为变量解析），它首先会从作用域链中的链尾也就是当前作用域进行查找是否有X属性，如果没有找到就顺着作用域链继续查找，直到查找到链头，也就是全局作用域链，仍未找到该变量的话，就认为这段代码的作用域链上不存在x变量，并抛出一个引用错误（ReferenceError）的异常。
> 作用域链:
作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到window对象即被终止，作用域链向下访问变量是不被允许的。

在JS中没有块级作用域，只有函数作用域。怪异现象：变量提升。
#### js变量提升(es6)
JavaScript函数中声明的所有变量（但不涉及赋值）都被“提前”至函数的顶部。
##### 举个栗子
```js
var scope = "global";
function myFunc(){
    console.log(scope); //undefined
    var scope = "local";
}
`````````````````````````````````````````````
var scope = "global";
function myFunc(){
    var scope;
    console.log(scope);
    scope = "local";
}
```

### 2、原型链
prototype，建立了变量查找机制。原型链的链头是object,它的prototype比较特殊，值为null。
原型链的作用是用于对象继承。
当访问对象的一个属性时, 首先查找对象本身, 找到则返回; 若未找到, 则继续查找其原型对象的属性(如果还找不到实际上还会沿着原型链向上查找, 直至到根). 只要没有被覆盖的话, 对象原型的属性就能在所有的实例中找到，若整个原型链未找到则返回undefined；
### 3、函数
普通函数的创建有：显式声明、匿名定义、new Function() 等三种方式。
#### 函数声明和函数表达式的区别
函数声明会提前
ECMAScript规范中表示，函数声明语句可以出现在全局代码中，或者内嵌在其他函数中，但是不能出现在循环、条件判、或者try/finally以及with语句中。
##### que0.1 : `spacify('rawraw')`  =>  `'r a w r a w'`  
answer : 
```js
function spacify(str) {  
  return str.split('').join(' ');
}
```
##### que0.2 : `spacify('rawraw')`  =>  `'r a w r a w'`
answer : 
```js
String.prototype.spacify = function(){  
  return this.split('').join(' ');
};
```
#### apply和call的区别
[详情见这里](2017-06-12-js01.html)
##### que0.1 : `log('hello world');` 
answer :
```js
function log(msg){  
  console.log(msg);
}
//apply
```
##### que0.2 : `log('hello', 'world');` 
answer :
```js
log('hello', 'world');
```
##### que0.3 : '(app) hello world'  
arguments是一个伪数组，我们需要先将它转换成正常的数组，我们可以使用Array.prototype.slice,
answer :
```js
function log(){  
  var args = Array.prototype.slice.call(arguments);
  args.unshift('(app)');  
  console.log.apply(console, args);
};
```
#### Context的理解
##### que0.1 : 运行结果

```js
 var User = {  
   count: 1,
 
   getCount: function() { 
    return this.count;
   }
 };
```

##### que0.2 : 运行结果

```js
console.log(User.getCount());
var func = User.getCount;  
console.log(func());  
//undefined,unc的上下文是 window，因此已经失去了count属性
```

##### que0.3 : 如何确保func的上下文始终都和User关联，这样可以使输出的答案是1
answer :

```js
var func = User.getCount.bind(User);  
console.log(func()); 
```

##### que0.4 : 老浏览器兼容
answer :
```js
Function.prototype.bind = Function.prototype.bind || function(context) {  
    var self = this;
    return function(){ 
           return self.apply(context,   arguments);
  };
}
```

### 4、函数指针 
this的指向：

* 作为普通函数调用（this指向全局对象window对象）
* 作为对象的方法调用（this指向该对象）
* 构造器调用（this指向用new返回的这个对象）
* call、apply、bind的调用（this指向第一个参数对象）

### 5、闭包
[去看闭包吧](2017-06-28-js02.html)
> 什么情况下会发生闭包，为什么需要闭包，什么场景下需要，闭包闭了谁，怎么释放被闭包的变量内存，闭包的优点是什么，缺点是什么等等。
> 《红宝书》：是指有权访问另一个函数作用域中的变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量。
《你不知道的javascript》：当函数可以记住并访问所在的词法作用域时，就产生了闭包，这个函数持有对该词法作用域的引用，这个引用就叫做闭包。

闭包其实是一个主动执行的代码块，这个代码块的特殊之处是可以永久保存局部变量，但又不污染全局变量，可以形成一个独立的执行过程，因此我们经常用闭包来定义组件。闭包本质还是函数，只不过这个函数绑定了上下文环境（函数内部引用的所有变量）。
#### 特性
* 函数嵌套函数
* 函数内部可以引用外部的参数和变量
* 参数和变量不会被垃圾回收机制回收

#### 缺点
常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。
#### 使用场景
可以用来管理私有变量和私有方法，将对变量（状态）的变化封装在安全的环境中，使得这些变量不能被外部随意修改，同时又可以通过指定的函数接口来操作。


### 6、事件系统 Event(事件模型及事件代理/委托)
(事件是用户与页面交互的基础，到目前为止，DOM事件从PC端的 鼠标事件(mouse) 发展到移动端的 触摸事件(touch) 和 手势事件(guesture)
 
 由于DOM结构可能会多层嵌套，因此也衍生出了两种事件流：事件捕获和事件冒泡，后者最常用。利用事件冒泡机制可以实现很多功能，比如页面点击统计。
 
 除此之外，在页面初始化、滚动、隐藏、返回等操作时分别内置了onload/onDOMContentLoaded、onscroll、onvisibility和onhashchange等事件，如果想要捕获这些事件，需要通过addEventLisener/attachEvent来进行绑定。)
#### 事件的三个阶段
捕获，目标，冒泡阶段(低版本IE不支持捕获阶段)
#### {事件的代理/委托}的原理以及优缺点
##### 优点
1. 大量节省内存占用，减少事件注册，比如在table上代理所有td的click事件就非常棒
2. 实现当新增子对象时无需再次对其绑定事件，对于动态内容部分尤为合适
事件代理的应用常用应该仅限于上述需求下，如果把所有事件都用代理就可能会出现事件误判，即本不应用触发事件的被绑上了事件

#### IE和W3C不同绑定事件解绑事件的方法有什么区别，参数分别是什么，以及事件对象e有什么区别
target，currentTarget，以及IE下的srcElement和this
#### 实现事件模型
即写一个类或是一个模块，有两个函数，一个bind一个trigger，分别实现绑定事件和触发事件，核心需求就是可以对某一个事件名称绑定多个事件响应函数，然后触发这个事件名称时，依次按绑定顺序触发相应的响应函数。

大致实现思路就是创建一个类或是匿名函数，在bind和trigger函数外层作用域创建一个字典对象，用于存储注册的事件及响应函数列表，bind时，如果字典没有则创建一个，key是事件名称，value是数组，里面放着当前注册的响应函数，如果字段中有，那么就直接push到数组即可。trigger时调出来依次触发事件响应函数即可。

不过还有很多细节，比如触发响应函数时的上下文应该是什么，触发响应函数的参数列表应该是什么，如果要求把调用trigger的参数列表都传到响应函数中还要考虑到吧arguments对象转化为纯数组才行等等。

还有一些面试官会问到事件如何派发也就是事件广播（dispatchEvent）等等，这里不再展开。

#### 代理
> 当我们需要对很多元素添加事件的时候，可以通过将事件添加到它们的父节点而将事件委托给父节点来触发处理函数。
```js
<ul id='list'></ul>
var count = 100;
var ulList = document.getElementById("list");
//动态构建节点
for(var i = count;i--;){
    var liDom = document.createElement('li');
    ulList.appendChild(liDom);
}
//绑定点击事件
var liNode = ulList.getElementByTagName("li");
for(var i=0, l = liNodes.length; i < l; i++){
    liNode[i].onClick = function(){
        //li点击事件
    }
}
var count = 100;
var ulList = document.getElementById("list");
//动态构建节点
for(var i = count;i--;){
    var liDom = document.createElement('li');
    ulList.appendChild(liDom);
}
//绑定点击事件
var liNode = ulList.getElementByTagName("li");
liNode.onClick = function(e){
    if(e.target && e.target.nodeName.toUpperCase == "LI") {
        // li点击事件
    }
}
```


### 7、单线程和异步队列
> setTimeout和setInterval

JS是单线程语言，在浏览器中，当JS代码被加载时，浏览器会为其分配一个主线程来执行任务(函数)，主线程会形成一个全局执行环境，执行环境采用栈的方式将待执行任务按顺序依次来执行。但在浏览器中有一些任务是非常耗时的，比如http请求、定时器、事件回调等，为了保证其他任务的执行效率不被影响，JS在执行环境中维护了一个异步队列(也叫工作线程)，并将这些任务放入队列中进行等待，这些任务的执行时机并不确定，只有当主线程的任务执行完成以后，才会去检查异步队列中的任务是否需要开始执行。这就是为什么setTimeout(fn,0) 始终要等到最后执行的原因。
#### Ajax
### 8、DOM对象:document/全局对象:window
(document对象里保存着整个web页面dom结构，在页面上所有的元素最终都会映射为一个dom对象。 document也提供了很多api来查找特定的dom对象，比如getElementById,querySelector等等。)
### Function.bind函数
#### 作用，应用场景，举个栗子
1、Function.bind返回的也是一个函数，所以注定发生了闭包；
2、在返回的这个函数中去调用一个其他的函数，这其实本质上就是函数钩子(HOOK)；
1、保持函数的this指向；
2、保持函数的所有参数都传递到目标函数；
3、保持函数的返回值；

```js
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    if (typeof this !== "function") {
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var aArgs = Array.prototype.slice.call(arguments, 1), 
        fToBind = this, 
        fNOP = function () {},
        fBound = function () {
          return fToBind.apply(this instanceof fNOP
                                 ? this
                                 : oThis || this,
                               aArgs.concat(Array.prototype.slice.call(arguments)));
        };

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  };
}
```
### 9、继承

### 算法
#### 去重

```js [基本数组去重]
Array.prototype.unique = function(){
    var result = [];
    this.forEach(function(v){
        if(result.indexOf(v) < 0){
            result.push(v);
        }
    });
    return result;
}
```

```js [利用hash表去重]
Array.prototype.unique = function(){
    var result = [],hash = {};
    this.forEach(function(v){
        if(!hash[v]){
            hash[v] = true;
            result.push(v);
        }
    });
    return result;
}
```
 
上面的方法存在一个bug，对于数组[1,2,’1’,’2’,3]，去重结果为[1,2,3]，原因在于对象对属性索引时会进行强制类型转换，arr[‘1’]和arr[1]得到的都是arr[1]的值，因此需做一些改变：   
```js
Array.prototype.unique = function(){
    var result = [],hash = {};
    this.forEach(function(v){
        var type = typeof(v);  //获取元素类型
        hash[v] || (hash[v] = new Array());
        if(hash[v].indexOf(type) < 0){
            hash[v].push(type);  //存储类型
            result.push(v);
        }
    });
    return result;
}
```

先排序后去重
```js
Array.prototype.unique = function(){
    var result = [this[0]];
    this.sort();
    this.forEach(function(v){
        v != result[result.length - 1] && result.push(v); //仅与result最后一个元素比较
    });
}
```

#### 排序
方法一(尽可能不用js数组方法）：
```js
function quickSort(arr){
    qSort(arr,0,arr.length - 1);
}
function qSort(arr,low,high){
    if(low < high){
        var partKey = partition(arr,low,high);
        qSort(arr,low, partKey - 1);
        qSort(arr,partKey + 1,high);
    }
}
function partition(arr,low,high){
    var key = arr[low];  //使用第一个元素作为分类依据
    while(low < high){
        while(low < high && arr[high] >= arr[key])
            high--;
        arr[low] = arr[high];
        while(low < high && arr[low] <= arr[key])
            low++;
        arr[high] = arr[low];
    }
    arr[low] = key;
    return low;
}
```

方法二（使用js数组方法）：
```js
function quickSort(arr){
   if(arr.length <= 1) return arr;
   var index = Math.floor(arr.length/2);
   var key = arr.splice(index,1)[0];
   var left = [],right = [];
   arr.forEach(function(v){
       v <= key ? left.push(v) : right.push(v);
   });
   return quickSort(left).concat([key],quickSort(right));
}
```



### 跨域问题 
http://www.cnblogs.com/rainman/archive/2011/02/20/1959325.html
http://www.cnblogs.com/scottckt/archive/2011/11/12/2246531.html
http://www.cnblogs.com/cat3/archive/2011/06/15/2081559.html
JSONP原理。这里简单讲就是HTML里面所有带src属性的标签都可以跨域，如iframe，img，script等。
### 正则

尽量不要拆字符，不可预知性
```js
function getQueryObject(url) {
    url = url == null ? window.location.href : url;
    var search = url.substring(url.lastIndexOf("?") + 1);
    var obj = {};
    var reg = /([^?&=]+)=([^?&=]*)/g;
    search.replace(reg, function (rs, $1, $2) {
        var name = decodeURIComponent($1);
        var val = decodeURIComponent($2);                
        val = String(val);
        obj[name] = val;
        return rs;
    });
    return obj;
}
```

# 性能优化
网络性能优化，加快访问速度，浏览器并行加载数量，怎样实现原生JS异步载入，CDN加速的原理，如何将不同静态资源发布到多个域名服务器上，发布后这些静态字段的url路径改怎么批量改写，用什么工具进行项目打包，css打包后的相对路径怎么转换为绝对路径，用什么工具进行项目模块依赖管理，怎么进行cookie优化
文件合并
文件最小化/文件压缩
使用CDN托管
缓存的使用
## 函数节流
http://www.alloyteam.com/2012/11/javascript-throttle/

# 前端设计模式
比较多的有观察者模式，职责链模式，工厂模式。
比如如何去设计一个前端UI组件，应该公开出哪些方法，应该提供哪些接口，应该提供哪些事件。哪部分逻辑流程应该开放出去让用户自行编写，如何实现组件与组件之间的通信，如何实现高内聚低耦合，如何实现组件的高复用等等

[前端面试问题合集](https://github.com/darcyclarke/Front-end-Developer-Interview-Questions)

# 了解这家公司
## 版本管理
## 流程管理
每天怎么知道要做什么事情？
