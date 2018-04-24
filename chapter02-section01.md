# java语法基础-常量

### 常量定义
>  ------在程序执行中永远不会发生改变的量
>  常量都是大写，每个单词用下划线隔开

### 常量分类

1. 字面量：整数|小数|布尔值
``` java
    System.out.println(1);//整数
    System.out.println(2.4);//小数
    System.out.println(true);//布尔真
    System.out.println(false);//布尔假
```

2. final修饰的变量
``` java
    public static  final  String SAVA_STATUS_SUCCESS="成功";
    public static  final  String SAVA_STATUS_ERROR="保存失败";
    修饰基本数据类型:代表值不变
    修饰引用数据类型:指向的地址是不能变的，但是地址中存的值是可以变的
```