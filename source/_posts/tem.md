---
title: 在table中margin 失效
date: 2018-05-20 14:38:47
tags: [css]
categories: Note
---

想写个某几行`tr`滑动的动画，发现margin在table里没有用，那我总不能特地搞个定位来弄这个动画吧。气。
<div align=center>
![“封面”](/images/bg/0131.jpeg)
</div>
<!--more-->

当`display：table`,`margin`会不起作用

### 方案一

`border-spacing`
设置单元格td的边在横向和纵向上的间距。
指定一个length值时，这个值将作用于横向和纵向上的间距;
指定两个length值时，第一个将作用于横向间距，第二个值将作用于纵向间距。
`table{border-spacing:5px 10px;}`

```css
    table{
        border-collapse:separate;
        border-spacing: -15px;
    }
```
