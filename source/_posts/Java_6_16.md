---
title: Java相关小知识_6_15
date: 2018-06-15 12:35:55
tags: [GitHub, Mysql, Java]
---

实体完整性要求每个表都有唯一标识符，每一个表中的主键字段不能为空或者重复的值。
<!--more-->


参照完整性要求关系中不允许引用不存在的实体。设定相应的更新删除插入规则来更新参考表。

Java语言使用的是```Unicode```字符集。而ASCII是国际上使用最广泛的字符编码；BCD是一种数字压缩存储编码方法。

---
HashMap不能保证元素的顺序，HashMap能够将键设为null，也可以将值设为null，与之对应的是Hashtable，(注意大小写：不是HashTable)，Hashtable不能将键和值设为null，否则运行时会报空指针异常错误。<br>
HashMap线程不安全，Hashtable线程安全

---
for循环的执行顺序：<br>
for(条件1;条件2;条件3) {
    //语句
}
执行顺序是条件1->条件2->语句->条件3->条件2->语句->条件3->条件2........
如果条件2为true，则一直执行。如果条件2位false，则for循环结束


---
java1.8后，抽象类中的抽象方法和非抽象方法在不加修饰符的情况下，都是默认的default

---
substring    方法将返回一个包含从    start    到最后（不包含    end    ）的子字符串的字符串。（左闭右开）

---
### 在为传统面向对象语言的程序做单元测试的时候,经常用到mock对象。Mock对象通过反射数。请问反射最大程度破坏了面向对象的以下哪个特性？ ：封装性

mock对象：也成为伪对象，在测试中的利用mock对象来代替真实对象，方便测试的进行。<br>
java的封装性：指的是将对象的状态信息隐藏在对象内部，不允许外部程序直接访问对象内部信息，通过该类提供的方法实现对内部信息的操作访问。<br>
反射机制：在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法;对于任意一个对象，都能够调用它的任意一个方法和属性。<br>
反射破坏代码的封装性，破坏原有的访问修饰符访问限制  

---
### try-catch-finally执行顺序<br>
>博文try-catch-finally执行顺序详解：http://qing0991.blog.51cto.com/1640542/1387200
try块中抛出异常，try、catch和finally中都有return语句

```
public static int WithException(){

int i=10;

try{

System.out.println("i in try block is ： "+i);

i = i/0;

return --i;

}

catch(Exception e){

System.out.println("i in catch - form try block is ： "+i);

--i;

System.out.println("i in catch block is ： "+i);

return --i;

}

finally{

System.out.println("i in finally - from try or catch block is--"+i);

--i;

System.out.println("i in finally block is--"+i);

return --i;

}

}
```

执行结果：

```
============WithException==================

i in try block is ： 10

i in catch - form try block is ： 10

i in catch block is ： 9

i in finally - from try or catch block is--8

i in finally block is--7

6
```
===============================<br>
执行顺序：

抛出异常后，执行catch块，在catch块的return的--i执行完后，并不直接返回而是执行finally，因finally中有return语句，所以，执行，返回结果6。

结论：

try块中抛出异常，try、catch和finally中都有return语句，返回值是finally中的return。

总体结论：

结论一：

return语句并不是函数的最终出口，如果有finally语句，这在return之后还会执行finally（return的值会暂存在栈里面，等待finally执行后再返回）
结论二：

finally里面不建议放return语句，根据需要，return语句可以放在try和catch里面和函数的最后。可行的做法有四：
（1）return语句只在函数最后出现一次。
（2）return语句仅在try和catch里面都出现。
（3）return语句仅在try和函数的最后都出现。
（4）return语句仅在catch和函数的最后都出现。
注意，除此之外的其他做法都是不可行的，编译器会报错

---
Statement在JDBC中相当于SQL语句的载体<br>
Statement---是最基本的用法，采用字符串拼接的方式，存在注入漏洞<br>
PreparedStatement---对Statement中的SQL语句进行预编译，同时检查合法性，效率高<br>
CallableStatement--接口扩展 PreparedStatement，用来调用存储过程,它提供了对输出和输入/输出参数的支持。CallableStatement 接口还具有对 PreparedStatement 接口提供的输入参数的支持。<br>
BatchedStatement--不是标准的Statement类