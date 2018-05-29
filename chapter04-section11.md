

# 网络编程

### 什么是计算机网络

> 按照区域的划分，不同的计算机之间进行的通信，数据的分享和传递



### 网络通信三要素

##### IP

> ip是唯一标识网路中的一台计算机

> ipv4 32位  0-255.0-255.0-255.0255

> ipv6 128位

##### 端口

>  唯一确定一台计算机中的应用程序 0-65535个

> 0-1024这个范围内的端口不要使用 ftp:21:23 数据库:3306 tomcat:8080 IIS:80

##### 协议

> 是网络中制定的网络通信的标准和规范 底层协议：tcp/UDP  上层协议：http/ftp



### 基本概念

##### DNS|域名|IP

> DNS作用就是把域名解析到IP

##### URI|URL

> URI是统一资源标识符：唯一标识资源（身份证|指纹|DNA|住址）

> URL是统一资源定位符: 唯一定位资源  (住址)

> URL是URI的特例

##### B/S|C/S

> C/S  QQ  | 大型网络游戏

> B/S  通过浏览器和服务端通信



### InetAddress





### 套接字 Socket

> TCP用主机的IP地址加上主机上的端口号作为TCP连接的端点，这种端点就叫做套接字（socket）或插口



### UDP编程

##### DatagramSocket

> 此类表示用来发送和接收数据报包的套接字

##### DatagramPacket

> 此类表示数据报包

##### 实现步骤

``` java
1.客户端：创建套接字->数据封装到数据包->发送到服务端->关闭套接字
2.服务端: 创建套接字监听客户端->分配一个数据用来存储客户端发来数据包->接收数据包->查看数据->关闭套接字
```

##### 案例一

> 模拟客户端

``` java
public class Client {
    public static void main(String[] args) throws IOException {
        //客户端创建套接字
        DatagramSocket ds = new DatagramSocket();
        //模拟数据
        String data ="我是数据";
        byte[] bytes = data.getBytes();
        //封装到数据包中
        DatagramPacket dp = new DatagramPacket(bytes, bytes.length, InetAddress.getByName("localhost"),8888);
        ds.send(dp);//通过套接字发送数据包
        ds.close(); //关闭此数据报套接字
    }
}
```

> 模拟服务端

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        //监听客户端发来的数据包
        DatagramSocket ds = new DatagramSocket(8888);
        byte[]  data = new byte[1024];
         //指定一个数据包用来装发来的数据
        DatagramPacket dp = new DatagramPacket(data,data.length);
         //接收数据
        ds.receive(dp);
        System.out.println("数据来自于："+dp.getAddress().getHostName());
        System.out.println("客户端发来的数据为："+new String(dp.getData(),0,dp.getLength()));
        ds.close();
    }
}
```

> 测试先启动服务端，再启动客户端

##### 案例二

> 使用线程池，分别模拟客户端向服务端发送信息

```java
public class Test {
    public static void main(String[] args) throws IOException, InterruptedException {
        //写一个线程，用作服务端
        ScheduledExecutorService ses = Executors.newScheduledThreadPool(2);
        //监听客户端发来的数据包
        final DatagramSocket ds = new DatagramSocket(8888);
        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                try {
                    byte[]  data = new byte[1024];
                    //指定一个数据包用来装发来的数据
                    DatagramPacket dp = new DatagramPacket(data,data.length);
                    //接收数据
                    ds.receive(dp);
                    System.out.println("数据来自于："+dp.getAddress().getHostName());
                    System.out.println("客户端发来的数据为："+new String(dp.getData(),0,dp.getLength()));

                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,100, TimeUnit.MILLISECONDS);

        Thread.sleep(100); //让服务端先启动

        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                try {
                    //客户端创建套接字
                    DatagramSocket ds = new DatagramSocket();
                    //模拟数据
                    Scanner s  =new Scanner(System.in);
                    String next = s.next();
                    byte[] bytes  =next.getBytes();
                    //封装到数据包中
                    DatagramPacket dp = new DatagramPacket(bytes, bytes.length, InetAddress.getByName("localhost"),8888);
                    ds.send(dp);//通过套接字发送数据包

                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,100, TimeUnit.MILLISECONDS);
    }
}
```

### TCP编程

##### Socket

##### ServerSocket

> 案例一：客户端发信息到服务端，服务端接收数据

> 客户端

```java
public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
        OutputStream outputStream = socket.getOutputStream();//往外写
        PrintWriter  pw = new PrintWriter(outputStream,true);
        pw.println("客户机向服务机发消息");
        pw.close();
        socket.close();
    }
}
```

> 服务端

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket   serverSocket = new ServerSocket(8888);
        Socket socket = serverSocket.accept();//会阻塞，直到有客户机访问
        System.out.println("接收到客户机"+socket.getInetAddress().getHostName()+"的访问");
        InputStream inputStream = socket.getInputStream();
        BufferedReader br = new BufferedReader(new InputStreamReader(inputStream));
        System.out.println(br.readLine());
        br.close();
        socket.close();
    }
}
```

> 案例二：客户端发信息到服务端，服务端接收数据回消息给客户端，客户端接收数据

> 客户端

```java
public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
        OutputStream outputStream = socket.getOutputStream();//往外写
        PrintWriter  pw = new PrintWriter(outputStream,true);
        pw.println("客户机向服务机发消息");
        InputStream inputStream = socket.getInputStream();
        BufferedReader br = new BufferedReader(new InputStreamReader(inputStream));
        System.out.println("接收到服务端消息:"+br.readLine());
        br.close();
        pw.close();
        socket.close();
    }
}
```

> 服务端

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket  serverSocket = new ServerSocket(8888);
        Socket socket = serverSocket.accept();//会阻塞，直到有客户机访问
        System.out.println("接收到客户机"+socket.getInetAddress().getHostName()+"的访问");
        InputStream inputStream = socket.getInputStream();
        BufferedReader br = new BufferedReader(new InputStreamReader(inputStream));
        System.out.println("接收到客户消息："+br.readLine());
        OutputStream outputStream = socket.getOutputStream();//往外写
        PrintWriter  pw = new PrintWriter(outputStream,true);
        pw.println("服务机向客户机回消息");
        pw.close();
        br.close();
        socket.close();
    }
}
```

##### 注意事项

> readLine()读取数据要求有换行标识，write()要输出换行标识，要调用flush()刷新缓冲区

``` java
writer.write(msg);
writer.newLine(); //或者writer("\t\n");
writer.flush();
```

> 案例三  客户端和服务端交替发送和接收信息

``` java
public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
        OutputStream outputStream = socket.getOutputStream();//往外写
        PrintWriter  pw = new PrintWriter(outputStream,true);
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        InputStream inputStream = socket.getInputStream();
        BufferedReader bfr = new BufferedReader(new InputStreamReader(inputStream));
        while (true){
            String  input =br.readLine();
            if("exit".equals(input))break;
            pw.println(input); //写到服务端
            System.out.println(bfr.readLine());
        }
        socket.close();
    }
}
```

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket  serverSocket = new ServerSocket(8888);
        Socket socket = serverSocket.accept();//会阻塞，直到有客户机访问
        System.out.println("接收到客户机"+socket.getInetAddress().getHostName()+"的访问！");
        InputStream inputStream = socket.getInputStream();
        BufferedReader bfr = new BufferedReader(new InputStreamReader(inputStream));
        OutputStream outputStream = socket.getOutputStream();
        PrintWriter pw =new PrintWriter(outputStream,true);
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        while (true){
            System.out.println("接收到客户机消息："+bfr.readLine());
            String input =br.readLine();
            if("exit".equals(input))break;
            pw.println(input);
        }
        socket.close();
    }
}
```

> 案例四  客户端和服务端可以互相读写彼此信息

> 客户端

``` java
public class Client {
    public static void main(String[] args) throws IOException {
       Socket socket = new Socket(InetAddress.getLocalHost(), 8888);
       final PrintWriter  pw = new PrintWriter(socket.getOutputStream(),true);
       final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
       final BufferedReader bfr = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        //开启线程池
        ScheduledExecutorService ses = Executors.newScheduledThreadPool(2);
        //执行发信息到服务器线程
        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                String  input = null;
                try {
                    input = br.readLine();
                    pw.println(input); //发信息到服务端
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,10, TimeUnit.MILLISECONDS);
        //执行从服务器读信息线程
        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                try {
                    System.out.println(bfr.readLine());
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,10, TimeUnit.MILLISECONDS);
    }
}
```

> 服务端

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket   serverSocket = new ServerSocket(8888);
        Socket socket = serverSocket.accept();//会阻塞，直到有客户机访问
        System.out.println("接收到客户机"+socket.getInetAddress().getHostName()+"的访问！");
        final  BufferedReader bfr = new BufferedReader(new InputStreamReader(socket.getInputStream()));
        final  PrintWriter pw =new PrintWriter(socket.getOutputStream(),true);
        final  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        //开启线程池
        ScheduledExecutorService ses = Executors.newScheduledThreadPool(2);
        //执行发信息到客户端线程
        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                String  input = null;
                try {
                    input = br.readLine();
                    pw.println(input); //发信息到客户端
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,10, TimeUnit.MILLISECONDS);
        //执行从客户端读信息线程
        ses.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                try {
                    System.out.println(bfr.readLine());
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        },0,10, TimeUnit.MILLISECONDS);
    }
}
```



> 案例五 多客户端群聊

>客户端一

``` java
public class Client {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(),9999);
        //读取服务端信息
        new ReadMsg(socket);
        //发给服务端信息
        new SendMsg(socket);
    }
}
```

> 客户端二

``` java
public class Client1 {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(InetAddress.getLocalHost(),9999);
        //读取服务端信息
        new ReadMsg(socket);
        //发给服务端信息
        new SendMsg(socket);
    }
}
```

> 客户端读取服务端信息线程

``` java
public class ReadMsg extends  Thread {
    private Socket socket;
    private BufferedReader br;
    public  ReadMsg(Socket socket){
        this.socket=socket;
        try {
            br = new BufferedReader(new InputStreamReader(this.socket.getInputStream()));
        } catch (IOException e) {
            e.printStackTrace();
        }
        this.start();
    }
    @Override
    public void run() {
        try {
            while (true){
                System.out.println(br.readLine());//读取服务端消息
            }
        }catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

> 客户端发消息发服务端线程

``` java
public class SendMsg extends  Thread {
    private  Socket socket;
    private PrintWriter pw; //发送到服务器的输出流
    private BufferedReader br;//从键盘读取信息
    public  SendMsg(Socket socket){
        this.socket=socket;
        try {
           pw = new PrintWriter(this.socket.getOutputStream());
           br =new BufferedReader(new InputStreamReader(System.in));
        } catch (IOException e) {
            e.printStackTrace();
        }
        this.start();
    }
    @Override
    public void run() {
        while (true){
            try {
               pw.println(br.readLine());//发送消息到服务端
               pw.flush();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

> 服务端主程序

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        Integer count =0; //统计当前在线用户数
        ServerSocket  serverSocket =new ServerSocket(9999);
        HashMap<String,Socket>  sockets = new HashMap<>(); //存储客户端所有的socket
        while (true){
            Socket socket = serverSocket.accept();//等待客户端
            count++;
            String  currentSocketKey =socket.getInetAddress().getHostName()+ UUID.randomUUID();
            System.out.println("客户端"+currentSocketKey+"请求中"+",当前在线用户"+count);
            sockets.put(currentSocketKey,socket);
            new CurrentClient(socket,sockets,currentSocketKey); //每一个客户端开启一个线程
        }
    }
}
```

> 服务端为每个客户端开启一个处理线程

``` java
public class CurrentClient extends  Thread {
    private Socket socket;
    private HashMap<String,Socket> sockets;
    private String  currentSocketKey;
    public  CurrentClient(Socket socket,HashMap<String,Socket> sockets,String currentSocketKey){
        this.socket =socket;
        this.sockets =sockets;
        this.currentSocketKey=currentSocketKey;
        this.start();
    }
    @Override
    public void run() {
        try {
            while (true){
                //读取当前socket消息
                BufferedReader  bf = new BufferedReader(new InputStreamReader(this.socket.getInputStream()));
                String  message = bf.readLine();
                //把当前消息转发到所有的客户机(除了自己)
                Set<String> keySet = sockets.keySet();
                for(String item:keySet){
                    if(!currentSocketKey.equals(item)){
                        Socket socket = sockets.get(item);
                        PrintWriter pw = new PrintWriter(socket.getOutputStream());
                        pw.println(message);
                        pw.flush();
                    }
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

> 群聊+私聊

> 服务端

``` java
public class Server {
    public static void main(String[] args) throws IOException {
        Integer count =0; //统计当前在线用户数
        ServerSocket  serverSocket =new ServerSocket(9999);
        HashMap<String,Socket>  sockets = new HashMap<>(); //存储客户端所有的socket
        while (true){
            Socket socket = serverSocket.accept();//等待客户端
            count++;
            String  currentSocketKey ="客户端"+count;
            sockets.put(currentSocketKey,socket);
            new CurrentClient(socket,sockets,currentSocketKey,currentSocketKey+"进入聊天室"+",当前共"+count+"个用户在线"); //每一个客户端开启一个线程
        }
    }
}
```

> 服务端服务线程

``` java

public class CurrentClient extends  Thread {
    private Socket socket;
    private HashMap<String,Socket> sockets;
    private String  currentSocketKey;
    private String  notice;
    public  CurrentClient(Socket socket,HashMap<String,Socket> sockets,String currentSocketKey,String notice){
        this.socket =socket;
        this.sockets =sockets;
        this.currentSocketKey=currentSocketKey;
        this.notice=notice;
        this.start();
    }
    @Override
    public void run() {
        try {
            Set<String> keys = sockets.keySet();
            for(String item:keys){
                    Socket socket = sockets.get(item);
                    PrintWriter pw = new PrintWriter(socket.getOutputStream());
                    pw.println(this.notice+";私聊请使用:"+this.currentSocketKey+"@内容");
                    pw.flush();
            }
            while (true){
                //读取当前socket消息
                BufferedReader  bf = new BufferedReader(new InputStreamReader(this.socket.getInputStream()));
                String  message = bf.readLine();
                //根据发送消息判断是私聊还是群聊
                int i = message.indexOf("@");
                Boolean isAll =true; //群聊为true|私聊为false
                Socket toOnePersion=null; //私聊对象
                if(i!=-1){
                    String[] messageArr = message.split("@");
                    if(messageArr!=null && messageArr.length>0){
                        Set<String> keySet = sockets.keySet();
                        for(String item:keySet){
                            if(messageArr[0].equals(item)){
                                isAll =false;
                                toOnePersion =sockets.get(item);
                                break;
                            }
                        }
                    }
                }
                if(!isAll){
                    //私聊
                    PrintWriter pw = new PrintWriter(toOnePersion.getOutputStream());
                    pw.println(this.currentSocketKey+"对你说:"+message.substring( message.indexOf("@")+1,message.length()));
                    pw.flush();
                }else{
                    //群聊
                    Set<String> keySet = sockets.keySet();
                    for(String item:keySet){
                        if(!currentSocketKey.equals(item)){
                            Socket socket = sockets.get(item);
                            PrintWriter pw = new PrintWriter(socket.getOutputStream());
                            pw.println(message);
                            pw.flush();
                        }
                    }
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```

> 其他代码参考群聊

