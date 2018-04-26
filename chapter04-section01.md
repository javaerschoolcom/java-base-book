# 核心类-包装类

###  包装类
>  包装类其实就是8大基本数据类型封装成的类,后面操作的数据可就是对象，就需要把基本数据类型转换成类的方式

###  包装类
|byte|short|char|int|long|float|double|boolean|
|Byte|Short|Character|Integer|Long|Float|Double|Boolean|

###  包装类和基本类型互转
``` java
     基本数据类型转包装类
     Byte   B= new  Byte(String b) //字符串必须手动转

     Byte   B =Byte.valueOf(String b)// 字符串必须手动转

     包装类型转基本数据类型
     byte  b = B.byteValue();
```

### 自动装箱
>  把基本数据类型自动转为包装类型

### 自动拆箱
>  把包装类型自动转为基本数据类型

### BigInteger类
>  应用场景long类型存不下的整数，就可以使用该类

1. 构造函数：BigInteger(String val);
2. BigInteger add(BigInteger val) //加
3. BigInteger subtract(BigInteger val)  //减
4. BigInteger multiply(BigInteger val)  //乘
5. BigInteger divide(BigInteger val)  //除

###  BigDecimal类
> 解决float和double无法精确表示小数的问题

1. 使用该类构造的时候，传入不精确的数依然无法表示精确的数，常采用字符串构造精确的数

### Math类
> Math类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数

###### Math类特点
> Math类都是静态方法

###### Math类常用方法
1. static double max(double a, double b) //求两个数的最大值
``` java
    System.out.println(Math.max(2.0,3.0)); //3.0
```
2. static double min(double a, double b) //求两个数的最小值
``` java
    System.out.println(Math.min(2.0,3.0)); //2.0
```
3. static double random()  //生成[0,1)随机数
``` java
    System.out.println(Math.random()); // 随机数的范围[0,1)
```
4. static long round(double a) // 四舍五入
``` java
    System.out.println(Math.round(1.51)); //2
    System.out.println(Math.round(1.5)); //2
    System.out.println(Math.round(1.49)); //1
```
5. static double floor(double a)  //向下取
``` java
    System.out.println(Math.floor(1.51)); //1.0
    System.out.println(Math.floor(1.5)); //1.0
    System.out.println(Math.floor(1.49)); //1.0
    System.out.println(Math.floor(-1.51)); //-2
    System.out.println(Math.floor(-1.5)); //-2
    System.out.println(Math.floor(-1.49)); //-2
```
6. static double ceil(double a)   //向上取
``` java
    System.out.println(Math.ceil(1.51)); //2.0
    System.out.println(Math.ceil(1.5)); //2.0
    System.out.println(Math.ceil(1.49)); //2.0
    System.out.println(Math.ceil(-1.51)); //-1.0
    System.out.println(Math.ceil(-1.5)); //-1.0
    System.out.println(Math.ceil(-1.49)); //-1.0
```





















