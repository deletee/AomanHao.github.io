---
title: C++入门
date: 2018-07-19 09:39:40
tags: [C++]
---

C++入门

<!--more-->

### 指针入门
>指针作用：  引用类型，传递地址，减少内存消耗
案例
int p >定义变量p
int* p >定义指针变量p
使用指针，先要定义指针变量
```
#include<stdio.h>
int main() {
    int *p;     //int* p >定义指针变量p
    int a=3; 
    p=&a;   //&a是把a的地址赋给指针p，&：取址符a
    printf("%d\n",*p)   //输出为3
    return 0; 
}

```

```
& 取变量的地址 &(变量名)
* 指针运算符（取值运算） *(变量名)
& *互为逆运算 *(&(int i =6))=6
```

指针变量是存储地址的变量，随机分配
例如：
```
int *p1;
char *name
---
int x;int *p; p=&x;
答：*P=3;
p是x的地址，*p是x的值
```

常用错误：
1、指针不能直接复制
```
错误：
int *p; 
p =100;//错误

正确：
int i, *p, *t;
p=&i;
t=p;
*p *t是指针，把i的地址赋给pt指针（元素地址） 
```
2、不能直接给指针赋值(不能直接变量取值)
```
int x= 20;
printf("%d,&(*x));
```

Scanf函数:函数后的参数应该传入指针，不应该是值
```
int score;
printf("shuru :\n");
scanf("%d",score);

```

Swap函数：
```
#include<stdio.h>

void swap(int *x, int *y)
{
    int temp;//中间变量
    temp=*x;
    *x = *y;
    *y = temp;

    printf("x=%d, y=%d \n", *x, *y);
}

main(){
    int i =13, j =45;
    swap(&i, &j);
    printf("i=%d, j=%d\n",i ,j);
}

//输出： x=45,y=13    i=45,j=13
```
---
### 二级指针
>C语言的参数传递都是值传递，当传传递一个指针给函数的时，其实质上还是值传递，除非使用双指针。
只有一个*号的时候，我们叫它一级指针。** 两个星号的叫二级指针。

```
void  
swap ( int *a, int *b ){  
    int c;  
    c = *a;  
    *a = *b;  
    *b = c;  
}  
int  
main(int argc, char **argv){  
    int a,b;  
    a = 16;  
    b = 32;  
    swap( &a, &b);  
    return ( a - b );  
}  
```
段代码编译成汇编语言之后，除了会有代码段，数据段，堆栈，那么在调用的时候，会把main函数的参数变量压入main函数的栈帧，然后接着会压入swap函数的局部变量和参数

![](http://hi.csdn.net/attachment/201002/9/4758664_12657012034TT4.jpg)

我们申明 **a之后，其实双指针变量a其实已经存在,内存效果如下
![](http://hi.csdn.net/attachment/201002/9/4758664_1265703222WluB.jpg)
```
p中放的是中间桥梁bridge的地址&bridge
*p就是中间桥梁bridge的内容(即是目标操作数的地址&income)，
**p就是目标操作数

中间的bridge是桥梁，中间件使用的，过度吧
```
>双指针主要用在但我们想向一个A函数传递参数的时候，但是我们希望在A内部对参数做任何修改都能保存起来，那么就是用双指针吧。

---
### 输入输出流
IO库：
|头文件|类型|||
|-|-|-|-|
|iostream|istream,wistream 从流读取数据|ostream, wostream向流写入数据|iostream. wiostream读写流|
|fstream|ifstream, wifstream从文件读取数据|ofstream, wofstream向文件写入数据|fstream, wfstream读写文件|
|sstream|istringstream. wistringstream string 读取数据|ostringstream, wostringstream string 写入数据|stringstream, wstringstream string 读写string|


```
类型ifsream和istringstream都继承自istream;
类型ofsream和ostringstream都继承自ostream;
类型fsream和stringstream都继承自iostream;
```

1、创建使用文件流对象
```
ifstream in(ifile);//构造一个ifstream并打开给定文件
ofstream out;//构造输出文件流，未关联任何文件

in.close();//关闭文件
in.open(ifile + "2");//打开另一个文件
```
ifstream,ofstream和fstream是实现文件读写操作的类型

案例
```
#include <iostream>                                                                                                                                
#include <fstream>
#include <stdlib.h>
#include <vector>
using namespace std;
int main(){
   char buffer[256];
   ifstream in("input.txt");//文件不存在会返回错误
   if (! in.is_open()){
       cout << "Error opening file"<<endl;
       exit (1);
   }
   vector<string> a;
   while (!in.eof()){
       in.getline (buffer,100);
       //cout << buffer << endl;
       a.push_back(buffer);
    }   
   for(unsigned int i=0;i<a.size();i++)
       cout<<a[i]<<endl;
  return 0;
}
```

### resize(),reserve()
resize()，设置大小（size）;
reserve()，设置容量（capacity）;
size()是分配容器的内存大小，而capacity()只是设置容器容量大小，但并没有真正分配内存。

###  ifstream
```
ifstream infile(fname,ios::in);
```
定义ifstream的对象infile,打开文件faname,ios::in是读取

### sizeof
sizeof 求对象或者类型的大小
[cankao](https://blog.csdn.net/tao20dage/article/details/52372604)
```
特性0：sizeof是运算符，不是函数
特性1：sizeof不能求得void类型的长度
特性2：sizeof能求得void类型的指针的长度
特性3：sizeof能求得静态分配内存的数组的长度!
特性4：sizeof不能求得动态分配的内存的大小!
特性5：sizeof不能对不完整的数组求长度！
特性6：当表达式作为sizeof的操作数时，它返回表达式的计算结果的类型大小，但是它不对表达式求值！
```

### new(std::nothrow)
 顾名思义，即不抛出异常，当new一个对象失败时，默认设置该对象为NULL，这样可以方便的通过if(p == NULL) 来判断new操作是否成功