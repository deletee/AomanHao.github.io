---
title: hexo-github博客首页菜单中文乱码两种解决方案
date: 2018-02-06 23:22:06
tags: [GitHub, Hexo]
---
方案一：

<!--more-->
菜单设置成中文显示，编辑博客根目录下的_config.yml文件


![配置文件](http://p3qhnc0eg.bkt.clouddn.com/TIM%E6%88%AA%E5%9B%BE20180206230112.png)


设置language字段如下:

language: zh-Hans

或者

language: zh-CN




![语言分类](http://p3qhnc0eg.bkt.clouddn.com/TIM%E6%88%AA%E5%9B%BE20180206230033.png)



取决于你的主题theme目录下的language目录下有zh-Hans.yml还是zh-CN.yml





方案二：

根目录下的配置文件是_config.yml文件

![配置文件](http://p3qhnc0eg.bkt.clouddn.com/TIM%E6%88%AA%E5%9B%BE20180206230112.png)

我们需要打开此文件，然后编辑文字。

但是保存之后的格式可能跟文件本身的格式编码不一样，所以会出现乱码问题。

推荐用sublime，VScode，atom等文本编辑器打开，这三款开源软件写代码也很便利。
此处用atom文本编辑器打开编辑，保存后不会出现乱码问题了

![文件](http://p3qhnc0eg.bkt.clouddn.com/TIM%E6%88%AA%E5%9B%BE20180206230542.png)

[简书文章地址](https://www.jianshu.com/p/81027eb27a39)

[本人博客小站](http://www.haoloverongrong.top/)
