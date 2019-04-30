---
title: npm常用命令
date: 2018-03-27 22:08:37
tags: [npm]
categories: Note
---


npm常用命令以及npm包发布

<!--more-->

# 安装升级
安装node以后自动会安装NPM。
## 淘宝镜像
`npm install -g cnpm --registry=https://registry.npm.taobao.org`
## 升级
`$ npm install -g npm`
# 常用
## 安装包
`$ npm install <pkg>` 或者 `$ npm install <pkg>@<version>`
## 卸载包
`$ npm uninstall <pkg>` 或者  `$ npm uninstall <pkg>@[<version>]`
## 查看当前项目下的包列表
`$ npm ls`
#查看全局包列表
`$ npm ls －g`
#清理缓存
`$ npm cache clean`
#显示包的package.json信息,后面可以跟属性名称。
e.g.：`$ npm view <pkg> versions`  其中versions是`package.json`的`versions`属性
`$ npm view <pkg> [attribute]`


# 发布自己的npm包
## 登陆
第一次：
`$ npm adduser`
输入password的时候会自动隐藏，管自己输就好了
然后邮箱一直enter不了，一直报e400的错。然后想到之前装的淘宝镜像。然后就用`cnpm`就完全o**k！！
所以 所有的命令行 自己自动都改c吧，懒得一个个改了。
not 第一次：
`$ npm login`
### 查看当前用户
`$ npm whoami `
## 发布
`$ npm init`
动次打次 怼怼怼
`$ npm publish`
`$ npm publish <pkg>@<version>`
### 报错集合
`ERR 403`:包名字重了
`npm please try running this command again as root`：未登录

## 迭代
`$ npm publish <pkg>@<version>`
### 快速升级方法
#### 小版本号升级一个版本
`$ npm version patch`
#### 中版号升级一个版本
`$ npm version minor`
#### 大版本号升级一个版本
`$ npm version major`
npm社区版本号规则采用的是semver(语义化版本)，主要规则如下：
版本格式：主版号.次版号.修订号，版号递增规则如下：
	主版号：当你做了不相容的 API 修改，
	次版号：当你做了向下相容的功能性新增，
	修订号：当你做了向下相容的问题修正。
	先行版号及版本编译资讯可以加到「主版号.次版号.修订号」的后面，作为延伸。
## 删除
不能删除整个包，只能某个版本
`$ npm unpublish <pkg>[@<version>]`
