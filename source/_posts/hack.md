---
title: CSS hack
date: 2017-07-07 13:21:24
tags: [css,杂,兼容]
categories: 杂
---

待整理。
目前还不怎么需要，先搜集了一下网上大家的方法，以后方便看咯。
<!--more-->
  
# 概念
 由于不同种类的浏览器（`Internet Explorer,Safari,Mozilla Firefox,Chrome...`）或者同一浏览器的不同版本 对CSS的解析认识不一样，导致生成的页面效果不一样。针对不同的浏览器去写不同的CSS，让它能够同时兼容不同的浏览器，能在不同的浏览器中也能得到我们想要的页面效果。
# 整理

### IE 6
 ```
 * html #footer {
    position:absolute;
    top:expression((0-(footer.offsetHeight)+(document.documentElement.clientHeight ? document.documentElement.clientHeight : document.body.clientHeight)+(ignoreMe = document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop))+'px');
 }
 ```
 
###  Selector Hacks

```
/* IE6 and below */
* html #uno  { color: red }
```

```
/* IE7 */
*:first-child+html #dos { color: red } 
```

```
/* IE7, FF, Saf, Opera  */
html>body #tres { color: red }
```

```
/* IE8, FF, Saf, Opera (Everything but IE 6,7) */
html>/**/body #cuatro { color: red }
```

```
/* Opera 9.27 and below, safari 2 */
html:first-child #cinco { color: red } 
```

```
/* Safari 2-3 */
html[xmlns*=""] body:last-child #seis { color: red } 
```

```
/* safari 3+, chrome 1+, opera9+, ff 3.5+ */
body:first-of-type #ocho {  color: red }
```

```
/* saf3+, chrome1+ */
@media screen and (-webkit-min-device-pixel-ratio:0) {#diez  { color: red  }}
```

```
/* iPhone / mobile webkit */
@media screen and (max-device-width: 480px) {#veintiseis { color: red  }} 
```

```
/* Safari 2 - 3.1 */
html[xmlns*=""]:root #trece  { color: red  } 
```

```
/* Everything but IE6-8 */
:root *> #quince { color: red  }
```

```
/* IE7 */
*+html #dieciocho {  color: red }
```

```
/* Firefox only. 1+ */
#veinticuatro,  x:-moz-any-link  { color: red }
```

```
/* Firefox 3.0+ */
#veinticinco,  x:-moz-any-link, x:default  { color: red  }
```

### Attribute Hacks 

```
/* IE6 */
#once { _color: blue } 
```

```
/* IE6, IE7 */
#doce { *color: blue; /* or #color: blue */ }
```

```
/* Everything but IE6 */
#diecisiete { color/**/: blue }
```

```
/* IE6, IE7, IE8 */
#diecinueve { color: blue\9; }
```

```
/* IE7, IE8 */
#veinte { color/*\**/: blue\9; }  
```

```
/* IE6, IE7 -- acts as an !important */
#veintesiete { color: blue !ie; } /* string after ! can be anything */
```