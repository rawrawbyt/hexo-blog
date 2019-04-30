---
title: API大全整理/from github
date: 2017-06-13 17:47:54
tags: [api]
categories: 别人家的好东西
---
偶然发现的github上的API，蛮好用的吼、
<div align=center>
![“封面”](/images/bg/0038.jpeg)
</div>
<!--more-->
# emoji表情包大全
`https://api.github.com/emojis`
`GET`
返回数据格式：
```js
{
  "+1": "https://assets-cdn.github.com/images/icons/emoji/unicode/1f44d.png?v7",
  "-1": "https://assets-cdn.github.com/images/icons/emoji/unicode/1f44e.png?v7",
  "100": "https://assets-cdn.github.com/images/icons/emoji/unicode/1f4af.png?v7",
  "1234": "https://assets-cdn.github.com/images/icons/emoji/unicode/1f522.png?v7",
  //...
  }
```
# markdown编辑器
`https://api.github.com/markdown`
`POST`
```js
data = 
{   "text":"#test",
    "mode": "gfm",
    "context": "github/gollum"
    }
```
返回数据：html
