---
title: gulp配置
date: 2019-04-18 14:22:21
tags: [gulp]
categories: Note
---

gulp配置
<div align=center>
![“封面”](/images/bg/0164.jpg)
</div>

<!--more-->

# config

## 端口

```
gulp.task('connect', function () {
    connect.server({
        port: 3006,
        livereload: true,
        host: '0.0.0.0'
    });
});
```

## 自定义标签

### if_eq

```
hbs.handlebars.registerHelper('if_eq',function(v1,v2,name){
    if(v1 == v2){
        return name.fn(this)
    }else{
        return name.inverse(this)
    }
})
```
