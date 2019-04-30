---
title: 微信小程序是真的讨厌
date: 2018-03-01 11:04:08
tags: [wechat]
categories: oh my bug
---

   微信小程序出现好久了，一直没仔细了解。从一开始就是莫名的排斥，公司关于小程序的项目也是都直接丢给新人。今天抖音刷到一个吃饭吃什么的段子，就想说这很easy,自己写一个玩一下啊。嗯，写一个放哪儿，那就小程序吧。但是好像一点都不酷，嗯，那我给它做成云标签墙吧。
   想象中，一切都很美好。
<div align=center>
![“封面”](/images/bg/0058.jpg)
</div>

<!--more-->

# START

原来做过一个小demo是这样子的。
<div align=center>
![“效果”](/images/result/wall.gif)
</div>
讲道理一堆食物这样子滚应该很诱人吧。然后就开始一边看看文档一边写。
一切顺利地进行到这一步
<div align=center>
![“代码”](/images/code/20180301001.png)
</div>


# QUESTION

## getElement
可以直接标签内操作，但是烦。
## appendChild
可以用模板做，但是烦。而且无限的append的好像就有点难做了。



