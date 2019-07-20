---
title: vue-cli
date: 2019-07-18 15:08:51
tags: [vue,vue-cli]
categories: note
---

<div align=center>
![“封面”](/images/bg/0106.jpeg)
</div>

<!--more-->

# vue-cli3

###  一直运行 /sockjs-node/info?t= 解决方案

 sockjs-node 是一个JavaScript库，提供跨浏览器JavaScript的API，创建了一个低延迟、全双工的浏览器和web服务器之间通信通道。

服务端：sockjs-node（https://github.com/sockjs/sockjs-node）
客户端：sockjs-clien（https://github.com/sockjs/sockjs-client）

如果你的项目没有用到 sockjs，vuecli3 运行 yarn serve 之后 network 里面一直调研一个接口：http://localhost:8080/sockjs-node/info?t=1462183700002

源码关闭：

找到`/node_modules/sockjs-client/dist/sockjs.js`第1605行

```js
  try {
  //  self.xhr.send(payload); 把这里注掉
  } catch (e) {
    self.emit('finish', 0, '');
    self._cleanup(false);
  }
```
