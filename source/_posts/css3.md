---
title: 好用的小东西整理
date: 2017-05-03 15:40:56
tags: [css,JavaScript]
categories: Note
---

常用的css3巴拉巴拉的，js小技巧-_-
<div align=center>
![“封面”](/images/bg/0008.jpeg)
</div>
<!--more-->

# CSS部分
---
## 移动端
### 将文本分成多列
```
#test{
   -moz-column-count:3; 
   -webkit-column-count:3; 
   column-count:3;
}
```
### 创建模糊文本
```
#test {
   color: transparent;
   text-shadow: 0 0 5px rgba(0,0,0,0.5);
}   
```   
### pre标签内文本自动换行
```
    pre{
        overflow: auto;
        background-color: #f1f1f1;
        overflow-x: auto; /* Use horizontal scroller if needed; for Firefox 2, not
        white-space: pre-wrap; /* css-3 */
        white-space: -moz-pre-wrap !important; /* Mozilla, since 1999 */
        word-wrap: break-word; /* Internet Explorer 5.5+ */
        margin: 0;
        padding:5px 5px 3px 5px;
        white-space : normal; /* crucial for IE 6, maybe 7? */
    }
```
### 表格自动宽度
```
td {
    white-space: nowrap;
}
```
### 让滚动条顺溜地滑
定位后的滑动会出现卡顿
```
body {
  -webkit-overflow-scrolling: touch;
  overflow-scrolling: touch;
}
```
### 长按闪退
```
#test{
  -webkit-touch-callout: none;
}
```
### select 设置右对齐
```
select option {
    direction: rtl;
}
```
### touch时有半透明灰色遮罩（ios和android）
```
#test{
  -webkit-tap-highlight-color:rgba(255,255,255,0)
}
```
### 输入框默认内阴影、以及默认样式(ios)
```
#test{
  -webkit-appearance: none; 
}
```
### 部分机型存在type为search的input，自带close按钮样式
>`#Search::-webkit-search-cancel-button{
    display: none; 
  }`

### 默认首字母会大写(ios)
>`<input type="text" autocapitalize="off" />`

### 圆角失效(某些Android)
```
#test{
  background-clip: padding-box; 
}
```
### 移动端伪类 `:active` 失效
移动端应该是touch
>`<body ontouchstart="">` 
>或者`document.addEventListener('touchstart',function(){},false);`

## 浏览器
### 禁止复制、选中文本
```
#test{
    -webkit-user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
     user-select: none;
}
```

### 消除 IE10 的叉号
>`input:-ms-clear{display:none;}`

### css垂直居中
 ![去这里看](center)         
          
## CSS3
### 伪类
#### 修改选中文本的颜色：
```css [ 举一个栗子 ]
user-select:none
::selection{
color: white;
background-color: red;
}
 
::-moz-selection {
color: white;
background-color: red;
}
```
#### 首字母设置
```
#test:first-child::first-letter{
  font-size: 28px;
  font-weight: bold;
}
/*首字下沉*/
p:first-letter{
    display:block;
    margin:5px 0 0 5px;
    float:left;
    color:#FF3366;
    font-size:60px;
    font-family:Georgia;
    }
```
### 透明度的兼容
```
#test {
    filter: alpha(opacity=50); /* internet explorer */
    -khtml-opacity: 0.5;      /* khtml, old safari */
    -moz-opacity: 0.5;       /* mozilla, netscape */
    opacity: 0.5;           /* fx, safari, opera */
}
```
### webkit mask遮罩
要记得来写
http://www.cnblogs.com/cosiray/archive/2012/12/06/2804770.html
### transform出现锯齿
```
-webkit-transform: rotate(-4deg) skew(10deg) translateZ(0);
 transform: rotate(-4deg) skew(10deg) translateZ(0);
 outline: 1px solid rgba(255,255,255,0)
```
### 渐变

```CSS [ 举一个栗子 ]
/*上至下，默认方向*/
#test{
  background: -webkit-linear-gradient(#000, #fff); 
  background: -o-linear-gradient(#000, #fff); 
  background: -moz-linear-gradient(#000, #fff);
  background: linear-gradient(#000, #fff); 
}
/*左至右*/
#test2 {
  background: -webkit-linear-gradient(left, #000 , #fff);
  background: -o-linear-gradient(right, #000, #fff); 
  background: -moz-linear-gradient(right, #000, #fff); 
  background: linear-gradient(to right, #000 , #fff); 
}
/*角度。12点方向为0deg,顺时针增加deg*/
#test3 {
  background: -webkit-linear-gradient(180deg, #000, #fff); 
  background: -o-linear-gradient(180deg, #000, #fff); 
  background: -moz-linear-gradient(180deg, #000, #fff);
  background: linear-gradient(180deg, #000, #fff);
}
/*也可以径向渐变，多种颜色，透明度*/
#test4{
  background: -webkit-radial-gradient(#000 , #fff 10%, #000 20%);
  background: -o-radial-gradient(#000, #fff 10%, #000 20%); 
  background: -moz-radial-gradient(#000, #fff 10%, #000 20%); 
  background: radial-gradient(#000, #fff 10%, #000 20%); 
}
```

# JS部分
---

## 中文输入法输入英文时，有六分之一空格（ios）
>`this.value = this.value.replace(/\u2006/g, '');`

## 移动端autoplay 失效问题
必须由用户来触发才可以播放。
touchstart 触发播放并暂停（音频开始加载，后面用 JS 再操作就没问题了）。
>`document.addEventListener('touchstart', function () {
  document.getElementsByTagName('audio')[0].play();
  document.getElementsByTagName('audio')[0].pause();
});`

## 批量修改样式

```js [ 举一个栗子 ]
div.style.cssText = 'width:100px;height:100px;'
```

## 展开select的option
```
function showDropdown(sltElement) {
  var event;
  event = document.createEvent('MouseEvents');
  event.initMouseEvent('mousedown', true, true, window);
  sltElement.dispatchEvent(event);
};
```

# HTML部分
---

## meta标签
### apple-mobile-web-app-capable
apple-mobile-web-app-capable是设置Web应用是否以全屏模式运行。
>`<meta name="apple-mobile-web-app-capable" content="yes">`

### 缓存
有时候改了bug刷新并没有卵用，然后就好气啊。
手机页面通常在第一次加载后会进行缓存，然后每次刷新会使用缓存而不是去重新向服务器发送请求。
>`<meta http-equiv="Cache-Control" content="no-cache" />`
format-detection 启动或禁用自动识别页面中的电话号码。
>`<meta name="format-detection" content="telephone=no">`

### 奇怪的浏览器强制屏幕

```
<!-- QQ浏览器私有 -->
<!-- 全屏模式 -->
<meta name="x5-fullscreen" content="true">
<!-- 强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- 强制横屏 -->
<meta name="x5-orientation" content="landscape">
<!-- 应用模式 -->
<meta name="x5-page-mode" content="app">
 
<!-- UC浏览器私有 -->
<!-- 全屏模式 -->
<meta name="full-screen" content="yes">
<!-- 强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- 强制横屏 -->
<meta name="screen-orientation" content="landscape">
<!-- 应用模式 -->
<meta name="browsermode" content="application">
```

## 移动端拨打电话功能（安卓、ios都可以）
>`<a href="tel:10086">10086</a>`

## app
### 横屏字体
text-size-adjust 为 none 可以解决 iOS 上的问题，但桌面版 Safari 的字体缩放功能会失效，因此最佳方案是将 text-size-adjust 为 100% 
>-webkit-text-size-adjust: 100%;
 -ms-text-size-adjust: 100%;
 text-size-adjust: 100%;
### 顶部状态栏背景色
先指定全屏模式 `apple-mobile-web-app-capable`
>`<meta name="apple-mobile-web-app-status-bar-style" content="blank" />`

> content:default               正常显示
          blank                 黑色背景
          lank-translucent      黑色半透明，页面主体会向上占据位置
          
### 桌面图标
图片尺寸可以设定为57*57（px）或者Retina可以定为114*114（px），ipad尺寸为72*72（px)
><link rel="apple-touch-icon" href="touch-icon-iphone.png" />
 <link rel="apple-touch-icon" sizes="76x76" href="touch-icon-ipad.png" />
 <link rel="apple-touch-icon" sizes="120x120" href="touch-icon-iphone-retina.png" />
 <link rel="apple-touch-icon" sizes="152x152" href="touch-icon-ipad-retina.png" />
 
去光泽
> `<link rel="apple-touch-icon-precomposed" href="touch-icon-iphone.png" />` 

### 启动画面
>`<link rel="apple-touch-startup-image" href="start.png"/>`
iOS下页面启动加载时显示的画面图片，避免加载时的白屏。
可以通过madia来指定不同的大小：
```
<!--iPhone-->
 <link href="apple-touch-startup-image-320x460.png" media="(device-width: 320px)" rel="apple-touch-startup-image" />
  
 <!-- iPhone Retina -->
 <link href="apple-touch-startup-image-640x920.png" media="(device-width: 320px) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image" />
  
 <!-- iPhone 5 -->
 <link rel="apple-touch-startup-image" media="(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2)" href="apple-touch-startup-image-640x1096.png">
  
 <!-- iPad portrait -->
 <link href="apple-touch-startup-image-768x1004.png" media="(device-width: 768px) and (orientation: portrait)" rel="apple-touch-startup-image" />
  
 <!-- iPad landscape -->
 <link href="apple-touch-startup-image-748x1024.png" media="(device-width: 768px) and (orientation: landscape)" rel="apple-touch-startup-image" />
  
 <!-- iPad Retina portrait -->
 <link href="apple-touch-startup-image-1536x2008.png" media="(device-width: 1536px) and (orientation: portrait) and (-webkit-device-pixel-ratio: 2)" rel="apple-touch-startup-image" />
  
 <!-- iPad Retina landscape -->
 <link href="apple-touch-startup-image-1496x2048.png"media="(device-width: 1536px) and (orientation: landscape) and (-webkit-device-pixel-ratio: 2)"rel="apple-touch-startup-image" />
 
```