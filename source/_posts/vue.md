---
title: vue集合
date: 2018-05-20 14:38:18
tags: [vue]
categories: Note
---

<div align=center>
![“封面”](/images/bg/0163.jpeg)
</div>

<!--more-->

# bugs

### 1

<font color='red'>[Vue warn]: Error in render: "TypeError: _self.$scopedSlots.default is not a function”</font>

> 究其原因，是因为表格是element-ui通过循环产生的，而vue在dom重新渲染时有一个性能优化机制，就是相同dom会被复用，这就是问题所在，所以，通过key去标识一下当前行是唯一的，不许复用，就行了。

方案：添加 <font color='red'>:key="Math.random()"</font>




