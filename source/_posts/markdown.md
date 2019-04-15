---
title: markdown常用语法
date: 2017-04-11 10:18:51
tags: [markdown,hexo]
---

markdown：语法比较少也简单，用来写作排版很棒哦、
markdownpad：编译+预览的功能。纯编译的话，一般编辑器都可以。
[markdownpad2破解绿色中文版下载](http://pan.baidu.com/s/1dF25AX7)&emsp;提取密码：2ne1
<!--more-->
# 一、标题
##### 1.第一种方法的标题

<font color='#0080ff'>code：</font>

```markdown 
# 一级标题
## 二级标题
### 三级标题 
#### 四级标题
##### 五级标题
###### 六级标题
```
<font color='#0080ff'>结果：</font>
<font color='red'>最小到6个\#\#\#\#\#\#</font>

# 一级标题
## 二级标题
### 三级标题 
#### 四级标题
##### 五级标题
###### 六级标题

##### 2. 第二种方法的标题

<font color='#0080ff'>code：</font>

```markdown
一级标题
=============

二级标题
----
```
<font color='#0080ff'>结果：</font>

一级标题
=============

二级标题
----

##### 3. 第三种方法的标题

<font color='#0080ff'>code：</font>

```markdown
<font size=1>rawraw</font>
<font size=2>rawraw</font>
<font size=3>rawraw</font>
<font size=4>rawraw</font>
<font size=5>rawraw</font>
<font size=6>rawraw</font>
<font size=7>rawraw</font>
<font size=8>rawraw</font>
```
<font color='#0080ff'>结果：</font>
<font color='red'>最大到7</font>
<font size=1>rawraw</font>
<font size=2>rawraw</font>
<font size=3>rawraw</font>
<font size=4>rawraw</font>
<font size=5>rawraw</font>
<font size=6>rawraw</font>
<font size=7>rawraw</font>
<font size=8>rawraw</font>

# 二、排序

<font color='#0080ff'>code：</font>

```markdown
//无序 * == + == -
* raw
* rawraw
* raw
+ raw
+ rawraw
+ rawrawraw
- raw
- rawraw
- rawrawraw
//有序，相当于自己写吧
1. 提莫
2. 娑娜
3. 莫甘娜
```
<font color='#0080ff'>结果：</font>

* raw
* rawraw
* raw
+ raw
+ rawraw
+ rawrawraw
- raw
- rawraw
- rawrawraw
1. 提莫
2. 娑娜
3. 莫甘娜

# 三、引用

<font color='#0080ff'>code：</font>

```markdown
    > 这是一段引用
    >> 这是一段引用的嵌套
```

<font color='#0080ff'>结果：</font>

> 这是一段引用
>> 这是一段引用的嵌套

# 四、图片

<font color='#0080ff'>code：</font>

```markdown
![“好看死了的图片”](/images/bg/0004.jpg)
```

<font color='#0080ff'>结果：</font>

![“好看死了的图片”](/images/bg/0004.jpg)

# 五、链接

<font color='#0080ff'>code：</font>

```markdown
[去吧，皮卡丘](nothing)
[回到主页](http://rawraw.info)
飞去百度吧[Baidu] [1] ,或者[Rawraw] [2] 或者 [nothing] [3].
  [1]: http://www.baidu.com/    "Baidu"
  [2]: http://rawraw.info  "Rawrawh"
  [3]: nothing    "nothing"
```

<font color='#0080ff'>结果：</font>

[去吧，皮卡丘](nothing)
[回到主页](http://rawraw.info)
飞去百度吧[Baidu] [1] ,或者[Rawraw] [2] 或者 [nothing] [3].
  [1]: http://www.baidu.com/    "Baidu"
  [2]: http://rawraw.info  "Rawraw"
  [3]: nothing    "nothing"
  
*文章内部链接的话，可以利用a的锚点*   
  
# 六、代码  

<font color='#0080ff'>code：</font>

```markdown
    //行内代码
    `body { margin: 0; padding: 0; }`
    //行内代码代码块
    ```CSS [reset.css]
    body { margin: 0; padding: 0; }
    \`\`\`
```

<font color='#0080ff'>结果：</font>

`body { margin: 0; padding: 0; }`

```CSS [reset.css]
    body { margin: 0; padding: 0; }
```

# 七、分割线

<font color='#0080ff'>code：</font>

```markdown 
    ***
    //或者
    ---
```

<font color='#0080ff'>结果：</font>

***

---

# 八、斜体

<font color='#0080ff'>code：</font>

```markdown 
//_和* 一样
_我是歪的_
*我是歪的*
```
<font color='#0080ff'>结果：</font>

_我是歪的_
*我是歪的*

# 九、表格

好麻烦

<font color='#0080ff'>code：</font>

```markdown
| 立正！        | 向左看！       | 向右看齐！|
| :----------: |----------    | -----:  |
| 拉克丝        | 潘森          | 伊泽瑞尔 |
| 弗拉基米尔     | 波比          | 崔丝塔娜 |
| 费德提克       | 雷克顿        |    库奇 |
```

<font color='#0080ff'>结果：</font>

| 立正！        | 向左看！       | 向右看齐！|
| :----------: |----------    | -----:  |
| 拉克丝        | 潘森          | 伊泽瑞尔 |
| 弗拉基米尔     | 波比          | 崔丝塔娜 |
| 费德提克       | 雷克顿        |    库奇 |

# 十、phpstorm中的markdown插件

Setting --> Plungins --> 搜索markdown ，install



