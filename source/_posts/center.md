---
title: CSS居中方法合集
date: 2017-04-09 16:54:12
tags: [css]
categories: 积累
---

居中方法合集
<div align=center>
![“封面”](/images/bg/0032.jpeg)
</div>
<!--more-->
[看demo去吧/](https://git.oschina.net/rawraw/rawrawdemo.git)
# 行元素居中
## 水平居中
`text-align:center`
## 垂直居中
`line-height`
# 块元素居中
## 水平居中
`margin: 0 auto`
## 水平垂直居中
### 方法一: 纯position + margin
本元素：`position: absolute;left: 50%;top: 50%;margin-left: -50px;margin-top: -50px;`
父元素：`position: relative;`
兼容性：兼容所有
margin值为本元素宽高的一半
```[html]
	<div class="box1">
		<div class="center"></div>
	</div>
```
```[css]
    .box1{
        position: relative;
        width: 200px;
        height: 200px;
        background: #ffd2e9;
    }
    .box1 .center {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 100px;
        height: 100px;
        background: #8cebf6;
        margin-left: -50px;
        margin-top: -50px;
    }
```
### 方法二: position + margin	
本元素：`margin: auto;position: absolute;left: 0;right: 0;top: 0;bottom: 0;`
父元素：`position: relative`
兼容：不兼容ie6
```[html]
	<div class="box2">
		<div class="center"></div>
	</div>
```
```[css]
    .box2 {
        position: relative;
        width: 200px;
        height: 200px;
        background: #ffd2e9;
    }
    .box2 .center {
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        width: 100px;
        height: 100px;
        background: #8cebf6;
        margin: auto;
    }
```
### 方法三: position + transform
#### 方法三-01
本元素：`position: absolute;top:50%;left:50%;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%);`
父元素：`position: relative`
#### 方法三-02
本元素：`position: relative;top: 50%;left:50%;display: inline-block;-webkit-transform: translate(-50%);transform: translate(-50%);`
父元素：nothing
兼容性：ie9以下不支持 transform
position定位父元素元素的宽高50%，transform定位本元素的宽高50%
```[html]
	<div class="box3">
		<div class="center"></div>
	</div>
    <div class="box3_">
        <div class="center">
            11111111
        </div>
    </div>
```
```[css]
    .box3{
        position: relative;
        width: 200px;
        height: 200px;
        background: #ffd2e9;
    }
    .box3 .center {
        position: absolute;
        top:50%;
        left:50%;
        width: 100px;
        height: 100px;
        background: #8cebf6;
        -webkit-transform:translate(-50%,-50%);
        transform:translate(-50%,-50%);
    }
    .box3_{
        width: 200px;
        height: 200px;
        background: #ffd2e9;
    }
    .box3_ .center{
        position: relative;
        top: 50%;
        left:50%;
        display: inline-block;
        background: #8cebf6;
        -webkit-transform: translate(-50%);
        transform: translate(-50%);
    }
```
### 方法四: flex + center
本元素：nothing~~
父元素：`display: flex;align-items: center;justify-content: center;`
兼容性：适合移动端
```[html]
	<div class="box4">
		<div class="center"></div>
	</div>
```
```[css]
    .box4{
        display: flex;
        width: 200px;
        height: 200px;
        align-items: center;/*垂直居中*/
        justify-content: center;/*水平居中*/
        background: #ffd2e9;
    }
    .box4  .center {
        width: 100px;
        height: 100px;
        background: #8cebf6;
    }
```
### 方法五: flex + margin
本元素：`margin: auto;`
父元素：`display: flex;`
兼容性：适合移动端
```[html]
	<div class="box5">
		<div class="center"></div>
	</div>
```
```[css]
    .box5 {
        display: flex;
        width: 200px;
        height: 200px;
        background: #ffd2e9;
    }
    .box5 .center {
        width: 100px;
        height: 100px;
        margin: auto;
        background: #8cebf6;
    }
```
### 方法六:table-cell + inline-block
本元素：`display: inline-block;`
父元素：`display: table-cell;vertical-align: middle;text-align: center;`
兼容性：不兼容ie6/7
```[html]
	<div class="box6">
		<div class="center"></div>
	</div>
```
```[css]
    .box6{
        display: table-cell;
        width: 200px;
        height: 200px;
        background: #ffd2e9;
        vertical-align: middle;
        text-align: center;
    }
    .box6 .center{
        display: inline-block;
        width: 100px;
        height: 100px;
        background: #8cebf6;
    }
```

## 不定宽高的元素居中

上述方法四五六



