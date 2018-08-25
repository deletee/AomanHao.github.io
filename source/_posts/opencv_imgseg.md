---
title: Opencv图像分割
date: 2018-07-19 09:39:40
tags: [Opencv, 图像处理, 图像分割]
toc: true
---

Opencv图像分割

<!--more-->

```
/*
 *
 * 功能：通过灰度图做简单的图像分割,再使用findContours去掉多余的轮廓
 *
 */
 
#include <vector>
 
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>
 
using namespace cv;
using namespace std;
 
void contours();
 
int main()
{
    contours();
}
 
void contours()
{
    //--1.读入图片
    Mat image = imread("horse_hw.jpg");
 
    Mat gray;//mat类型数据存放图片，opencv特有
  
    cvtColor(image,gray,CV_RGB2GRAY);
 
    Mat binary;
    threshold(gray,binary,60,255,THRESH_BINARY_INV);
 
    vector<vector<Point> > contours;
    Mat binary_copy; //因为findcontours函数会改变输入的图像，所以复制一个图像作为函数的输入
    binary.copyTo(binary_copy);
    findContours(binary_copy,contours,CV_RETR_EXTERNAL/*获取外轮廓*/,CV_CHAIN_APPROX_NONE/*获取每个轮廓的每个像素*/);
 
    //遍历每一个轮廓，把多余的轮廓去掉
    vector<vector<Point> >::const_iterator it=contours.begin();
    while(it!=contours.end())
    {
        if(it->size()<500)
            it = contours.erase(it);
        else
            ++it;
    }
    Mat dst(image.size(),CV_8U,Scalar(0));
    drawContours(dst,contours,-1/*绘制所有轮廓*/,Scalar(255)/*绘制为白色*/,CV_FILLED/*轮廓全部填充*/);
 
 
    //--4.显示结果(原图和结果图显示在一起)
    const int width  = image.cols;
    const int height = image.rows;
    Mat show_image(Size(3*width,height),CV_8UC3);
    //将image拷贝到显示图片指定位置
    image.copyTo(show_image(Rect(0,0,width,height)));
    //将binary,dst转换为3通道，使得show_image和dst通道数一致，或者使用convertTo()函数做操作
    cvtColor(binary,binary,CV_GRAY2RGB);
    cvtColor(dst,dst,CV_GRAY2RGB);
    //将binary,dst拷贝image指定位置
    binary.copyTo(show_image(Rect(width,0,width,height)));
    dst.copyTo(show_image(Rect(2*width,0,width,height)));
    //显示
    imshow("show",show_image);
    waitKey(0);
}

```