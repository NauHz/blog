---
title: C
date: '2021-12-13 09:06:00'
tags:
  - C
  - 编程
categories: 编程笔记
cover: /img/C.JPG
abbrlink: 3dd7ffa7
top_img: "#0f4c81"
---

## Hello,Wrod!

```C
#inclued "stdio.h"
viod main()
{
    printf("hello,wrod!");
}
```
## 32个关键字

**指在高级语言中已经定义过的字，使用者不能再将这些字作为变量名或过程名使用。
每种程序设计语言都规定了自己的一套保留字。
例如：BASIC语言规定不能使用LIST作为变量名或过程名，因为LIST是一个BASIC语言专用于显示内存程序的命令。
C有22+10 = 32个关键字/C++ 有22+10+11+20 = 63 个关键字/JAVA 有22+ 9+ 17 = 48 个关键字**

|关键字 |函数介绍 |
|---------- |--------------------------------------- |
|auto |跳出循环或switch语句 |
|break |跳出循环或switch |
|case |定义switch中的case子句 |
|char |定义字符型变量或指针 |
|const |定义常量或参数 |
|continue |在循环语句中，回到循环体的开始处重新执行循环 |
|default |定义switch中的default子句 |
|do |定义do-while语句 |
|double |定义双精度浮点数变量 |
|else |定义枚举类型 |
|enum |声明外部变量或函数 |
|extern |声明外部变量或函数 |
|float |定义浮点型变量或指针 |
|for |定义for语句 |
|goto |定义goto语句 |
|if |定义if语句或if-else语句 |
|int |定义整型变量或指针 |
|long |定义长整型变量或指针 |
|register |指定变量的存储类型是寄存器变量，Turbo c中用自动变量代替 |
|return |从函数返回 |
|short |定义短整型变量或指针 |
|signed |定义有符号的整型变量或指针 |
|sizeof |获取某种类型的变量或数据所占内存的大小，是运算符 |
|static |指定变量的存储类型是静态变量，或指定函数是静态函数 |
|struct |定义结构体类型 |
|switch |定义switch语句 |
|typedef |为数据类型定义别名 |
|union |定义无符号的整型或字符型变量或指针 |
|unsigned |定义无符号的整型变量或数据 |
|void |定义空类型变量或空类型指针，或指定函数没有返回值 |
|volatile |变量的值可能在程序的外部被改变 |
|while |定义while或do-while语句 |

## 简单题型

### 选择结构

**输入:1+3,结果显示4.(限定为加、减、乘、除运算)**

```C
#inclued "stdio.h"
int main()
{
	int a,b;
	char c;
	printf(请输入想要计算加减乘除的数(列如1+2)：);
	scanf(%d%c%d,&a,&c,&b);
	switch(c)
	{
	case'+'printf(结果为：%dn,a+b);break;
	case'-'printf(结果为：%dn,a-b);break;
	case''printf(结果为：%dn,ab);break;
	case''printf(结果为：%dn,ab);break;
	defaultprintf(请重新输入n);
	}
	return 0;
}
```
### 循环结构

**求1+2+3+4+……+100的值(分别用while、do while、for实现)**

#### while
```C
#include "stdio.h"
int main()
{
    int a=0,b=1;
    while(a<=100)
    {
     a+=b;
     b+=1;
    }
    printf("%d\n",a);
    return 0;
}
```
#### do while

```C
#include "stdio.h"
int main()
{
    int a=0,b=1;
    do
    {
     a+=b;
     b+=1;
    }while(b<=100);
    printf("%d\n",a);
    return 0;
}
```
#### for

```C
#include "stdio.h"
int main()
{
    int a=0,b=1;
    for(;b<=100;)
    {
     a+=b;
     b+=1;
    }
    printf("%d\n",a);
    return 0;
}
```

**若一个口袋中放有12个球,其中有3个红色球,3个白色球和6个黑色球,从中任取8个球,问共有多少不同的颜色搭配，把每种搭配显示出来**

```C
#include "stdio.h"
int main()
{
	int hose,baise,heise,a=0;
	printf("搭配颜色如下：\n红色  白色  黑色\n");
	for(hose=0;hose<=3;hose++)
		for(baise=0;baise<=3;baise++)
			for(heise=0;heise<=6;heise++)
	if(hose+baise+heise==8)
	{
		a++;
		printf("%d      %d      %d\n",hose,baise,heise);
	}
	printf("一共有%d种搭配方案\n",a);
	return 0;
}
```

**求1！+2！+3！+……+10!**

```C
#include "stdio.h"
int main()
{
	int a;
	double b=1,c=0;
	for(a=1;a<=10;a++)
	{
		b*=a;
		c+=b;
	}
	printf("%ld\n",c);
	return 0;
}
```

### 数组

**输入10个数，求其平均数**
```C
#include "stdio.h"
int main()
{
	int i,s;
	float a[10],c=0.0;
	printf("请输入10位数：\n");
	for(i=0;i<10;i++)
	{
		scanf("%f",&a[i]);
		c+=a[i];
	}
		printf("平均值为：%.2f\n",c/10);
		return 0;
}
```
**将数组num[10]={0,1,2,3,4,5,6,7,8,9}中的最后一个数移到最前面，其余数依次往后移一个位置**

```C
#include "stdio.h"
int main()
{
	int i,num[10]={0,1,2,3,4,5,6,7,8,9};
	for(i=0;i<=9;i++)
		num[i]=i;
	for(i=9;i>=0;i--)
		printf("%d,",num[i]);
    return 0;
}
```

**①输入三个字符串，将第二个字符串连接到第一个字符串的后面，然后输出连接后的字符串②比较第二个字符串和第三个字符串的大小③将第二个字符串和第三个字符串交换**

```C
#include <stdio.h>
#include <string.h>
	int main()
{
	char s1[100];
	char s2[100];
	char s3[100];
	char d[100];
	scanf("%s", s1);
	scanf("%s", s2);
	scanf("%s", s3);
		if (strcmp(s2,s3)>0)
		{printf("第二个字符串大于第三个字符\n");}
		else if (strcmp(s2,s3)<0)
				{printf("第二个字符串小于第三个字符\n");}
						else if (strcmp(s2,s3)==0)
				{printf("第二个字符串等于第三个字符\n");}
	strcpy(d, s1);
	strcpy(s1, s2);
	strcpy(s2,d);
	strcpy(d, s2);
	strcat(s1,s2);
	printf("%s\n",s1);
	strcpy(s2, s3);
	strcpy(s3,d);
	printf("%s,%s\n",s2,s3);
	return 0;
}
```

### 函数

**函数调求1乘2乘3*…15的积**

```C
#include "stdio.h"
double product(double c)
{	int i;
	for(i=1;i<=15;i++)
	c=c*i;
	return (c);
}
double main()
{	double a=1,b;
	b=product(a);
	printf("1*2*3*....15=%.lf\n",b);
	return 0;
}
```

### 指针

**输入a和b两个整数，用指针变量输出a和b的值**

```C
#include <stdio.h>
int main()
 { int *p1,*p2,a,b;
   printf("输入a和b两个整数:");
   scanf("%d%d",&a,&b);
   p1=&a;
   p2=&b;           
   printf("a=%d,b=%d\n",*p1,*p2);
   return 0;
}
```

**指针变量输出数组a[5]={1.2,1.3,2.4,5.0,6.7}中的元素，并求出各元素相加的和**

```C
#include "stdio.h"
int main()
{
	float *p,a[5]={1.2,1.3,2.4,5.0,6.7};
	int i;
	double num=0;
	for(p=a;p<(a+5);p++)
		printf("%.1f ",*p);
    for(i=0;i<6;i++)
        num=num+a[i];
    printf("\n%.lf",num);
    return 0;
}
```