---
title: 移动端兼容性整理以及优化
date: 2018-03-23 13:28:21
tags: [兼容]
categories: 小结
---

移动端兼容性整理
<!--more-->

# 插件
Modernizr：兼容CSS3、HTML5新特性

# List
### contenteditable元素只能输入纯文本
-webkit-user-modify: read-only|read-write|read-write-plaintext-only
### IE6-8和FF3-浏览器不支持":nth-child"选择器
:nth-child(2n),:nth-child(even)
:nth-child(n+5)这个选择器是选择从第五个元素开始选择
:nth-child(4n+1)这种方法是实现隔几选一的效果，比如我们这里是隔三选一
::selection
user-select:none
# 优化
### 增加该属性，可以增加弹性（在绝对定位的时候会用到）
-webkit-overflow-scrolling: touch;
### 输入法
开始中文输入时会触发compositionstart事件
选词结束后会触发compositionend事件