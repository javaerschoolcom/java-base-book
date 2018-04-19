# java语法基础-方法

### 什么是方法/为什么要使用方法
1. 方法是一段可以重复使用的代码,是解决一类问题的步骤的有序组合
2. 简化代码
3. 利于维护
4. 重复使用

### 方法定义
``` java
[修饰符] 返回数据类型[void] 方法名([数据类型1 参数名1,数据类型2 参数名2...数据类型N 参数名N]){
       //方法体
       return  返回结果表达式
}
```
*  修饰符：private protected  public 缺省的 /static final abstract synchronized等
*  void:当方法没有返回结果的时候使用
*  方法名：一般以动词开始，如果有多个单词，一般遵从驼峰法命名，方法名和参数表共同构成方法签名
*  形式参数：参数是一个占位符，方法被调用时用于传递值，方法可以没有参数
*  方法体：方法体包含具体的语句，定义该方法的功能
*  return:返回数据类型一般和return一起使用，有return就没有void

> 没有参数没有返回类型的方法

``` java
public static void  printOneWord(){
    System.out.println("没有参数没有返回类型的方法");
}
```
> 有一个参数的方法但没有返回值的方法

``` java
public static void  printTwoWord(int s){
    System.out.println(s);
}
```
> 有多个参数没有返回值的方法

``` java
public static void  sum(int x,int y){
   System.out.println(x+y);
}
```
> 有多个参数并且有返回值的方法

``` java
public static int dev(int x,int y){
   return x/y;
}
```
### 注意事项
>  方法直接定义在类中，方法与方法之间是平级关系，不能在方法内部再定义方法

``` java
public class Deom_method {
    public static void main(String[] args) {
        //错误：方法内部不能再定义方法
        public static void  printTwoWord(int s){
               System.out.println(s);
           }
    }
```
>  返回数据类型要和return后面表达式类型相同

``` java
//错误：方法返回类型与return后面表达式类型不一致
public static boolean dev(int x,int y){
    return x/y;
}
```
### 方法使用
1. 对象.方法名(实际参数1,实际参数2...实际参数N);
2. 类名.方法名(实际参数1,实际参数2...实际参数N);
3. 如果使用同一个类中的其他方法:方法名(实际参数1,实际参数2...实际参数N) ;

### 方法设计思想
1. 解决问题的未知条件作为方法参数传入方法体
2. 在方法体中方法参数作为已知数使用，当成该数已经存在
3. 解决的问题若需要一个结果，则写在return后面的表达式中，这个表达式的结果和返回数据类型相同

### 方法重载
1. 方法名相同|同一个类中(两同一不同)
2. 参数不同(参数的个数不同，参数的顺序不同，参数的类型不同)
3. 方法只是返回类型不一样，不能构成重载条件

### 方法递归
>  定义的方法内部又在调用自己本身

1. 递归方法不要嵌套太深，内存不足，执行效率低
2. 递归方法一定要有一个出口

> 求n的阶乘

``` java
//递归调用
public  static int getSub(int x){
    if(x==1){
        return 1;
    }else{
        return  x*getSub(x-1);//递归调用
    }
}
```

