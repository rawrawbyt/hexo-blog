---
title: navicat for mysql安装问题
date: 2017-05-16 14:57:22
tags: [mysql]
categories: Note
---

navicat for mysql安装问题小集合
<div align=center>
![“封面”](/images/bg/0024.jpeg)
</div>
<!--more-->
# 1045

```
C:\xampp\MySQL\bin mysql -u root mysql  
mysql> UPDATE user SET Password=PASSWORD('newpassword') where USER='root';
mysql> FLUSH PRIVILEGES;
mysql> quit  
```