---
title: Angular 1 vs. Angular 2 
date: 2017-07-21 13:26:52
tags: [angular]
categories: 笔记
---

Angular 1 对比 Angular 2 

<!--more-->

# get Angular 2.0
`cnpm install angular@2.0.0-alpha.6 `

# 比较
## 1.双向数据绑定
单向数据绑定
2.0中会有方法实现双向绑定，虽然实现的背后数据是单向的。这听起来很像React的Flux所做的工作。这种结构也可以被Angular来使用。
## 2.观察器
Zone.js
$scope.$watch, $scope.$apply, $timeout这些都不在需要了，这也是1.x版本有如此之大的学习曲线的原因。
Zone.js可以帮Angular实现变化的自动检测。这听起来很像React的差异比较算法。
## 3.组件通信
2.0：除了$broadcast 和 $emit，2.0还有一些小得变化，1）你可以在DOM层发送消息，而不是在scope；2）你可以组件嵌套，然后link他们，这看上去很像每个组件都使用它们独立的scope。
## 4. DOM
2.0：从很多方面可以看出，Angular 2.0对于DOM样式的操作很像React的virtual DOM，它引用的是最近呈现的view层。关于Angular Native，Misko提到，这个view层可以运行于web worker，甚至是native。
## 5. scope

## 6. 模块
2.0将肯定使用ES6的模块语法。同时，2.0还希望通过懒加载来引入依赖注入。和以往通过单例方式管理不同的是，2.0希望使用一种层次化数据结构来提供继承特性。你将能够控制模块的生命周期，比如services。
## 7. 指令
## 8. Router
## 9. HTML



[参考](http://www.html-js.com/article/AngularJS-mass-Angular-2-and-1x-comparison)