---
title: 看看图，听听歌
tags:
---
<div align=center>
![“封面”](/images/bg/0009.jpg)
</div>

<!--more-->
<div align=center>
![“图片”](/images/words/0001.png)
</div>

要有深度。追究本质的原因，而不是绕过去。
低端文人研究道德，高端文人研究美感。


如果生活像鲨鱼而不是温火，我们会不会游的更快一些？ ​​​​
2013，别忘了答应自己要做的事，别忘了答应自己要去的地方。 ​​​​
可能我只是你生命里的一个过客，但你不会遇见第二个我。 ​​​​
"一个人过的很好的表现：他基本可以远离社交网络"
越有故事的人越沉静简单，越肤浅单薄的人越浮躁不安。 ​​​​
人和狗的区别就是 狗一直是狗 但人有时却不是人
当有人侮辱你的时候 要记得 狮子不会因为听到狗吠而回头
我走得很慢，但是我从来不会后退 -- 林肯
那些曾经泼过我冷水的人 我一定会烧开了还给你们
【心理科普：炫耀源于内心的不自信】心理学上认为，“爱向别人炫”是一种内心需要被关注被肯定的表现，很可能是因为某种东西自己不常有，一旦拥有，希望藉以外界的羡慕来建立自信。不向别人晒自己的幸福会憋死你么？如果会，最好问问为什么。记住：生活不是演戏，自己精彩就好！
长大后，这个社会教会了我，没心没肺，没感觉，不痒不疼，不在乎。
有些烦恼，丢掉了，才有云淡风轻的机会。 ​​​​
Change will not come if we wait for some other person or some other time. We are the ones we've been waiting for. We are the change that we seek.。 
如果我们总是等着别人或其他时机，改变永远不会到来。我们自己就是我们一直等待的人，我们自己就是我们所寻求的改变。——奥巴马 ​​​​


书单：
《潜意识：控制你行为的潜意识》蒙洛迪诺

1、移动端点击300ms延迟

300ms尚可接受，不过因为300ms产生的问题，我们必须要解决。300ms导致用户体验并不是很好，解决这个问题，我们一般在移动端用tap事件来取代click事件。
推荐两个js，一个是fastclick，一个是tap.js
关于300ms延迟，具体请看：http://thx.github.io/mobile/300ms-click-delay/

2、写出几种IE6 BUG的解决方法

双边距BUG：float引起的，使用display；
像素问题：使用float引起的，使用dislpay:inline -3px；
超链接hover点击后失效：使用正确的书写顺序 linkvisited hover activen  
IE z-index问题：给父级添加position:relative
Png 透明：使用js代码改
Min-height 最小高度 ！Important 解决’
select 在ie6下遮盖：使用iframe嵌套；
为什么没有办法定义1px左右的宽度容器(IE6默认的行高造成的，使用over:hidden,zoom:0.08line-height:1px)
