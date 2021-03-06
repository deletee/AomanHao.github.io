---
title: git入门
date: 2018-06-25 12:35:55
tags: [GitHub, Git]
---

git入门

<!--more-->

#场景1：我要开始一个新项目，想用git管理代码（待更新）
### 注册账号
第一步，我们需要先注册`github`帐号。

第二步，新建项目，填上项目名称，`git`地址等信息以后，就可以新建一个项目了。

第三步，填加`ssh`的`key`，添加`key`的作用是允许你的电脑访问`git`仓库。如果`git`项目是私有的，那么就要指定谁可以访问谁不能访问。我们把自己计算机上的`ssh key`添加到`git`项目上，就表示我们电脑里的`key`能访问了，可以理解成`key`的白名单。配置方法如下：

### 邮箱地址填注册git时用的邮箱，然后按3个回车。
```ssh-keygen -t rsa -C "xxx@happymmall.com"```

### 在git.oschina的项目里添加公钥，查看公钥内容：
```cat ~/.ssh/id_rsa.pub```

第四步，从远程拉下代码，这`git`项目就算建好了。

### 使用项目的ssh形式的地址
```git clone xxx```
##场景2：我要开始开发了，要怎么玩？
进入开发前，要先了解`git`的分支使用规范。当我们项目`clone`下来以后，默认会处在`master`分支上，也就是`git`的默认分支。通常我们是不在这个分支上做开发的，如果更规范一点，`master`分支会对开发人员设置成只读的，最终由上线人员把要上线的代码合并到`master`分支上。这时候我们就要做一个自己的开发分支。执行如下：

###  切换到master分支
```git checkout master```

###  拉取最新代码
```git pull```

###  以master分支为基础，新建本地分支，新分支名以mmall_v1.0为例
```git checkout -b mmall_v1.0  ```

###  在远程建立对应的分支，只有新建分支时需要执行这步，以后只需要git push
```git push --set-upstream origin mmall_v1.0```
然后就可以在新分支上开始写代码。

##场景3：我要在一个已有的分支上开发点东西
因为是已有分支，就不用自己新建了，直接切换到指定分支，这里还是以`mmall_v1.0`为例。

###  切换分支
```git checkout mmall_v1.0```

### 拉取当前分支最新代码
```git pull```
然后还是一样的，就可以进入开发了。

##场景4：开发到一定程度，想看看改动了什么内容
###  看文件的改动
```git status```

### 看文件内容的变动
```git diff```
## 场景5：代码开发完成了，想提交代码
### 首先是追踪变更的文件
```git add .```

###  然后提交到本地
```git commit -am '我是提交的说明'```

###  提交到远程
```git push```
场景6：当前分支代码都开发完了，准备提交上线
在上线的时候，一般是由管理员或发布人员把开发分支的代码合并到`master`分支上，上线前我们要先把远程`master`最新的代码合并到我们的分支上再提交，才能保证我们的开发分支版本高于`master`分支。如果不这么干，有多个人开发的话，就有可能造成`A`发布了一个版本，等`B`发布的时候会把`A`发布的内容冲掉。

###  合并远程分支
```git merge origin master```

###  注意：如果发现merge的结果里有CONFLICT，就表示当前分支和远程master分支有文件冲突，我们要手动解决一下冲突再做一次提交才可以。

###  没冲突或解决完冲突后，提交到当前分支的远程
```git push```
`merge`完成后，就可以做提交了，通常使用`pull request`提交合并到`master`分支的请求，管理员合并后，我们的分支内容就可以上线了。


作者：Rosen_Gao
链接：http://www.imooc.com/article/19060
来源：慕课网
本文原创发布于慕课网 ，转载请注明出处，谢谢合作