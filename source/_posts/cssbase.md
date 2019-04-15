---
title: css基础小结
date: 2018-03-19 20:52:43
tags: [css] 
categories: 小结
---
css tips~

<!--more-->

## 初始化
>不同浏览器的一些标签的默认值不同

## 盒子模型

默认为box-sizing是content-box；
标准盒子模型（content-box）：宽度=内容的宽度（content）+ border + padding + margin
低版本IE盒子模型（border-box）：宽度=内容宽度（content+border+padding）+ margin

## 选择器
id、类、标签选择器、相邻选择器、子选择器（ul > li）、后代选择器（li a）、通配符选择器（*）、属性选择器（a[rel=”external”]）、伪类选择器

## 优先级算法
元素选择符： 1
class选择符： 10
id选择符：100
元素标签：1000
!important

## 继承性
盒子属性不可继承
可继承的属性：font-size, font-family, color
不可继承的样式：border, padding, margin, width, height

## 居中
自己去翻那篇居中的
有空来放个链接

## a的hover顺序
 `a:link {} a:visited {} a:hover {} a:active {}`
 
## 隐藏的几种方法
1.display：none 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）
2.visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）
3.层级z-index
4.定位定到天边去吧

chrome中，使用visibility：collapse值和使用hidden没有区别。
firefox，opera和IE，使用collapse值和使用display：none没有什么区别。 
 
## float
清浮动:伪类
浮动元素的display:block
 
## CSS3新特性

* rgba
* `background-image background-origin(content-box/padding-box/border-box) background-size background-repeat`
* `word-wrap：break-word`
* `text-shadow： 1px 1px 1px #666666;`
* `border-radius`
* `border-image: url(border.png) 30 30 round`
* `box-shadow: 10px 10px 5px #666666`
* font-face属性：定义自己的字体
* 媒体查询：定义两套css，当浏览器的尺寸变化时会采用不同的属性

## 兼容性问题

* IE6双边距bug
块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大。hack：display:inline;将其转化为行内属性。
* 渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用“9”这一标记，将IE浏览器从所有情况中分离出来。接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。
```
{
background-color:#f1ee18;/*所有识别*/
.background-color:#00deff9; /*IE6、7、8识别*/
+background-color:#a200ff;/*IE6、7识别*/
_background-color:#1e0bd1;/*IE6识别*/
}
```

* 设置较小高度标签（一般小于10px），在IE6，IE7中高度超出自己设置高度。
hack：给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。
* IE下，可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性；
Firefox下，只能使用getAttribute()获取自定义属性。
解决方法:统一通过getAttribute()获取自定义属性。
* Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,可通过加入 CSS 属性 `-webkit-text-size-adjust: none;` 解决。

## BFC规范(块级格式化上下文：block formatting context)
定位方案：

* 内部的Box会在垂直方向上一个接一个放置。
* Box垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的margin会发生重叠。
* 每个元素的margin box 的左边，与包含块border box的左边相接触。
* BFC的区域不会与float box重叠。
* BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
* 计算BFC的高度时，浮动元素也会参与计算。

满足下列条件之一就可触发BFC

* 根元素，即html
* float的值不为none（默认）
* overflow的值不为visible（默认）
* display的值为inline-block、table-cell、table-caption
* position的值为absolute或fixed

举个栗子：
上下margin重合的问题：在重合元素外包裹一层容器，并触发该容器生成一个BFC。`overflow: hidden; `

## 响应式设计
一个网站能够兼容多个终端，通过媒体查询检测不同的设备屏幕尺寸做处理。
`<meta name="’viewport’" content="”width=device-width," initial-scale="1." maximum-scale="1,user-scalable=no”"/>`

## 媒体查询
* <head>:`<link rel=”stylesheet” type=”text/css” href=”xxx.css” media=”only screen and (max-device-width:480px)”>`
* CSS : `@media only screen and (max-device-width:480px)`

## 浏览器是怎样解析CSS选择器的？
CSS选择器的解析是从右向左解析的。若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面。
而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 Render Tree。

## 在网页中的应该使用奇数还是偶数的字体？为什么呢？
使用偶数字体。偶数字号相对更容易和 web 设计的其他部分构成比例关系。Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。

## 怎么让Chrome支持小于12px 的文字？
   `p{font-size:10px;-webkit-transform:scale(0.8);}`
  
## 让页面里的字体变清晰 
  只在ios`webkit-font-smoothing：antialiased 灰度平滑`
  
## android：position:fixed无效
`<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>`
  
## 手动写动画的最小时间间隔是多久   
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms。
   
## inline-block间隙 
float/font-size:0、letter-spacing、word-spacing

## 行内级元素末尾实现换行,用伪元素代替<br>
```css
.test::after{
    content: "A";//0x000A,00A
    white-space: pre;
}
```
   
* 百分比的padding和margin的依据都是父元素的width
* 视差滚动插件：parallax-scrolling
* 多行文本垂直居中：需要设置display属性为inline-block。