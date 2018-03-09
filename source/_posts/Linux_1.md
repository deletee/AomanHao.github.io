---
title: Linux入门及初体验
date: 2018-02-04 10:59:59
tags: Linux
---
# 1.linux 文件夹含义
<!--more-->
	主要的目录的有/、/root、/home、/usr、/bin等。
其中：

/bin 普通用户的可执行文件，系统的任何用户都可以执行该目录中的命令
/boot 存放Linux操作系统启动时所需要的文件
/dev 系统中所有设备文件
/etc 系统中的配置文件
/home 普通用户的宿主目录，每个用户在该目下都有一个于用户名同名的目录。
/mnt 中的子目录用于系统中可移动设备的挂载点
/root 超级用户root的宿主目录
/sbin 系统中的管理命令，普通用户不能执行
/tmp 系统的临时目录
/usr  系统应用程序的相关文件
/var 系统中经常变化的文件如日志文件和用户邮件



## 2.1	Linux命令
	进入系统控制台，看到>[root@loca~],
其中#代表当前是root用户登录，如果是$表示当前为普通用户。
cd  /home	进入/home目录
cd /root	进入/root目录
cd ..		返回上一级目录
cd  .		当前目录；（.和..可以理解为相对路径；例如cd /hom/test ，cd加完整的路径，可以理解为绝对路径）

ls  .		查看当前目录所有的文件和目录。
ls  -a		查看所有的文件，包括隐藏文件,以.开头的文件。

pwd		显示当前所在的目录。
mkdir		创建目录，用法mkdir  test ，命令后接目录的名称。
rmdir		删除空目录
rm		删除文件或者目录，用法 rm –rf  test.txt (-r表示递归，-f表示强制)。
cp		拷贝文件，用法：cp  old.txt  /tmp/new.txt ，常用来备份；如果拷贝目录需要加 –r参数。

mv		重命名或者移动文件或者目录，用法, mv old.txt new.txt
touch		创建文件，用法，touch test.txt，如果文件存在，则表示修改当前文件时间。
Useradd		创建用户，用法 useradd wugk ，userdel删除用户。
Groupadd	创建组，用法 groupadd wugk1 ，groupdel删除组。

find		查找文件或目录，用法 find  /home  -name  “test.txt”,命令格式为:
find		后接查找的目录，-name指定需要查找的文件名称，名称可以使用*表示所有。
find  /home  -name  "*.txt" ;	查找/home目录下，所有以.txt结尾的文件或者目录。

vi		修改某个文件，vi有三种模式：命令行模式、文本输入模式、末行模式。
默认vi打开一个文件，首先是命令行模式，然后按i进入文本输入模式，可以在文件里写入字符等等信息。
写完后，按esc进入命令模式，然后输入:进入末行模式。	例如输入:wq表示保存退出。如果想直接退出，不保存，可以执行:q!， q!叹号表示强制退出。
cat		查看文件内容，用法 cat test.txt 可以看到test.txt内容
more		查看文件内容，分页查看，cat是全部查看，如果篇幅很多，只能看到最后的篇幅。可以使用cat和more同时使用,例如： cat  test.txt |more 分页显示text内容，|符号是管道符，用于把|前的输出作为后面命令的输入。
echo		回显，用法 echo ok，会显示ok，输入什么就打印什么。
echo		ok  > test.txt ；把ok字符覆盖test.txt内容，>表示追加并覆盖的意思。>>两个大于符号，表示追加，echo ok >> test.txt,表示向test.txt文件追加OK字符，不覆盖原文件里的内容。

## 2.2	Linux基本命令
shutdown - h now	立刻关机
shutdown - r now	重启
reboot			重启
clear			清除屏幕命令
history			查看历史命令记录

## 2.3	用户操作命令
su-			切换成系统管理员
su			用户之间的切换
logout			用户注销
useradd  A		 添加用户（root下）
passwd A		设置A的密码
userdel  A		删除用户
userdel -r A		删除用户及其主目录

## 2.4	修改用户属性
usermod –g<主组名> -G <组名> -d <用户主目录> -s <用户shell>
在添加用户时，可以指定将该用户添加到哪个组中，同样的用root的管理权限可以改变 某个用户所在的组：usermod -g 组名 用户名
可以用 usermod -d 目录名 用户名 改变该用户登录的初始目录
groupadd <新组名>	增加用户组
groupdel <组名>		删除用户组
修改组成员：直接编辑/etc/group文件，将用户名写到对应的组名的后面
whoami			命令的功能在于显示用户自身的用户名。
who			[选项]：该命令主要用于查看当前在线的用户情况
w			用于显示登录到系统的用户情况
finger			命令可用于查找和显示用户信息，并且在查找后显示指定账号的相关信息
chfn			命令能够改变系统存储的用户信息

## 2.5	设置系统时间
1.date命令。可以直接输入date 来查看系统时间
2.利用date命令来更改系统时间
date MMDDHHMCCYY.SS	指定月月日日时时分分年年年年.秒秒

## 2.6	Linux用户管理
在Linux操作系统中，root的权限是最高的，相当于windows的administrator，拥有最高权限，能执行任何命令和操作。在系统中，通过UID来区分用户的权限级别，UID等于0，表示此用户具有最高权限，也就是管理员。其他的用户UID依次增加，通过/etc/passwd用户密码文件可以查看到每个用户的独立的UID。
