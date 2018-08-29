---
title: Hexo博客 报错 Cannot read property 'replace' of null
date: 2018-08-28 09:39:40
tags: [Hexo, Github]
toc: true
---

Hexo博客 报错 Cannot read property 'replace' of null

<!--more-->

### 报错内容-情况

报错内容如下
```
FATAL Cannot read property 'replace' of null
TypeError: Cannot read property 'replace' of null

```
如图：
![](http://p3qhnc0eg.bkt.clouddn.com/blog/img/hexo_error_replace.png)

报错情况，执行 `hexo clean` 清理本地缓存或者 `hexo g` 生成本地缓存时报此错误



### 解决方法

打开 hexo配置文件，配置
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://www.aomanhao.top
root: AomanHao.github.io
permalink: :year/:month/:day/:title/
permalink_defaults:

```

root，url属性配置正确，填写自己对应的


[cankao](https://www.jianshu.com/p/449accb044b4)