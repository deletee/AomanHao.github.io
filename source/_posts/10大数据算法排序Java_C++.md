---
title: 10大数据算法排序Java_C++
date: 2018-08-16 09:39:40
tags: [Java, C++, 算法]
toc: true
---

10大数据算法排序Java_C++

<!--more-->
![](https://images0.cnblogs.com/blog2015/731178/201508/272007357503007.jpg)

### 冒泡排序
>依次比较n与后面的数字，大的放右面，小的放左边
Java代码
```
/**
     * 冒泡排序
     * 比较相邻的元素。如果第一个比第二个大，就交换他们两个。  
     * 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。  
     * 针对所有的元素重复以上的步骤，除了最后一个。
     * 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。 
     * @param numbers 需要排序的整型数组
     */
    public static void bubbleSort(int[] numbers)
    {
        int temp = 0;
        int size = numbers.length;
        for(int i = 0 ; i < size-1; i ++)
        {
        for(int j = 0 ;j < size-1-i ; j++)
        {
            if(numbers[j] > numbers[j+1])  //交换两数位置
            {
            temp = numbers[j];
            numbers[j] = numbers[j+1];
            numbers[j+1] = temp;
            }
        }
        }
    }


```
C++代码
```
待补充
```

### 选择排序
>选择n个数组成的数组arr里最大的一个数，放在arr[n-1]，<br>
然后维数n-1<br>
选择前n-1个数组成的数组，取最大数，放在arr



Java代码：
```
/**
     * 选择排序算法
     * 在未排序序列中找到最小元素，存放到排序序列的起始位置  
     * 再从剩余未排序元素中继续寻找最小元素，然后放到排序序列末尾。 
     * 以此类推，直到所有元素均排序完毕。 
     * @param numbers
     */
    public static void selectSort(int[] numbers)
    {
    int size = numbers.length; //数组长度
    int temp = 0 ; //中间变量
    
    for(int i = 0 ; i < size ; i++)
    {
        int k = i;   //待确定的位置
        //选择出应该在第i个位置的数
        for(int j = size -1 ; j > i ; j--)
        {
        if(numbers[j] < numbers[k])
        {
            k = j;
        }
        }
        //交换两个数
        temp = numbers[i];
        numbers[i] = numbers[k];
        numbers[k] = temp;
    }
    }
```

C++代码：
```
待补充
```



### 快速排序及其改进算法C++实现

>快速排序可以看成是插入排序的改进，它是一种分治的排序算法
![一次快排](http://my.csdn.net/uploads/201207/20/1342782317_4426.jpg)
![快排流程](http://my.csdn.net/uploads/201207/20/1342782329_8314.jpg)

Java代码：
```
public class FastSort{

     public static void main(String []args){
        System.out.println("Hello World");
        int[] a = {12,20,5,16,15,1,30,45,23,9};
        int start = 0;
        int end = a.length-1;
        sort(a,start,end);
        for(int i = 0; i<a.length; i++){
             System.out.println(a[i]);
         }
        
     }
     
     public void sort(int[] a,int low,int high){
         int start = low;
         int end = high;
         int key = a[low];
         
         
         while(end>start){
             //从后往前比较
             while(end>start&&a[end]>=key)  //如果没有比关键值小的，比较下一个，直到有比关键值小的交换位置，然后又从前往后比较
                 end--;
             if(a[end]<=key){
                 int temp = a[end];
                 a[end] = a[start];
                 a[start] = temp;
             }
             //从前往后比较
             while(end>start&&a[start]<=key)//如果没有比关键值大的，比较下一个，直到有比关键值大的交换位置
                start++;
             if(a[start]>=key){
                 int temp = a[start];
                 a[start] = a[end];
                 a[end] = temp;
             }
         //此时第一次循环比较结束，关键值的位置已经确定了。左边的值都比关键值小，右边的值都比关键值大，但是两边的顺序还有可能是不一样的，进行下面的递归调用
         }
         //递归
         if(start>low) sort(a,low,start-1);//左边序列。第一个索引位置到关键值索引-1
         if(end<high) sort(a,end+1,high);//右边序列。从关键值索引+1到最后一个
     }
     
}
```
C++代码：
[cankao](https://blog.csdn.net/liuchen1206/article/details/6954074)
```
#include<iostream>
using namespace std;
int main()
{
	int array[]={34,65,12,43,67,5,78,10,3,70},k;
	int len=sizeof(array)/sizeof(int);
	cout<<"The orginal arrayare:"<<endl;
	for(k=0;k<len;k++)
		cout<<array[k]<<",";
	cout<<endl;
	quickSort(array,0,len-1);
	cout<<"The sorted arrayare:"<<endl;
	for(k=0;k<len;k++)
		cout<<array[k]<<",";
	cout<<endl;
	system("pause");
	return 0;
}
 
void quickSort(int s[], int low, int high)
{
	if (low< high)
	{      
		int i = low, j = high, x = s[low];
		while (i < j)
		{
			while(i < j && s[j]>= x) // 从右向左找第一个小于x的数
				j--; 
			if(i < j)
				s[i++] = s[j];
			while(i < j && s[i]< x) // 从左向右找第一个大于等于x的数
				i++; 
			if(i < j)
				s[j--] = s[i];
		}
		s[i] = x;
		quickSort(s, low, i - 1); // 递归调用
		quickSort(s, i + 1, high);
	}
}

```



### 归并排序
>归并排序（MERGE-SORT）是利用归并的思想实现的排序方法，该算法采用经典的分治（divide-and-conquer）策略（分治法将问题分(divide)成一些小的问题然后递归求解，而治(conquer)的阶段则将分的阶段得到的各答案"修补"在一起，即分而治之)。<br>
分治思想：
![](http://p3qhnc0eg.bkt.clouddn.com/blog/img/guibing_1.png)
合并步骤如下
![](http://p3qhnc0eg.bkt.clouddn.com/blog/img/guibing_2.png)

Java代码：[cankao](https://www.cnblogs.com/chengxiao/p/6194356.html)
```
package sortdemo;

import java.util.Arrays;

/**
 * Created by chengxiao on 2016/12/8.
 */
public class MergeSort {
    public static void main(String []args){
        int []arr = {9,8,7,6,5,4,3,2,1};
        sort(arr);
        System.out.println(Arrays.toString(arr));
    }
    public static void sort(int []arr){
        int []temp = new int[arr.length];//在排序前，先建好一个长度等于原数组长度的临时数组，避免递归中频繁开辟空间
        sort(arr,0,arr.length-1,temp);
    }
    private static void sort(int[] arr,int left,int right,int []temp){
        if(left<right){
            int mid = (left+right)/2;
            sort(arr,left,mid,temp);//左边归并排序，使得左子序列有序
            sort(arr,mid+1,right,temp);//右边归并排序，使得右子序列有序
            merge(arr,left,mid,right,temp);//将两个有序子数组合并操作
        }
    }
    private static void merge(int[] arr,int left,int mid,int right,int[] temp){
        int i = left;//左序列指针
        int j = mid+1;//右序列指针
        int t = 0;//临时数组指针
        while (i<=mid && j<=right){
            if(arr[i]<=arr[j]){
                temp[t++] = arr[i++];
            }else {
                temp[t++] = arr[j++];
            }
        }
        while(i<=mid){//将左边剩余元素填充进temp中
            temp[t++] = arr[i++];
        }
        while(j<=right){//将右序列剩余元素填充进temp中
            temp[t++] = arr[j++];
        }
        t = 0;
        //将temp中的元素全部拷贝到原数组中
        while(left <= right){
            arr[left++] = temp[t++];
        }
    }
}
```

C++代码：[cankao](https://www.cnblogs.com/orion7/p/8242774.html)
```
#include<iostream>
using namespace std;
const int maxn=500000,INF=0x3f3f3f3f;
int L[maxn/2+2],R[maxn/2+2];
void merge(int a[],int n,int left,int mid,int right)
{
    int n1=mid-left,n2=right-mid;
    for(int i=0;i<n1;i++)
        L[i]=a[left+i];
    for(int i=0;i<n2;i++)
        R[i]=a[mid+i];
    L[n1]=R[n2]=INF;
    int i=0,j=0;
    for(int k=left;k<right;k++)
    {
        if(L[i]<=R[j])
            a[k]=L[i++];
        else
            a[k]=R[j++];
    }
}
void mergesort(int a[],int n,int left,int right)
{
    if(left+1<right)
    {
        int mid=(left+right)/2;
        mergesort(a,n,left,mid);
        mergesort(a,n,mid,right);
        merge(a,n,left,mid,right);
    }
}
int main()
{
    int a[maxn],n;
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>a[i];
    mergesort(a,n,0,n);
    for(int i=0;i<n;i++)
    {
        if(i)
            cout<<" ";
        cout<<a[i];
    }
    cout<<endl;
    return 0;
}
```


### 堆排序
 http://www.cnblogs.com/MOBIN/p/5374217.html
>堆排序主要在于理解堆的构造过程和在输出最大元素后如何对堆进行重新调整

大顶堆：父结点始终>子节点<br>![大顶堆](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410150915593-1435777167.png) 

小顶堆：父结点始终<子节点<br>![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410150948406-1525110244.png)
```
算法思想(以大顶堆为例)：
1.将长度为n的待排序的数组进行堆有序化构造成一个大顶堆
2.将根节点与尾节点交换并输出此时的尾节点
3.将剩余的n -1个节点重新进行堆有序化
4.重复步骤2，步骤3直至构造成一个有序序列
```
我们开始只需要扫描一半的元素（n/2-1 ~ 0）,因为(n/2-1)~0的节点才有子节点
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151057625-469827986.png)

构建有序堆：
1、第一次for循环将节点3和它的子节点7 8的元素进行比较，最大者作为父节点（即元素60作为父节点）
红色表示交换后的状态
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151437250-974257904.png) 
2、第二次for循环将节点2和它的子节点5 6的元素进行比较，最大者为父节点（元素80作为父节点）
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151453015-690847102.png)
3、第三次for循环将节点1和它的子节点3 4的元素进行比较，最大者为父节点（元素70作为父节点）
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151523218-139482913.png)

调整堆
1、堆顶元素80和尾40交换后-->调整堆
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151713156-328299797.png)
2、堆顶元素70和尾30交换后-->调整堆
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151728406-2042556892.png)
。。。
完成调整
![](https://images2015.cnblogs.com/blog/776259/201604/776259-20160410151755062-2073568164.png)

左右父节点下标:
```
左：i*2+1
右：i*2+2
父：(i-1)/2
```

Java代码：
```
public class HeapSort {
private static void heapSort(int[] arr) {
int len = arr.length -1;
//堆构造，调整结构，符合大顶堆或者小顶堆
for(int i = len/2 ; i >=0; i --){ 
heapAdjust(arr,i,len);
}
while (len >=0){
swap(arr,0,len--); //将堆顶元素与尾节点交换后，长度减1，尾元素最大
heapAdjust(arr,0,len); //再次对堆进行调整
}
}

public static void heapAdjust(int[] arr,int i,int len){
int left = 2*i+1,right = 2*i+2,largest = i;
if(left <= len && arr[left] > arr[i])
largest = left;
if(right <= len && arr[right] > arr[largest])
largest = right;
if(largest != i) {
swap(arr, i, largest);
heapAdjust(arr,largest,len);
}
}
public static void swap(int[] arr,int i,int len){
int temp = arr[i];
arr[i] = arr[len];
arr[len] = temp;
}
public static void main(String[] args) {
int array[] = {20,50,20,40,70,10,80,30,60};
System.out.println("排序之前：");
for(int element : array){
System.out.print(element+" ");
}
heapSort(array);
System.out.println("\n排序之后：");
for(int element : array){
System.out.print(element+" ");
}
}
}
```

C++代码：
```
待补充
```


### 插入排序

Java代码：
```
待补充
```

C++代码：
```
待补充
```




Java代码：
```
待补充
```
C++代码：
```
待补充
```



Java代码：
```
待补充
```

C++代码：
```
待补充
```




Java代码：
```
待补充
```

C++代码：
```
待补充
```




Java代码：
```
待补充
```
C++代码：
```
待补充
```