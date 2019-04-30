---
title: Babel安装、编译、配置（cmd和phpstorm）
date: 2017-03-27 09:56:18
tags: [babel,JavaScript,es6]
categories: Note
---
讲道理 这里我要找一张好看的图片
（没写完啊没写完，不生气了再写）
<div align=center>
![“封面”](/images/bg/0001.jpeg)
</div>
<!--more-->
# 开始
Babel转码器
工具：cmd、phpstorm10.0.3
环境：Windows 10
好多爹一样的浏览器不支持666的ES6啊！大Babel帮你ES6编译成ES5哦~省事儿~
作用：
    ①让code支持es6
    ②支持react的一些特性（eg:JSX）
# 安装环境
```
    cnpm install babel-cli -g
    cnpm install babel-cli --save-dev
```
# 安装插件
前面新建的es5.js和源文件es6.js是一毛一样的，毕竟还没有配置。
## 新建配置文件.babelrc
```js
{
"presets":[],
"plugins":[]
}
```
## 安装预设
```
$ cnpm install --save-dev babel-preset-es2015
```
啊啊啊啊啊啊啊啊啊啊啊啊啊！！！！！
答应我这一步千万不要用Terminal来装！！不要用Terminal来装！！不要用Terminal来装！！
会炸啊会炸！！<font color='red'>老老实实把这个项目关了去打开cmd！</font>无响应了一个世纪、
看到红色的这句话，省你一个小时时间！装完趁早吧，好气！
也别轻易把node_modules给ignore，找个吃饭的时间弄，不然真当卡死。哦，还有气死！
另外，如果phpstorm一直好卡一直indexing的话，可以在phpstorm.vmoptions里面，最后加上
```java
-Dawt.usesystemAAFontSettings=lcd  
-Dawt.java2d.opengl=true 
```
回归正题，在.babelrc文件里加上es2015的字段，在package.js加上对应字段。
```js [.babelrc]
{
"presets":["es2015"],
"plugins":[]
}
```
```js [package.js]
  "babel": {
    "presets": ["es2015"]
  }
```
## 安装展开符插件
```
$ cnpm install babel-plugin-transform-object-rest-spread --save-dev
```
在.babelrc文件里加上transform-object-rest-spread的字段
```js
{
"presets":["es2015"],
"plugins":["transform-object-rest-spread"]
}
```
# 三、编译
## es6文件夹底下新建es6.js
```js
    let number = [1,2,3];
    let double = number.map((n) => n*2);
    console.log(double);
```

如果出现红红黄黄的报错
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
File  =>  settings  =>  Languages  =>  JavaScript  =>  JavaScript language version 改为ECMAScript6
<div align=center>
![“好看死了的图片”](/images/code/20170327001.png)
</div>
然后apply一下、
## cmd编译
`$ babel es6.js` 
cmd窗口的结果：
```cmd
"use strict";

/**
*Created by rawraw on 2017/3/27.
var number = [1, 2, 3];
var double2 = number.map(function (n) {
  return n * 2;
});
console.log(double2);
```
## 手动编译 
先试一下安装的杂七杂八能不能运行起来
### cmd
#### 文件 to 文件
```
$ babel es6/es6.js -o es5/es5.js
//或者
$ babel es6/es6.js --out-file es5/es5.js
```
#### 文件夹 to 文件夹
```
$ babel es6 -d es5
//或者
$ babel es6 --out-dir es5
```
#### 文件夹 to 文件
```
$ babel es6 -d es5
//或者
$ babel es6 --out-file es5/es5.js
```
#### 直接运行es6 code
`babel-node`
### 通过phpstorm下面的terminal
<div align=center>
![“好看死了的图片”](/images/code/20170327012.png)
</div>
嗯，好，很完美。然后es5文件夹下es5.js的内容试这样子的
```js [es5.js]
"use strict";
var number = [1, 2, 3];
var double2 = number.map(function (n) {
  return n * 2;
});
console.log(double2);
```
## 自动编译
### cmd监听
```
$ babel es6/es6.js -w -o es5/es5.js
//或者
$ babel es6/es6.js --watch --out-file es5/es5.js
```

### phpstorm添加事件监听
这个时候，如果讲道理的话，自己会弹出来这个，那就很happy地点击add添加事件监听。
<div align=center>
![“好看死了的图片”](/images/code/20170327002.png)
</div>
不讲道理的话，
↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
File  =>  settings  =>  Tools  =>  File Watchers  =>  +  =>  Babel
![“好看死了的图片”](/images/code/20170327003.png)
![“好看死了的图片”](/images/code/20170327005.png)
![“好看死了的图片”](/images/code/20170327006.png)
名字随意取咯~
如果这个时候apply,不设置编译后目标文件夹，默认是在该文件下生成一个js和js.map
Tips:在babel监听配置之前，已存在的js文件，需要发生修改，才会触发自动编译。可以在中间回车几下。
不过好丑好难过啊，还是整一个文件夹给它吧(自动编译定位在虚线内，也可以跳过啊，并没有影响)
![“好看死了的图片”](/images/code/20170327008.png)
---
好啦好啦，开始正式配置了、
主要修改scope 和 output paths,就是编译前的文件夹和编译后的文件夹
![“好看死了的图片”](/images/code/20170327004.jpg)
需要进行编译的文件夹：
![“好看死了的图片”](/images/code/20170327007.png)
绿色框框的是哪个按钮啥意思自己去百度哈，总之就是选文件夹用的、
如果这个时候apply,不设置编译后目标文件夹，默认是在该文件下生成一个js和js.map
![“好看死了的图片”](/images/code/20170327008.png)
![“好看死了的图片”](/images/code/20170327009.png)
![“好看死了的图片”](/images/code/20170327010.png)
![“好看死了的图片”](/images/code/20170327011.png)
原：`$FileNameWithoutExtension$-compiled.js:$FileNameWithoutExtension$-compiled.js.map`
改：`$ProjectFileDir$\es5\$FileNameWithoutExtension$.js`

---
并且，很稳地出现报错：
<div align=center>
![“好看死了的图片”](/images/code/20170526001.png)
</div>
主要就是这句：`Error: Couldn't find preset "env" relative to directory "es5"`