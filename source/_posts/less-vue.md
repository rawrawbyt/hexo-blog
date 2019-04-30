---
title: less=>vue中引入
date: 2019-04-18 14:45:19
tags: [vue,less]
categories: Note
---

在vue中引入less

<div align=center>
![“封面”](/images/bg/0160.jpeg)
</div>

<!--more-->

# step 1
`npm install less less-loader --save`
or
`yarn add less less-loader --save`

# step2

修改webpack.config.js文件，配置loader加载依赖，让其支持外部的less,在原来的代码上添加

```
{
    test: /\.less$/,
    loader: "style-loader!css-loader!less-loader",
},

```

or

```
    或者
    @import './index.less'; //引入全局less文件
    ）。

webpack.base.conf.js
    {  
        test: /\.scss$/,   
        loaders: ["style", "css", "sass","style-loader!css-loader!less-loader"]
    },
    {
        test:/\.less$/,
        loader:'less-loader'
    }
```



