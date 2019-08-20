---
title: mvc/mvvm
date: 2019-03-16 14:24:55
tags: [mvc,mvvm]
categories: Note
---

mvc/mvvm区别

<!--more-->

# MVC
Model View Controller

Model（模型）：是应用程序中用于处理应用程序数据逻辑的部分。通常模型对象负责在数据库中存取数据。
View（视图）：是应用程序中处理数据显示的部分。通常视图是依据模型数据创建的。
Controller（控制器）：是应用程序中处理用户交互的部分。通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。

MVC的思想：一句话描述就是Controller负责将Model的数据用View显示出来

众所周知，MVC 是开发客户端最经典的设计模式，iOS 开发也不例外，但是 MVC 有让人无法忽视的严重问题。

## 特点
* Model和View永远不能相互通信，只能通过Controller传递。
* Controller可以直接与Model对话（读写调用Model），Model通过Notification和KVO机制与Controller间接通信。
* Controller可以直接与View对话，通过outlet,直接操作View,outlet直接对应到View中的控件,View通过action向Controller报告事件的发生(如用户Touch我了)。Controller是View的直接数据源（数据很可能是Controller从Model中取得并经过加工了）。Controller是View的代理（delegate),以同步View与Controller。

## 缺点

View的可扩展性相当低。
在通常的开发中，除了简单的 Model、View 以外的所有部分都被放在了 Controller 里面。Controller 负责显示界面、响应用户的操作、网络请求以及与 Model 交互。这就导致了 Controller：

* 逻辑复杂，难以维护；
* 和 View 紧耦合，无法测试；

# MVVM
Model View ViewModel

Controller的存在感被完全的降低了。
本质上是一个精心优化的 MVC 架构；
既然 View 和 Controller 是一对好基友，在 MVVM 里面，干脆把它们当做 View。
现在将原来 Controller 的部分职责拆分出来由 View Model 承担，主要包括：

* 校验用户输入；
* 网络请求；
* 展示层的逻辑，比如格式化字符串；
* 其他不能放入 Model，与 View 无关的逻辑；

## 优点

* MVVM 兼容 MVC，可以先创建一个简单的 View Model，再慢慢迁移。
* MVVM 使得 app 更容易测试，因为 View Model 部分不涉及 UI。

MVVM 最好配合 binding 机制，Model 的变化需要同步到 View Model，View Model 的变化也需要同步到 View

[发展史](https://www.jianshu.com/p/b0aab1ffad93)


