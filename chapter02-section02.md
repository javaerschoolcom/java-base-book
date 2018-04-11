# java语法基础-变量

### 变量定义
> ----变量代表内存中一块存储区域，用来存放某一类型的常量，可以重复使用且没有固定的值，也可以存储某类型的未知数据

### 变量的声明方式
1. 数据类型  变量名=常量;
``` java
    int x=10;
```
2. 数据类型  变量名；
``` java
    int y;
```
3. 数据类型  变量名1,变量名2,...变量名N;
``` java
    int m,n;
```

### 变量注意事项
1. 变量使用前一定要初始化
``` java
    int x;
    System.out.println(x); //错误:未初始化
```
2. 变量一定要先声明再使用
``` java
    System.out.println(x); //错误:未先声明直接使用
    int x;
```
3. 变量可以重复使用
``` java
    int x=10;
    System.out.println(x); //10
    x=11; //正确:重复使用变量x
    System.out.println(x); //11
```
4. 同一作用域中的变量不能重复定义
``` java
    {
        int temp=10;
        System.out.println(temp); //10
        int temp=11; //错误:同一作用域重复定义变量temp
        System.out.println(temp); //11
    }
```
5. 变量的值只能够在同一种数据类型中变化
``` java
    int temp=10;
    System.out.println(temp); //10
    temp=true; //错误:布尔类型不能赋值给int类型
    System.out.println(temp); //报错
```

### 变量的作用域
> 作用域：变量的存在范围，超过变量定义的区域则无法使用变量

1. 全局作用域：直接定义在类中的变量，在类中任何位置都能使用(全局变量)
``` java
    class Second{
       static int x =4;
       public static void main(String[] args){
         System.out.println(x);//main方法作用域
         say();
       }

       public static void say(){
         System.out.println(x);//say方法作用域
       }
    }
```

2. 局部作用域：不是全局作用域的变量就是局部作用域，只在定义区域有效(局部变量)
``` java
    class Second{
       public static void main(String[] args){
         int x=10; //main方法作用域
         System.out.println("我是main方法作用域中的x:"+x);
         say();
       }

       public static void say(){
         int x=11; //say方法作用域
         System.out.println("我是say方法作用域中的x:"+x);
       }
    }
```
3. 有效范围：变量在最近的一个被包含的{}内有效

### 变量的使用方式
1. 局部变量可以通过引用变量名方式使用
