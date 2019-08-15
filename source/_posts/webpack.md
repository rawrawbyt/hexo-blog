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


