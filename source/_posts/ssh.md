---
title: ssh哦
date: 2019-07-18 11:07:55
tags: [ssh]
categories: Note
---

<div align=center>
![“封面”](/images/bg/0171.jpg)
</div>
<!--more-->


#### 检查.ssh文件夹是否存在

`$ ls -al ~/.ssh`

#### 不存在

新建.ssh文件夹
`$ mkdir ~/.ssh`
`$ cd ~/.ssh`
`$ ssh-keygen -t rsa -C "your_email@example.com"`
连续按三次回车`id_rsa   id_rsa.pub`

#### 查看公钥

`$ cat id_rsa.pub`

#### 将密钥复制到剪贴板

`pbcopy < ~/.ssh/id_rsa.pub`

#### 生成多个ssh
`ssh-keygen -t rsa -C "xxx@gmail.com"`
命名`id_rsa_rawraw`
会生成`id_rsa_rawraw   id_rsa_rawraw.pub`

