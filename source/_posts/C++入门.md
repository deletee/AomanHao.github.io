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




