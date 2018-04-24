# 面向对象-抽象类

### 抽象类应用场景
>  在同一个体系中父类中的方法无法确定实现细节的时候，就可以使用抽象类

### 抽象类定义
>  使用了关键词abstract声明的类叫作抽象类，抽象类中的功能可能是不完善的，需要子类自己完善功能

###### 语法
``` java
    [修饰符] abstract class 类名(){}
```
1. 抽象类可以没有抽象方法
2. 抽象类可以有普通类的所有成员
3. 抽象类不能创建对象
4. 最终的子类继承了抽象类必须覆写所有的抽象方法
5. 抽象类中不能有抽象的静态方法
6. abstract不能和private,static,final共存

### 抽象方法定义
>  使用abstract修饰的方法，并且该方法没有方法体

######语法
``` java
    [修饰符] abstract 返回类型 方法名();//没有方法体
```


