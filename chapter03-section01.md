# 面向对象-概述

### 为什么会出现面向对象思想

### 面向过程
> 面向过程研究的是解决问题的过程，是一个逐步求解的过程，到一定的程度，不管是开发还是维护都变的非常困难。

### 面向对象
1.对象
>  把研究的问题转为对象进行研究，对象与对象之间就会通信。所有要研究的事物都可以称为对象|万物皆是对象

2.类
>  把对象具有的共同属性和行为抽象出来，类的本质是抽象的，有边界的，是一组对象的抽象。

3.类和对象关系
> 对象是类的具象事物，类是对象的抽象

### 定义类
``` java
    [修饰符]  class   类名{
     //属性|成员变量
     //行为|成员方法
     //内部类
    }
```
1. 成员变量定义:[修饰符] 数据类型  变量名；
2. 成员方法定义:同方法定义

### 类的使用
1. 通过类创造对象
``` java
    类类型   对象名=new 构造器();
```
2. 使用类的成员变量
``` java
    赋值：数据类型  变量名 =  对象名.成员变量;
    获取：对象名.成员变量；
    没有初始化使用默认值:char默认为"\u0000"|数值默认为0|小数默认为0.0|布尔值默认为fasle|引用数据类型默认为null
```
3. 使用类的成员方法
``` java
    对象名.成员方法名();
```
4. 在类中方法的内部可以直接通过[类名.成员变量名]来使用成员变量

5. 创建的每个对象都会复制一份所属类中的成员变量，它们是独立的不会相互影响

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

1. 如果类中没有提供构造方法，系统就会有一个没有参数的构造方法
2. 构造方法没有return,也没有返回类型，也没有void
3. 构造方法可以传递参数
4. 如果显示的提供了构造方法，那么最好把无参数的构造方法写出来
5. 构造方法可以重载

