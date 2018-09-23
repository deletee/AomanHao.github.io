---
title: Git配置
date: 2018-09-19 09:39:40
tags: [VScode]
toc: true
---
Git配置

<!--more-->

### 右键菜单配置 Git Bash Here 功能键


运行regedit.exe进入注册表，在HKEY_CLASSES_ROOT\Directory\Background\shell中进行设置。

1.新建项Git Bush Here，此时你可以看到在桌面右键会出现“Git Bush Here”菜单。

2.添加Git Bush Icon，在第一步的新建项Git Bush Here下，新建字符串值Icon，然后编辑该值为“C:\Program Files\Git\mingw64\share\git\git-for-windows.ico”，你需要根据你安装的Git 目录进行配置修改。完成此步后，你会发现右键菜单“Git Bush Here”会多出一个Icon。

![](http://p3qhnc0eg.bkt.clouddn.com/img/blog/git_bash1.png)

![](http://p3qhnc0eg.bkt.clouddn.com/img/blog/git_bash2.png)

3.添加Command项。在“Git Bush Here”下再新建项“Command”，将其默认值改为“C:\Program Files\Git\bin\bash.exe --login -i”，这样，你就可以通过右键菜单的方式快速进入Git命令行工具，进行代码版本管理。

![](http://p3qhnc0eg.bkt.clouddn.com/img/blog/git_command1.png)

![](http://p3qhnc0eg.bkt.clouddn.com/img/blog/git_command2.png)