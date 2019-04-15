---
title: xampp配置虚拟主机
date: 2017-05-16 14:56:42
tags: [xampp]
---
xampp配置虚拟主机
<div align=center>
![“封面”](/images/bg/0019.jpeg)
</div>
<!--more-->
首先，xampp要可以基本运行起来
# 域名配置
<div align=center>
![“路径”](/images/code/20170516001.png)
</div>
以管理员身份运行hosts,新增`127.0.0.1 test.com`
# xampp配置

```
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host2.example.com
    DocumentRoot "E:/test"  ## 文件根目录
    ServerName  test.com    ## 虚拟域名
    <Directory E:/test>     ## 文件根目录
        Options -Indexes
        AllowOverride ALL
        DirectoryIndex index.php index.html
        Require all granted
    </Directory>
</VirtualHost>
```

