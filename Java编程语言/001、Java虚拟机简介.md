## Java虚拟机概念
Java虚拟机（JVM）是运行Java程序的抽象计算机，它是一种计算机设备的规范，可以采用不同的方式进行实现。Java程序通过运行在JVM中从而实现跨平台特性。
[Java虚拟机规范官方文档](https://docs.oracle.com/javase/specs/index.html)

## 常见的JVM实现
![在这里插入图片描述](./resource/jvm-mind-map.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3R6dzE5OTI=,size_16,color_FFFFFF,t_70)
- **Sun Classic VM：** 世界上第一款商用Java虚拟机。这款虚拟机只能使用纯解释器方式来执行Java代码，如果要使用JIT编译器，就必须进行外挂。如果外挂了JIT编译器，那么虚拟机的执行系统将被JIT全面接管，解释器便不再工作。
- **Sun HotSpot VM：** 是Sun JDK和OpenJDK的默认虚拟机，从JDK1.2开始引入，一直到现在还在使用，可见其优秀程度。
  * HotSpot Client VM：为在客户端环境中减少启动时间而优化。
  * HotSpot Server VM：为在服务器环境中最大化程序执行速度而设计。
  * 通过修改 /JDK_HOME/jre/lib/[ i386|amd64 ]/jvm.cfg 文件，调整 -server 和 -client 的顺序可以切换不同的实现。
## JVM基本架构
![在这里插入图片描述](./resource/jvm-framework.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3R6dzE5OTI=,size_16,color_FFFFFF,t_70)
- Class Loader：依据特定的格式，加载class文件到内存。
- Execution Engine：对命令进行解析。
- Native Interface：融合不同开发语言的原生库为Java所用。
- Runtime Data Area：JVM内存空间结构模型（JMM）。
## 类加载器（ClassLoader）
ClassLoader主要工作在Class装载的加载阶段，其主要作用是从系统外部获得Class二进制数据流加载到内存中，并对数据进行校验、转换解析和初始化，最终形成可以被虚拟机直接使用的Java类型。所有的Class都是由ClassLoader进行加载的。
**1. ClassLoader的种类**
- Bootstrap ClassLoader：启动类加载器，C++编写，用于加载核心库 java.*
- Extension ClassLoader：扩展类加载器，Java编写，用于加载扩展库 javax.*
- Application ClassLoader：应用程序类加载器，Java编写，用于加载程序所在目录的类
- Custom ClassLoader：自定义类加载器，Java编写，用于定制化加载类

**2. 类的生命周期**
- 加载（Loading）：
  * 通过一个类的全限定名来获取定义此类的二进制字节流。
  * 将这个字节流所代表的静态存储结构转换为方法区的运行时数据结构。
  * 在内存中生成一个代表这个类的 java.lang.Class 对象，作为方法区这个类的各种数据的访问入口。
- 验证（Verification）：验证是连接阶段的第一步，这一阶段的目的是为了确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。
  * 文件格式验证
  * 元数据验证
  * 字节码验证
  * 符号引用验证
- 准备（Preparation）：准备阶段是正式为类变量分配内存并设置类变量初始值的阶段，这些变量所使用的内存都将在方法区中进行分配。
- 解析（Resolution）：解析阶段是虚拟机将常量池内符号引用替换为直接引用的过程。
  * 类或接口的解析
  * 字段解析
  * 类方法解析
  * 接口方法解析
- 初始化（Initialization）：初始化阶段是执行类构造器 < clinit >() 方法的过程。只有在主动引用时才会触发类的初始化。在该阶段才真正开始执行类中定义的Java程序代码。
  * 遇到new、getstatic、putstatic或invokestatic这4条指令时。
  * 使用java.lang.reflect包的方法对类进行反射调用时。
  * 当初始化一个类的时候，发现其父类还没有进行初始化，则需先触发其父类的初始化。
  * 当虚拟机启动时，用户需指定一个要执行的主类（包含main方法的类），虚拟机会先初始化这个主类。
  * 当使用JDK1.7的动态语言支持时，如果一个java.lang.invoke.MethodHandle实例最后的解析结果REF_getStatic、REF_putStatic、REF_invokeStatic的方法句柄，并且这个方法句柄所对应的类没有进行过初始化，则需要先触发其初始化。
- 使用（Using）：使用该类所提供的功能。包括主动引用和被动引用。
- 卸载（Unloading）：从内存中释放。
  * 该类的所有实例都已经被回收。
  * 加载该类的ClassLoader被回收。
  * 该类对应的java.lang.Class对象没有在任何地方被引用，无法在任何地方通过反射访问该类的方法。

**3. 类加载器的双亲委派机制**
![在这里插入图片描述](./resource/jvm-classloader.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3R6dzE5OTI=,size_16,color_FFFFFF,t_70)
如果一个类加载器收到了类加载的请求，它首先不会自己去尝试加载这个类，而是把这个请求委派给父类加载器去完成，每一个层次的类加载器都是如此，因此所有的加载请求最终都应该传送到顶层的启动类加载器中，只有当父加载器反馈自己无法完成这个加载请求时，子加载器才会尝试自己去加载。双亲委派机制可以有效避免多份同样的字节码被重复加载。
## Java内存模型
**1. 程序计数器**
程序计数器是一块较小的内存空间，它可以看作是当前线程所执行的字节码的行号指示器。在虚拟机的概念模型中，字节码解释器的工作就是通过改变这个计数器的值来选取下一条需要执行的字节码指令。为了线程切换后能恢复到正确的执行位置，每条线程都有一个独立的程序计数器，各条线程之间计数器互不影响，独立存储，所以程序计数器是线程私有的。如果线程正在执行的是一个Java方法，这个计数器记录的是正在执行的虚拟机字节码指令的地址。如果执行的是Native方法，这个计数器值则为Undefined。由于程序计数器只是记录指令的地址，所以该区域不用担心内存泄露的问题。

**2. Java虚拟机栈**
Java虚拟机栈也是线程私有的，它的生命周期与线程相同。每个方法在执行的同时都会创建一个栈帧用于存储局部变量表、操作数栈、动态链接、方法出口等信息。每一个方法从调用到执行完成的过程，就对应着一个栈帧在虚拟机栈中入栈到出栈的过程。
![在这里插入图片描述](./resource/jmm-stack.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3R6dzE5OTI=,size_16,color_FFFFFF,t_70)
- 局部变量表：是一组变量值存储空间，用于存放方法参数和方法内部定义的局部变量。在Java程序编译为Class文件时，就在方法的Code属性的max_locals数据项中确定了该方法所需要分配的局部变量表的最大容量。
  * 局部变量表的容量以变量槽（Slot）为最小单位，每个Slot都应该能存放一个boolean、byte、char、short、int、float、reference或returnAddress类型的数据。long和double这两种数据类型需要占用64位地址空间，所以需要分配两个Slot进行存储。
- 操作数栈：是一个后入先出栈。最大深度实在编译的时候写入到Code属性的max_stacks数据项中。当一个方法刚开始执行的时候，该方法的操作数栈是空的，在方法的执行过程中，会有各种字节码指令往操作数栈中写入和提取数据，也就是出栈 / 入栈操作。
- 动态连接：每个栈帧都包含一个指向运行时常量池中该栈帧所属方法的引用，持有这个引用是为了支持方法调用过程中的动态连接。Class文件的常量池中存有大量的符号引用，字节码中的方法调用指令就以常量池中指向方法的符号引用作为参数。这些符号引用一部分在类加载阶段或者第一次使用的时候就转化为直接引用，这种转换称为静态解析。另外一部分将在每一次运行期间转换为直接引用，这部分称为动态连接。
- 方法返回地址：有两种退出方式：一种是执行引擎遇到任意一个方法返回的字节码指令，这时可能会有返回值传递给上层的方法调用者，是否有返回值和返回值的类型由遇到何种方法返回指令来决定。第二种是方法执行过程中遇到了异常，并且这个异常没有在方法体内得到处理，该方式造成的退出不会给上层调用者产生任何返回值。
- 附加信息：这部分信息取决于具体的虚拟机实现。

**3. 本地方法栈**
本地方法栈与虚拟机栈作用非常类似，它们的区别在于虚拟机栈为虚拟机执行Java方法服务，本地方法栈为虚拟机执行Native方法服务。

**4. Java堆**
待完善

**5. 方法区**
待完善