---
title: webpack config
date: 2019-08-13 11:18:57
tags: [webpack]
categories:
---

<div align=center>
![“封面”](/images/bg/0128.jpeg)
</div>

<!--more-->

## 打包原理
webpack只是一个打包模块的机制，只是把依赖的模块转化成可以代表这些包的静态文件。webpack就是识别你的 入口文件。识别你的模块依赖，来打包你的代码。
webpack做的就是分析代码，转换代码，编译代码，输出代码。

webpack中每个模块有一个唯一的id，是从0开始递增的。整个打包后的bundle.js是一个匿名函数自执行。参数则为一个数组。数组的每一项都为个function。function的内容则为每个模块的内容，并按照require的顺序排列。

如何实现一个简单的webpack
* 读取文件分析模块依赖
* 对模块进行解析执行(深度遍历)
* 针对不同的模块使用相应的loader
* 编译模块，生成抽象语法树AST。
* 循环遍历AST树，拼接输出js。

loader原理
在解析对于文件，会自动去调用响应的loaderloader 本质上是一个函数，输入参数是一个字符串，输出参数也是一个字符串。当然，输出的参数会被当成是 JS 代码，从而被 esprima 解析成 AST，触发进一步的依赖解析。webpack会按照从右到左的顺序执行loader。

[打包原理](https://www.jianshu.com/p/e24ed38d89fd)

## 区分环境
```js
const fs = require('fs');
const exec = require('child_process').exec;

exec('git rev-parse --abbrev-ref HEAD', (_error, stdout, _stderr) => {
  let url = stdout.replace(/^\s+|\s+$/g, '');
  let pageUrl = '';
  if (url === 'master') {
    url = 'https://api.duoxuanmall.com';
    pageUrl = 'https://native.duoxuanmall.com'
  } else {
    url = 'https://dailyapi.duoxuanmall.com';
    pageUrl = 'https://dailynative.duoxuanmall.com'    
  }
  const content = `
    export const rootUrl = '${url}'
    export const pageUrl = '${pageUrl}'
  `
  fs.writeFile('./config/rootUrl.js', content, function (err) {
    if(err) {
      console.log(err);
    }else{
      console.log('success')
    }
  })
})
```
##### [生成的文件]

```js
    export const rootUrl = ''
    export const pageUrl = ''
```

## 自定义ip
`"dev": "node bin/get_enviroment.js && webpack-dev-server --config ./webpack.config.js --host 192.168.7.236 --port 8086",`


