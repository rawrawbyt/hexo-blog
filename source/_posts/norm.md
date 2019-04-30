---
title: HTML5/JavaScript/CSS书写规范
date: 2017-06-14 14:46:21
tags: [summary,JavaScript,CSS,HTML5]
categories: rule
---
作为强迫症，就是特别喜欢介个样子//

<div align=center>
![“封面”](/images/bg/0047.jpeg)
</div>
<!--more-->
# HTML5
# 头部
```html    
<!DOCTYPE html>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<meta http-equiv="X-UA-Compatible" content="IE=Edge" />
<meta name="description" content="">
<meta name="keywords" content="">    
<title>HTML5 standardization</title>
//type属性：省略
```
# 区分浏览器
no-js标签是需要与Modernizr等类库配合使用的
`<script src="js/libs/modernizr-2.5.0.min.js"></script>`
```html
<!--[if lt IE 7]> <html class="no-js lt-ie9 lt-ie8 lt-ie7" lang="zh"> <![endif]-->
<!--[if IE 7]>    <html class="no-js lt-ie9 lt-ie8" lang="zh"> <![endif]-->
<!--[if IE 8]>    <html class="no-js lt-ie9" lang="zh"> <![endif]-->
<!--[if gt IE 8]><!--> <html class="no-js" lang="zh"> <!--<![endif]-->
```
* 避免IE6条件注释引起的高版本IE文件阻塞问题
* 与Modernizr等特征检测类库使用相同的class，更具备通用性
* 优于使用CSS Hack

## 嵌套规则
* 块元素可以包含内联元素或某些块元素，但内联元素却不能包含块元素，它只能包含其它的内联元素；
* <p>里面不能放块级元素；
* 块级元素与块级元素并列、内嵌元素与内嵌元素并列；

## 文档内容
* 自定义属性：`data-*`
* 不要使用内联样式
* 不要使用<em>和<strong>,用css来控制。不要使用<i>和<b>，HTML5不赞成使用

## 实体字符引用
| 字符          | 实体名       | 实体数        |
| :----------: |:----------: | :----------: |
| "            | 	`&quot;` | `&#34;`      |
| '            |`&apos;(IE不支持)`| `&#39;`  |
| &            | 	`&amp;`  |    `&#38;`   |
| >            | 	`&gt;`   | `&#62;`      |
| <            | 	`&lt;`   |   	`&#60;` |
| &nbsp;       | `&nbsp;`    | 	`&#160;`    |
| &emsp;       | `&emsp;`    | `&#12288;`   |
| ￥&yen;       | 	`&yen;`  | `&#165;`     |
| &brvbar;     |`&brvbar;`   | `&#39;`      |
| &copy;       | 	`&copy;` |              |
| &reg;        | 	`&reg;`  | `&#169;`     |
| &trade;      | 	`&trade;`|   `&#8428;`  |
| &middot;	   | `&middot;`  | 	`&#183;`    |
|  &laquo;     | `&laquo;`   | `&#171;`     |
| &raquo;      |`&raquo;`    | `&#187;`     |
| 	&deg;      | 	`&deg;`  |    `	&#176;` |
| &times;      | 	`&times;`| `&#215;`     |
| &divide;     |   `&divide;`|   	`&#247;`|
| &permil;	   | `&permil;`  | 	`&#8240;`   |

## 图片
* 给图片添加width和height，提升页面加载速度
* 给所有img添加alt属性
* 不要使用或尽量少用gif文件

# CSS
## 引用结构
按照顺序引入
CSS 一律写在 CSS 文件中，原则上不写内联样式，不直接为标签添加样式（reset 除外）。
* 基础框架（reset / grid ...）
* 通用模块（theme/ common...）
* 页面样式（page...）

## 命名规范
* CSS对大小写敏感
* 不采用驼峰式命名，不用中文拼音
* 不允许使用具体的样式名称命名，也不应包含颜色、位置等与现实效果相关的信息。
* 加上适当的命名空间（前缀），以避免命名冲突。命名空间不使用单个字母，以免与通用样式冲突。

### 文件命名
CSS 文件命名由小写字母、下划线（_）组成。
### 选择器命名
CSS 文件命名由小写字母、中划线（-）组成。
|布局（grid） .g-|模块（module） .m-|元件（unit）|功能（function）|状态 .z-|皮肤（skin） .s-|JS选择器 .j-|
## 书写规范
* `;`分行书写
* 属性值为 0 时，单位可以省略。
* 属性值为小数时，小数点之前的 0 不可以省略。
* 省略 url 中的引号，其他需要引号的地方使用单引号。

## 书写顺序
### 属性
| 显示属性 | display, visibility, position, float, clear, list-style, top 等 |
| 自身属性 | width, height, margin, padding, border, overflow 等 |
| 文本及修饰属性 | font, text-align, text-decoration, vertical-align, white-space, color, background 等 |
| CSS3 属性 | border-radius, box-shadow, gradients, transforms, animations 等 |
### 链接
a:link -> a:visited -> a:hover -> a:active
## 优化
### 合并选择器
### 属性值缩写
* margin
* padding
* border
* background
* font
* color
* list-style

## 避免耗性能的属性
*  `width: expression(this.width>100?'100px':'auto');`
*   ` filter: alpha(opacity=50);`

### 图片合并（sprite）
### 文件压缩
# JavaScript
## 使用`===`/`!==`
`==`和`!=`不判断类型
### 特殊情况
在判断函数是否为空的情况下，使用`==`或`!=`是可以的。
```js
//如果foo没有被初始化，它默认的值是undefined而不是null。当然underfined更不会等于null了。
//因此这种情况应该使用==和!=。
if (foo == null) {
    ...
}
```
## `DELETE`在数组中
数组可以被`DELETE`，但是会留下`undefined`元素。
可以用shift( )/pop( )/splice(index,num)
```js
var myArray = [ 'a', 'b', 'c', 'd' ];
delete myArray[2]; 
// Noncompliant. myArray => ['a', 'b', undefined, 'd']
console.log(myArray[2]); // 'undefined' 
```
## `for...in..`的循环在每次操作前需要进行过滤判断
"for … in"这种循环允许开发人员按照属性的名字遍历对象。不幸的是，这个属性的集合包括了对象自身和对象继承的对象的所有属性。如果程序不考虑这点就会出现错误。都应该包括一个if判断来过滤你需要的属性。
```js
for (name in object) {
    if (object.hasOwnProperty(name)) {
        doSomething(name);
    }
}
```
## `NaN`不要出现在比较中
NAN不等于包括自身在内的任何值。因此与NAN作比较是得不到你需要的结果的，但是这种错误有可能会出现。
事实上，判断值是否等于NAN最好的方法就是和它自己作比较即NAN!==NAN，因为正常的变量都是等于自身的，如果不等于自身成立，就说明这个值是NAN。
## 保证函数调用时传入的参数都被使用
```js
function doSomething(a, b) {
    compute(arguments);
}
doSomething(1, 2, 3) 
function say(a, b) {
    print(a + ' ' + b);
}
say('hello', 'world', '!'); 
```

## 选择器得到的结果一定要用LENGTH判断
无论是否找到该对象，选择器总是返回一个对象。
```js
if ($('.test')) {
       // ...
     }
if ($('.test').length > 0) {
  //  ...
}
```
## 用逻辑短路防止出现空的错误
```js
if (str != null && str.length == 0) {
  console.log('String is empty');
}
if (str != undefined && str.length == 0) {
  console.log('String is empty');
}
if (str == null || str.length > 0) {
  console.log('String is not empty');
}
if (str == undefined || str.length > 0) {
  console.log('String is not empty');
}
```

## 易错点
* 用`null`,不要用`undefined`（尚未创建）赋值给变量。
* `var i = 0;i = i++;`
* parseInt函数有两个版本的，一个是只有一个参数的，而另一个是需要两个参数的。然而，旧版的浏览器不支持一个参数的parseInt方法。
  `parseInt("010", 10);`
  

## 性能优化
* `var input = $( 'form input[type=radio]' );`代替`var input = $( 'form input:radio' );`
* `var $productIds = $('#products').find('div.id');`代替`var $productIds = $('#products div.id');`
*  选择结果应该被保存，`var paragraph = $('p');paragraph.hide();paragraph.show();`
* 尽量不要通配选择器*`$( '.buttons' ).children();`代替`$( '.buttons > *' ); `
* 使用`===`/`!==`，`==`和`!=`不判断类型

## 约定规范
* 每一条声明须要由“;”结尾
* 注释不应该写在每一行的最后面；一行代码不要太长（不超过80）；多分行分行
* 文件后面应该包含一个空行（这条规则会使得在利用一些工具，例如Git的时候配合的更好）
* 声明STRING类型的变量是需要用单引号
* 源代码文件应该有足够的注释（默认15%）
* FUNCTIONS不应该有太多行（阈值：300），难以理解以及维护。
* 函数不应该有太多的参数（临界值为7）
* 一个表达式不应该有超过三个的操作符，以增加表达式的可读性。
* 循环不应该包括多余一个的BREAK或者CONTINUE语句，否则重构
* 结尾的逗号不应该被使用`var settings = {'foo': oof,'bar': rab};`
* `ARGUMENTS.CALLER`和`ARGUMENTS.CALLEE`在ECMAScript5中，这两个函数在strict模式下都被禁止使用。在最新的Javascript版本中不建议被使用。
* 不要省略大括号（）if，作为范围控制
* `SWITCH`的每个条件结尾都要有`BREAK`
* 发布版本中不要有`alert()`,`console`,给攻击者泄露敏感信息
* `//TODO`，`// FIXME`只在 开发过程中。
* 开发人员不能注释代码，因为会影响代码可读性。不再使用的代码就删除。
* `new`关键字应该和构造函数一起使用
* 不要使用`ARRAY`和`OBJECT`的构造方法。超过一个参数，会新建多个array.
* 不要重载内置对象
* 及时释放无用的储存