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
[cankao](https://blog.csdn.net/kingstar158/article/details/6859379)<br>
1、文件打开
```
ifstream infile(fname,ios::in);
```
定义ifstream的对象infile,打开文件faname,ios::in是读取

|打开文件的方式在ios类(所以流式I/O的基类)中定义||
|-|-|
|IO流的定义|含义|
|ios::in|为输入(读)而打开文件|
|ios::out|为输出(写)而打开文件|
|ios::ate|初始位置：文件尾|
|ios::app|所有输出附加在文件末尾|
|ios::trunc|如果文件已存在则先删除该文件|
|ios::binary|二进制方式|
	
2、关闭文件：
```
infile.close	
```
3、文本文件的读写

类ofstream, ifstream 和fstream 是分别从ostream, istream 和iostream 中引申而来的。这就是为什么 fstream 的对象可以使用其父类的成员来访问数据。
```
写入内容：
#include <fiostream.h>
    int main () {
        ofstream out("out.txt");
        if (out.is_open()) 
       {
            out << "This is a line.\n";
            out << "This is another line.\n";
            out.close();
        }
        return 0;
    }
   //结果: 在out.txt中写入：
   This is a line.
   This is another line

读取内容：
// reading a text file
    #include <iostream.h>
    #include <fstream.h>
    #include <stdlib.h>
    
    int main () {
        char buffer[256];
        ifstream in("test.txt");
        if (! in.is_open())
        { cout << "Error opening file"; exit (1); }
        while (!in.eof() )
        {
            in.getline (buffer,100);
            cout << buffer << endl;
        }
        return 0;
    }
    //结果 在屏幕上输出
     This is a line.
     This is another line
```	
状态标识符
```
bad()
如果在读写过程中出错，返回 true 。例如：当我们要对一个不是打开为写状态的文件进行写入时，或者我们要写入的设备没有剩余空间的时候。

fail()
除了与bad() 同样的情况下会返回 true 以外，加上格式错误时也返回true ，例如当想要读入一个整数，而获得了一个字母的时候。

eof()
如果读文件到达文件末尾，返回true。

good()
这是最通用的：如果调用以上任何一个函数返回true 的话，此函数返回 false 。
```
要想重置以上成员函数所检查的状态标志，你可以使用成员函数clear()，没有参数。

---
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

---
### new(std::nothrow)
 顾名思义，即不抛出异常，当new一个对象失败时，默认设置该对象为NULL，这样可以方便的通过if(p == NULL) 来判断new操作是否成功
 建议在c++代码中，凡是涉及到new操作，都采用new(std::nothrow)，然后if(p==NULL)的方式进行判断

 ---
### vector
[cankao](https://blog.csdn.net/duan19920101/article/details/50617190/)<br>
在c++中，vector是一个十分有用的容器。
作用：它能够像容器一样存放各种类型的对象，简单地说，vector是一个能够存放任意类型的动态数组，能够增加和压缩数据。<br>
>1、如果你要表示的向量长度较长（需要为向量内部保存很多数），容易导致内存泄漏，而且效率会很低；<br>
2、Vector作为函数的参数或者返回值时，需要注意它的写法：
   double Distance(vector<int>&a, vector<int>&b) 其中的“&”绝对不能少！！！

   c++基本操作
   ```
   1 、基本操作

(1)头文件#include<vector>.
(2)创建vector对象，vector<int> vec;
(3)尾部插入数字：vec.push_back(a);
(4)使用下标访问元素，cout<<vec[0]<<endl;记住下标是从0开始的。
(5)使用迭代器访问元素.
vector<int>::iterator it;
for(it=vec.begin();it!=vec.end();it++)
    cout<<*it<<endl;
(6)插入元素：    vec.insert(vec.begin()+i,a);在第i+1个元素前面插入a;
(7)删除元素：    vec.erase(vec.begin()+2);删除第3个元素
vec.erase(vec.begin()+i,vec.end()+j);删除区间[i,j-1];区间从0开始
(8)向量大小:vec.size();
(9)清空:vec.clear();
   ```

---
### 二维数组
```
#include "stdafx.h"
#include <cv.h>
#include <vector> 
#include <iostream> 
using namespace std;
int main()
{
	using namespace std;
	int out[3][2] = { 1, 2, 
			 3, 4,
			5, 6 };
	vector <int*> v1;
 
	v1.push_back(out[0]);
	v1.push_back(out[1]);
	v1.push_back(out[2]);
 
	cout << v1[0][0] << endl;//1
	cout << v1[0][1] << endl;//2
	cout << v1[1][0] << endl;//3
	cout << v1[1][1] << endl;//4
	cout << v1[2][0] << endl;//5
	cout << v1[2][1] << endl;//6
 
	return 0;
}

```