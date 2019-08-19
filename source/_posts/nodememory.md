---
title: node.js内存溢出
date: 2019-08-19 10:24:09
tags: [node]
categories:
---

转的整理；
<div align=center>
![“封面”](/images/bg/0139.jpeg)
</div>

<!--more-->

### 现象

1. 密集型运算；批量处理数据，大量循环；
2. 操作的数据量较大；对象需要频繁的创建/销毁，或操作对象本身较大；

### 原因

#### V8内存分配机制

1. V8本身分配的内存较小;
2. JavaScript语言本身限制;
3. 程序员使用不当;

> V8是 Google 在 Chrome 浏览器中使用的 JavaScript 引擎。而在浏览器环境中，运算一般不需要多大内存。
V8 对每个进程分配的运行内存，在32位系统中约为700MB，而在64位系统中约为1.4GB。

### 方案

1. 使用 async/await防止事件堆积,变为同步操作； V8 获得内存回收的机会；
每次循环V8都会回收内存一次，因此内存不会再溢出。但这样做必然会造成运行效率的降低，而应该在速度在安全之间平衡，控制好循环的安全次数。
说明:实际开发中，上面这种虽然解决了内存溢出，但是仍然会造成进程阻塞，可以开启一个进程/线程来解决阻塞问题
[深入理解Node.js 进程与线程](https://mp.weixin.qq.com/s/fkrHHMwx75NLhvv4P3rk-w)
2. 增加V8内存空间
`node --max-old-space-size=4096 app`
3. 使用非V8内存
V8内存：数组、字符串等JavaScript内置对象，运行时使用“V8内存”
系统内存：Buffer是一个Node.js的扩展对象，使用底层的系统内存，不占用V8内存空间。与之相关的文件系统fs和流Stream流操作，都不会占用V8内存。
[fs学习]（https://mp.weixin.qq.com/s/m1SqvFaqTn3Bh2Fg9500sQ）
[stream学习]（https://mp.weixin.qq.com/s/HQmualyyEV4t7lG0PZf8zQ）
[Buffer学习](https://mp.weixin.qq.com/s/t5oZmD1tR5rSlJAmSlwXOg)





