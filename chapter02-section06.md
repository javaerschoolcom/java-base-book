# java语法基础-流程控制

### 顺序结构
>  代码始终是从main方法开始执行，而且是从上到下一行一行的执行,不会发生跳跃或者遗漏

``` java
    System.out.println(1);
    System.out.println(2);
    System.out.println(3);  //结果永远按照1 2 3输出  不会变成3 1 2 |1 3 2
```
### 分支结构
>  程序执行中遇到分支结构，会选择部分分支执行

1. if结构语法
```
   if(boolean表达式){
     //当布尔表达式为true 执行该分支
   }
```
``` java
    import java.util.Scanner;
    public class Lero{
         Scanner s = new Scanner(System.in);
         System.out.println("请输入一个整数");
         int x = s.nextInt();
         int result =0;
         if(i>10){
              result++;
         }
         System.out.println("结果为："+result); //输入数大于10，则result=1;
    }
```

> 练习题

> 1.从键盘分别输入3个整数分别依次代表小时(0-23)分钟(0-59)秒(0-59),然后输入下一秒时间15:09:09

> 2.从键盘分别输入3个整数，求出最大值并输入

> 3.写个彩票游戏：分别随机生成2个一位数，提示用户猜测如果完全匹配奖励1000，只匹配数字没顺序奖励300，只匹配1个数字奖50，没匹配则没中奖









