---
title: chorme扩展工具
date: 2019-07-18 11:32:11
tags:
categories:
---


换了台笔记本，vpn也上不去了。只能瞎搞了。
![“封面”](/images/bg/0140.jpeg)
<!--more-->

# React Devtools调试工具

## Git 地址

[Git 地址](https://github.com/facebook/react-devtools`)

`git clone https://github.com/facebook/react-devtools.git`

## 进入react-devtools文件夹，安装依赖
`npm --registry https://registry.npm.taobao.org install`

## 打包一份扩展程序

`npm run build:extension:chrome`
项目目录中生成一个新的文件夹，`react-devtools -> shells -> chrome -> build -> unpacked`文件夹

## 加载

打开chrome扩展程序chrome://extensions/，加载已解压的扩展程序，选择第3步中的生成的unpacked文件夹。

# vue-devtools

## https://github.com/vuejs/vue-devtools
`git clone https://github.com/vuejs/vue-devtools.git`
`npm i`
修改manifest.json文件
把"persistent":false改成true
`npm run build`
选择vue-devtools>shells下的chrome文件夹







