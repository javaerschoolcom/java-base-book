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

### 整数
1. 整数常量默认值是int类型
2. byte|short|int|long声明的变量所表示的整数在自身范围内可直接使用，会隐式转换
``` java
    byte x=127; //127默认int类型，但是127在byte范围之内，就会自动转为byte存储
    short y=32767; //32767默认int类型，但是32767在short范围之内，就会自动转为short存储
    long z=2147483647; //2147483647默认int类型，但是2147483647在long范围之内，就会自动转为long存储
    long z=2147483648L; //2147483648不在int范围之内(存储不下)，此时必须加上L，变成long存储
```
3. 整数在临界时的计算要特别小心
``` java
     int a =2147483647;
     System.out.println(a+1); -2147483648 //变成了最小值
```

###  浮点数
>精度 有效小数位,大的数需要转换成小数的指数形式.例如:8317637.5其有效小数位:8.3176375E6七位

1. 浮点常量默认是double类型
2. float的精度为6~7位，能保证6位为绝对精确，7位一般也是正确的，8位就不一定了
``` java
     float x =1.234567896F;
     System.out.println(x); //1.2345679 精度为7位
```
3. double的精度为15~16位，能保证15，一般16位
``` java
     double x =1.2345678901234567891234;
     System.out.println(x); //1.2345678901234567 精度为17位
```
4. 浮点数是不准确的数，涉及到金钱相关的要特别注意
``` java
     double x =1.0;
     System.out.println(x+0.000000000000000001); //1.0  结果是在一定的误差范围内，但不能准确表示
```

### 布尔类型
1. java中有且只有2个值：true|false

### 字符char
1. 字符类型的值是用单引号引起来的一个字符
``` java
     char x ='&';
     System.out.println(x); //&
```
2. 字符使用unicode编码,它把0-65535每个整数与一个字符进行一一对应,可以直接使用这个范围内整数表示字符
``` java
     char x =97; //unicode编码为a
     System.out.println(x); //a
```
3. 字符也可以使用'\uX'表示，其中X表示4位的16进制数
``` java
     char x ='\u0061'; //unicode的a字符对应编码整数为97,97转16进制为61
     System.out.println(x); //a
```
4. char类型有2个字节，可以表示一个汉字
``` java
     char x ='中';
     System.out.println(x); //中
     char y ='\u4e2d';  //unicode的‘中’字符对应编码为16进制数4e2d
     System.out.println(y); //中
```
5.特殊字符转义:某些符合在java中有特殊的用途，会解析java语法，为了还原符号的本意，因此需要转义

``` java
     char x='\'';//表示单引号
     char y='\"';//表示双引号
     char z='\r';//表示回车键
     char m='\n';//表示换行符
     char n='\t';//表示制表符
```

### 数据类型转换
1.  隐式转换
> 从小到大，可以隐式转换，数据类型将自动提升，但是bybe转char,short转char,char转short不会隐式转换。

byte，short，char -->int  -->long -->float -->double
``` java
     byte x=10;
     int y=x;
     System.out.println(y); //编译通过 byte类型的变量a隐式转换为int类型的变量b
```
``` java
     byte x=10;
     char y=x;
     System.out.println(y); //编译报错
```

2.  强制转换
> 从大到小，不会发生隐式转换，只能使用强制转换

``` java
     int x=10;
     byte y=x;
     System.out.println(y); //编译错误  int类型x赋值给byte类型y,属于从大转小
```
> 强制转换使用方法

``` java
     byte x=126;
     y=(byte)y+1; //强制转换写法
     System.out.println(y); //127  编译通过
```

3.  数值表达式自动提升
>   数值表达式(结果是数值)的运算结果类型和参与运算类型最高的一个一致

``` java
     byte x=1;
     int  y=2;
     float z=x+y*0.1;  //编译失败   x类型为byte,y类型为int,常量0.1默认类型为double.结果类型应该为double
     System.out.println(z); // 不会执行
```

``` java
     byte x=1;
     int  y=2;
     double z=x+y*0.1;  //编译通过
     System.out.println(z); //1.2
```

### 字符串
>   字符串属于引用类型一个使用频率很高的类类型

1. 使用方法:用双引号把多个依次排列的字符包裹起来
``` java
     String s="我是一个字符串";
     System.out.println(s); //我是一个字符串
```
2.  使用连接符（+）可以把多个变量或者常量或者字符串本身进行连接，结果把每个因子转换为字符串，再依次连接。
``` java
     String s="我是一个字符串";
     int  j =100;
     System.out.println(s+":"+j+1); //我是一个字符串:1001
```
3.  字符串中使用转义符号
``` java
     System.out.println("\"hello\""); //"hello"
```



