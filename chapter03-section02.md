# 面向对象-封装

### 封装性

###### 什么是封装
>  是指利用抽象数据类型(类)将数据(成员变量)和基于数据的操作(成员方法)封装在一起，使其构成一个不可分割的独立实体，尽可能地隐藏内部的细节，只保留一些对外接口使之与外部发生联系。

###### 为什么使用封装
1. 提高安全性,防止访问者非法访问和非法读写数据。
2. 提高内聚，减少耦合
3. 隐藏实现细节和信息

###### 如何使用封装
1. 使用private修饰要隐藏的成员变量,成员方法,构造函数,内部类等
2. 对于成员变量可以提供一组set/get方法来提供对外访问的接口

###  权限修饰符
>  权限修饰符的作用就是控制对外访问的权限。可以修饰类,成员变量,成员方法,构造函数,内部类等

|修饰符|本类可以访问|同包可以访问|同包及子类可以访问|所有包可以访问|
|:---|:---|:---|:---|:---|
|private|是|否|否|否|
|缺省的|是|是|否|否|
|protected|是|是|是|否|
|public|是|是|是|是|

### this关键字
>  this是一个**对象**

1. 可以解决参数命名冲突
``` java
public class Rectangle {
    private int  width;
    public void setWidth(int width) { //成员变量名和局部变量名相同
        this.width = width; // 可以给成员变量width赋值
    }
    public void setWidth_temp(int width) {
        width =width;  //无法给成员变量赋值
    }
    public int getWidth() {
        return width;
    }
}
```

``` java
public class TestRectangle {
    public static void main(String[] args) {
        Rectangle r_temp = new Rectangle();
        r_temp.setWidth_temp(10);
        r_temp.getWidth(); // 0

        Rectangle r = new Rectangle();
        r.setWidth(10);
        r.getWidth(); // 10
    }
}

```

2. 可以作为方法的返回值,常用于链式调用
``` java
public class Rectangle {
    private int  number;
    public  Rectangle add(int number){
        this.number+=number;
        return this;
    }
    public void showAdd(){
        System.out.println("加数的结果为:"+this.number);
    }
}
```

``` java
public class TestRectangle {
    public static void main(String[] args) {
        new Rectangle().add(1).add(2).add(3).showAdd(); //链式调用 6
    }
}

```

3. 可以作为方法的参数使用


4. 可以在一个方法中调用自己类的另一个方法

5. 可以在构造器中调用另外的构造器，但是必须放在第一行

6. static和this不能共存


