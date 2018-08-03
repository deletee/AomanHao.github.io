---
title: 机器学习_分类_KNN
date: 2018-07-16 09:39:40
tags: [GitHub, Mysql]
---


机器学习_分类_KNN

<!--more-->
K最近邻(kNN，k-NearestNeighbor)分类算法

在KNN中，通过计算对象间距离来作为各个对象之间的非相似性指标，避免了对象之间的匹配问题，在这里距离一般使用欧氏距离或曼哈顿距离：

```
步骤：
其算法的描述为：

1）计算测试数据与各个训练数据之间的距离；

2）按照距离的递增关系进行排序；

3）选取距离最小的K个点；

4）确定前K个点所在类别的出现频率；

5）返回前K个点中出现频率最高的类别作为测试数据的预测分类。
```

---
KNN算法的优点：
```
1）简单、有效。 
2）重新训练的代价较低（类别体系的变化和训练集的变化，在Web环境和电子商务应用中是很常见的）。 
3）计算时间和空间线性于训练集的规模（在一些场合不算太大）。 
4）由于KNN方法主要靠周围有限的邻近的样本，而不是靠判别类域的方法来确定所属类别的，因此对于类域的交叉或重叠较多的待分样本集来说，KNN方法较其他方法更为适合。 
5）该算法比较适用于样本容量比较大的类域的自动分类，而那些样本容量较小的类域采用这种算法比较容易产生误分。
```

KNN算法缺点：

```
1）KNN算法是懒散学习方法（lazy learning,基本上不学习），一些积极学习的算法要快很多。 
2）类别评分不是规格化的（不像概率评分）。 
3）输出的可解释性不强，例如决策树的可解释性较强。 
4）该算法在分类时有个主要的不足是，当样本不平衡时，如一个类的样本容量很大，而其他类样本容量很小时，有可能导致当输入一个新样本时，该样本的K个邻居中大容量类的样本占多数。该算法只计算“最近的”邻居样本，某一类的样本数量很大，那么或者这类样本并不接近目标样本，或者这类样本很靠近目标样本。无论怎样，数量并不能影响运行结果。可以采用权值的方法（和该样本距离小的邻居权值大）来改进。 
5）计算量较大。目前常用的解决方法是事先对已知样本点进行剪辑，事先去除对分类作用不大的样本。
```

opencv3代码
```
#include "stdafx.h"
#include "opencv2\opencv.hpp"
#include <iostream>
using namespace std;
using namespace cv;
using namespace cv::ml;

int main()
{
    Mat img = imread("E:/opencv/opencv/sources/samples/data/digits.png");
    Mat gray;
    cvtColor(img, gray, CV_BGR2GRAY);
    int b = 20;
    int m = gray.rows / b;   //原图为1000*2000
    int n = gray.cols / b;   //裁剪为5000个20*20的小图块
    Mat data,labels;   //特征矩阵
    for (int i = 0; i < n; i++)
    {
        int offsetCol = i*b; //列上的偏移量
        for (int j = 0; j < m; j++)
        {
            int offsetRow = j*b;  //行上的偏移量
            //截取20*20的小块
            Mat tmp;
            gray(Range(offsetRow, offsetRow + b), Range(offsetCol, offsetCol + b)).copyTo(tmp);
            data.push_back(tmp.reshape(0,1));  //序列化后放入特征矩阵
            labels.push_back((int)j / 5);  //对应的标注
        }

    }
    data.convertTo(data, CV_32F); //uchar型转换为cv_32f
    int samplesNum = data.rows;
    int trainNum = 3000;
    Mat trainData, trainLabels;
    trainData = data(Range(0, trainNum), Range::all());   //前3000个样本为训练数据
    trainLabels = labels(Range(0, trainNum), Range::all());

    //使用KNN算法
    int K = 5;
    Ptr<TrainData> tData = TrainData::create(trainData, ROW_SAMPLE, trainLabels);
    Ptr<KNearest> model = KNearest::create();
    model->setDefaultK(K);
    model->setIsClassifier(true);
    model->train(tData);

    //预测分类
    double train_hr = 0, test_hr = 0;
    Mat response;
    // compute prediction error on train and test data
    for (int i = 0; i < samplesNum; i++)
    {
        Mat sample = data.row(i);
        float r = model->predict(sample);   //对所有行进行预测
        //预测结果与原结果相比，相等为1，不等为0
        r = std::abs(r - labels.at<int>(i)) <= FLT_EPSILON ? 1.f : 0.f;          

        if (i < trainNum)
            train_hr += r;  //累积正确数
        else
            test_hr += r;
    }

    test_hr /= samplesNum - trainNum;
    train_hr = trainNum > 0 ? train_hr / trainNum : 1.;

    printf("accuracy: train = %.1f%%, test = %.1f%%\n",
        train_hr*100., test_hr*100.);
    waitKey(0);
    return 0;
}
```