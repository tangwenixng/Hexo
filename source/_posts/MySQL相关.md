---
title: MySQL相关
tags: [MySQL]
categories: [数据库]
---

授予访问权限：

1. 登入Mysql:   ```mysql -u root -p```
2. ```grant all privileges on  *.* to root@'%' identified by 'qwer';```//给予所有数据库访问权限，若要指定固定IP，替换%即可
   ``` grant all privileges on test.* to 'root'@'%' identified by 'qwer';```//给予指定数据库访问权限；

[参考来源](http://www.111cn.net/database/mysql/41034.htm)

---

导入sql文件： `source filename`