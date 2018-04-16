# java语法基础-运算符

### 算术运算符
> 算术运算符有：+ - * / % ++ --

###### +运算
1. +作为一元运算符 表示正数
2. +作为二元运算符 表示加法运算
``` java
     System.out.println(1+2); //左右算子均为数值
```
3. 加法运算中算子均为char时候，会转为unicode码进行整数运算，最后再转为字符
``` java
     char x=97;
     char y=1;
     char c=(char)(x+y);
     System.out.println(c); // b
```
``` java
     char x='a';
     char y=1;
     char c=(char)(x+y);
     System.out.println(c); // b
```
4. 加法运算中算子有字符串时候，会把算子先转为字符串，再进行连接
``` java
     String x="hello";
     char y=1;
     System.out.println(x+y); // helloa
     System.out.println("lero"+1+1); // lero11
```

###### -运算
1. -作为一元运算符 表示负数
2. -作为二元运算符 表示减法运算
``` java
     System.out.println(2-1); //左右算子均为数值
```

###### *运算
1. *为二元运算符 表示乘法运算
``` java
     System.out.println(2*1); //2
```

###### /运算
1. /为二元运算符 表示除法运算
``` java
     System.out.println(2/1); //2
```
2. 当被除数为整数，除数不能为0
``` java
     System.out.println(2/0); //运行报错
```
3. 当被除数为小数,除数可以为0；则结果是无穷大
``` java
     System.out.println(2.0/0); //Infinity
```
4. 当被除数为整数,除数为0.0；结果是无穷大
``` java
     System.out.println(2/0.0); //Infinity
```
5. 当被除数为0.0，除数为0.0或者0；结果为NaN  not a number
``` java
     System.out.println(0.0/0.0); //NaN
```
6. 整数除以整数结果小数部分舍去
``` java
     System.out.println(10/3); //3
```
###### %运算
1. %为二元运算符  表示求模/求余数
``` java
     System.out.println(10%3); //1
```
2.求模的结果取决于被除数，被除数为整数结果为正，被除数为负结果为负
``` java
     System.out.println(-10%3); //-1
     System.out.println(10%-3); //1
     System.out.println(-10%-3); //-1
```

###### ++运算
1. ++为一元运算符 表示累加，算子可以在运算符左边，也可以在运算符右边
``` java
     int i=1;
     System.out.println(i++); //1
     int j=1;
     System.out.println(++i); //2
```
2. 算子在左边  算子++  不管怎么算子本身总是加1 表达式的值是算子加一【前】的值
``` java
     int i=1;
     System.out.println(i++); // 表达式(i++)的值是1
     System.out.println(i); //算子i的值是2
```
3. 算子在右边  ++算子  不管怎么算子本身总是加1 表达式的值是算子加一【后】的值
``` java
     int i=1;
     System.out.println(++i); // 表达式(++i)的值是2
     System.out.println(i); //算子i的值是2
```
###### --运算
1. --为一元运算符 表示累减，算子可以在运算符左边，也可以在运算符右边
``` java
     int i=1;
     System.out.println(i--); //1
     int j=1;
     System.out.println(--i); //0
```
2. 算子在左边  算子--  不管怎么算子本身总是减1 表达式的值是算子减一【前】的值
``` java
     int i=1;
     System.out.println(i--); // 表达式(i--)的值是1
     System.out.println(i); //算子i的值是0
```
3. 算子在右边  --算子  不管怎么算子本身总是减1 表达式的值是算子减一【后】的值
``` java
     int i=1;
     System.out.println(--i); // 表达式(--i)的值是0
     System.out.println(i); //算子i的值是0
```

###  赋值运算符
> 赋值运算符号有= += -= *= /= %=
> 赋值运算符运算规则：把符号左边和右边相(加|减|乘|除|模)的结果重新赋值给左边

1. 基本使用
``` java
    int x=1;// 赋值符=：把右边的1赋值给左边的x
    x+=1;  //相当于 x=x+1
    System.out.println(x);//2
```

2. 赋值运算符含有隐式转换
``` java
    short x=1;
    x=x+1;  //编译失败
    System.out.println(x);
```

``` java
    short x=1;
    x+=1;  //编译成功  隐含了这步操作 x=(short)(x+1)
    System.out.println(x);
```

### 比较运算符
>  比较运算符有> >= == != < <=
>  比较运算符的结果一定是布尔值

1. 比较的是数值,不能是布尔类型
``` java
    System.out.println(1>2);  //false
    System.out.println(1>=2); //false
    System.out.println(1==2); //false
    System.out.println(1!=2); //true
    System.out.println(1<2);  //true
    System.out.println(1<=2); //true
    //System.out.println(true>false); //编译失败
```
2. ==和!=两个运算符可以比较字符串(比较是地址，一般采用equal方法)
``` java
    String  x="abc";
    String  y="a"+"b"+"c";
    String  z=new String("abc");
    System.out.println(x==y);  //true 都在常量区，地址一样
    System.out.println(x==z); //false 比较的是地址，存储的地址不一样
    System.out.println(x.equals(z)); //true  比较的是地址中存储的值
```

### 逻辑运算符
>  逻辑运算符有| & ^ || &&  !
>  逻辑运算的结果一定是布尔值

1. 逻辑运算符的算子是布尔值或者布尔表达
``` java
    System.out.println(true|false); //有真则真  true
    System.out.println(true&false); //有假则假   false
    System.out.println(true^false); //同假异真   true
    System.out.println(true^true); //同假异真   false
    System.out.println(false^false); //同假异真   false
    System.out.println(true||false); //有真则真  true
    System.out.println(true&&false); //有假则假  false
    System.out.println(1>3&&false); //有假则假   false
    System.out.println(!!false); //求反  true
```
2. &和&&的区别
``` java
    int x =1;
    System.out.println(false&x++); //&运算符左边为假，依旧会进行右边运算
    System.out.println(x);// x=2

    System.out.println(false&&x++);  //&运算符左边为假，不会进行右边运算
    System.out.println(x);// x=1
```

### 位运算符
>  位运算符有| &  ~  ^  << >>  >>
>  位运算符都是把整数转为二进制，作用于每一位

``` java
    int x =3; // 00000000_00000000_00000000_00000011
    int y =4; // 00000000_00000000_00000000_00000100
    System.out.println(x|y); // 00000000_00000000_00000000_00000111    结果为7
    System.out.println(x&y);//  00000000_00000000_00000000_00000000    结果为0
    System.out.println(x^y);//  00000000_00000000_00000000_00000111    结果为7

    int z=2; //如何快速计算2的3次方？
    System.out.println(2<<2);  // 8
    int j=16; //如何快速把16变为2
    System.out.println(16>>3);// 2
```
1. 不使用额外变量,交换两个存储整数变量的值,两个变量连续异或三次，就会交换位置

``` java
    int x =3;
    int y =4;
    x=x^y;
    y=x^y;
    x=x^y;
    System.out.println(x); // 4
    System.out.println(y);//  3
```

### 三目运算符
>   数据类型  result=布尔表达式?表达式1:表达式2
>   注意事项：表达式1的类型要和表达式2的类型一至或者兼容

1. 若布尔表达式的结果为true,则result为表达式1的值；若表达式的结果为false,则result为表达式2的值
``` java
    //需求：求x和y的最大值
    int x =3; //
    int y =4; //
    int result= (x>4)?x:y ;
    System.out.println(result);// 4
```


