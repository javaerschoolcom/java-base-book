 # IO类

### 什么是I/O

> I/O是 input/output的缩写，分为IO设备和IO接口两个部分
>
> 我们常说的I/O是用来处理设备之间的数据传输 ,Java对数据的操作是通过流的方式，即IO流

### 常用概念

> 位(bit)：计算机中的一个二进制位
>
> 字节(Byte):一个字节占8个bit位，在java一个byte数据刚好占一个字节
>
> 1KB：指的是1024个字节

### 基本流

|        | 输入流      | 输出流       |
| ------ | ----------- | ------------ |
| 字节流 | InputStream | OutputStream |
| 字符流 | Reader      | Writer       |

### 流的使用

##### 输入流

1. 创建数据源对象
2. 创建输入流对象，并把输入流对象和数据源对象关联
3. 程序从**输入流**中读取数据

#####  输出流

1. 创建数据存储的目标对象
2. 创建输出流对象，并把输出流对象和目标对象关联
3. 程序把数据写入到**输出流**

###  文件流

> 字节流的类名后缀都是以xxputStream结尾

##### 文件字节输入流(FileInputStream)

> 从输入流中一次读取一个数据字节

``` java
FileInputStream in = new FileInputStream(new File("c:\\test.txt"));
int  data =0; //从输入流中读取的数据
while ((data =in.read())!= -1){// 当in.read()返回结果为-1，表明文件读完
    System.out.println(data);
}
in.close();
```

> 从输入流中一次读入多个字节，并放入byte数组中

``` java
FileInputStream in = new FileInputStream(new File("c:\\test.txt"));
int  length =0;//从输入流中读取的字节数
byte[] data = new byte[3];//划分内存用于存储从输入流中一次性读入的字节
while ((length =in.read(data))!= -1){
    System.out.println(data);
}
in.close();
```

##### 文件字节输出流(FileOutputStream)

> 将指定的一个字节写入输出流

``` java
FileOutputStream in = new FileOutputStream(new File("c:\\test.txt"));
out.write(97);
out.close();
```

> 将多个字节从指定的byte数组写入输出流

```java
FileOutputStream in = new FileOutputStream(new File("c:\\test.txt"));
byte data =new byte[]{97,98,99};
out.write(data);
out.close();
```

> 将多个字节从指定的byte数组的某一段写入输出流

``` java
FileOutputStream in = new FileOutputStream(new File("c:\\test.txt"));
byte data =new byte[]{97,98,99};
out.write(data,1,2);
out.close();
```

###### 拷贝文件

``` java
public static void main(String[] args) throws IOException {
    InputStream in = new FileInputStream(new File("c:\\source.mp4"));
    OutputStream out = new FileOutputStream(new File("c:\\target.mp4"));
    long start = System.currentTimeMillis();
    byte[] data = new byte[1024];//输入流在内存中一次性读满该数组，才会一次写到硬盘中
    int length = -1;
    while ((length=in.read(data))!=-1){
        out.write(data,0,length);
    }
    in.close();
    out.close();
    System.out.println(System.currentTimeMillis()-start);
}
```

####

> 适应用读取字符类的文件（文本），而对于字节类型的文件不适合(视频，音频，图像)

> 字符流的类名后缀都是以xxputStream结尾

##### 文件字符输出流（FileWriter）

> 该类常用于写入字符文件



##### 文件字符输入流（FileReader）

> 该类常用于读取字符文件



### 缓冲流

> 对基本的节点流进行读写加强，提高了性能

##### 字符输入缓冲流（BufferedReader）

> 从字符输入流中读取文本，缓冲字符，提供了高效读取

##### 字符输出缓冲流（BufferedWriter）

> 将文本写入字符输出流，缓冲字符，提供了高效写入

##### 字节输入缓冲流(BufferedInputStream)

> 从字节输入流中读取文本，缓冲字节，提供了高效读取

##### 字节输出缓冲流(BufferedOutputStream)

> 将字节写入字节输出流，缓冲字节，提供了高效写入

###### 使用方式

``` java
    BufferedXXX  bf  =  new BufferedXXX(基本流)；
```

### 转换流

> 把字节流转换成字符流或者是把字符流转换成字节流，转换的目的是允许给文件编码

##### 字符流转字节流(OutputStreamWriter)

##### 字节流转字符流(InputStreamReader)

> 建议统一使用utf-8进行保存文件

### 打印流

> 提供了更简单的方法进行打印操作

###### PrintWriter

> 适用于打印字符

###### PrintStream

> 把字符按照平台默认编码打印成字节



### 标准流

##### 标准输入流（InputStream）

##### 标准输出流（PrintStream）



### 对象流

> 要把对象永久存储或者是在网络中传输 比如：HttpSession

> 对象所在的类一定要实现可序列化接口Serializable

> 对象所在的类进行序列化的时候，强力建议加上一个序列化的版本号标识serialVersionUID，反序列就会根据版本号验证，如果相同则可以反序列化成功，不同则失败

> transient关键字不会序列化

使用方式

``` java
 ObjectXXXStream  os  =  new ObjextXXXStream(基本字节流)；
```

##### 对象字节输入流(ObjectInputStream)

##### 对象字节输出流(ObjectOutputStream)

###  数据流

> 可以读写内存中的数据，有些数据需要快速的存储或者读取，可以不使用外存而使用内存。

##### 字节数组输入流(ByteArrayInputStream)

##### 字节数组输出流(ByteArrayOutputStream)

##### 字符数组输入流(CharArrayReader)

##### 字符输出输出流(CharArrayWriter)

##### 字符串输入流(StringWriter)

##### 字符串输入流(StringReader)

### 合并流

> 作用:把多个文件复制到一个文件

##### 合并输入流(SequenceInputStream)

> 合并两个文件

``` java
public static void main(String[] args) throws IOException {
    SequenceInputStream sis = new SequenceInputStream(new FileInputStream("c:a.txt"), new FileInputStream("c:b.txt"));
    FileOutputStream fis = new FileOutputStream("c:total.txt");
    fis.write(sis.read());
    fis.write(sis.read());
    //先开的流后关闭，后开的流先关闭
    fis.close();
    sis.close();
}
```

> 合并多个文件

``` java
public static void main(String[] args) throws IOException {
    Vector<InputStream> v = new Vector<>();
    v.add(new FileInputStream("c:a.txt"));
    v.add( new FileInputStream("c:b.txt"));
    v.add( new FileInputStream("c:c.txt"));
    Enumeration<InputStream> elements = v.elements();
    SequenceInputStream sis = new SequenceInputStream(elements);
    FileOutputStream fis = new FileOutputStream("c:total.txt");
    fis.write(sis.read());
    fis.write(sis.read());
    fis.write(sis.read());
    //先开的流后关闭，后开的流先关闭
    fis.close();
    sis.close();
}
```



### 随机访问文件(RandomAccessFile)

> 多线程下载任务，断点续传任务

> 支持读取，也可以支持输出

``` java
public static void main(String[] args) throws IOException {
    RandomAccessFile rw = new RandomAccessFile("c:access.txt", "rw");
    rw.writeInt(97); //4
    System.out.println("当前指向的位置："+rw.getFilePointer());
    rw.writeChar('A');//2
    System.out.println("当前指向的位置："+rw.getFilePointer());
    rw.writeUTF("中国");//8
    System.out.println("当前指向的位置："+rw.getFilePointer());
    rw.seek(0);//移动指向的位置
    rw.writeInt(97);//
    System.out.println("当前指向的位置："+rw.getFilePointer()); //4
}
```



### 管道流

> 用于多线程环境，网络编程会用到

##### 字节输入管道流(PipedInputStream)

##### 字节输出管道流(PipedOutputStream)

##### 字符输入管道流(PipedReader)

##### 字符输出管道流(PipedWriter)

> 创建一个输入管道流线程

``` java
public class ThreadA extends  Thread {
    PipedInputStream pis =null;
    public ThreadA(PipedInputStream pis) {
        this.pis = pis;
    }
    @Override
    public void run() {
        try {
            int read = -1;
            while ((read=this.pis.read())!= -1){
                System.out.print((char)read);
            }
            this.pis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

> 创建一个输出管道流线程

``` java
public class ThreadB extends  Thread {
    PipedOutputStream  pos =null;
    public ThreadB(PipedOutputStream pos) {
        this.pos = pos;
    }
    @Override
    public void run() {
        try {
            pos.write("helloA".getBytes());
            pos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

> 测试

``` java
public class TestThread {
    public static void main(String[] args) throws IOException {
        PipedInputStream pis = new PipedInputStream();
        ThreadA threadA = new ThreadA(pis);
        PipedOutputStream pos =new PipedOutputStream();
        ThreadB threadB = new ThreadB(pos);
        pis.connect(pos); //使此管道输入流连接到管道输出流
        threadA.start();//开启线程
        threadB.start();//开启线程
    }
}
```





