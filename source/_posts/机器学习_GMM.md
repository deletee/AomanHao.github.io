---
title: 机器学习—聚类降维
date: 2018-07-16 09:39:40
tags: [GitHub, Mysql]
---


机器学习—聚类降维

<!--more-->

---

机器学习—Kmeans

聚类属于无监督学习，朴素贝叶斯、SVM等都是有类别标签y的，即已经给出了样本的分类

```
1、随机给K个聚类质心 v
2、重复下面过程直到收敛
2.1对于每一个样例i，计算其应该属于的类 
隶属度 ：zi=argmin||xi−μj||^2
求距离近的
2.2 
聚类中心 u=

```

---

机器学习—GMM
常用作聚类，可以运动目标检测。

高斯混合模型（Gaussian Mixed Model）指的是多个高斯分布函数的线性组合，理论上GMM可以拟合出任意类型的分布，通常用于解决同一集合下的数据包含多个不同的分布的情况（或者是同一类分布但参数不一样，或者是不同类型的分布，比如正态分布和伯努利分布）

```
//  基于混合高斯模型的运动目标检测
//  Author： http://blog.csdn.net/icvpr  
 
 
#include <iostream>
#include <string>
 
#include <opencv2/opencv.hpp>
 
 
int main(int argc, char** argv)
{
	std::string videoFile = "../test.avi";
 
	cv::VideoCapture capture;
	capture.open(videoFile);
 
	if (!capture.isOpened())
	{
		std::cout<<"read video failure"<<std::endl;
		return -1;
	}
 
 
	cv::BackgroundSubtractorMOG2 mog;
 
	cv::Mat foreground;
	cv::Mat background;
 
	cv::Mat frame;
	long frameNo = 0;
	while (capture.read(frame))
	{
		++frameNo;
 
		std::cout<<frameNo<<std::endl;
 
		// 运动前景检测，并更新背景
		mog(frame, foreground, 0.001);       
		
		// 腐蚀
		cv::erode(foreground, foreground, cv::Mat());
		
		// 膨胀
		cv::dilate(foreground, foreground, cv::Mat());
 
		mog.getBackgroundImage(background);   // 返回当前背景图像
 
		cv::imshow("video", foreground);
		cv::imshow("background", background);
 
 
		if (cv::waitKey(25) > 0)
		{
			break;
		}
	}
	
 
 
	return 0;
}

```

---
EM算法：

第一步先求出要估计参数的粗略值。
第二步使用第一步的值最大化似然函数。因此要先求出GMM的似然函数。