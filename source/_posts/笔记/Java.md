---
title: 'Java'
date: '2022-2-28 16:31:00'
description: 世界上最好的语言
sticky: 2
tags:
- Java
- 编程
categories: 编程笔记
top_img:
cover:  /img/java.jpg
---

# 第二章
**什么叫标识符？标识符的规则是什么？false是否可以作为标识符？**
- 标识符是用来标识包名、类名、方法名、变量名、参数名、数组名、对象名、接口名、文件名的字符序列。标识符由数字、字母、下划线_和符号$组成，第一个字符不能是数字，关键字当作标识符使用，标识符是区分大小写的。
- Java命名约定如下：
1. 包名所有字母小写，如com.seehope.web
2. 类名和接口名可以由多个单词组成，每个单词的首字母大写，如MyClass、HelloWorld、Time等
2. 方法名、变量名和对象名可以由多个单词组成，第一单词的首字母小写、其余单词的首字母大写，如getName、setTime、myName等。这种命名方法叫做驼峰式命名法。变量命名要尽量做到见名知义，便于理解和阅读。例如，标识符userName，一看便知是‘用户名’。
- False不能作为标识符
**什么叫关键字？true 和 false 是否是关键字？请说出六个关键字**
- 关键字是Java语言中已经被赋予特定含义的一些单词，不能用作标识符，前面见过的class、public、static、void等都是关键字。
- True和false不是关键字
- Boolean char double int long float

## 实验

### 奇偶数判断 
要求：输入一个数字，输出是奇数还是偶数。
分析：接收键盘输入的整数，如果除 2 求余为 0 则是偶数，否则为奇数，判断时会用到三元运算符。
```Java
package chapter2;
import java.util.Scanner;

public class experiment01 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入一个数：");
        int num=sc.nextInt();
        String s =(num % 2 == 0 ? "偶数" : "奇数");
        System.out.println("这个数为："+s);
    }
}
```

### 变量值交换 
要求：将键盘输入的两个整型数据分别赋给两个变量，然后交换两个变量的值。
分析：要使用一个中间变量暂存变量值才能实现交换。
```Java
package chapter2;
import java.util.Scanner;

public class experiment02 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入两个数：");
        int num=sc.nextInt();
        int Num=sc.nextInt();
        int a;
        System.out.println("交换前\n"+"第一位数为："+num+",第二位数为："+Num);
        a=num;num=Num;Num=a;
        System.out.println("交换后\n"+"第一位数为："+num+",第二位数为："+Num);
    }
}
```

### 判断闰年 
要求：利用本章所学知识，编写一个实用程序，判断给定的某个年份是否为闰年。 
分析：闰年的判断规则如下。
(1)若某个年份能被 4 整除但不能被 100 整除，则是闰年。
(2)若某个年份能被 400 整除，则是闰年
```Java
package chapter2;
import java.util.Scanner;

public class experiment03 {
    public static void main(String[] args){
      Scanner sc=new Scanner(System.in);
      System.out.println("请输入年份：");
      int year=sc.nextInt();
      String num=((year%4==0)&(year%100!=0)|(year%400==0)?"闰年":"平年");
        System.out.println(num);
    }
}
```

### 用户登录
要求：分别用两个变量接收用户输入的用户名与密码，假设输入用户名为 admin,密码为123提示登录成功，否则提示用户或密码不正确。
分析：使用三元运算,用表达式判断用户名和密码是否正确,分别返回不同结果。
```Java
package chapter2;
import java.util.Scanner;

public class experiment04 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入用户名：");
        System.out.println("请输入密码：");
        String userName=sc.nextLine();
        int Key=sc.nextInt();
        /*运算符==是针对整形int，long int和浮点数的比较。
        .equals（）是针对String的比较*/
        String s=(userName.equals("admin")&(Key==123)?"登录成功！":"用户或密码不正确");
        System.out.println(s);
    }
}
```

## 作业
### 输入一个小写字母输出大写字母
```Java
package chapter2;
import java.util.Scanner; 

public class experiment1 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入一个小写字母：");
        String Str1=sc.nextLine();
        //toUpperCase() 方法用于将小写字符转换为大写//
        String Str2=Str1.toUpperCase();
        System.out.println(Str2);
    }
}
```

### 汉字你、我、他、在 Unicode 表中的位置
```Java
package chapter2; 
public class experiment2 {
public static void main(String[] args){
        char Char1='你',Char2='我',Char3='他';
        System.out.println("汉字："+Char1+"、"+Char2+"、"+Char3+"\n在Unicode表中的位置分别为\n" + (int) Char1+"\n"+(int)Char2+"\n"+(int) Char3);
    }
}
```

### 计算几何六边形面积
- 六边形面积可以通过下面公式计算（s 是边长)：(6 * s * s) / (4 * Math.tan(Math.PI / 6))
```Java
package chapter2;
import java.util.Scanner;
public class experiment3 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入六边形的边长");
        double sl =sc.nextDouble();
        //Math.PI 返回 PI（圆的面积与其半径的平方之比，约为 3.14）
        //Math.tan 方法返回数字的切线
        double area=(6 * sl * sl) / (4 * Math.tan(Math.PI / 6));
        System.out.println("六边形的面积为："+area);
    }
}
```

### 顶点坐标
- 假设一个正五边形的中心位于（0, 0)，其中一个点位于 0 点位置，编写一个程序，提示用户输入正五边形外切圆的半径，显示正五边形上五个顶点的坐标。
```Java
package chapter2; 
import java.util.Scanner;

public class experiment4 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入正五边形外切圆的半径：");
        Double sl=sc.nextDouble();
        double a1,b1,a2,b2,a3,b3,a4,b4,a5,b5;
        a1 = sl * Math.cos(Math.PI / 2 - ( 2 * Math.PI / 5));
        b1 = sl * Math.sin(Math.PI / 2 - ( 2 * Math.PI / 5));
        a2 = sl * Math.cos(Math.PI / 2);
        b2 = sl * Math.sin(Math.PI / 2);
        a3 = sl * Math.cos(Math.PI / 2 + (2 * Math.PI / 5));
        b3 = sl * Math.sin(Math.PI / 2 + (2 * Math.PI / 5));
        a4 = sl * Math.cos(Math.PI / 2 + 2 * (2 * Math.PI/5));
        b4 = sl * Math.sin(Math.PI / 2 + 2 * (2 * Math.PI/5));
        a5 = sl * Math.cos(Math.PI / 2 - 2 * (2 * Math.PI/5));
        b5 = sl * Math.sin(Math.PI / 2 - 2 * (2 * Math.PI/5));
        System.out.println("正五边形5个顶点分别为：");
        System.out.printf("(%.2f,%.2f)\n",a1,b1);
        System.out.printf("(%.2f,%.2f)\n",a2,b2);
        System.out.printf("(%.2f,%.2f)\n",a3,b3);
        System.out.printf("(%.2f,%.2f)\n",a4,b4);
        System.out.printf("(%.2f,%.2f)\n",a5,b5);
    }
}
```

### 输入十进制数输出二进制数
```Java
package chapter2;
import java.util.Scanner; 

public class experiment5 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入十进制数0~9：");
        int num=sc.nextInt();
        // String toBinaryString(int i)     以2为基返回整数参数的字符串表示形式，表示为无符号整数
        System.out.println(Integer.toBinaryString(num));
    }
}
```

### 输入十六进制数输出二进制数
```Java
package chapter2;
import java.util.Scanner;

public class experiment6 {
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入十六进制数0~F：");
        String num=sc.nextLine();
        int z=Integer.valueOf(num,16);
        System.out.println(Integer.toBinaryString(z));
    }
}
```

### 实现会员注册
- 要求用户名长度不小于 3，密码长度不小于 6，若不满足需有提示信息，提示输入有误；注册时两次输入密码必须相同（字符串）。
```Java
package chapter2;
import java.util.Scanner;

public class experiment7 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("注册用户名(用户名长度大于3)：");
        String userName = sc.nextLine();
        System.out.println("注册密码(密码长度大于6)：");
        String userKey = sc.nextLine();
        System.out.println("确定注册密码：");
        String userKEy = sc.nextLine();
        if (userName.length()>3 & userKey.length()>6 & userKEy.equals(userKey)){
            System.out.println("注册成功！");}
        else{
            System.out.println("注册信息有误！");}
    }
}
```

### 输出全部的希腊字母
```Java
package chapter2;

public class experiment8 {
    public static void main(String[] args){
        char alpha = 'α', omega = 'ω';
        for (int i = (int)alpha; i <= (int) omega; ++i){
            System.out.println(" "+(char) i );
        }
    }
}
```


### 100以内的素数
```Java
package chapter2;

public class experiment9 {
    public static void main(String[] args){
    int i,a;
    for (i = 1; i <= 50; i++){
        if (i == 1 || i == 2){
            System.out.println(i);continue;}
        for (a = 2; a < i; a++){
            if (i % a == 0) break;
            if (a == i-1)System.out.println(i+" ");
        }
    }
    }
}
```

### 计算输出表达式 12+5>3 || 12-5<7 的值
```Java
package chapter2;

public class experiment10 {
    public static void main(String[] args){
         boolean num = (12+5>3 || 12-5<7);
         System.out.println(num);
    }
}
```