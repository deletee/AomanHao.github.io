---
title: 算法Code_Java_C++
date: 2018-07-16 09:39:40
tags: [Java, C++]
---

算法Code_Java_C++

<!--more-->

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
>思路：从左下角元素往上查找，右边元素是比这个元素大，上边是的元素比这个元素小。
Java代码
```
public class Solution {
    public boolean Find(int target, int [][] array) {
        //填写
        int row = array.length;
        int col = array[0].length;
        int i=row-1,j=0;
        while(i>=0&&j<=col-1){
            if(target<array[i][j]){
                i--;
            }else if(target>array[i][j]){
                j++;
            }else
                return true;
        }
        return false;
    }
}
```
C++代码
```
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        // array是二维数组，这里没做判空操作
        int rows = array.size();
        int cols = array[0].size();
        int i=rows-1,j=0;//左下角元素坐标
        while(i>=0 && j<cols){//使其不超出数组范围
            if(target<array[i][j])
                i--;//查找的元素较少，往上找
            else if(target>array[i][j])
                j++;//查找元素较大，往右找
            else
                return true;//找到
        }
        return false;
    }
};
```

----
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。
Java代码：
```
public class Solution {
    public String replaceSpace(StringBuffer str) {
    	String str1 = str.toString();
        String str2 = str1.replace(" ","%20");
        return str2;
    }
}
```

c++代码
```
class Solution {
public:
	void replaceSpace(char *str,int length) {
    int count = 0;
        for (int i=0;i<length;i++){
            if (str[i]==' '){
                count++;
            }
            for (int i=length-1;i>=0;i--){
                if (str[i]==' '){
                    count--;
                  str[i+2*count]='%';
                str[i+2*count+1]='2';
                str[i+2*count+2]='0';
                }else{
                      str[i+2*count]=str[i];
                }
            }
        }
	}
};
```