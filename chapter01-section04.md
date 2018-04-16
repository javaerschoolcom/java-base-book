# java概述-语言特点

### 简单
> ----Java语言的语法与C语言和C++语言很接近，但是不使用指针，而是引用。并提供了自动的垃圾回收，使得程序员不必为内存管理而担忧

### 面向对象
> ----Java语言是一个纯的面向对象程序设计语言。封装，继承，多态是面向对象的三大特点

### 分布式
> ----Java包括一个支持HTTP和FTP等基于TCP/IP协议的子库。因此，Java应用程序可凭借URL打开并访问网络上的对象，其访问方式与访问本地文件系统几乎完全相同

### 健壮
> ----Java的强类型机制、异常处理、垃圾的自动收集等是Java程序健壮性的重要保证。对指针的丢弃是Java的明智选择。Java的安全检查机制使得Java更具健壮性

### 安全
> ----Java的存储分配模型是它防御恶意代码的主要方法之一，Java对通过网络下载的类具有一个安全防范机制（类ClassLoader），如分配不同的名字空间以防替代本地的同名类、字节代码检查，并提供安全管理机制（类SecurityManager）让Java应用设置安全哨兵

### 解释型
> ----Java平台中的Java解释器对字节码进行解释执行，执行过程中需要的类在连接阶段被载入到运行环境中

### 高性能
> ----Java是一种先编译后解释的语言，所以它不如全编译性语言快。但是有些情况下性能是很要紧的，为了支持这些情况，Java设计者制作了“及时”编译程序，它能在运行时把Java字节码翻译成特定CPU（中央处理器）的机器代码，也就是实现全编译了。与那些解释型的高级脚本语言相比，Java的确是高性能的

### 多线程
> ----Java的多线程功能使得在一个程序里可同时执行多个小任务

### 跨平台
> ----Java程序（后缀为java的文件）在Java平台上被编译为体系结构中立的字节码格式（后缀为class的文件），然后可以在实现这个Java平台的任何系统中运行。这种途径适合于异构的网络环境和软件的分发

### 动态性
> ----Java允许程序动态地装入运行过程中所需要的类，也可以通过网络来载入所需要的类