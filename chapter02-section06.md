# java语法基础-流程控制

### 顺序结构
>  代码始终是从main方法开始执行，而且是从上到下一行一行的执行,不会发生跳跃或者遗漏

``` java
    System.out.println(1);
    System.out.println(2);
    System.out.println(3);  //结果永远按照1 2 3输出  不会变成3 1 2 |1 3 2
```
### 分支结构
1. 程序执行中遇到分支结构，会选择部分分支执行
2. 使用场景：当业务可能出现的条件是一个范围的时候

###### if结构语法
``` java
   if(boolean表达式){
     //当布尔表达式为true 执行该分支
   }
```
>  案例：输入一个整数，如果该整数大于10，则该数加一再输出

``` java
    import java.util.Scanner;
    public class Lero{
         Scanner s = new Scanner(System.in);
         System.out.println("请输入一个整数");
         int x = s.nextInt();
         if(x>10){
              x++;
         }
         System.out.println("结果为："+x); //输入的整数大于10则x++,否则x为本身
    }
```
###### if-else结构
``` java
   if(boolean表达式){
     //当布尔表达式为true 执行该分支
   }else{
     //当布尔表达式为false 执行该分支
   }
```
>   案例：输入一个整数，判断是否能被2整除

``` java
    import java.util.Scanner;
    public class Lero{
         Scanner s = new Scanner(System.in);
         System.out.println("请输入一个整数");
         int x = s.nextInt();
         if(i%2==0){
              System.out.println("该数能被2整除");
         }else{
              System.out.println("该数不能被2整除");
         }
    }
```

###### if-elseif-elseif-else结构
``` java
   if(boolean表达式1){
     //当布尔表达式1为true 执行该分支
   }else if(boolean表达式2){
     //当布尔表达式2为true 执行该分支
   }else if(boolean表达式3){
     //当布尔表达式3为true 执行该分支
   }else if(boolean表达式N){
     //当布尔表达式N为true 执行该分支
   }else{
    //当布尔表达式1,表达2,表达式3...表达式N都为false 执行该分支
   }
```

###### IF练习题
1. 从键盘分别输入3个整数分别依次代表小时(0-23)分钟(0-59)秒(0-59),然后输入下一秒时间15:09:09
2. 从键盘分别输入3个整数，求出最大值并输入
3. 写个彩票游戏：分别随机生成2个一位数，提示用户猜测如果完全匹配奖励1000，只匹配数字没顺序奖励300，只匹配1个数字奖50，没匹配则没中奖

###### switch结构
1. switch条件表达式结果只能是byte,char,short,int,String,枚举
2. case分支后只能是常量或者常量表达式
3. break用于结束switch分支
4. default用于匹配case不匹配的条件，一般放在最后
5. 使用场景：当业务可能出现的条件个数是有穷可罗列的时候

``` java
   标准结构
   switch(表达式){
      case 常量1: //一条或多条语句 ;break
      case 常量2: //一条或多条语句 ;break
      ...
      case 常量N: //一条或多条语句 ;break
      default: //一条或多条语句
   }
```
> 案例：根据输入的月份，判断是什么季节

``` java
    import java.util.Scanner;
    public class Demo_switch {
        public static void main(String[] args) {
            System.out.println("请输入一个1到12的整数代表月份");
            Scanner next = new Scanner(System.in);
            int month =next.nextInt();
            switch (month){
                case 1: System.out.println("这是春季");break;
                case 2: System.out.println("这是春季");break;
                case 3: System.out.println("这是春季");break;
                case 4: System.out.println("这是夏季");break;
                case 5: System.out.println("这是夏季");break;
                case 6: System.out.println("这是夏季");break;
                case 7: System.out.println("这是秋季");break;
                case 8: System.out.println("这是秋季");break;
                case 9: System.out.println("这是秋季");break;
                case 10:System.out.println("这是冬季");break;
                case 11:System.out.println("这是冬季");break;
                case 12:System.out.println("这是冬季");break;
                default:
                    System.out.println("你输入的不是约定的数字");
            }
            System.out.println("switch执行完毕");
        }
    }

```
6. 若case语句没有使用break,会发生case穿透,有时候可以合理利用case穿透特性

``` java
    import java.util.Scanner;
    public class Demo_switch {
        public static void main(String[] args) {
            System.out.println("请输入一个1到12的整数代表月份");
            Scanner next = new Scanner(System.in);
            int month =next.nextInt();
            switch (month){
                case 1:
                case 2:
                case 3: System.out.println("这是春季");break;
                case 4:
                case 5:
                case 6: System.out.println("这是夏季");break;
                case 7:
                case 8:
                case 9: System.out.println("这是秋季");break;
                case 10:
                case 11:
                case 12:System.out.println("这是冬季");break;
                default:
                    System.out.println("你输入的不是约定的数字");
            }
            System.out.println("switch执行完毕");
        }
    }
```
###### switch练习题
> 1. 分别输入年月日三个整数，求当年过了多少天

``` java
    import java.util.Scanner;
    public class Demo_switch_practice {
        public static void main(String[] args) {
            Scanner s = new Scanner(System.in);
            System.out.println("请输入年份：");
            int year = s.nextInt();
            System.out.println("请输入月份：");
            int month = s.nextInt();
            System.out.println("请输入日期：");
            int day = s.nextInt();
            int total =0; //存储过了多少天
            switch (month){
                case 12:
                    total+=30;
                case 11:
                    total+=31;
                case 10:
                    total+=30;
                case 9:
                    total+=31;
                case 8:
                    total+=31;
                case 7:
                    total+=30;
                case 6:
                    total+=31;
                case 5:
                    total+=30;
                case 4:
                    total+=31;
                case 3:
                    if((year%4==0&&year%100!=0)||year%400==0){
                          total+=29;
                    }else{
                          total+=28;
                    }
                case 2:
                     total+=31;
                case 1: total+=day;
            }
            System.out.println(year+"年已经过去了"+total+"天");
        }
    }
```

> 2. 输入星期的首字母，判断是星期几，如果首字母不能判断，则根据第二个字母判断

``` java
    import java.util.Scanner;
    public class Demo_switch_practice1 {
        public static void main(String[] args) {
            Scanner input = new Scanner(System.in);
            System.out.println("请输入第一个字母");
            String first = input.next();
            switch (first){
                case "M":
                    System.out.println("星期一");break;
                case "T":
                    System.out.println("请输入第二个字母");
                    String second = input.next();
                    if(second.equals("U")){
                        System.out.println("星期二");
                    }else{
                        System.out.println("星期四");
                    }
                    break;
                case "W":
                    System.out.println("星期三");break;
                case "F"  :
                    System.out.println("星期三");break;
                case "S":
                    System.out.println("请输入第二个字母");
                    String second1 = input.next();
                    if(second1.equals("A")){
                        System.out.println("星期六");
                    }else{
                        System.out.println("星期天");
                    }
                    break;
            }
        }
    }
```
### 循环结构
>  一段程序重复执行很多次

###### while循环
* 循环一定要有一个出口终止循环
* 使用场景：不能够清除的知道一段程序到底要执行多少次

1.基本语法
``` java
   while(boolean表达式){
      //
   }
```
``` java
     int day =1;
     while (day<7){
        System.out.println("今天是星期"+i);
        day++;
    }
```

2.使用break可以跳出while循环
``` java
   while(boolean表达式){
       if(boolean表达式条件){
         break;
       }
   }
```
``` java
     int day =1;
     while (true){
        if(day>7){
            break; // 跳出最近的循环
        }
        System.out.println("今天是星期"+i);
        i++;
    }
```
3. while练习
*  每次输入一个整数，当输入到-1就结束循环(-1不参与其中)，求出最大值
*  输入正数和负数，求正数输入了多少个，负数输入了多少个，并求输入所有数的和  输入-1结束
*  输入一个正整数，颠倒输出该数
``` java
    import java.util.Scanner;
    public class Demo_for_other {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("请输入一个正整数");
            int i = scanner.nextInt();
            String result="";
            while (i>0){
                result=result+(i%10);
                i/=10;
            }
            System.out.println("颠倒过来的结果是："+result);
        }
    }
```

###### do...while循环
*  dowhile循环比while循环多执行一次循环体

``` java
    do{
       //循环体
    }while(boolean表达式);
```

###### for循环
* 使用场景：知道要循环的次数
* 可以和while循环相互转换

``` java
    for(①初始化条件;②boolean表达式;③表达式){
        //④循环体
    }
    执行顺序：①->②(true)->④->③->②(true)->④->③->②(false)结束循环体
```
1. 基本使用
>  求1+2+3+...+100的和

``` java
    int sum =0;
    for(int i=1;i<=100;i++){
        sum +=i;
    }
    System.out.println("和为:"+sum); //5050
```
2. 嵌套循环
>  输出九九乘法表

``` java
    for(int i=1;i<10;i++){
        for(int j=1;j<=i;j++){
            int temp =i*j;
            System.out.print(j+"*"+i+"="+temp+"\t");
        }
        System.out.println();
    }
```
3. for循环中continue用于结束本次循环，会进入下一次循环
>  求100以内偶数的和，但是要排除50

4. for循环中break用于终止当前层循环
>  找出给定两个整数之间的前10个偶数

5. 嵌套循环中控制其它层循环
>  找到给定整数区间内的第一个质数就停止查找

6. 增强for循环用于遍历数组和集合

7. for循环练习
* 求任意两个区间内的质数
``` java
    import java.util.Scanner;
    public class Demo_for_other {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("请输入第一个正整数");
            int i = scanner.nextInt();
            System.out.println("请输入第二个正整数");
            int j = scanner.nextInt();
            if(i>j){
                i=i^j;
                j=i^j;
                i=i^j;
            }
            for (int k=i;k<=j;k++){
                boolean flag =true;
                for (int m =2;m<=k/2;m++){
                    if(k%m==0){
                        flag =false;
                        continue;
                    }
                }
                if(flag){
                    System.out.println("质数有"+k);
                }
            }
        }
    }
```

* 把一个正整数逆序输出
``` java
    import java.util.Scanner;
    public class Demo_for_other {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.println("请输入一个正整数");
            String result="";
            for(int i = scanner.nextInt();i>0;i/=10){
                result=result+(i%10);
            }
            System.out.println("颠倒过来的结果是："+result);
        }
    }
```
