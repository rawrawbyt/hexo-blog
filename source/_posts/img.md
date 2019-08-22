---
title: 消除图片间的间隙（行内元素）
date: 2018-09-22 14:34:11
tags: [css]
categories: Note
---

<div align=center>
![“封面”](/images/bg/0133.jpeg)
</div>
<!--more-->

### 原因

img标签为inline元素，该元素默认垂直对齐方式为以父元素的baseline，但是展示时又是以bottomline为对齐方式，因此造成了上下两个img标签之间的间隙

top-line/middle-line（top和bottom的中间）/base-line/bottom-line

### 方案

1.`img{ display:block}`
过于暴力，相当于从根本上改变了img。
2.`img{vertical-align:top;}`
改变其垂直对齐方式
3.`div{font-size:0};`
把父元素的文字大小设置为0
4.`div{ margin-bottom:-3px };`
这可真low
