# 多线程

### 为什么要使用多线程？

> 华罗庚泡茶

* 算法一：

> 第一步 烧水60S；  第二步  水烧开后，洗刷茶具30S； 第三步 沏茶10S   总时间：100S

* 算法二：

> 第一步 烧水60S：  第二步 烧水过程中，洗刷茶具30S 第三步 水烧开后沏茶10S  总时间：70S

* 多线程本质是：提高了CUP的占用率

###  多线程相关概念

> 并发：同一个**时间段**内多个任务同时进行| 用电脑聊天，先回复小A，再回复小B
>
> 并行：同一**时刻**多个任务同时进行  |左手用一台电脑打字的同时右手也在用另一台电脑打字

> 进程：正在运行中的程序 ，是资源分配的最小单元 ，cup给进行分配独立堆栈空间
>
> 线程：线程是进程中的一部分，是任务执行的最小单元，线程的栈是独立，堆空间共用
>
> 多线程：一个进程中有多个线程

* 对于java来说，至少有两个线程。一个是main方法线程，一个是垃圾回收线程

###  创建线程方式

##### 继承Thread类

> 创建线程方式

  ``` java
public class ThreadA extends  Thread {
    @Override
    public void run() {
        //线程执行的任务
        for(int i=0;i<60;i++){
            try {
                Thread.sleep(1000);
                System.out.println("任务线程A执行第"+i+"秒");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
  ```

> 开启线程方式

``` java
public class Test {
    public static void main(String[] args) throws InterruptedException {
        ThreadA threadA = new ThreadA();
        //threadA.run();// 调用run方法，是当成普通方法，不会开启线程
        threadA.start(); //开启线程方法
    }
}
```

##### 实现Runnable接口

> 创建线程方式

``` java
public class Task implements  Runnable{
    @Override
    public void run() {
        //线程执行的任务
        for(int i=0;i<60;i++){
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Runnable线程执行第"+i+"秒");
        }
    }
}
```

> 把任务交给Thread类执行

``` java
public class Test {
    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(task);
        thread.start();
    }
}
```

##### 使用匿名内部类

``` java
public class Test {
    public static void main(String[] args) throws InterruptedException {
        //方式一：只对runnable接口匿名
        Thread thread1 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 60; i++) {
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("Thread3线程执行中" + i);
                }
            }
        });
        thread1.start();

        //方式二：对thread类和runnable接口均匿名
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 60; i++) {
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("Thread3线程执行中" + i);
                }
            }
        }).start();

        //方式三：对thread类匿名
        new Thread(){
             @Override
             public void run() {
                 System.out.println(1);
             }
        }.start();
    }
}
```



### 多线程导致共享数据安全性问题

> 使用3个线程模拟三个售票窗口卖50张票

``` java
public class TheadS1 extends Thread{
    private static int  tick=50;
    @Override
    public void run() {
        for(;TheadS1.tick>0;){
            try {
                Thread.sleep(100); //模拟网络延迟
                System.out.println(Thread.currentThread().getName()+"当前所售票为第"+(51-TheadS1.tick)+"张");
                TheadS1.tick --;
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

```

``` java
public class Shopping {
    public static void main(String[] args) {
        TheadS1 theadS1 = new TheadS1();
        theadS1.start();
        TheadS1 theadS2 = new TheadS1();
        theadS2.start();
        TheadS1 theadS3 = new TheadS1();
        theadS3.start();
    }
}
```

### 多线程特点

* 线程与线程间相互独立运行
* 线程的执行先后顺序是随机的
* 线程操作共享数据可能会有安全隐患

### 多线程常用方法

* 设置或者获取线程名字
* 获取当前线程
* 线程优先级（1-10级）线程优先级可以继承，主线程优先级是5
* 中断线程，一个线程中断另一个线程
* 守护线程：为前台线程服务的线程，如果所有的前台线程结束，守护线程自动结束  设置为守护线程要在start()方法调用前使用
* 等待线程终止
* 线程休眠


 ### synchronized关键字

>  修饰方法或者代码块

> 一段代码加了同步锁，线程访问该段代码的时候，要获取访问权限

> 对象锁(任何对象都是一把锁，而这把锁只有一把钥匙)，线程访问加了synchronized关键子的代码片段的时候，需要锁的钥匙，如果钥匙被别的线程拿走了，只有等待其他线程释放钥匙。该线程才能去拿取

> 已经获取了锁钥匙的线程，在离开加了synchronized关键子的代码片段的时候，会自动归还对象锁

> 至此就可以保证一个线程同时只能访问该代码片段，同步

###### 例如：上厕所案例

##### synchronized修饰代码块

> 普通锁

```  java
synchronized(同一个对象){
    //todo 同步代码区域
}
```

>  类锁

``` java
synchronized(类.class){
    //todo 同步代码区域
}
```

##### synchronized修饰普通方法

> 语法

``` java
public  void  synchronized doSomeThing(){
    //todo 同步代码区域
}
```

##### synchronized修饰静态方法

> 语法

> 同时只能有一个线程访问该类的静态方法，其他线程必须等待该静态方法访问完毕后，才能访问其他的静态方法(包括字节)，对于普通方法可以有其他线程访问

``` java
public static void  synchronized doSomeThing(){
    //todo 同步代码区域
}
```



### 线程协作

> wait和notify一定是在同步代码区内使用

#####  线程等待(wait)

> 当前线程调用锁的wait方法，就让出cpu的使用权，然后一直阻塞，直到其他线程唤醒它，它才会继续接着原来的位置执行





##### 线程唤醒(notify|notifyAll)

> notify：当前线程唤醒持有同一把锁的其他线程中的一个

> notifyAll:当前线程唤醒持有同一把锁的其他线程所有线程



###  生产者消费者模式



### 线程的生命周期

> 创建>就绪>运行>阻塞>死亡



### Lock













