---
title: 解决连接MySQL，报错10061，系统错误5
date: 2018-06-04 12:59:59
tags: [Mysql, Java]
---
<!--more-->

## 1.解决连接MySQL，报错10061，系统错误5

mysql登录不上去，报错10061，百度后得，mysql服务未启动。。

### 方法一、选择dos窗口命令行打开mysql

输入代码

```
net start mysql
```

报错，如图所示。系统错误 5


![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/mysql_error5.png)


解决办法：使用管理员身份运行cmd.exe
成功了，如下图

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/mysql_error5_success.png)


-----
### 方法二、手工启动

计算机->右键->管理->计算机管理
找到mysql，右键启动

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/mysql_error5_a.png)