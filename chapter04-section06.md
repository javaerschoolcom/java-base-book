# 泛型

###  为什么使用泛型
1. 在类型转换的时候，可能需要强转
2. 代码不具有通用性
3. 不会影响性能
4. 安全性检查

###  什么是泛型
> 参数化的类型就是泛型

###### 类型参数<T>
> 常用一对带单个字母的尖括号表示类型参数

1. 表示一种引用数据类型的时候使用T  type
2. K,V表示一种键值对的关系
3. E表示一种元素  element
4. U

###  泛型分类

######  泛型类
> 类型参数写在类名的后面

``` java
    public class Plate<T>{}
```
* 该类所有成员都会使用该类型参数进行替换

``` java
    public class Plate<T>{
      private  T  fruit;
      public T getFruit() {
         return fruit;
      }
      public void setFruit(T fruit) {
         this.fruit = fruit;
      }
    }
```

*  对于静态成员不支持类型参数

``` java
    public class Plate<T>{
      private static T  fruit; //编译不通过
      public static T getFruit() {  //编译不通过
         return fruit;
      }
      public void setFruit(T fruit) {
         this.fruit = fruit;
      }
    }
```

*  类型泛型支持多个类型参数，每个参数用逗号隔开

``` java
    public class Plate<T,V>{
      private  T  fruit;
      private  V  place;
      public T getFruit() {
         return fruit;
      }
      public void setFruit(T fruit) {
         this.fruit = fruit;
      }
      public V getPlace() {
          return place;
      }
      public void setPlace(V place) {
          this.place = place;
      }
    }
```
#####  泛型方法
>  当类中只有局部方法需要设计成泛型的，就可采用泛型方法，而不使用泛型类去设计

*  泛型方法使用时候必须声明

``` java
    public class Plan {
        public <T> void showInfo(T t){
            System.out.println(t);
        }
    }
```
* 单独的泛型方法支持静态的方法

``` java
    public class Plan {
        public static  <T> void showInfo(T t){
            System.out.println(t);
        }
    }
```
* 泛型方法的使用

> 非静态泛型方法使用

``` java
    public class TestPlan {
        public static void main(String[] args) {
            Plan plan = new Plan();
            plan.<String>showInfo("hello"); //非静态泛型方法使用
        }
    }
```

> 静态泛型方法使用

``` java
    public class TestPlan {
        public static void main(String[] args) {
            Plan.<String>showInfo("hello"); //静态泛型方法使用
        }
    }
```
* 当既使用泛型类又同时使用泛型方法的时候,优先使用泛型方法自己的定义

``` java
    public class Plan<T> {
        private  T  fruit;
        public   <T> T showInfo(T t){
            System.out.println(t);
            return T;
        }
    }

    public class TestPlan {
        public static void main(String[] args) {
            Plan<String> stringPlan = new Plan<>();//类泛型传入了String
            Integer  result = plan.<Integer>showInfo(1); //方法泛型传入了Integer    结果:1
        }
    }
```

######  泛型接口
> 接口上使用的泛型

``` java
    public interface BaseDao<T> {
        void  add(T t);
        void  update(Integer id);
        void  delete(Integer id);
        void  select(T t);
    }
```
* 泛型接口的使用方式一

``` java
    public class ArticleImp implements BaseDao<j20180425_1.Article>{
        @Override
        public void add(Article article) {
        }
        @Override
        public void update(Integer id) {
        }
        @Override
        public void delete(Integer id) {
        }
        @Override
        public void select(Article article) {
        }
    }
```
* 泛型接口使用方式二

``` java
    public class ArticleImp<T> implements BaseDao<T>{
        @Override
        public void add(T t) {
        }
        @Override
        public void update(Integer id) {
        }
        @Override
        public void delete(Integer id) {
        }
        @Override
        public void select(T t) {
        }
    }
```

######  泛型上限
>  当方法内部可能会使用到类型参数对应对象的方法时候，Object中又没有该方法，就可以使用泛型上限

``` java
    public class Fruit {
        public void eat(){
            System.out.println("水果可以吃");
        }
    }

    public class Apple extends Fruit {
    }

    public class Plan<T extends Fruit> {
        private  T  fruit;
        public Plan(T fruit) {
            this.fruit = fruit;
        }
        public  void showInfo(){
            fruit.eat();
        }
    }

    public class TestFruit {
        public static void main(String[] args) {
            Plan<Apple> plan = new Plan<Apple>(new Apple());
            plan.showInfo(); //水果可以吃
        }
    }

```

######  通配符<?>
> 可以表示任何的数据类型对象，但是又不是具体的哪一种数据类型。一般用在方法参数里，用于限定类型

######  通配符上限<? extends E>
> 也不能装任何数据类型对象，用于限定某个范围内的数据,主要用于取数据，取数据不需要强转

######  通配符下限<? supper E>
> 可以自己以及继承自己的类型的对象对象，用于限定某个范围内的数据，需要装数据，不需要取数据，取数需要强转

######
> 如果需要装数据，又需要取数据，不要使用通配符


######  使用泛型注意事项
// new T(); T.class; new T[]();


















