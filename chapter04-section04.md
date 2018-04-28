# 核心类-异常类

### 异常
>  不正常的状态,导致程序无法继续往下执行

### 异常分类
>   Throwable类是异常的父类，Error和Exception是异常的直接子类

1. Error:指的是不能处理的错误如系统崩溃,内存溢出,堆栈溢出等。以后看到异常以Error结束，就代表是不能被处理的错误
2. Exception:指的是程序发生了异常,可以通过程序处理,处理过后能够让系统继续工作

######  编译时异常
> 指的是编译成class字节码前必须要处理的异常
>
> 常见的编译时异常`StackOverflowError`,`InterruptedException`

######  运行时异常
> 指的是编译能通过,但是运行代码的时候,可能会出现的异常
>
> RuntimeException以及它的子类都是运行时异常

###  异常处理
> 异常处理过后，代码能够继续往下执行

###### 语法1
``` java
    try{
       //可能会发生异常的代码
    }catch(异常类型1  异常名){
       //异常发生处理逻辑
    }catch(异常类型2  异常名){
       //异常发生处理逻辑
    }catch(异常类型N  异常名){
       //异常发生处理逻辑
    }
    //建议:异常类型1<异常类型2<异常类型N
    //todo 处理异常后代码能够继续往下执行
```
1. 一旦异常发生,try代码块后续代码将不被执行，异常代码被对应的catch块捕捉,处理完成后，代码能继续往下执行

``` java
    try{
        String  s =null;
        s.charAt(1);
        System.out.println("----------------------");
        System.out.println(1/0);
        String[]  arr = new String[]{"1","2"};
        System.out.println(arr[3]);
    }catch (ArithmeticException e){
        System.out.println("除数为0异常被处理了");
    }catch (ArrayIndexOutOfBoundsException e){
        System.out.println("数组越界异常被处理");
    }catch(Exception e ){
        System.out.println("其他异常处理");
    }
    System.out.println("我能被执行吗？");
```
> 运行结果

``` java
    其他异常处理
    我能被执行吗？
```

######  catch块中参数的使用

``` java
    public  static  void  showInfo(){
        try{
            System.out.println(1/0);
        }catch (Exception e){
            System.out.println(e.getMessage()); // /by zero
            e.printStackTrace(); //打印出错堆栈信息
        }
    }
```

###  finally关键字

###### 语法2

``` java
    try{
       //可能会发生异常的代码
    }catch(异常类型1  异常名){
       //异常发生处理逻辑
    }catch(异常类型2  异常名){
       //异常发生处理逻辑
    }catch(异常类型N  异常名){
       //异常发生处理逻辑
    }finally{
       //无论是否发生异常都会执行的代码块
    }
    //建议:异常类型1<异常类型2<异常类型N
    //有finally的时候，可以没有catch块
    //todo 处理异常后代码能够继续往下执行
```
1. finally不会执行的特例:断电,系统发了错误,强制JVM停止

```  java
    try{
        System.out.println(1/0); // 断电
        String  s =null;
        s.charAt(1);
        System.out.println("----------------------");
        String[]  arr = new String[]{"1","2"};
        System.out.println(arr[3]);
    }catch (Exception e){
        System.exit(0);//强制jvm结束
    }
    finally{
        System.out.println("我总是被执行");//扫尾工作
    }
    System.out.println("我能被执行吗？");
```

2. 如果在catch和finally同时存在return语句,会返回finally中的return表达式结果

``` java
    public  static  int  showInfo(){
        try{
            System.out.println(1/0);
        }catch (Exception e){
            return 1;
        }
        finally{
            System.out.println("我总是被执行");
            return -1;
        }
    }
```
> 运行结果

``` java
   我总是被执行
   -1
```

3. 已经在catch块中return的表达式结果,finally再次修改无效

``` java
    public  static  int  showInfo(){
        int i =1;
        try{
            System.out.println(1/0);
        }catch (Exception e){
            return i;
        }
        finally{
            System.out.println("我总是被执行");
             ++i;
        }
        return  0;
    }
```
> 运行结果

``` java
    我总是被执行
    1
```

### Throws和throw抛出异常

### 自定义异常类














