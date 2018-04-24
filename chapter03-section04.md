# 面向对象-多态

### 为什么要使用多态
>  为了提高代码的通用性,便于拓展

### 多态定义
>  只有在运行的时候，才能确定一个引用类型的变量到底会指向哪个类的实例对象。

######语法

``` java
    父类类型   对象名 = new 子类名();
    Animal     animal = new Pig();
```

###  多态两种表现方式
1. 编译类型：就是声明对象的类型
2. 运行类型：对象的真实类型
3. 如果编译时类型和运行时类型不一致，会出现所谓的多态

###  多态存在的前提
1. 存在继承关系或者实现关系
2. 存在覆写
3. 父类型的引用指向一个子对象(编译时类型和运行时类型不一致->向上转型)

###  类型的强制转换
> 当使用多态的方式调用子类特有的方法(父类没有),就需要把编译时类型强制转为运行时类型

###  隐藏&覆写
>  继承关系中，父类和子类存在同名的成员方法名或者成员变量名

1. 对于成员变量的隐藏：会调用编译类型所对应类中的成员变量，不会调用子类同名变量
2. 对于静态方法的隐藏：会调用编译类型所对于类中的方法，不会调用子类同名方法
3. 对于非静态方法叫覆写
4. 对于成员变量没有覆写

###  final关键字
> final可以修饰类(非抽象类),方法(非抽象方法),变量,不可以修饰构造方法

1. final修饰类：表示该类不能被继承，太监类 使用场景：不希望该类再次被拓展，有些工具类
2. final修饰方法：表示该方法不能被覆写 使用场景：父类中方法不需要再次被覆写， 通用的算法，通用的代码块能够适应子类需求
3. final修饰变量：该变量只能赋值一次,并且是在初始化的时候赋值， 必须手动初始化，默认值无效(final是唯一一个修饰局部变量的修饰符）

### 类成员初始化顺序

###### 无继承关系

>  静态成员(静态变量|静态代码块|静态方法)>普通成员(普通变量|普通代码块|普通方法)>构造方法

``` java
    public class Init{
        static  InitTest1  init1 =new InitTest1(); //静态变量
        InitTest2  init2 =new InitTest2(); //普通变量
        static {
            System.out.println("静态代码块init");
        }
        {
        System.out.println("普通代码块init");
        }
        public Init(){
            System.out.println("构造方法init");
        }
    }

    public class InitTest1 {
        public InitTest1(){
            System.out.println("静态变量init");
        }
    }

    public class InitTest2 {
        public InitTest2(){
            System.out.println("普通变量init");
        }
    }

    public class Test {
        public static void main(String[] args) {
            Init init1 = new Init();
            System.out.println("=========================");
            Init init2 = new Init();
        }
    }
```
###### 运行结果

``` java
    静态变量init
    静态代码块init
    普通变量init
    普通代码块init
    构造方法init
    =========================
    普通变量init
    普通代码块init
    构造方法init
```

>  静态成员之间按代码声明自然顺序初始化,普通成员之间按代码声明自然顺序初始化

``` java
    public class Init{
        static {
                System.out.println("静态代码块init");
            }
        static  InitTest1  init1 =new InitTest1(); //交换位置
        {
                System.out.println("普通代码块init");
        }
        InitTest2  init2 =new InitTest2(); //交换位置
        public Init(){
            System.out.println("构造方法init");
        }
    }

    public class InitTest1 {
        public InitTest1(){
            System.out.println("静态变量init");
        }
    }

    public class InitTest2 {
        public InitTest2(){
            System.out.println("普通变量init");
        }
    }

    public class Test {
        public static void main(String[] args) {
            Init init1 = new Init();
            System.out.println("=========================");
            Init init2 = new Init();
        }
    }
```
###### 运行结果
``` java
   静态代码块init
   静态变量init
   普通代码块init
   普通变量init
   构造方法init
   =========================
   普通代码块init
   普通变量init
   构造方法init
```

###### 存在继承关系

``` java
    public class InitFater {
        static  InitTest1  init1 =new InitTest1(null); //父静态变量
        InitTest2  init2 =new InitTest2(null); //父普通变量
        {
            System.out.println("父普通代码块init");
        }
        static {
            System.out.println("父静态代码块init");
        }
        public InitFater(){
            System.out.println("父构造方法init");
        }
    }

    public class Init extends  InitFater{
        static {
            System.out.println("静态代码块init");
        }
        static  InitTest1  init1 =new InitTest1(); //静态变量
        {
            System.out.println("普通代码块init");
        }
        InitTest2  init2 =new InitTest2(); //普通变量
        public Init(){
            System.out.println("构造方法init");
        }
    }

    public class InitTest1 {
        public InitTest1(){
            System.out.println("静态变量init");
        }
        public InitTest1(String s){
            System.out.println("父静态变量init");
        }
    }

    public class InitTest2 {
        public InitTest2(){
            System.out.println("普通变量init");
        }
        public InitTest2(String s){
            System.out.println("父类普通变量init");
        }
    }

    public class Test {
        public static void main(String[] args) {
            Init init1 = new Init();
            System.out.println("=========================");
            Init init2 = new Init();
        }
    }
```

###### 运行结果
``` java
    父静态变量init
    父静态代码块init
    静态代码块init
    静态变量init
    父类普通变量init
    父普通代码块init
    父构造方法init
    普通代码块init
    普通变量init
    构造方法init
    =========================
    父类普通变量init
    父普通代码块init
    父构造方法init
    普通代码块init
    普通变量init
    构造方法init
```