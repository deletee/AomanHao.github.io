---
title: Git配置
date: 2018-09-19 09:39:40
tags: [Git]
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

### git 命令


1.git config

该命令允许你获得和设置配置变量；这些变量可以控制Git的外观和操作的各个方面。
```
使用方法: git config –global user.name “[name]”

使用方法: git config –global user.email “[email address]”
```


2.git init


git init命令创建一个空的Git仓库或重新初始化一个现有仓库。
```
使用方法：git init [repository name]
```

3.git clone

git clone命令将存储库克隆到新目录中。
```
使用方法：git clone [url]
```

4.git add

git add命令将文件内容添加到索引(将修改添加到暂存区)。也就是将要提交的文件的信息添加到索引库中。
```
使用方法: git add [file] ;
```

5.git commit
该命令用于将更改记录(提交)到存储库。将索引的当前内容与描述更改的用户和日志消息一起存储在新的提交中。

```
使用方法: git commit -m “[ Type in the commit message]”

使用方法：git commit -a
```

在修改文件后,需要使用gitadd把文件加入暂存区,这样gitcommit时才能把已经修改的信息加入版本库,而使用gitcommit-a可以不用再git add。


6.git diff

该命令用于显示提交和工作树等之间的更改。此命令比较的是工作目录中当前文件和暂存区域快照之间的差异，也就是修改之后还没有暂存起来的变化内容。
```
使用方法: git diff

使用方法：git diff –staged
```
gitdiff--staged显示的是暂存区和版本库差异

```
使用方法：git diff [first branch] [second branch]
```
命令显示两个分支之间的差异。


7.git reset
git reset命令用于将当前HEAD复位到指定状态。一般用于撤消之前的一些操作(如:git add,git commit等)。
```
使用方法: git reset [file]

使用方法: git reset [commit]
```
撤消指定提交后的所有提交，并在本地保留更改。

```
使用方法：git reset –hard [commit]
```
丢弃所有历史记录并返回到指定的提交。


8.git status
该命令用于显示工作目录和暂存区的状态。
```
使用方法: git status
```

9.git rm
该命令用于从工作区和索引中删除文件。
```
使用方法: git rm [file]
```

10.git log
该命令用于显示提交日志信息。
```
使用方法: git log

使用方法：git log –follow[file]
```
列出文件的版本历史记录，包括文件的重命名。


11.git show
该命令用于显示各种类型的对象。
```
使用方法: git show [commit]
```

12.git tag
该命令用于创建,列出,删除或验证使用GPG签名的标签对象。
```
使用方法: git tag [commitID]
```

13.git branch

该命令列出当前存储库中的所有本地分支。
```
使用方法: git branch

使用方法：git branch [branch name]
```
创建一个新分支。

```
使用方法：git branch -d [branch name]
```
删除分支


14.git checkout

该命令命令用于从一个分支切换到另一个分支。

使用方法：git checkout [branch name]


使用方法: git checkout -b [branch name]

该命令创建一个新分支并切换过去。


15.git merge
该命令用于将两个或两个以上的开发历史加入(合并)一起。

使用方法: git merge [branch name]


16.git remote
该命令管理一组跟踪的存储库。

使用方法: git remote add [variable name] [Remote Server Link]




17.git push
该命令用于将本地分支的更新,推送到远程主机。

使用方法: git push [variable name] master


使用方法：git push [variable name] [branch]

将分支提交到远程存储库。


使用方法：git push –all [variable name]

将所有分支推送到远程存储库。


使用方法: git push [variable name] :[branch name]

删除远程存储库上的分支。


18.git pull
该命令用于从另一个存储库或本地分支获取并集成(整合)。

使用方法: git pull [Repository Link]


19.git stash
该命令临时存储所有已修改的跟踪文件。。

使用方法: git stash save


使用方法：git stash pop

可恢复最近隐藏的文件。


使用方法：git stash list

列出所有存储的更改集。


使用方法：git stash drop

移除stash