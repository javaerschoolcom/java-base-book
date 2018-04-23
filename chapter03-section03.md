# 面向对象-继承

### 为什么使用继承
>  从一般到特殊的关系问题研究的时候，一是为了解决类中代码重复书写的问题，二是为了让每个类做专一的事

### 什么是继承
>  继承是从已有的类中派生出新的类，新的类能吸收已有类的数据属性和行为，并能扩展新的能力。

### 继承语法
``` java
权限修饰符  class  子类  extends  父类{
   //todo
}
```
###### 注意事项
1. 继承只能支持直接单继承，不能直接多继承，但是可以间接继承
2. 具有继承关系的子类创建对象的时候，会首先调用父类的构造器，调用顺序总是从最顶层往下
3. 具有继承关系的子类创建对象的时候，默认调用父类的无参数的构造器，如果父类有构造器重载却没有提供无参数构造器，会出错

### 哪些类成员可以被继承
1. public修饰的成员变量，成员方法能被继承，构造器,代码块不能被继承
2. 默认权限修饰符，只能在同包下才能被继承
3. protected修饰的，不是管是同包还是非同包都被继承
4. private修饰的理论上可以被继承，但是访问不到，没意义

### Object类
1. Object类是继承关系中的最顶层，所有的类都是继承自该类
2. 具体方法：
2.1  public boolean equals(Object obj)//子类需要覆写该方法
2.2  public String toString()//子类需要覆写
2.3  public final Class<?> getClass()
2.4  public int hashCode()//

### 方法的覆写
1. 方法覆写的前提拥有继承关系或者实现关系
2. 一同两小一大
2.1. 一同:方法签名一样(方法名一样，参数一样)
2.2  两小：子类的返回类型要比父类的小或者是相同|子类抛出的异常信息类型也是要和父类相同或者是比父类小
3. 一大：子类的权限修饰符小于等于父类的权限修饰符

### 如何覆写
1. 使用@Override放在方法体的上面，用于验证该方法是否是覆写方法


### super关键字
1. 可以修饰成员变量，用于子类访问父类成员变量
2. 可以修饰成员方法，用于调用父类的方法
3. 可以调用父类的构造器
4. super不能和static共同存在


