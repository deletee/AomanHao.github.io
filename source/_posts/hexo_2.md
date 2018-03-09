---
title: hexo博客yilia主题_more截断文章_多标签添加
date: 2018-02-08 17:00:06
tags: [GitHub, Hexo, yilia]
---

以下均为自己遇到的问题并加以修改或者纠正.

<!--more-->
在文章下方可以使用more语句进行截断，这样博客首页只会出现文章的前面一小部分，看起来很清爽简约

> 或者
>
> anguage: zh-CN
>
> ``` <!--more--> ```//在需要阶段的地方插入该代码语句
>
> aa

在这里，yilia主题会判断含有`<!--more-->`的位置，然后文章截断两部分，第一部分展示在博客首页，第二部分即上方的aa只能点开展开全文，才能继续阅读文章。


截断效果如下图：

![效果](http://upload-images.jianshu.io/upload_images/6280966-dff71bcc18df7583.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在这里我对yilia主题做了修改

原始效果为：

![原始效果](http://upload-images.jianshu.io/upload_images/6280966-2bc7446857bc04e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


修改后为：去掉了more按钮，打开文章可以点击文章或者点击展开全文

![修改效果](http://upload-images.jianshu.io/upload_images/6280966-51ea736ffd940d2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

做法很简单，进入theme目录，打开yilia目录下的_config.yml文件，修改excerpt_link参数：

```
excerpt_link：之后的more单词换成空格
注：‘excerpt_link： ’。其中：后有一个空格键
```

修改图如下图

![这里写图片描述](http://upload-images.jianshu.io/upload_images/6280966-c3ec0b215421bcee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


如何给文章加多个标签：

修改如下图，格式为 [tag1, tag2]

注：逗号之后要有一个空格。[tag1, tag2]= [tag1+逗号+空格+tag2]

修改如下图所示：

![这里写图片描述](http://upload-images.jianshu.io/upload_images/6280966-62305c940fee2082.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
