---
title: 机器学习_分类_adaboost
date: 2018-07-21 09:39:40
tags: [机器学习, C++]
toc: true
---

机器学习_分类_adaboost

<!--more-->
### 简介
Boosting, 也称为增强学习或提升法，是一种重要的集成学习技术， 能够将预测精度仅比随机猜度略高的弱学习器增强为预测精度高的强学习器。
>AdaBoost是英文"Adaptive Boosting"（自适应增强）的缩写

---

### 步骤
```
1）首先，是初始化训练数据的权值分布D1。假设有N个训练样本数据，则每一个训练样本最开始时，都被赋予相同的权值：w1=1/N。
2）然后，训练弱分类器hi。具体训练过程中是：如果某个训练样本点，被弱分类器hi准确地分类，那么在构造下一个训练集中，它对应的权值要减小；相反，如果某个训练样本点被错误分类，那么它的权值就应该增大。权值更新过的样本集被用于训练下一个分类器，整个训练过程如此迭代地进行下去。
3）最后，将各个训练得到的弱分类器组合成一个强分类器。各个弱分类器的训练过程结束后，加大分类误差率小的弱分类器的权重，使其在最终的分类函数中起着较大的决定作用，而降低分类误差率大的弱分类器的权重，使其在最终的分类函数中起着较小的决定作用。
```
>误差率低的弱分类器在最终分类器中占的权重较大，否则较小。

alpha值是基于每个弱分类器的错误率进行计算,计算出alpha值之后，可以对权重向量进行更新，以使得那些正确分类的样本的权重降低而错分样本的权重升高，直到错误率为0或者弱分类器的数目达到用户的指定值为止

---

### 算法过程

![](http://p3qhnc0eg.bkt.clouddn.com/blog/img/adaboost_liucheng1.png)

![](http://p3qhnc0eg.bkt.clouddn.com/blog/img/adaboost_liucheng2.png)

![](http://p3qhnc0eg.bkt.clouddn.com/blog/img/adaboost_liucheng3.png)


---

[参考文章地址](https://blog.csdn.net/guyuealian/article/details/70995333)

[参考文章](https://blog.csdn.net/v_july_v/article/details/40718799)



---

数据分类模型
```
#include "opencv2/core/core.hpp"  
#include "opencv2/highgui/highgui.hpp"  
#include "opencv2/imgproc/imgproc.hpp"  
#include "opencv2/ml/ml.hpp"  
  
#include <iostream>  
using namespace cv;  
using namespace std;  
  
int main( int argc, char** argv )  
{     
    //训练样本  
    float trainingData[42][2]={ {40, 55},{35, 35},{55, 15},{45, 25},{10, 10},{15, 15},{40, 10},  
                            {30, 15},{30, 50},{100, 20},{45, 65},{20, 35},{80, 20},{90, 5},  
                            {95, 35},{80, 65},{15, 55},{25, 65},{85, 35},{85, 55},{95, 70},  
                            {105, 50},{115, 65},{110, 25},{120, 45},{15, 45},  
                            {55, 30},{60, 65},{95, 60},{25, 40},{75, 45},{105, 35},{65, 10},  
                            {50, 50},{40, 35},{70, 55},{80, 30},{95, 45},{60, 20},{70, 30},  
                            {65, 45},{85, 40}   };  
    Mat trainingDataMat(42, 2, CV_32FC1, trainingData);   
    //训练样本的响应值  
    float responses[42] = {'R','R','R','R','R','R','R','R','R','R','R','R','R','R','R','R',  
                            'R','R','R','R','R','R','R','R','R','R',  
                        'B','B','B','B','B','B','B','B','B','B','B','B','B','B','B','B' };  
    Mat responsesMat(42, 1, CV_32FC1, responses);  
  
    float priors[2] = {1, 1};    //先验概率  
  
    CvBoostParams params( CvBoost::REAL, // boost_type    
                          10, // weak_count    
                          0.95, // weight_trim_rate    
                          15, // max_depth    
                          false, // use_surrogates    
                          priors // priors   
                          );    
  
    CvBoost boost;  
    boost.train (   trainingDataMat,   
                    CV_ROW_SAMPLE,   
                    responsesMat,  
                    Mat(),    
                    Mat(),  
                    Mat(),  
                    Mat(),    
                    params  
                    );    
    //预测样本  
    float myData[2] = {55, 25};  
    Mat myDataMat(2, 1, CV_32FC1, myData);  
    double r = boost.predict( myDataMat );  
  
    cout<<endl<<"result:  "<<(char)r<<endl;  
  
    return 0;  
 }
```
基于的OpenCV的检测Demo

```
#include <opencv/highgui.h>
#include <opencv/cv.h>
#include <opencv2/imgproc/imgproc_c.h>
#include <opencv2/objdetect/objdetect.hpp>

using namespace cv;

int main(int argc, char** argv)
{

    CascadeClassifier stFaceCascade;
    IplImage *pstImage = NULL;
    std::vector<Rect> faceRects;

    if( !stFaceCascade.load("D:\\ProgramFiles\\develop\\opencv2.4.8\\sources\\data\\lbpcascades\\lbpcascade_frontalface.xml") )
    { 
        printf("Loading cascade error\n"); 
        return -1; 
    }
    
    pstImage = cvLoadImage("D:\\test.jpg", CV_LOAD_IMAGE_COLOR);

    stFaceCascade.detectMultiScale(pstImage, 
        faceRects,            //检出结果
        1.1,                  //缩放步长
        2,                    //框融合时的最小检出个数
        0|CV_HAAR_SCALE_IMAGE,//标志 |CV_HAAR_FIND_BIGGEST_OBJECT|CV_HAAR_DO_ROUGH_SEARCH|CV_HAAR_DO_CANNY_PRUNING
        Size(30, 30),         //最小人脸尺寸
        Size(300, 300) );     //最大人脸尺寸
    printf("Face Num[%d]\n", faceRects.size());

    for( unsigned int j = 0; j < faceRects.size(); j++ )
    {
        cvRectangle(pstImage, 
            cvPoint(faceRects[j].x, faceRects[j].y), 
            cvPoint(faceRects[j].x + faceRects[j].width, faceRects[j].y + faceRects[j].height),
            cvScalar(0,255,0),
            2,8,0);
    }
    cvShowImage("FDWin", pstImage);
    cvWaitKey(0);


    cvReleaseImage(&pstImage);
    return 0;
}
```