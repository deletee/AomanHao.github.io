---
title: git_update_error1
date: 2018-08-01 11:58:40
tags: [GitHub, Git]
---

github上传文件报错failed to push some refs解决

<!--more-->

报错内容，不能推送文件到github上
```
error: failed to push some refs to github地址
```

原因是github项目与本地文件夹一些关键文件的确实，比如.git，readme.md文件等等

本地文件夹打开控制命令台 
解决： 
1、添加本地文件夹，github项目更新到本地
```
git add .
git pull origin master
```

2、再上传文件夹到github
```
git push -u origin master
```