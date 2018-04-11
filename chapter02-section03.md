# java语法基础-表达式

### 表达式定义
> ----由常量，变量，运算符，小括号排列组合，并且最终求得唯一有意义的结果

``` java
    class Second{
       public static void main(String[] args){
         int x=10;
         int y=20;
         System.out.println(+x);  //是表达式
         System.out.println(x*(y+20)); //是表达式
         System.out.println(true&&(y+20>10)); //是表达式
       }
    }
```