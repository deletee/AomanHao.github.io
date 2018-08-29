---
title: 机器学习_分类_KNN_EM
date: 2018-07-19 09:39:40
tags: [机器学习]
toc: true
---


机器学习_分类_KNN_EM

<!--more-->
### K最近邻(kNN，k-NearestNeighbor)分类算法

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


### EM算法
EM的策略就是先随便给一个条件概率p1(x1|thera)，然后找到一个l(thera)的下界函数r(x1|thera),求r的最大值p2(x2|thera)，再找到经过p2点的下界函数r2(x2|thera)，重复该过程直到收敛到局部最大值。








灰度图分割：[参考](https://blog.csdn.net/u014612806/article/details/65442061)

point.h文件
```
#ifndef POINT_H
#define POINT_H
//point结构主要用来存储图像中节点的横坐标，纵坐标以及灰度值
struct point
{
    int row;
    int col;
    double pixVal;
    point(int row, int col, double pixVal) :row(row),col(col),pixVal(pixVal) {}
};
#endif
```
keams.h头文件：
```
#ifndef KMEANS_H
#define KMEANS_H

#include<opencv2\opencv.hpp>
#include<random>
#include<time.h>
#include<stdio.h>
#include<stdlib.h>
#include<list>
#include<iostream>
#include<math.h>
#include"point.h"

using namespace cv;
using namespace std;

class Kmeans{
private:
    //存储所有点
    vector<point> points;
    //存储簇的中心点
    vector<point> centers;
    //存储每个点到相应的簇
    vector<point>* clusters;
    //向量的维数
    int dimension;
    //簇的个数
    int k;
public:
    //构造函数
    Kmeans(vector<point> points, vector<point> centers, int k, int dimension)
    {
        this->points = points;
        this->centers = centers;
        this->dimension = dimension;
        this->k = k;
        clusters = new vector<point>[k];
    }

    //析构函数
    ~Kmeans()
    {
        delete clusters;
    }

    //获取簇
    vector<point>* getClusters()
    {
        return this->clusters;
    }

    //计算两个向量之间的欧式距离
    double getDistanceBetweenTwoPoints(const point& point1, const point& point2)
    {
        double sum = 0;
        //double tmp;
        //for (int i = 0; i < dimension; i++)
        //{
        //tmp = pow(point1.pixVal - point2.pixVal,2);
        //sum += tmp;
        //}
        sum = pow(point1.pixVal - point2.pixVal, 2);
        return sqrt(sum);
    }

    //计算每个点到离它最近的簇中心点，结果保存到vector中
    vector<int> getClosetClusterCenterLabel()
    {
        double min;
        int label;
        vector<int> labels;
        for (int i = 0; i < points.size(); i++)
        {
            label = 0;
            min = getDistanceBetweenTwoPoints(points[i], centers[0]);
            for (int j = 1; j < centers.size(); j++)
            {
                double tmp = getDistanceBetweenTwoPoints(points[i], centers[j]);
                if (tmp < min)
                {
                    min = tmp;
                    label = j;
                }
            }
            labels.push_back(label);
        }
        return labels;
    }

    //将每个点放入它离的最近的中心点对应的簇中
    void computeClusters(const vector<int>& labels)
    {
        for (int i = 0; i < k; i++)
        {
            clusters[i].clear();
        }
        for (int i = 0; i < labels.size(); i++)
        {
            int label = labels[i];
            clusters[label].push_back(points[i]);
        }
    }

    //重新计算所有簇的中心点的灰度值
    void computeCenters()
    {
        centers.clear();
        for (int i = 0; i < k; i++)
        {
            double sum = 0;
            for (int j = 0; j < clusters[i].size(); j++)
            {
                sum += clusters[i][j].pixVal;
            }
            double meanVal = sum / clusters[i].size();
            point cp(-1, -1, meanVal);
            centers.push_back(cp);
        }
    }

    //确定新的中心点后重新计算一次cost
    double computeCost()
    {
        double sum = 0;
        for (int i = 0; i < k; i++)
        {
            vector<point> tmpVec=clusters[i];
            for (int j = 0; j < tmpVec.size(); j++)
            {
                sum += getDistanceBetweenTwoPoints(tmpVec[j], centers[i]);
            }
        }
        return sum / points.size();
    }

    //迭代执行k-means算法的步骤
    void kmeans()
    {
        double oldCost, newCost;
        vector<int> labels=getClosetClusterCenterLabel();
        computeClusters(labels);
        newCost = computeCost();

        computeCenters();
        labels = getClosetClusterCenterLabel();
        computeClusters(labels);
        oldCost = newCost;
        newCost = computeCost();

        while (oldCost != newCost)
        {
            oldCost = newCost;
            computeCenters();
            labels = getClosetClusterCenterLabel();
            computeClusters(labels);
            newCost = computeCost();
        }
        cout <<"Final Cost: "<< newCost << endl;
    }
};
#endif
```

测试的kmeans.cpp文件：
```
#include "kmeans.h"
//图片的存放位置
const String imageFolder = "F:\\";
//簇的个数（即k的大小，根据自己需要调整）
const int numOfCluster =4;
//最大像素值
const int MAX_PIX_VALUE = 255;
//存放所有点
vector<point> points;
//存放所有簇中心
vector<point> centers;
//存放所有点颜色特征(i,j)->i*rows+j
vector<double> pixVec;

//读取图像
Mat readImage(String imageName)
{
    String imageLoc = imageFolder + imageName;
    Mat image=imread(imageLoc);
    return image;
}

//初始化k-means聚类中心
void initializeCenters(const Mat& img)
{
    srand((unsigned)time(NULL));
    for (int i = 0; i < numOfCluster; i++)
    {
        int randomX = rand() % img.rows;
        int randomY = rand() % img.cols;
        uchar pixVal = img.at<uchar>(randomX, randomY);
        point cp(randomX, randomY, (double)pixVal);
        centers.push_back(cp);
    }
}

//将图像中的所有点装入points中
void initializePoints(const Mat& img)
{
    for (int i = 0; i < img.rows; i++)
    {
        const uchar* data = img.ptr<uchar>(i);
        for (int j = 0; j < img.cols; j++)
        {
            uchar pixVal = data[j];
            point p(i,j, (double)pixVal);
            points.push_back(p);
        }
    }
}

int main()
{
    String imageName = "lena.jpg";
    Mat img = readImage(imageName);
    cvtColor(img, img, CV_RGB2GRAY);//转化为灰度图像
    namedWindow(imageName,WINDOW_NORMAL);
    imshow(imageName, img);
    waitKey(0);
    int rows = img.rows;
    int cols = img.cols;
    initializeCenters(img);
    initializePoints(img);
    Kmeans* km=new Kmeans(points, centers, numOfCluster, 1);
    cout << "---------------k-means start-------------" << endl;
    km->kmeans();
    cout << "---------------k-means end---------------" <<endl;
    vector<point>* clusters = km->getClusters();
    Mat res(img.rows,img.cols,img.type());
    double div = MAX_PIX_VALUE / numOfCluster;
    for (int i = 0; i < numOfCluster; i++)
    {
        vector<point> tmpVec = clusters[i];
        for (int j = 0; j < tmpVec.size(); j++)
        {
            res.at<uchar>(tmpVec[j].row, tmpVec[j].col) = i*div;
        }
    }
    namedWindow("kmeansResult",WINDOW_NORMAL);
    imshow("kmeansResult", res);
    waitKey(0);
    imwrite("./segment_lena.jpg", res);
    system("pause");
}
```


彩色图像分割：[参考](https://blog.csdn.net/owen7500/article/details/51604906)

主函数：
```
#include "clusterImagePixels.hpp"
 
int main()
{
	Mat testImage = imread("E:\\testImage\\board.jpg");
	if (testImage.empty())
	{
		return -1;
	}
 
	ClusterPixels clusterPix(testImage,3);
 
	Mat colorResults = clusterPix.clusterColorImageByKmeans();
	Mat grayResult = clusterPix.clusterGrayImageByKmeans();
 
	if (!colorResults.empty())
	{
		hconcat(testImage, colorResults, colorResults);
		imshow("clusterImage", colorResults);
	}
 
	if (!grayResult.empty())
	{
		hconcat(testImage, grayResult, grayResult);
		imshow("grayCluster", grayResult);
	}
 
	if (waitKey() == 27)
		return 0;
}

```
```
#include <opencv.hpp>
using namespace cv;
 
 
Scalar colorTab[] =     //10个颜色
{
	Scalar(0, 0, 255),
	Scalar(0, 255, 0),
	Scalar(255, 100, 100),
	Scalar(255, 0, 255),
	Scalar(0, 255, 255),
	Scalar(255, 0, 0),
	Scalar(255, 255, 0),
	Scalar(255, 0, 100),
	Scalar(100, 100, 100),
	Scalar(50, 125, 125)
};
 
class ClusterPixels
{
private:
	Mat image;			//待聚类图像
	Mat labels;			//聚类后的标签
	int clusterCounts;	//分类数,不得大于10，只是颜色定义只有10类，并不是算法限制
 
public:
	ClusterPixels() :clusterCounts(0){}
	ClusterPixels(const Mat& src, int clusters = 5) :clusterCounts(clusters){ image = src.clone(); }
 
	void setImage(const Mat& src){ image = src.clone(); };
	void setClusters(int clusters){ clusterCounts = clusters; }
 
	Mat getLabels()	{return labels;	};		//返回聚类后的标签
 
	Mat clusterGrayImageByKmeans()
	{
		//转换成灰度图
		if (image.channels() != 1)
			cvtColor(image, image, COLOR_BGR2GRAY);
 
		int rows = image.rows;
		int cols = image.cols;
		
		//保存聚类后的图片
		Mat clusteredMat(rows, cols, CV_8UC3);
		clusteredMat.setTo(Scalar::all(0));
 
		Mat pixels(rows*cols, 1, CV_32FC1);	//pixels用于保存所有的灰度像素
 
		for (int i = 0; i < rows;++i)
		{
			const uchar *idata = image.ptr<uchar>(i);
			float *pdata = pixels.ptr<float>(0);
			for (int j = 0; j < cols;++j)
			{
				pdata[i*cols + j] = idata[j];
			}
		}
 
		kmeans(pixels, clusterCounts, labels, TermCriteria(TermCriteria::EPS + TermCriteria::MAX_ITER, 10, 0), 5, KMEANS_PP_CENTERS);
 
		for (int i = 0; i < rows;++i)
		{
			for (int j = 0; j < cols;++j)
			{
				circle(clusteredMat, Point(j,i), 1, colorTab[labels.at<int>(i*cols + j)]);		//标记像素点的类别，颜色区分
			}
		}
 
		return clusteredMat;
	}
 
	Mat clusterColorImageByKmeans()
	{
		assert(image.channels() != 1);
 
		int rows = image.rows;
		int cols = image.cols;
		int channels = image.channels();
 
		//保存聚类后的图片
		Mat clusteredMat(rows, cols, CV_8UC3);
		clusteredMat.setTo(Scalar::all(0));
 
		Mat pixels(rows*cols, 1, CV_32FC3);	//pixels用于保存所有的灰度像素
		pixels.setTo(Scalar::all(0));
 
		for (int i = 0; i < rows; ++i)
		{
			const uchar *idata = image.ptr<uchar>(i);
			float *pdata = pixels.ptr<float>(0);
 
			for (int j = 0; j < cols*channels; ++j)
			{
					pdata[i*cols*channels + j] = saturate_cast<float>(idata[j]);			
			}
		}
 
		kmeans(pixels, clusterCounts, labels, TermCriteria(CV_TERMCRIT_EPS + CV_TERMCRIT_ITER, 10, 0), 5, KMEANS_PP_CENTERS);
 
		for (int i = 0; i < rows; ++i)
		{
			for (int j = 0; j < cols*channels; j += channels)
			{
				circle(clusteredMat, Point(j/channels,i), 1, colorTab[labels.at<int>(i*cols + (j/channels))]);		//标记像素点的类别，颜色区分
			}
		}
 
		return clusteredMat;
	}
};

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