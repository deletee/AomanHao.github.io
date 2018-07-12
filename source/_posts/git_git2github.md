---
title: git上传文件到Github
date: 2018-07-01 12:35:55
tags: [GitHub, Git]
---

准备工作：

<!--more-->

1、电脑装有Git
2、GitHub 已有仓库

1、克隆GitHub仓库，到本地

文件夹右键选择Git Bash Here，输入代码<br>

```
    Git clone git@github.com:用户名/仓库名.git
```
2、放置代码内容到第一步下载的文件夹里

3、执行代码

```
git add .
git commit -m "情况说明"
git push origin master
```

4、上传成功