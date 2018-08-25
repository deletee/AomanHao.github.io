---
title: Opencv_斑点检测
date: 2018-07-16 09:39:40
tags: [图像处理, Opencv]
toc: true
---

Opencv_斑点检测

<!--more-->
### opencv中检测Blobs的类为SimpleBlobDetector
这个类在opencv中的定义如下：
```
class SimpleBlobDetector : public FeatureDetector
{
public:
struct Params
{
    Params();
    float thresholdStep;
    float minThreshold;
    float maxThreshold;
    size_t minRepeatability;
    float minDistBetweenBlobs;

    bool filterByColor;
    uchar blobColor;

    bool filterByArea;
    float minArea, maxArea;

    bool filterByCircularity;
    float minCircularity, maxCircularity;

    bool filterByInertia;
    float minInertiaRatio, maxInertiaRatio;

    bool filterByConvexity;
    float minConvexity, maxConvexity;
};

SimpleBlobDetector(const SimpleBlobDetector::Params &parameters = SimpleBlobDetector::Params());

protected:
    ...
};
```
算法的大致步骤如下：

对[minThreshold,maxThreshold)区间，以thresholdStep为间隔，做多次二值化。
对每张二值图片，使用findContours()提取连通域并计算每一个连通域的中心。
根据2得到的中心，全部放在一起。一些很接近的点［由theminDistBetweenBlobs控制多少才算接近］被归为一个group,对应一个bolb特征..
从3得到的那些点,估计最后的blob特征和相应半径，并以key points返回。
同时该支持提取特征的方法，一共有5个选项，这里就不多加描述了，默认是提取黑色圆形的Blob特征。下面是一个示例
```
int main(int argc, char** argv) 
{ 
    Mat image = imread(argv[1]); 
    vector<KeyPoint> keyPoints; 
    SimpleBlobDetector::Params params;

    SimpleBlobDetector blobDetect(params); 
    blobDetect.create("SimpleBlob"); 
    blobDetect.detect(image, keyPoints); 
    cout << keyPoints.size() << endl; 
    drawKeypoints(image, keyPoints, image, Scalar(255,0,0));

    namedWindow("blobs"); 
    imshow("blobs", image); 
    waitKey(); 
    return 0; 
}

```
总体来说，OpenCV的斑点检测效果还算不错，但是在有些图像的效果上明显不如LOG算子检测的检测效果