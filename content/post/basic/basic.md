+++
title = 'Basic'
date = 2024-02-19T12:19:53+08:00
draft = false
+++

## C/C++关键字  
1. static关键字  
C语言中,关键字static主要作用：  
- 在函数体内，静态变量在函数被调用过程中值维持不变。  
- 在模块内，静态变量或函数仅可被模块内的函数访问，模块外禁止访问。  
分析以下代码:  
```c
#include<stdio.h>

void fun(int i)
{
    static int value = i++;
    value = i++;
    printf("%d\n",value);
}

int main()
{
    fun(0);
    fun(1);
    fun(2);
    return 0;
}
```
程序输出为:  
1  
1  
2  
静态变量初始化只执行1次  

在C++中，声明类的成员为static时，该数据成员为类内部的静态数据成员，具有以下特点：  
- 静态数据成员在类的所有对象中是共享的  
- 静态数据成员存储在全局数据区，定义时要分配空间，所以不能在类的声明中定义。  
- 静态数据成员的初始化不能放在类的定义中，可以在类的外部通过使用范围解析运算符 :: 来重新声明静态变量从而对它进行初始化  
- 静态数据成员和普通数据成员一样遵循public,protected,private访问规则  

2. const关键字  
const是C/C++中常见的关键字，在C语言中，它主要用于定义变量为常类型以及修饰函数参数与返回值，而在C++中还可以修饰函数的定义  
一般而言，const有以下几个方面的作用:  
- const修饰普通变量，其值不允许修改。  
- const修饰指针变量  
```c
const int *p=8;//指针指向的内容不能改变  

int a = 8;
int* const p = &a;//指针指向的内存地址不能改变

int a = 8;
const int * const p = &a;//指针指向的地址和内容都不能改
```
- const修饰参数和返回值  
A: 值传递的const参数，一般这种情况不需要const修饰，因为函数会生成临时变量拷贝实参值  
B: const参数为指针，可以防止指针被意外篡改  
```cpp
#include<iostream>
 
using namespace std;
 
void Cpf(int *const a)
{
    cout<<*a<<" ";
    *a = 9;
}
 
int main(void)
{
    int a = 8;
    Cpf(&a);
    cout<<a; // a 为 9
    system("pause");
    return 0;
}
```
- const修饰类成员函数  
```cpp
#include<iostream>
using namespace std;
class Test
{
public:
    Test(int _m,int _t):_cm(_m),_ct(_t){}
    void Kf()const
    {
        ++_cm; // 错误
        ++_ct; // 正确
    }
private:
    int _cm;
    mutable int _ct;
};
 
int main(void)
{
    Test t(8,7);
    return 0;
}
```

