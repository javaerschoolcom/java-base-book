# 核心类-String类

###  String类
>  用双引号把依次排列的字符包裹起来，称之为字符串。String类底层的本质是通过对char[]扩容实现

###### String常见面试

``` java
    String  a ="AB"; //字面量字符串存在常量池中
    String  b ="A"+"B"; //字面量字符串存在常量池中
    String  c =new String("AB"); //new关键字生成的对象存在堆中
    String  d =b+""; //对于变量,编译只检查语法是否有错,不会转为对应的字面量

    System.out.println(a==b);//true
    System.out.println(a==c);//false
    System.out.println(a==d);//false
    System.out.println(c==d); //false
```
###### String类常用构造方法
1. String(byte[] bytes)  //解码指定的byte数组，构造一个新的 String
2. String(char[] value)  //分配一个新的 String，使其表示字符数组参数中当前包含的字符序列
3. String(String original)//新创建的字符串是该参数字符串的副本

``` java
    System.out.println(new String(new byte[]{65,66,67})); //ABC
    System.out.println(new String(new byte[]{'a','b','c'})); //abc
    System.out.println(new String(new char[]{'A','B','C'})); //ABC
    System.out.println(new String("ABC")); //ABC
    System.out.println("ABC"); //ABC
```
###### String常用方法

###### 返回int方法
>  int  length() //返回字符串由char字符构成的长度

``` java
     System.out.println("lero".length()); //4
```
>  int indexOf(int ch) //返回指定字符在此字符串中第一次出现处的索引(**有多个重载方法**)

``` java
     System.out.println("lerolero".indexOf('e')); // 参数为char：l
     System.out.println("lerolero".indexOf("ro")); //参数为String:2
```
>  int lastIndexOf(int ch) //返回指定字符在此字符串中最后一次出现处的索引(**有多个重载方法**)

``` java
     System.out.println("lerolero".lastIndexOf('e')); // 参数为char：5
     System.out.println("lerolero".lastIndexOf("ro")); //参数为String:6
```
###### 返回boolean方法
>  boolean contains(CharSequence s)//当且仅当此字符串包含指定的char值序列时,返回true

``` java
     System.out.println("lero".contains("e")); // 参数为String：true
```
>  boolean equals(Object anObject) //比较两个字符串值(非地址)是否相等，相等返回true

``` java
     System.out.println("lero".equals(new String("lero"))); // true
```
>  boolean equalsIgnoreCase(String anotherString)  //忽略大小写比较两个字符串值(非地址)是否相等，相等返回true

``` java
     System.out.println("lero".equals(new String("LERO"))); // true
```
>  boolean isEmpty() //当且仅当length()为 0 时返回 true

``` java
     System.out.println("lero".isEmpty()); // false
     System.out.println("lero".isEmpty()); // true
```
>  boolean startsWith(String prefix) //测试此字符串是否以指定的前缀开始

``` java
     System.out.println("lero".startsWith("le")); // true
```
>  boolean endsWith(String prefix) //测试此字符串是否以指定的后缀结束

``` java
     System.out.println("lero".endsWith("o")); // true
```
###### 返回一个新的字符串方法
>  String concat(String str)//将指定字符串连接到此字符串的结尾

``` java
    String  name ="lero";
    String  result =name.concat(name);
    System.out.println(result); // lerolero
    System.out.println(name==result); // false
    System.out.println(name.equals(result)); // false
```
> String replace(char oldChar, char newChar) //返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的(**有多个重载方法**)

``` java
    String  name ="lero";
    String  result =name.replace('l','L');
    System.out.println(result); // Lero
    System.out.println(name==result); // false
    System.out.println(name.equals(result)); // false

    //重载方法：replace(CharSequence target, CharSequence replacement)
    System.out.println("lero".replace("er","ER"));参数为String的重载方法 // lERo
```
> String substring(int beginIndex) //返回一个新的字符串，它是此字符串的一个子字符串(**有多个重载方法**)

``` java
    String  name ="lero";
    String  result =name.substring(2);
    System.out.println(result); // ro
    System.out.println(name==result); // false
    System.out.println(name.equals(result)); // false

    //重载方法：String substring(int beginIndex, int endIndex)
    System.out.println("lero".substring(1,3));// er
```
> String trim() //返回字符串的副本，忽略前导空白和尾部空白

``` java
    String  name ="    lero  ";
    String  result =name.trim();
    System.out.println(result); // lero
    System.out.println(name==result); // false
    System.out.println(name.equals(result)); // false
```
> String substring(int beginIndex) //返回一个新的字符串，它是此字符串的一个子字符串

``` java
    System.out.println("lero.java".substring(5)); // java
    System.out.println("lero.java".substring(0,4)); // lero
```
> String[] split(String regex) //根据给定正则表达式的匹配拆分此字符串

``` java
     String temp = "username=lero&qq=125836941";
     System.out.println(Arrays.toString(temp.split("&"))); // [username=lero, qq=125836941]

     String demo ="lero.username";
     System.out.println(Arrays.toString(demo.split("\\."))); // 点号是特殊的字符，使用正则匹配
```
> String toLowerCase() //将此 String 中的所有字符都转换为小写

``` java
     System.out.println("LERO".toLowerCase()); // lero
```

> String toUpperCase() //将此 String 中的所有字符都转换为大写

``` java
     System.out.println("lero".toUpperCase()); // LERO
```
> static String valueOf(基本数据类型|char[] b) //返回基本数据类型或者char[]的字符串表示形式

``` java
    System.out.println(String.valueOf(true)); // true
    System.out.println(String.valueOf(1)); // 1
    System.out.println(String.valueOf('A')); // A
    System.out.println(String.valueOf(100L)); // 100
    System.out.println(String.valueOf(1.0F)); // 1.0
    System.out.println(String.valueOf(new char[]{'A','B'})); // AB
```
###### 返回其他类型
> char charAt(int index)  //返回指定索引处的char值

``` java
     System.out.println("Lero".charAt(0)); //L
```
> byte[] getBytes()  // String编码为byte序列，并将结果存储到一个新的byte数组中

``` java
     byte[]  arr = "Lero".getBytes();
     System.out.println(Arrays.toString(arr)); //[76, 101, 114, 111] 为字符对应的整数编码
```

> char[] toCharArray() //将此字符串转换为一个新的字符数组

``` java
     char[]  arr = "Lero".toCharArray();
     System.out.println(Arrays.toString(arr)); //[L, e, r, o]
```

### StringBuilder类
>  一个可变的字符序列,若是字符序列经常变动，建议使用该类

###### 构造方法
> StringBuilder()
>
>StringBuilder(CharSequence seq)

``` java
    System.out.println(new StringBuffer()); //
    System.out.println(new StringBuffer("lero")); //lero
```
###### 常用方法

>  StringBuilder append(基本数据类型 变量|char[] str) //追加字符串**具有重载方法**

``` java
     System.out.println(new StringBuilder().append(true).append('L').append("E").append(new char[]{'R','O'}).append(1.0).append(1.0F).append(1L)); //trueLERO1.01.01
```
>  StringBuilder delete(int start, int end) //删除索引区间字符串
>
>  StringBuilder deleteCharAt(int index)  //删除指的索引字符串

``` java
     System.out.println(new StringBuilder("lero").delete(2,3)); //leo
     System.out.println(new StringBuilder("lero").deleteCharAt(1)); //lro
```
>   StringBuilder insert(int offset, 基本数据类型 变量|char[] str)  //插入字符串**具有重载方法**

``` java
     System.out.println(new StringBuilder("lero").insert(2,true)); //letruero
     System.out.println(new StringBuilder("lero").insert(2,new char[]{'A','B'})); //leABro
```
> String toString() //返回此序列中数据的字符串表示形式

``` java
     System.out.println(new StringBuilder("lero").toString()); //lero
```
> StringBuilder replace(int start, int end, String str) //使用给定 String 中的字符替换此序列的子字符串中的字符

``` java
     System.out.println(new StringBuilder("lero").replace(1,3,"AA")); //lAAo
```
> void setCharAt(int index, char ch) //将给定索引处的字符设置为指定字符

``` java
     StringBuilder  sb= new StringBuilder("lero");
     sb.setCharAt(1,'A');
     System.out.println(sb); // lAro
```
### StringBuffer类
>  和StringBuilder功能一样，适用于多线程环境，效率比StringBuilder低一些

### String&StringBuilder&StringBuffer异同
###### 相同点
>它们三者都能操作字符序列

###### 不同点
1. StringBuilder和StringBuffer更适合操作经常需要变动的字符序列,不会开辟额外的空间。而String每次创建的都是固定的字符序列
2. StringBuilder和StringBuffer功能一样的，但StringBuffer更适用于多线程环境；StringBuffer效率比StringBuilder低一些
3. String更适用于创建一次后不会再变动的字符序列
4. 它们三者都可以相互转换

### 正则表达式

















