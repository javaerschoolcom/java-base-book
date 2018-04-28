# 核心类-日期类

###  Date类
>  用于日期的表示

###### 构造方法
* Date d= new Date();//本地时区系统当前时间
* Date(int year, int month, int date) // 构造的year要减去1900

###### 常用方法
*  String toLocaleString()//返回本地日期表示形式


### Calendar类
>  提供了比Date类更强大的功能

###### 构造方法
* static Calendar getInstance() //获取系统当前时间

###### 常用方法
* int get(int field) //返回给定日历字段的值
* int set(int fiele,int value) //设置指定的日历字段
* abstract void add(int field, int amount) //根据日历的规则，为给定的日历字段添加或减去指定的时间量
* Date getTime() //Calander转Date的方法
* void setTime(Date date) //Date转Calander


### SimpleDateFormat类
> 用于格式化或者是解析日期

######  格式化日期


######  解析日期



















