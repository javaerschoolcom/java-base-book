# 面向对象-内部类

### 内部类定义
>  定义在类中的类

### 为什么要使用内部类
1. 可以封装一个类中细节和功能，在结构上更加清晰合理
2. 可以弥补单继承的缺陷

#### 内部类分类
1. 普通内部类
2. 静态内部类
3. 局部内部类
4. 匿名内部类

### 普通内部类

###### 语法
``` java
    定义：
    [修饰符] class  外部类名{
        [修饰符] class 内部类名1{}
        [修饰符] class 内部类名2{}
    }
    使用:
    外部类名.内部类名  变量名 = new 外部类名().new 内部类名();
```
> 案例

``` java
     public class Father {
         public  class  Child{
             public  void showInfo(){
                 System.out.println("内部类");
             };
         }
     }

      public class Test {
             public static void main(String[] args) {
                 Father father = new Father();
                 Father.Child child = father.new Child();
                 child.showInfo();  //结果:内部类
             }
      }

```
1. 普通内部类不能有静态成员
2. 普通内部类可以直接访问外部类的成员，如果出现同名的时候采用以下方式
``` java
    public class Father {
        private  int  age=30;
        public  class  Child{
            private int age=5;
            public  void showInfo(int age){
                System.out.println("内部使用自己局部成员："+age);
                System.out.println("内部使用自己类的成员："+this.age);
                System.out.println("内部使用外部类的成员:"+Father.this.age);
            };
        }
    }

    public class Test {
        public static void main(String[] args) {
            Father father = new Father();
            Father.Child child = father.new Child();
            child.showInfo(1);
        }
    }
```
###### 运行结果
``` java
    内部使用自己局部成员：1
    内部使用自己类的成员：5
    内部使用外部类的成员:30
```
3. 外部类对于内部类的所有成员也都有访问权，包括内部类的私有成员和方法
>  弥补不能多继承的缺陷,封装细节(只有内部类可以用private修饰)
``` java
    public class Son {
        private class Fater{
            void isHeight(){
                System.out.println("长的高");
            }
        }
        private class Mother{
            void isBeautiful(){
                System.out.println("长的美");
            }
        }
        public  void  beautifulAndHeight(){
            Fater fater = new Fater();
            fater.isHeight();
            Mother mother =new Mother();
            mother.isBeautiful();
        }
    }

    public class Test {
        public static void main(String[] args) {
            Son son = new Son();
            son.beautifulAndHeight();
        }
    }
```
###### 运行结果
``` java
    长的高
    长的美
```

###  静态内部类
>  使用static修饰的类

``` java
    定义：
    [修饰符] class  外部类名{
        [修饰符] static class 内部类名1{}
        [修饰符] static class 内部类名2{}
    }
    使用:
    外部类名.内部类名  变量名 = new 外部类名.内部类名();
```
1. 静态内部类中可以存在静态的成员
2. 静态内部类中只能访问外部内中的静态成员

###  局部内部类
> 定义在成员方法中的类

``` java
    定义：
    [修饰符] class  外部类名{
         [修饰符]  返回类型   方法名(){
              class 内部类名1{};
         }
    }
    使用:
    局部内部类只是在所定义的方法中被使用
```
``` java
    public interface IEvent  {
          void execute();
    }

    public class EventListener {
          public  IEvent  listener(){
               final int count =1;
               class ClickEvent  implements  IEvent{
                  @Override
                  public void execute() {
                      System.out.println("点击事件处理....."+count);
                  }
              }
              return  new ClickEvent();
          }
    }

    public class Test {
        public static void main(String[] args) {
            EventListener listener = new EventListener();
            IEvent clickEvent = eventListener.listener();
            clickEvent.execute();
        }
    }

```
1. 局部内部类访问的局部变量要加final修饰
2. 局部内部类不能使用public private protected static修饰
3. 局部内部类只能在所定义的方法中使用
4. 局部内部类可以访问外部类的成员
5. 局部内部类返回值类型不能是局部内部类名，只能是接口和父类()
``` java
    //编译不通过
    public class EventListenr {
          public  ClickEvent  listener(){ //编译检查到返回类型的时候,该类还未定义
              class ClickEvent {  //类定义
                  public void execute() {
                      System.out.println("点击事件处理.....");
                  }
              }
              return  new ClickEvent();
          }
    }
```

###  匿名内部类
``` java
    定义：
    [修饰符] class  外部类名{
         [修饰符]  返回类型   方法名(){
              new 内部类名(){
               //覆写接口或者抽象类方法
              };
         }
    }
```


























