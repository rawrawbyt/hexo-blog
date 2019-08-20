---
title: 依赖包管理npm、yarn
date: 2019-05-16 16:31:30
tags: [npm,yarn]
categories: Note
---

npm和yarn区别
<!--more-->

# yarn

Yarn 同样是一个从 npm 注册源获取模块的新的 CLI 客户端。注册的方式不会有任何变化；
Yarn 是 Facebook, Google, Exponent 和 Tilde 开发的一款新的 JavaScript 包管理工具。就像我们可以从官方文档了解那样，它的目的是解决这些团队使用 npm 面临的少数问题，即：

* 安装的时候无法保证速度/一致性
* 安全问题，因为 npm 安装时允许运行代码

# 优势
* yarn.lock 文件
* 并行安装
每当 npm 或 Yarn 需要安装一个包时，它会进行一系列的任务。在 npm 中这些任务是按包的顺序一个个执行，这意味着必须等待上一个包被完整安装才会进入下一个；Yarn 则并行的执行这些任务，提高了性能。
* 清晰的输出
npm 默认情况下非常冗余，例如使用 npm install 时它会递归列出所有安装的信息；而 Yarn 则一点也不冗余，当可以使用其它命令时，它适当的使用 emojis 表情来减少信息（Windows 除外）。

# pnpm
可阅读pnpm的作者Zoltan Kochan发表的[“为什么要用pnpm？”](https://www.kochan.io/nodejs/why-should-we-use-pnpm.html)

* pnpm运行起来非常的快，超过了npm和yarn
* pnpm采用了一种巧妙的方法，利用硬链接和符号链接来避免复制所有本地缓存源文件，这是yarn的最大的性能弱点之一
* 使用链接并不容易，会带来一堆问题需要考虑。
* pnpm继承了yarn的所有优点，包括离线模式和确定性安装
