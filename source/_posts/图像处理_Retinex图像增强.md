---
title: 图像处理_Retinex图像增强
date: 2018-08-17 09:39:40
tags: [图像处理, Opencv, 图像增强]
toc: true
---

图像处理_Retinex图像增强

<!--more-->


###单尺度SSR
(Single Scale Retinex)

图像$S(x,y)$分解为两个不同的图像：反射图像$R(x,y)$,入射图像$L(x,y)$
![](https://img-blog.csdn.net/20170508211020962?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWppYW55aW5neGlhb3FpbmdoYW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

图像可以看做是入射图像和反射图像构成，入射光照射在反射物体上，通过反射物体的反射，形成反射光进入人眼。最后形成的图像$r(x,y)$可以如下公式表示

$$r(x,y)=logR(x,y)=log\frac{S(x,y)}{L(x,y)}$$

R(x, y)表示了物体的反射性质，即图像内在属性，我们应该最大程度的保留；而L(x, y)表示入射光图像，决定了图像像素能达到的动态范围，我们应该尽量去除。 

我们把照射图像假设估计为空间平滑图像，原始图像为S(x, y)，反射图像为R(x, y)，亮度图像为L(x, y)，使用公式
$$r(x,y)=logR(x,y)=log\frac{S(x,y)}{L(x,y)}$$
或者
$$r(x,y)=logS(x,y)-log[F(x,y)⨂S(x,y)]$$

其中r(x, y)是输出图像,卷积运算，$F(x, y)$是中心环绕函数

$$F(x,y)=\lambda*e^{-\frac{x^2+y^2}{c^2}}$$

其中C是高斯环绕尺度，λ是一个尺度，满足$∫∫F(x,y)dxdy=1$

>SSR算法中的卷积是对入射图像的计算，其物理意义是通过计算像素点与周围区域在加权平均的作用下，估计图像中照度的变化，并将L(x,y)去除，只保留S(x,y)属性。


### 多尺度MSR
(Multi-Scale Retinex)
>MSR是在SSR基础上发展来的，优点是可以同时保持图像高保真度与对图像的动态范围进行压缩的同时，MSR也可实现色彩增强、颜色恒常性、局部动态范围压缩、全局动态范围压缩，也可以用于X光图像增强。

$$r(x,y)=∑_k^Kw_klogS(x,y)-log[F_k(x,y)*S(x,y)]$$
K是高斯中心环绕函数的个数。当K=1时，MSR退化为SSR,K取值通常为3
$$w1=w2=w3=\frac13$$

>缺点:边缘锐化不足，阴影边界突兀，部分颜色发生扭曲，纹理不清晰，高光区域细节没有得到明显改善，对高光区域敏感度小

### 带颜色恢复的MSR方法MSRCR
(Multi-Scale Retinex with Color Restoration)
SSR和MSR普遍都存在明显的偏色问题
>MSRCR在MSR的基础上，加入了色彩恢复因子C来调节由于图像局部区域对比度增强而导致颜色失真的缺陷。

改进公式：
$$R_{MSRCR_i}(x,y)=C_i(x,y)R_{MSR_i}(x,y)$$
其中
$$C_i(x,y)=f[I_i^{'}(x,y)]=f[\frac{I_i(x,y)}{∑_{j=1}^{N}I_j(x,y)}]$$
其中
$$f[I_i^{'}(x,y)]=βlog[αI_i^{'}(x,y)]=β{log[αI_i^{'}i(x,y)]-log[∑_{j=1}^NI_j(x,y)]} $$

参数说明
```
Ii(x, y)表示第i个通道的图像
Ci表示第i个通道的彩色回复因子，用来调节3个通道颜色的比例；
f(·)表示颜色空间的映射函数；
β是增益常数；
α是受控制的非线性强度；
```
MSRCR算法利用彩色恢复因子C，调节原始图像中3个颜色通道之间的比例关系，从而把相对较暗区域的信息凸显出来，达到了消除图像色彩失真的缺陷。
处理后的图像局部对比度提高，亮度与真实场景相似，在人们视觉感知下，图像显得更加逼真。


[参考文章](https://blog.csdn.net/ajianyingxiaoqinghan/article/details/71435098)
