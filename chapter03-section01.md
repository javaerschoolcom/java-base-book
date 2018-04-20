# 面向对象-概述

### 为什么会出现面向对象思想

### 面向过程
> 面向过程研究的是解决问题的过程，是一个逐步求解的过程，到一定的程度，不管是开发还是维护都变的非常困难。

### 面向对象
1.对象
>  把研究的问题转为对象进行研究，对象与对象发生通信。所有要研究的事物的个体都可以称为对象，对象具有状态和行为。

2.类
>  把一组对象具有的共同状态和行为抽象出来。类的本质是抽象的，有边界的，是一组对象的抽象。

3.类和对象关系
> 对象是类的具象事物，类是对象的抽象

### 类的定义
``` java
    [修饰符]  class   类名{
     //属性|成员变量
     //行为|成员方法
     //内部类
    }
```
1. 成员变量定义:[修饰符] 数据类型  变量名；
2. 成员方法定义:同方法定义

>  创建一个人类

``` java
    public class Persion{
      String  name; //姓名       成员变量
      int  age;   //年龄         成员变量
      public  void  speak(){  // 成员方法
        System.out.println("人会讲话");
      }
    }
```

### 类的使用
1. 通过类创造对象
``` java
    类类型   对象名=new 构造器();
```
``` java
    public class PersonTest{
       public static void main(String[] args) {
              Persion  persion = new Persion();//创建一个人类的个体（对象）
       }
    }
```

2. 使用类的成员变量
``` java
    赋值：数据类型  变量名 =  对象名.成员变量;
    获取：对象名.成员变量；
    没有初始化使用默认值:char默认为"\u0000"|数值默认为0|小数默认为0.0|布尔值默认为fasle|引用数据类型默认为null
```
``` java
    public class PersonTest{
       public static void main(String[] args) {
              Persion persion = new Persion();//创建一个人类的个体（对象）
              persion.name="lero"  //给类的成员变量赋值
              System.out.println(persion.name); ///获取类的成员变量
          }
    }
```

3. 使用类的成员方法
> 类的对象只能调用自己类中的方法，不能调用别的类中的方法

``` java
    对象名.成员方法名();
```
``` java
    public class PersonTest{
       public static void main(String[] args) {
              Persion  persion = new Persion();//创建一个人类的个体（对象）
              persion.speak(); //使用类的成员方法
          }
    }
```

4. 在类中方法的内部可以直接通过[类名.成员变量名]来使用成员变量
``` java
    public class Persion{
      String  name;
      int  age;
      public  void  speak(){
        System.out.println("我叫"+name); // 在类的方法中使用成员变量
      }
    }
```
5. 创建的每个对象都会复制一份所属类中的成员变量，它们是独立的不会相互影响
``` java
    public class PersonTest{
       public static void main(String[] args) {
              Persion persion1 = new Persion();
              persion1.name="lero"
              System.out.println(persion1.name); // lero

              Persion persion2 = new Persion();
              persion2.name="张三"
              System.out.println(persion1.name); // 张三
          }
    }
```

6. 成员变量可以是自定义的类类型
``` java
    /**
     * 学生类[使用了自定义班级类和学校类作为成员变量]
     */
    public class Student {
        String name; //姓名
        int age;   //年龄
        Clazz  clzz;//班级
        School school;//学校
        public  void showInfo(){
            System.out.println("姓名："+name+"年龄："+age+clzz.level+"年级"+clzz.clazzName+"来自于"+school.schoolName+"位于"+school.address);
        }
    }
```
``` java
    /**
     * 班级类
     */
    public class Clazz {
        String  clazzName; //班级
        String   level ;//年级
        public  void showInfo(){
            System.out.println(level+"年级："+level+"班");
        }
    }
```
``` java
    /**
     * 学校类
     */
    public class School {
        String  schoolName;//学校名称
        String  address ;//地址
        public  void showInfo(){
            System.out.println("学校名称："+schoolName+"所在地址："+address);
        }
    }
```
``` java
    /**
     * 测试类
     */
    public class PersionTest {
        public static void main(String[] args) {
            Student  student = new Student();//创建学生
            student.name="张三";
            student.age=11;

            Clazz clazz =new Clazz();
            clazz.clazzName="3班";
            clazz.level="1";
            student.clzz=clazz;

            School  school =new School();
            school.schoolName="绵中";
            school.address="绵阳XX街道";
            student.school=school;

            student.showInfo();
            System.out.println("==========================");
        }
    }
```

### 类的构造方法

``` java
    [修饰符] 类名([参数类型1 参数1,参数类型2 参数2...参数类型N 参数N]){
      //构造体
    }
```
1. 构造方法没有return,也没有返回类型，也没有void
2. 构造方法可以传递参数
3. 如果类中没有提供构造方法，系统就会有一个没有参数的构造方法
4. 如果类中显示的提供了构造方法，那么最好把无参数的构造方法写出来
5. 构造方法可以重载
6. 构造方法不是方法，不能通过对象调用，而是通过new命令调用
7. 对象本质上是由构造方法创造的

>  给定义的人类添加构造方法

``` java
    public class Persion{
      public Persion(){} //无参构造方法

      public Persion(String _name){ //带参数的构造方法
         name =_name;
      }
      String  name;
      int  age;
      public  void  speak(){
        System.out.println("人会讲话");
      }
    }
```

### 构造代码块
>  使用场景：创建对象前需要做的初始化工作,或者创建对象前每次都要做的事情可以放到代码块中

1. 语法：
``` java
    {  代码块体 }
```
1. 构造代码块在每次创建对象的时候都会执行并且优先于构造方法执行
``` java
public class Persion {
    {
        System.out.println("代码块每次创建对象都会执行");
    }
    public Persion(){}

    public Persion(String name){
         System.out.println("构造器执行了,才执行我");
    }
}
```
``` java
public class PersionTest {
    public static void main(String[] args) {
         Persion p1  =new Persion(); //输出：代码块每次创建对象都会优先于构造器执行
         Persion p2  =new Persion(); //输出：代码块每次创建对象都会优先于构造器执行  构造器执行了,才执行我
    }
}
```


### 匿名对象
1. 没有名字的对象
2. 使用场景：如果一个对象只需要使用一次

### static关键字
1.  static是修饰符可以修饰成员变量,成员方法,内部类;修饰的成员属于类级别的,而不是归哪个对象私有
2.  static修饰的成员会随着类的字节码加载而加载,因此优先于对象存在
3.  static修饰成员变量，使用**[类名.成员变量名]**调用，该变量被该类所有的对象共享
``` java
public class Persion {
    static String  country ="中国";
    public void showCountry(){
        System.out.println("我是"+Persion.country+"人");
    }
}
```
``` java
public class PersionTest {
    public static void main(String[] args) {
         Persion p1  =new Persion();
         p1.showCountry();    //我是中国人
         Persion p2  =new Persion();
         Persion.country ="韩国";
         p2.showCountry();    // 我是韩国人
         Persion p3  =new Persion();
         p3.showCountry();  //我是韩国人
    }
}
```
4.  static修改成员方法，使用**[类名.方法名()]**直接调用
``` java
public class Persion {
    public static void showCountry(){
        System.out.println("我是static修饰的成员方法");
    }
}
```
``` java
public class PersionTest {
    public static void main(String[] args) {
         Persion.showCountry();  //我是static修饰的成员方法
    }
}
```
5.  static修饰的方法不能调非static修饰的方法
public class Persion {
    public static void showCountry(){
        System.out.println("我是static修饰的成员方法");
        showInfo();// 编译错误
    }
    public void  showInfo(){
       System.out.println("我是普通成员方法");
    }
}
```
6.  static修饰代码块，只会在第一次创建该类对象的时候执行一次
``` java
public class Persion {
    static{
       System.out.println("我是static修饰的代码块,只会执行一次");
    }
}
```
``` java
public class PersionTest {
    public static void main(String[] args) {
         Persion  p1 = new Persion(); //结果：我是static修饰的代码块,只会执行一次
         Persion  p1 = new Persion(); //结果：无
    }
}
```

### package关键字
> package在java中就是包的意思，包本质是分类归档的文件夹，目的就是方便管理和使用

1. 语法**[package 根包名.自包名;]** package必须在类的第一个位置：
``` java
    package com.lero;
```
2. package的命名规则：域名倒着写+项目系统名+模块名
3. 不同的package下面可以定义相同的类名

### import关键字
> 当一个类中依赖于其他类的时候，需要把其他类引入使用，这个时候就需要import关键字

1. 语法：**import 包名(全限定名)+类名(不加后缀);
``` java
    import java.util.Arrays;
    import java.util.Date;
```
2. 如果想使用一个包下面的许多个类,可以使用通配符*表示,但是不能使用该包中子包的类
``` java
    import java.util.*;
```
3. 当一个类中同使使用不同包下面的同名的类的功能的是,必须要直接用包的全限定名+类名直接使用
``` java
     import  java.util.Arrays;
     import  com.lero.Arrays;
     public class Test {
         public static void main(String[] args) {
             System.out.println(java.util.Arrays.toString(new String[]{"1"}));
             System.out.println(com.lero.Arrays.toString(new String[]{"1"}));
         }
     }
```
4. 在同一个包中可以不用引入|使用java.lang包下的类的功能也可以不引入,比如:
``` java
    System.out.println();//System可以用不引入，属于java.lang包
```
