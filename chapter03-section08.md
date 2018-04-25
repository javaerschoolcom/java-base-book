# 面向对象-枚举

###  枚举定义
>  就是有限可罗列的值组成的集合形成的新的数据类型

###### 语法
``` java
  [修饰符] enmu 枚举名{
      常量1,常量2...常量N;
  }
```
1. 枚举可以描述一组常量(只能放第一行)
``` java
    public enum Season {
        SPRING,SUMMER,AUTHOR,WINTER;
    }
```
2. 枚举在switch中的使用
>  注意在case后的枚举不是全限定名

``` java
    public enum Season {
     SPRING,SUMMER,AUTHOR,WINTER;
    }
    public class Test {
        public static void main(String[] args) {
           show();
        }
        public static void  show(){
            Season  season= Season.WINTER;
            switch (season){
                //错误写法 case Season.SPRING:
                //正确写法 case SPRING
                case SPRING:
                    System.out.println("春天");break;
                case SUMMER:
                    System.out.println("夏天");break;
                case AUTUMN:
                    System.out.println("秋天");break;
                case WINTER:
                    System.out.println("冬天");break;
            }
        }
    }

```

3. 所有的枚举都继承了Enum类,枚举可以当普通的类使用，枚举天生不能被继承，枚举的构造方法是私有的
``` java
    public enum Season {
        SPRING("春天",1),SUMMER("夏天",2),AUTUMN("秋天",3),WINTER("冬天",4);
        private int index;
        private String name;
        public void setName(String name) {
            this.name = name;
        }
        public String getName() {
            return name;
        }
        public void setIndex(int index) {
            this.index = index;
        }
        public int getIndex() {
            return index;
        }
        Season(){}; //默认权限修饰符 也是私有的
        private Season(String name,int index){
            this.name= name;
            this.index=index;
        }
        //通过字符串判断是否是制定的枚举类型
        public static Season  getRealEnum(String s){
            Season[] values = Season.values();
            for(Season item:values){
               if(s.equals(item.getName())){
                   return item;
               }
            }
            return null;
        }
    }

    public class Test {
        public static void main(String[] args) {
           show();
        }
        public static void  show(){
            //模拟从服务端传递字符串数据
            Scanner s = new Scanner(System.in);
            String next = s.next();
            Season season = Season.getRealEnum(next); //字符串和枚举比较，最后使用枚举类型方式
            switch (season){
                case SPRING:
                    System.out.println("春天");break;
                case SUMMER:
                    System.out.println("夏天");break;
                case AUTUMN:
                    System.out.println("秋天");break;
                case WINTER:
                    System.out.println("冬天");break;
            }
        }
    }

```
5. 使用接口定义很多组枚举

``` java
    public interface IEnum {
        //状态枚举
         enum  Status implements  IEnum{
             SUCCESS,ERROR;
         }
        //性别枚举
         enum  Gender implements  IEnum{
             MAN,WOMAN
         }
        //商品上下架 枚举
         enum  Goods implements  IEnum{
             ON,OFF
         }
    }
```
























