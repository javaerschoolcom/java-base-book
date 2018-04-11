# java语法基础-数据类型

###  数据类型定义
>  把数据划分成不同的种类，每一种均有有自己的特点

###  数据类型分类
1. 基本数据类型:byte|short|char|int||long|float|double|boolean
2. 引用数据类型:类|数组|接口

###  数据类型范围

> 位:数据存储的最小单位，也称为比特,每个0或1就是一个位(bit)

> 字节:计量存储容量的一种计量单位，通常情况下一字节等于有八位

* byte:1字节[-2^7到2^7-1]
* short:2字节[-2^15到2^15-1]
* char:2字节[-2^15到2^15-1]
* int:4字节[-2^31到2^31-1]
* long:8字节[-2^63到2^63-1]
* float:4字节[-3.4E38到3.4E38]
* double:8字节[-1.7E308到1.7E308]

### 数据类型使用：
* long类型的数据需要以L或者l结尾

* float类型的数据需要以F或者f结尾

``` java
    byte b=127;  //定义byte类型数据
    short s = 12345; //定义short类型数据
    int  i= 1234567; //定义int类型数据
    long l=34348294242L; //定义long类型数据
    float f =3.1F; //定义float类型数据
    double d=3.14; //定义double类型数据
    boolean bt=true; //定义boolean类型数据
    boolean bf=false; //定义boolean类型数据
```

### 数据表示方法

1.  十进制表示法
``` java
    byte x=127;
```
2.  科学计数法:以E分割指数位,通常用来表示double类型数据
``` java
    double x=3.1415926E8; //3.1415926乘以10的8次方
```
3.  二进制表示法:以0B开头,通常表示整数
``` java
    short x=0B00000000_00000011; // java7开始支持_分割字节，看起来更直观
    System.out.println(x);//3
```
4.  八进制表示法:以0开头,通常表示整数
``` java
    byte x=0_00000011;  //写全
    byte y=011;  // 简写
    System.out.println(x);//9
```
5.  十六进制表示法:以0X开头,通常表示整数
``` java
    byte x=0XF;
    System.out.println(x);//16
```




