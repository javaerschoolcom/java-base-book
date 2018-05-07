#  文件

#### 文件分割符

> 对于不同的平台,分隔符是不一样的

* unix 平台区分大小写，绝对路径名的前缀始终是 `"/"` ,分隔符使用的是：
* windows平台不区分大小写，绝对路径C:\ ，分隔符使用是;

### 文件操作

######  文件常用构造方法

``` java
File file = new File("C:\\hello.txt"); // 构建文件
File file1 = new File("C:\\test"); //构建文件夹
File file2 = new File("C:\\test","hello.text"); //构建文件夹
File file3 = new File(file1, "hello.text");
```

###### 创建文件

>  boolean createNewFile() //当且仅当不存在该抽象路径名指定名称的文件时创建文件

``` java
 File file1 = new File("C:\\lero.txt");
 file1.createNewFile(); //创建文件lero.text

 File file2 = new File("C:\\lero");
 file2.createNewFile(); //创建文件lero （是文件不是文件夹）

 File file3 = new File("C:\\lero\\demo.txt");
 file3.createNewFile(); // 若C盘中没有lero文件夹，则创建文件demo.text失败
```

###### 删除文件

> boolean delete() 删除此抽象路径名表示的文件或目录

``` java
 File file1 = new File("C:\\parentDirectory\\childDirectory");
 file1.delete(); // 若childDirectory不是最终的文件或者目录，则不会删除
```

###### 修改文件

> boolean renameTo(File dest) 重新命名此抽象路径名表示的文件或目录

``` java
 File file1 = new File("C:\\parentDirectory\\lero");
 // 修改失败：不能修改父路径
 file1.renameTo(new File("C:\\otherDirectory\\last"));

 // 若lero不是最终文件，下面还有子文件也能修改成功
 file1.renameTo(new File("C:\\parentDirectory\\last"));

```

###### 文件状态操作

``` java
 boolean setLastModified(long time) 设置此抽象路径名指定的文件或目录的最后一次修改时间
 boolean setReadOnly() 标记此抽象路径名指定的文件或目录，从而只能对其进行读操作
 boolean setWritable(boolean writable)  设置此抽象路径名所有者写权限的一个便捷方法
 boolean setReadable(boolean readable)  设置此抽象路径名所有者读权限的一个便捷方法
 boolean setExecutable(boolean executable)  设置此抽象路径名所有者执行权限的一个便捷方法

 File getAbsoluteFile() 返回此抽象路径名的绝对路径名形式
 String getAbsolutePath() 返回此抽象路径名的绝对路径名字符串

 String getName() 返回由此抽象路径名表示的文件或目录的名称
 String getPath() 将此抽象路径名转换为一个路径名字符串

 String getParent()  返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回 null。
 File getParentFile() 返回此抽象路径名父目录的抽象路径名；如果此路径名没有指定父目录，则返回 null。

```

###### 文件常用过滤条件

```java
 boolean exists() 测试此抽象路径名表示的文件或目录是否存在。
 boolean isAbsolute() 测试此抽象路径名是否为绝对路径名
 boolean isDirectory() 测试此抽象路径名表示的文件是否是一个目录。
 boolean isFile() 测试此抽象路径名表示的文件是否是一个标准文件。
 boolean isHidden() 测试此抽象路径名指定的文件是否是一个隐藏文件。
 long lastModified()  返回此抽象路径名表示的文件最后一次被修改的时间。
 long length() 返回由此抽象路径名表示的文件的长度

```

###### 创建文件夹

``` java
boolean mkdir() 创建此抽象路径名指定的目录。 (不会创建父目录)
boolean mkdirs() 创建此抽象路径名指定的目录，包括所有必需但不存在的父目录。 （会创建父目录）
```

###### 遍历文件及过滤

``` java
 String[] list() 返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中的文件和目录。

 File[] listFiles() 返回一个抽象路径名数组，这些路径名表示此抽象路径名表示的目录中的文件。

 String[] list(FilenameFilter filter) 返回一个字符串数组，这些字符串指定此抽象路径名表示的目录中满足指定过滤器的文件和目录。

 File[] listFiles(FileFilter filter) 返回抽象路径名数组，这些路径名表示此抽象路径名表示的目录中满足指定过滤器的文件和目录。

 File[] listFiles(FilenameFilter filter) 返回抽象路径名数组，这些路径名表示此抽象路径名表示的目录中满足指定过滤器的文件和目录。

static File[] listRoots() 列出可用的文件系统根
```













