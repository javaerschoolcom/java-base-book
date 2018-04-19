# java语法基础-数组

### 为什么需要数组
1. 当同种类型变量需要定义很多个的时候，非常麻烦

### 数组和变量区别
1. 变量是内存的一块存储区域
2. 数组是内存的一块连续的存储区域
3. 数组只能存储同一类型的数据

### 数组的定义
1. 动态定义数组：划分存储区域并分配默认值(整数默认为0|小数默认0.0|char默认值'\u0000'|对象默认为null|boolean默认fasle)
``` java
数据类型[]  数组名 = new 数据类型[5]; //推荐
数据类型  数组名[] = new 数据类型[5]; //不推荐使用
```
2. 静态定义数组：划分存储区域的同时分配数据
``` java
数据类型[]  数组名 = new 数据类型[]{元素1,元素2...元素N}; //完整写法
数据类型[]  数组名 = {1,2,3}; //简写
```
3. 不能同时使用静态和动态
``` java
数据类型[]  数组名 = new 数据类型[N]{元素1,元素2,元素3...元素N}; // **错误写法**
int[] init=new int[5]{1,2,3,4,5}  //错误
```
4.静态定义数组不能分开写
``` java
int[] arr;
arr = {1,2,3};//错误写法 编译不同过
```
5.定义了一个数组但是还没开辟空间
``` java
int[] arr =null; //正确
```

### 数组的操作

1. 数组使用
``` java
数据类型 变量名 = 数组名[索引];
```
2. 数组赋值
``` java
数组名[索引]=数值;
```
3. 数组的长度
``` java
**  定义一个数组长度就固定了，而且不能修改数组长度
**  数组提供了一个快速获取数组长度的属性length
**  获取方法：数组名.length
```
4. 数组的索引
``` java
**  索引是为了快速找到数组中的元素，索引是从0开始的，索引的大小始终是数组的长度-1
**  如果索引越界，就会报错
```

5. 数组的遍历
> for循环遍历数组或者给数组赋值

``` java
String[] arr ={"A","B","C","D","E"};
for(int i=0;i<arr.length;i++){
   System.out.println(arr[i]);
}
```
>  增强for循环只是用来遍历数组

``` java
String[] arr ={"A","B","C","D","E"};
for(int item:arr){
   System.out.println(item);
}
```
6. 数组排序

>  冒泡排序(数组相邻两个元素进行比较，大的在后，小的在前)

``` java
 /**
 * 初始序列：{23 45 12 76 28 2 9}
 　　第1趟：{23 12 45 28 2 9} 76
 　　第2趟：{12 23 28 2 9}45 76
 　　第3趟：{12 23 2 9}28 45 76
 　　第4趟：{12 2 9}23 28 45 76
 　　第5趟：{2 9}12 23 28 45 76
 　　第6趟： 2 9 12 23 28 45 76 完成
  */
 public static  void  sort(int[] arr){
        int temp = 0; //临时变量定义在此处，保证该方法只开辟一次
        for(int i=0;i<arr.length-1;i++){
            for(int j=0;j<arr.length-1-i;j++){
                if(arr[j]>arr[j+1]){
                     temp=arr[j];
                    arr[j]=arr[j+1];
                    arr[j+1]=temp;
                }
            }
        }
    }
```

>  比较排序(数组第N个元素和其他元素分别进行比较，找出最小的元素)

``` java
/**
* 初始序列：{49 27 65 97 76 12 38}
　　第1趟：12与49交换：12{27 65 97 76 49 38}
　　第2趟：27不动　：12 27{65 97 76 49 38}
　　第3趟：65与38交换：12 27 38{97 76 49 65}
　　第4趟：97与49交换：12 27 38 49{76 97 65}
　　第5趟：76与65交换：12 27 38 49 65{97 76}
　　第6趟：97与76交换：12 27 38 49 65 76 97 完成
 */
public static  void  sort(int[] arr){
     int temp =0;//临时变量用于交换元素
     for(int i=0;i<arr.length-1;i++){
         int index = i; //存放最小元素的索引
         for(int j=i+1;j<arr.length;j++){
             if(arr[index]>arr[j]){
                 index=j;
             }
         }
         System.out.println(index);
         temp =arr[i];
         arr[i]=arr[index];
         arr[index]=temp;
     }
 }
```

### 一维数组练习题
``` java
import java.util.Arrays;
/**
 * 模拟双色球开奖
 */
public class Demo_array_2 {
    public static void main(String[] args) {
        String[]  bools =bornBool(33);// 生成01-33个双色球
        boolean[] boolsFlags = bornFlag(33); //01-33个双色球对应的标志位
        String[]  result = new String[7]; //存放开奖结果的数组
        int resultIndex=0;//代表开奖数组的索引
         while (true){  //开奖
             int index = getIndex(33); //每次双色球对应的索引
             if(boolsFlags[index]){ //若该索引位置的双色球被取过，则重新摇球
                 continue;
             }
             result[resultIndex++]=bools[index];
             boolsFlags[index] =true;//给取过位置的双色球做标记
             if(resultIndex>5){
                 break;
             }
         }
        result[result.length-1]=(getIndex(16)+1)+"";//生成蓝色求
        System.out.println(Arrays.toString(result));
    }
    /**
     * 生成双色球
     * @param length  红球的个数
     * @return
     */
    public  static  String[]  bornBool(int length){
        String[]  bool = new String[length];
        for(int i=0;i<bool.length;i++){
            if(i<9){
                bool[i]="0"+(i+1)+"";
            }else{
                bool[i]=(i+1)+"";
            }
        }
       // System.out.println(Arrays.toString(bool));
        return   bool;
    }
    /**
     *  生成双色求对应的标志位
     * @param length  标志位的个数
     * @return
     */
    public  static  boolean[]  bornFlag(int length){
        boolean[]  bool = new boolean[length]; //每个元素默认为false
        return   bool;
    }
    /**
     *  生成双色球索引
     * @param length  索引的个数
     * @return
     */
    public  static  int  getIndex(int length){
        return  (int)(Math.random()*length);
    }
}
```

### 数组可以作为可变参数使用

1. 可变参数本质上是一个数组，就可以当成数组使用

2. 在一个方法中，可变参数只能有一个并且只能作为最后一个参数
```java
public static  int  sum(String x,int...args){
        int sum =0;
        for(int i=0;i<args.length;i++){
            sum+=args[i];
        }
        return sum;
}
```
### 值传递

### 二维数组
1. 有多个一维数组组成的数组就叫做二维数组
``` java
数据类型[][]  数组名 = new 数据类型[5][6]; //推荐
数据类型  数组名[][] = new 数据类型[5][6]; //不推荐使用
数据类型[]  数组名[] = new 数据类型[5][6]; //不推荐使用
```
2. 静态定义数组：划分存储区域的同时分配数据
```
```
4. 二维数组使用
``` java
数据类型 变量名 = 数组名[1][2];
```
5. 数组赋值
``` java
数组名[0][1]=数值;
```

### 二维数组综合练习

``` java
    import  java.util.Scanner;
    /**
     *龙门客栈前台客房系统
     */
    public class Demo_array_4 {
    public static void main(String[] args){
        String [][] rooms = new String[10][10];//初始化一个10层楼每层有10个房间的客栈
        System.out.println("欢迎来到龙门客栈");
        System.out.println("请输入要操作的命令:");
        System.out.println("[init]:开业大吉");
        System.out.println("[search]:查询客房状态");
        System.out.println("[in]:办理入住");
        System.out.println("[out]:办理退房");
        System.out.println("[exit]:退出系统");
        Scanner s = new Scanner(System.in);
        while(true)
        {
            String command = s.next() ;
            switch (command) {
                case "init":
                    init(rooms);
                    break;
                case "search":
                    search(rooms);
                    break;
                case "in":
                    in(rooms);
                    break;
                case "out":
                    out(rooms);
                    break;
                case "exit":
                    System.out.println("欢迎再次光临龙门客栈!");
                    return; //结束方法
                default:
                    System.out.println("不是正确的指令，请重新输入");
                    System.out.println("init初始化，search查询，in入住，out退房，exit退出系统");
            }
        }
    }

    /**
     * 退房 (输入房间号，直接退房---->需要判断房间是否存在，是否有入住)
     * @param rooms  客栈
     */
    public static void out(String[][]rooms){
        System.out.println("请输入客房号:");
        Scanner s = new Scanner(System.in);
        int roomNo = s.nextInt();
        //需要把房间号转换层楼层和房间--->使其和数组的下标去对应
        int floor = roomNo / 100 ; //--->根据房间号得到楼层
        //房间号
        int no = roomNo % 100 ; //得到楼层的房间号
        if(floor < 1 || floor > 12 || no < 1 || no > 10){ //超出客房编号范围
            System.out.println("输入的客房号有误,请输入out命令继续操作:");
            return ;
        }
        if("WAIT".equals(rooms[floor-1][no-1])){
            System.out.println("该客房没人入住，不需要退房,请输入out命令继续操作:");
            return ;
        }
        rooms[floor-1][no-1] = "WAIT";
        System.out.println("该客房退房成功");
    }

    /**
     * 查询客房状态
     * @param rooms  客栈
     */
    public static void search(String[][] rooms)
    {
        for(int i = 0 ; i < rooms.length ; i++)
        {    //打印客房号
            for(int j = 0 ; j < rooms[i].length ; j++)
            {
                if(i < 9 ){
                    System.out.print("0");
                }
                int roomNo = (i+1)*100 + j+1 ;
                System.out.print(roomNo + "\t");
            }
            System.out.println();
            //打印客房的状态
            for(int k = 0 ; k < rooms[i].length ; k++)
            {
                System.out.print(rooms[i][k] + "\t");
            }
            System.out.println();
        }
    }

    /**
     *  入住客栈
     * @param rooms
     */
    public static void in(String[][] rooms)
    {
        System.out.println("图示的客房代号为:WAIT的为可入住的客房");
        //打印现有的客房信息
        search(rooms);
        System.out.println();
        System.out.println("请输入客房号:");
        Scanner s = new Scanner(System.in);
        int roomNo = s.nextInt();
        //需要把房间号转换层楼层和房间--->使其和数组的下标去对应
        int floor = roomNo / 100 ; //--->根据房间号得到楼层
        //房间号
        int no = roomNo % 100 ; //得到楼层的房间号
        if(floor < 1 || floor > 12 || no < 1 || no > 10){ //入住函数结束
            System.out.println("输入的客房号有误,请输入in命令继续操作:");
            return ;
        }
        //判断房间是否有人入住
        if("WAIT".equals(rooms[floor-1][no-1])){
            System.out.println("请输入客官您的姓名:");
            String name = s.next();
            rooms[floor-1][no-1] = name ; //对数组进行赋值操作
            System.out.println("恭喜您，入住成功!");
        }else
        {
            System.out.println(roomNo+"已经有人入住,请输入in命令继续操作:");
            return ;
        }
    }

    /**
     * 初始化所有客房
     * @param rooms 客栈
     */
    public static void init(String[][] rooms)
    {
        for(int i = 0 ; i < rooms.length ; i++)
        {
            for(int j = 0 ; j < rooms[i].length ; j++)
            {
                rooms[i][j] = "WAIT";
            }
        }
        System.out.println("客房初始化完毕");
    }
    }

```





