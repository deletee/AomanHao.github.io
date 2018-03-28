---
title: 安装mysql，和遇到的一些错误及解决方案
date: 2018-03-28 10:59:59
tags: [Mysql, Java]
---

1、下载：
<!--more-->
mysql-5.7.20是解压版免安装的，mysql-5.7.20下载地址：http://dev.mysql.com/downloads/mysql/


----------


2、安装
  解压在你喜欢的位置


----------


3、配置
  新建一个ini文件，并命名为my.ini，放置到mysql根目录下，文件内容如下

```
[mysql]  
# 设置mysql客户端默认字符集  
default-character-set=utf8  
[mysqld]  
#设置3306端口  
port = 3306  
# 设置mysql的安装目录  
basedir=E:\program2\javaTool\mysql-5.7.20-winx64
# 设置mysql数据库的数据的存放目录  
datadir=E:\program2\javaTool\mysql-5.7.20-winx64\data
# 允许最大连接数  
max_connections=200  
# 服务端使用的字符集默认为8比特编码的latin1字符集  
character-set-server=utf8  
# 创建新表时将使用的默认存储引擎  
default-storage-engine=INNODB  
```

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_my_ini.png)

注：
设置mysql的安装目录 basedir=
设置mysql数据库的数据的存放目录 datadir=
这两个参数改为你所解压后的文件夹的位置


----------


4、安装mysql服务
4.1、管理员身份打开cmd.exe
文件位置C:\Windows\System32\cmd.exe,找到右击选择管理员身份打开（重点），如果没有一管理员身份打开运行cmd.exe，会报错

```
Install/Remove of the Service Denied! mysql
```

将目录切换到你mysql安装目录的bin目录后，在cmd窗口输入

```
mysqld install
```

回车运行即可。

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_succ_insta.png)

4.2、创建data文件
将目录切换到你mysql安装目录的bin目录后，再输入

```
mysqld --initialize -insecure --user=mysql
```
在软件目录下生成data文件夹。mysql登录的用户名为root，密码为空

之前的my.ini中两个参数要改为自己的：
设置mysql的安装目录 basedir=软件安装目录
设置mysql数据库的数据的存放目录   datadir=软件安装目录\data
这两个参数改为你所解压后的文件夹的位置，否则会报错“无法初始化库文件等”如下图

```
mysqld: Can't create/write to file
```

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_not_craet_direc.png)


4.3 测试启动
启动mysql服务：

将目录切换到你mysql安装目录的bin目录，输入 net start mysql 启动服务，OK成功。

4.3.1报错：

```
Found option without preceding group in config file:XXX;
Fatal error in defaults handling.
```

原因：用记事本配置my.ini编码格式有问题，一般情况下是UTF-8编码格式，但是这里需要ANSI编码格式
用记事本打开my.ini文件，然后点击：文件-->另存为-->将编码修改为：ANSI-->保存！

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_my_ini_word.png)

然后cmd窗口输入命令行启动mysql

4.3.2报错

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_error5.png)

解决：以管理员身份来运行cmd程序来启动mysql。


4.3.3运行net start mysql

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_starting.png)

报错：
```
服务正在启动或停止中，请稍候片刻后再试一次。
```

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_start_and_stop.png)

解决方法：打开任务管理器，把mysql进程关闭，再次启动mysql服务器


启动成功

![这里写图片描述](http://p3qhnc0eg.bkt.clouddn.com/blog/mysql_suc_start.png)
