---
title: hexo搭建个人博客
date: 2017-04-07 10:58:23
tags: [hexo]
categories: 别人家的好东西
---
很酷啊~hexo+github,再加上十几二十块买个酷酷的域名,完成这个小站哦~写写学习笔记，写写杂七杂八的小东西，虽然可能没什么人来看，但是，我开心呀~~~
<div align=center>
![“封面”](/images/bg/0020.jpeg)
</div>
<!--more-->
<font size=5>一、hexo</font>
先配hexo再拉git库吧，不然.git文件在hexo初始化的时候被删掉也是一个心烦的事情内。
<font size=4>//1、安装node环境（基本可以忽略，都装了吧）</font>

```
$ cnpm install npm -g
```
<font size=4>//2、全局安装hexo依赖</font> 
```
$ npm install -g hexo-cli
```
<font size=4>//3、初始化博客文件夹</font>
```
 $ npm init [folder]
```
第一次尝试的报错：
<div align=center>
![“报错”](/images/code/20170407001.png)
</div>
说是swig和minimatch要升级到3.0.2的问题，那就在安装一下swig,再升级一下minimatch咯

```
 $ npm install swig
 $ npm minimatch@”3.0.2”
```
第二次尝试的报错：
<div align=center>
![“报错”](/images/code/20170407003.png)
</div>
还是swig有问题咯，那就再装，哼，明明绿了
<div align=center>
![“报错”](/images/code/20170407002.png)
</div>
第三次尝试的报错：还是跟第二次一样！！
<div align=center>
![“报错”](/images/code/20170407004.png)
</div>
还有这个关于fsevents的报错，是可以忽略的
反正他跟你说缺啥，你就用npm install补啥
看到<font color='green'>INFO</font> Start blogging with Hexo!这句话就ok啦
<font size=4>//4、启动hexo</font>
```
 $ hexo sever
 //或者
 $ hexo s
 //可以自定义端口号，默认是4000，没事也就别改啦
 $ hexo server -p 1102  //指定1102端口
```
如果前面看到<font color='green'>INFO</font> Start blogging with Hexo!，这一步基本没问题。
<div align=center>
![“报错”](/images/code/20170407007.png)
</div>
听话地去浏览器打开http://localhost:4000，然后看到这样
<div align=center>
![“报错”](/images/code/20170407006.png)
</div>
没有报错最开心了！！第一步搞定！这是hexo的默认主题和配置，然后就可以开始屁颠屁颠改成自己喜欢的样子了咧。

<font size=5>二、github</font>
<font size=4>//1、建立github库</font>
Tip:命名必须 账户名.github.io
<font size=4>//2、项目拉取到本地</font> 
```
$ git clone https://github.com/yourname/yourname.github.io
```
<font size=5>三、hexo/github大合体</font>
<font size=4>//1、安装deployer依赖</font>

```
$ npm install hexo-deployer-git --save
```

<font size=4>//2、hexo配置修改</font>
<div align=center>
![“报错”](/images/code/20170407005.png)
</div>

```js
node_modules -->
scaffolds    -->
source       -->    文章、图片等资源
themes       -->    站点主题的相关配置
.gitignore   -->
_config.yml  -->    主要改这个文件！！！
package.json -->
```
yes!打开_config.yml,就先改<font color='#0080ff'># Site</font>和<font color='#0080ff'># Deployment</font>这两部分先，其他的以后熟了再细看吧。
[去看完整版(有空再写哈哈)](有空再写哈哈)
```yml [_config.yml]
 # Site
 title:          #你的网站的名字咧
 subtitle:       #你的网站的副标题咧
 description:    #你的网站的描述咧
 author:         #你的大名咧
 # Deployment
 deploy:
   type: git
   repo: https://github.com/yourname/yourname.github.io.git
   branch: master
```
<font color='red'>千万千万不要忘记每个冒号后面都要有空格！！WTF!</font>
<font size=4>//3、hexo新建文章</font>
```cmd
//新建文章
$ hexo new test     //默认post
//新建草稿和文件夹（先别试这个）
$ hexo new draft test
$ hexo new page test
```
可以发现source文件夹下的_posts文件夹下多了一个test.md的文件，
<div align=center>
![“报错”](/images/code/20170407008.png)
</div>

```js [test.md]
    ---
    title: test                 //该文章标题，可以和文件名不一样的
    date: 2017-04-07 15:00:51
    tags:                       //标签，多个用数组[ tag1 , tag2 ]
    ---
```
<font size=4>//4、hexo打包</font>
```js 
$ hexo generate  //打包，等同于hexo g
```
<font size=4>//5、hexo同步到git</font>
```js 
$ hexo deploy    //上传git,等同于hexo d
```
如果出现下图，一定是前面的_config.yml里面的<font color='#0080ff'># Deployment</font>部分没有配置好。
<div align=center>
![“报错”](/images/code/20170407009.png)
</div>
注意红色部分也要有个空格！WTF!
<div align=center>
![“报错”](/images/code/20170407010.png)
</div>

<font size=5>四、世界宇宙超级无敌酷的域名合体</font>
<div align=center>
![“报错”](/images/code/20170407011.png)
</div>
<div align=center>
![“报错”](/images/code/20170407012.png)
</div>
<font size=5>五、hexo常用语句整理</font>
```js
$ hexo n  =  hexo new       //新建
$ hexo s  =  hexo server    //开启
$ hexo c  =  hexo clean     //清缓存   
$ hexo g  =  hexo generate  //打包
$ hexo d  =  hexo deploy    //上传git

```