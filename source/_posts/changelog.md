---
title: changelog
date: 2020-04-07 16:52:00
tags:
categories:
---

<!-- <div align=center>
![“封面”](/images/bg/0150.jpeg)
</div> -->

项目自动化-cz-conventional-changelog

<!--more-->

<!-- https://www.cnblogs.com/zivxiaowei/p/10089201.html -->

`$ yarn add -g commitizen`
`npm install -g commitizen --ignore-scripts spawn-sync`

sudo mkdir -p /usr/local/include /usr/local/lib /usr/local/sbin
sudo chown -R $(whoami) /usr/local/include /usr/local/lib /usr/local/sbin
最后在重新进行软连接：
brew link node

全局安装
`$ yarn add -g cz-conventional-changelog`
本地安装
`$ yarn add cz-conventional-changelog --save-dev`
或者使用 commitizen 工具
`$ commitizen init cz-conventional-changelog --save-dev --save-exact`

全局安装完成后，我们需要在项目根目录下添加 .czrc 配置文件，文件内容如下：
```
// path 用来指定适配器
{ "path": "cz-conventional-changelog" }
```

本地安装，commitizen 工具会自动在package.json中添加配置相应的配置，如下：
```
  "config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
  }
```

安装并添加完后，我们便可以使用 git cz 命令替换 git commit 来使用




