---
title: \\这个插件还可以//之select2
date: 2017-04-19 11:19:41
tags: [plugin,select2,插件]
categories: Note
---
<div align=center>
![“封面”](/images/bg/0027.jpeg)
</div>
<!--more-->

*placeholder: 一定要加空的<option></option>*

```js [ 举一个栗子 ]
$('#test').select2({
    data:[
            {id:1,text:"teemo"},
            {id:2,text:"anni"},
            //...
    ]
})
```