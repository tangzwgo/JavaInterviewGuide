### 一、Java调试入门工具

**参考：**https://www.pdai.tech/md/java/jvm/java-jvm-debug-tools-list.html#jmap

#### 1.1、jps

jps是jdk提供的一个查看当前java进程的小工具， 可以看做是JavaVirtual Machine Process Status Tool的缩写。

参考地址：https://docs.oracle.com/javase/1.5.0/docs/tooldocs/share/jps.html

##### 1.1.1、jps常用命令

```
jps # 显示进程的ID 和 类的名称
jps –l # 输出输出完全的包名，应用主类名，jar的完全路径名 
jps –v # 输出jvm参数
jps –q # 显示java进程号
jps -m # main 方法
jps -l xxx.xxx.xx.xx # 远程查看
```

##### 1.1.2、jps参数 

```
-q：仅输出VM标识符，不包括classname,jar name,arguments in main method 
-m：输出main method的参数 
-l：输出完全的包名，应用主类名，jar的完全路径名 
-v：输出jvm参数 
-V：输出通过flag文件传递到JVM中的参数(.hotspotrc文件或-XX:Flags=所指定的文件 
-Joption：传递参数到vm,例如:-J-Xms512m
```

##### 1.1.3、jps原理

java程序在启动以后，会在java.io.tmpdir指定的目录下，就是临时文件夹里，生成一个类似于hsperfdata_User的文件夹，这个文件夹里（在Linux中为/tmp/hsperfdata_{userName}/），有几个文件，名字就是java进程的pid，因此列出当前运行的java进程，只是把这个目录里的文件名列一下而已。 至于系统的参数什么，就可以解析这几个文件获得。

#### 1.2、jstack

jstack是jdk自带的线程堆栈分析工具，使用该命令可以查看或导出 Java 应用程序中线程堆栈信息。

参考地址：https://www.jianshu.com/p/025cb069cb69

##### 1.2.1、jstack常用命令 

```
jstack 2815      # 基本
jstack -m 2815   # java和native c/c++框架的所有栈信息
jstack -l 2815   # 额外的锁信息列表，查看是否死锁
```

##### 1.2.2、jstack参数

```
-l 长列表. 打印关于锁的附加信息,例如属于java.util.concurrent 的 ownable synchronizers列表.
-F 当’jstack [-l] pid’没有相应的时候强制打印栈信息
-m 打印java和native c/c++框架的所有栈信息.
-h | -help 打印帮助信息
```

#### 1.3、jmap

命令jmap是一个多功能的命令。它可以生成 java 程序的 dump 文件， 也可以查看堆内对象示例的统计信息、查看 ClassLoader 的信息以及 finalizer 队列。

##### 1.3.1、jmap常用命令 

```
# 查看堆的情况（包含各个区域内存的使用情况）
jmap -heap 2815
# dump 堆内存快照
jmap -dump:live,format=b,file=/tmp/heap2.bin 2815
jmap -dump:format=b,file=/tmp/heap3.bin 2815
# 查看堆的占用
jmap -histo 2815 | head -10
```

##### 1.3.2、jmap参数 

```
no option：查看进程的内存映像信息,类似 Solaris pmap 命令。
heap：显示Java堆详细信息
histo[:live]：显示堆中对象的统计信息
clstats：打印类加载器信息
finalizerinfo：显示在F-Queue队列等待Finalizer线程执行finalizer方法的对象
dump:<dump-options>：生成堆转储快照
F：当-dump没有响应时，使用-dump或者-histo参数. 在这个模式下,live子参数无效.
help：打印帮助信息
J<flag>：指定传递给运行jmap的JVM的参数
```

#### 1.4、jstat

可以查看堆内存各部分的使用量，以及加载类的数量。

##### 1.4.1、jstat常用命令 

```
# 查看GC统计信息
jstat -gcutil PID 1000
# 响应内容说明
S0：年轻代中第一个survivor（幸存区）已使用的占当前容量百分比
S1：年轻代中第二个survivor（幸存区）已使用的占当前容量百分比
E：年轻代中Eden（伊甸园）已使用的占当前容量百分比
O：old代已使用的占当前容量百分比
P：perm代已使用的占当前容量百分比
YGC：从应用程序启动到采样时年轻代中gc次数
YGCT：从应用程序启动到采样时年轻代中gc所用时间(s)
FGC：从应用程序启动到采样时old代(全gc)gc次数
FGCT：从应用程序启动到采样时old代(全gc)gc所用时间(s)
GCT：从应用程序启动到采样时gc用的总时间(s)
```

##### 1.4.2、jstat参数 

```
-class (类加载器) 
-compiler (JIT) 
-gc (GC堆状态) 
-gccapacity (各区大小) 
-gccause (最近一次GC统计和原因) 
-gcnew (新区统计)
-gcnewcapacity (新区大小)
-gcold (老区统计)
-gcoldcapacity (老区大小)
-gcpermcapacity (永久区大小)
-gcutil (GC统计汇总)
-printcompilation (HotSpot编译统计)
```

#### 1.5、jinfo

jinfo 是 JDK 自带的命令，可以用来查看正在运行的 java 应用程序的扩展参数，包括Java System属性和JVM命令行参数；也可以动态的修改正在运行的 JVM 一些参数。当系统崩溃时，jinfo可以从core文件里面知道崩溃的Java应用程序的配置信息

##### 1.5.1、jinfo常用命令

```
# 输出当前 jvm 进程的全部参数和系统属性
jinfo 2815
# 输出所有的参数
jinfo -flags 2815
# 查看指定的 jvm 参数的值
jinfo -flag PrintGC 2815
# 开启/关闭指定的JVM参数
jinfo -flag +PrintGC 2815
# 设置flag的参数
jinfo -flag name=value 2815
# 输出当前 jvm 进行的全部的系统属性
jinfo -sysprops 2815
```

##### 1.5.2、jinfo参数

```
no option 输出全部的参数和系统属性
-flag name 输出对应名称的参数
-flag [+|-]name 开启或者关闭对应名称的参数
-flag name=value 设定对应名称的参数
-flags 输出全部的参数
-sysprops 输出系统属性
```

