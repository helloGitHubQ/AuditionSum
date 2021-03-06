<!-- TOC -->
- [牛客网刷题知识点](#牛客网刷题知识点)
	- [基础](#基础)
	
	- [框架](#框架)
	
	- [前端](#前端)

- [数据库](#数据库)
	
	- [其他](#其他)
	
	  <!-- TOC -->
	
	  
	
	  # 牛客网刷题知识点 
## 基础

- **volatile和synchronized关键字的区别：**

1.volatile关键字是线程同步的轻量级实现，所以volatile性能肯定比synchronized关键字要好。但是volatile关键字只能用于变量而synchronized关键字可以修饰方法以及代码块。synchronized关键字在JavaSE1.6之后进行了主要包括为了减少获得锁和释放锁带来的性能消耗而引入的偏向锁和轻量级锁以及其它各种优化之后执行效率有了显著提升，实际开发中使用 synchronized 关键字的场景还是更多一些。

2.多线程访问volatile关键字不会发生阻塞，而synchronized关键字可能会发生阻塞

3.volatile关键字能保证数据的可见性，但不能保证数据的原子性。

synchronized关键字两者都能保证。

4,volatile关键字主要用于解决变量在多个线程之间的可见性，而 synchronized关键字解决的是多个线程之间访问资源的同步性。

- try..catch..finally

如果 try 语句中有 return 	,返回的是 try 语句块中的变量值

	详细执行过程如下：
	如果有返回值，就把返回值保存到局部变量中；
	执行jsr指令跳到finally语句里执行；
	执行完finally语句后，返回之前保存在局部变量表里的值。

**如果 try 和 finally 语句中都有 return ,则忽略 try 中 return，使用 finally 中的 return**

总结：

	1、不管有木有出现异常，finally块中代码都会执行；
	2、当try和catch中有return时，finally仍然会执行；
	3、finally是在return后面的表达式运算后执行的（此时并没有返回运算后的值，而是先把要返回的值保存起来，
	管finally中的代码怎么样，返回的值都不会改变，任然是之前保存的值），所以函数返回值是在finally执行前确定的；
	4、finally中最好不要包含return，否则程序会提前退出，返回值不是try或catch中保存的返回值。


finally里面不建议放return语句，根据需要，return语句可以放在try和catch里面和函数的最后。可行的做法有四：

	（1）return语句只在函数最后出现一次。
	（2）return语句仅在try和catch里面都出现。
	（3）return语句仅在try和函数的最后都出现。
	（4）return语句仅在catch和函数的最后都出现

- 自动拆装箱

1. 基本型和基本型封装型进行“==”运算符的比较，基本型封装型将会自动拆箱变为基本型后再进行比较，因此Integer(0)会自动拆箱为int类型再进行比较，显然返回true；
2. 两个Integer类型进行“==”比较，如果其值在-128至127，那么返回true，否则返回false, 这跟Integer.valueOf()的缓冲对象有关，这里不进行赘述。
3. 两个基本型的封装型进行equals()比较，首先equals()会比较类型，如果类型相同，则继续比较值，如果值也相同，返回true
4. 基本型封装类型调用equals(),但是参数是基本类型，这时候，先会进行自动装箱，基本型转换为其封装类型，再进行3中的比较。
-  **JVM**

java虚拟机是可运行java字节码的假想计算机 java的跨平台性也是相对与其他编程语言而言的

先介绍一下c语言的编译过程吧先是C语言源程序 也就是c的文件经过C编译程序编译后，生成windows可执行文件exe文件，然后在windows中执行。再介绍java的编译过程先是java源程序扩展名为java的文件，由java编译程序将java字节码文件，就是class文件然后在java虚拟机中执行。机器码是由CPU来执行的。Java编译后是字节码， 电脑只能运行机器码。Java在运行的时候把字节码变成机器码。C/C++在编译的时候直接编译成机器码。

	两个最基本的java回收算法：复制算法和标记清理算法
	复制算法：两个区域A和B，初始对象在A，继续存活的对象被转移到B。此为新生代最常用的算法
	标记清理：一块区域，标记可达对象（可达性分析），然后回收不可达对象，会出现碎片，那么引出
	标记-整理算法：多了碎片整理，整理出更大的内存放更大的对象
	两个概念：新生代和年老代
	新生代：初始对象，生命周期短的
	永久代：长时间存在的对象
	整个java的垃圾回收是新生代和年老代的协作，这种叫做分代回收。
	P.S：Serial New收集器是针对新生代的收集器，采用的是复制算法
	Parallel New（并行）收集器，新生代采用复制算法，老年代采用标记整理
	Parallel Scavenge（并行）收集器，针对新生代，采用复制收集算法
	Serial Old（串行）收集器，新生代采用复制，老年代采用标记整理
	Parallel Old（并行）收集器，针对老年代，标记整理
	CMS收集器，基于标记清理
	G1收集器：整体上是基于标记 整理 ，局部采用复制


java虚拟机中的垃圾回收机制是一个类，当该对象没有更多的应用指向它时，就会被垃圾回收器给回收，从而释放资源。该机制不可以程序员手动调用去回收某个对象，系统自动回去调用，当然程序员可以建议垃圾回收器回收某个对象。所以java中无需程序员手动释放内存，系统自动释放无用内存。

堆被划分两个不同的区域：新生代（Young）、老年代（Old）。新生代（Young）又被划分为三个区域：Eden、From Survivor、To Survicor。这样的划分能够更好的管理堆中的对象，包括内存的分配一级回收。

- final关键字

final修饰的方法，不允许被子类覆盖。

final修饰的类，不能被继承。

final修饰的变量，不能改变值。

final修饰的引用类型，不能再指向别的东西，但是可以改变其中的内容。

- private 和 final：

private方法只可以在类的内部使用，在类外根本访问不到， 而final方法可以在类外访问，但是不可以重写该方法，就是说可以使用该方法的功能但是不可以改变其功能，这就是private方法和final方法的最大区别

- 对象的初始化方式：

1. new时初始化 ；
2. 静态工厂 newInstance；
3. 反射Class.forName()；
4. clone方式；
5. 反序列化；
- static
静态成员

static用来修饰类或类的成员，这时不需要创建实例就能访问（而且不能实例化），在被调用的时候自动实例化，且在内存中产生一个实例。当含有静态成员的非静态类实例化出对象后，这些对象公用这些静态成员，通过类名或对象名都能访问它们

- 事务

Java事务三种类型:JDBC事务、JTA（Java Transaction API）事务、容器事务

JDBC 事务是用 Connection 对象控制的。JDBC Connection 接口（ java.sql.Connection ）提供了两种事务模式：自动提交和手工提交。 

java.sql.Connection 提供了以下控制事务的方法：
容器事务主要是J2EE应用服务器提供的，容器事务大多是基于JTA完成，这是一个基于JNDI的，相当复杂的API实现。

- Vector是线程安全的
- 实例变量，局部变量，	类变量，final变量

**实例变量**:是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。分配了内存空间后会给所有的成员变量一次初始化，没有赋值的会给成员变量对应类型的值，数据类型不同则默认值不同。

**局部变量**:在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。用的时候是直接入栈的，如果没有赋值，这个变量就没有初始值，也就无法操作，所以局部变量要初始化。

**类变量**:类变量也声明在类中，方法体之外，但必须声明为static类型。

**final变量**，final 修饰的变量。如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。

- extends 和 implements

		1、Java 中多实现通过 implements 关键字，单继承通过 extends 关键字
		2、Java 中单继承通过 extends 关键字，没有多继承
		3、如果同时出现继承和实现，则必须先继承（extends）再实现（implements）
- 一个java文件里，public 的类只能出现一个，只能出现一个，只能出现一个，否则，不管你用哪一个类名命名文件名编译器都会报错
- 多态

子类继承了父类的所有成员，包括private权限的成员变量，但是继承的子类具有私有变量的拥有权但是没有使用权。
- 堆栈方法区

	用new创建的对象在堆区。堆内存用于存放由new创建的对象和数组。
	
	函数中的临时变量在栈去。 
	
	java中的字符串在字符串常量区

- == 和 equals

==可用于基本类型和引用类型：当用于基本类型时候，是比较值是否相同；当用于引用类型的时候，是比较对象是否相同。

- hashMap 和 hashTable

hashMap在单线程中使用大大提高效率，在多线程的情况下使用hashTable来确保安全。

hashTable中使用synchronized关键字来实现安全机制，但是synchronized是对整张hash表进行锁定即让线程独享整张hash表，在安全同时造成了浪费。

concurrentHashMap采用分段加锁的机制来确保安全

- javaBean:

		（1）懂得将 Bean 放在哪个目录下：在 Resin 中 JavaBean 放在 doc\web-inf\classes 目录 中。  
		（2）懂得如何使用 JBuilder 定义一个 Bean；其中的语法规范不一定要记住，但要理解 其中的结构。  
		（3）Java 文件和 Bean所定义的类名一定要相同，并且是大小写敏感。 
		（4）Bean中要声明公共方法，与 Bean的名字相同。 
		（5）懂得如何在JSP 文件中引用JavaBean，其实就是<jsp:useBean>的语句。  
		（6）一定要紧记Java 是区分大小写的。

- 先通过GBK编码还原字符串，在该字符串正确的基础上得到“UTF-8”所对应的字节串。
- 内联函数

**内联函数**
在计算机科学中，内联函数（有时称作在线函数或编译时期展开函数）是一种编程语言结构，用来建议编译器对一些特殊函数进行内联扩展（有时称作在线扩展）；也就是说建议编译器将指定的函数体插入并取代每一处调用该函数的地方（上下文），从而节省了每次调用函数带来的额外时间开支。
但在选择使用内联函数时，必须在程序占用空间和程序执行效率之间进行权衡，因为过多的比较复杂的函数进行内联扩展将带来很大的存储资源开支。另外还需要非常注意的是对递归函数的内联扩展可能带来部分编译器的无穷编译。
C、C++中可以声明内联函数，在java中不支持直接声明，但是jvm会根据情况进行优化内联。

**内联函数特点：** 

	（1）提升效率。如上说明。 
	（2）占更多内存空间。编译器直接将内联函数扩展开，调用多复制品就多，因此更占用内存。 
	（3）java中不需额外关注，jvm会自动进行优化
内联举例：

	int max (int a, int b){ if (a > b) return a; else return b;}
	void main() { .....  a = max (x, y); // 内联，等价于 "a = (x > y ? x : y);" 直接扩展开了，不再调用方法  ..... }

- 面向对象的五大基本原则

		​	单一职责原则（SRP）
	​	开放封闭原则（OCP） 
	​	里氏替换原则（LSP） 
	​	依赖倒置原则（DIP） 
	​	接口隔离原则（ISP）

- volatile能保证数据的可见性，但不能完全保证数据的原子性，synchronized即保证了数据的可见性也保证了原子性
- 导包只可以导到当前层，不可以再导入包里面的包中的类
- Java一律采用Unicode编码方式，每个字符无论中文还是英文字符都占用2个字节。

将字符串S以其自身编码方式分解为字节数组，再将字节数组以你想要输出的编码方式重新编码为字符串。

Java虚拟机中通常使用UTF-16的方式保存一个字符。

ResourceBundle能够依据Local的不同，选择性的读取与Local对应后缀的properties文件，以达到国际化的目的。
- **sleep 和 wait 和 yield 和 join（重要）**

**1.sleep()方法**

在指定时间内让当前正在执行的线程暂停执行，但不会释放“锁标志”。不推荐使用。
sleep()使当前线程进入阻塞状态，在指定时间内不会执行。

**2.wait()方法**

在其他线程调用对象的notify或notifyAll方法前，导致当前线程等待。线程会释放掉它所占有的“锁标志”，从而使别的线程有机会抢占该锁。
当前线程必须拥有当前对象锁。如果当前线程不是此锁的拥有者，会抛出IllegalMonitorStateException异常。
唤醒当前对象锁的等待线程使用notify或notifyAll方法，也必须拥有相同的对象锁，否则也会抛出IllegalMonitorStateException异常。
waite()和notify()必须在synchronized函数或synchronized　block中进行调用。如果在non-synchronized函数或non-synchronized　block中进行调用，虽然能编译通过，但在运行时会发生IllegalMonitorStateException的异常。

**3.yield方法**

暂停当前正在执行的线程对象。
yield()只是使当前线程重新回到可执行状态，所以执行yield()的线程有可能在进入到可执行状态后马上又被执行。
yield()只能使同优先级或更高优先级的线程有执行的机会。 

**4.join方法**

join()等待该线程终止。
等待调用join方法的线程结束，再继续执行。如：t.join();//主要用于等待t线程运行结束，若无此句，main则会执行完毕，导致结果不可预测

- 静态方法可以直接使用 类名.方法.
- 读进去  写出来
- 贪婪匹配和非贪婪匹配
- **派生类和基类**:派生类-子类，基类-父类

- **构造方法：**

是一种特殊的方法。具体有以下特点。

1. 构造方法的方法名必须和类名相同
2. 构造方法没有返回类型，也不能定义为 void ，在方法名前面不声明方法类型。
3. 构造方法的主要作用是完成对象的初始化工作，它能够把定义对象时的参数传给对象的域。
4. 一个类可以定义多个构造方法，如果在定义类时没有定义构造方法，则编译系统会自动插入一个无参数的默认构造器。这个构造器不执行任何代码
5. 构造方法可以重载，以及参数的个数、类型、顺序。


- **实例方法**

- **java8新特性**

- **泛型擦除**

- **外部类和内部类：**

内部类可以是静态static的也可用public,private,default和protected修饰。

外部类的修饰符只能是public,abstract,final。

内部类：

	1.静态内部类才可以声明静态方法
	2.静态方法不可以使用非静态变量
	3.抽象方法不可以有函数体

- **抽象类和接口：**

抽象类和接口不能被实例化!

* 抽象类

1. 抽象类中可以构造方法 
2. 抽象类中可以存在普通属性，方法，静态属性。 
3. 抽象类中可以存在抽象方法。 
4. 如果一个类中有一个抽象方法，那么当前类一定是抽象类；抽象类中不一定有抽象方法。 
5. 抽象类中的抽象方法，需要有子类实现，如果子类不实现，则子类也需要定义为抽象的。 
6. 抽象类不能被实例化，抽象类和抽象方法必须被abstract修饰

关键字使用注意： 

抽象类中的抽象方法（其前有abstract修饰）不能用private、static、synchronized、native访问修饰符修饰。

- 接口

1. 在接口中只有方法的声明，没有方法体。 
2. 在接口中只有常量，因为定义的变量，在编译的时候都会默认加上public static final 
3. 在接口中的方法，永远都被public来修饰。 
4. 接口中没有构造方法，也不能实例化接口的对象。（所以接口不能继承类） 
5. 接口可以实现多继承 
6. 接口中定义的方法都需要有实现类来实现，如果实现类不能实现接口中的所有方法则实现类定义为抽象类。 
7. 接口可以继承接口，用extends

默认是 public abstract 的，且实现该接口的类中对应的方法的可见性不能小于接口方法的可见性。

- System是java.lang包下的一个类，out为System的final静态成员（PrintStream类型），println()是PrintStream类的实例方法。

- java 关键词是小写

- 变量类型：原始数据类型、引用类型。枚举(enum)类型是Java5新增的特性，它是一种新类型，允许用常量来表示特定的数据片段，而且全部都以类型安全的形式表示，是特殊的类，可以拥有成员变量和方法。

- **sleep和wait的区别：**

1，这两个方法来自不同的类分别是Thread和Object

2，最主要是sleep方法没有释放锁，而wait方法释放了锁，使得敏感词线程可以使用同步控制块或者方法。

3，wait，notify和notifyAll只能在同步控制方法或者同步控制块里面使用，而sleep可以在
任何地方使用

	synchronized(x){
	x.notify()
	//或者wait()
	}
4,sleep必须捕获异常，而wait，notify和notifyAll不需要捕获异常

- **方法重载(overload)和方法重写(override)：（重要）**

**方法重载**

必须是同一个类；

1. 方法名（也可以加函数）一样；
2. 参数类型不一样或参数数量不一样。
3. 与返回值类型无关

**方法重写**

方法重写的前提： 必须要存在继承的关系。
方法的重写: 子父类出了同名的函数，这个我们就称作为方法的重写。
什么时候要使用方法的重写？ 父类的功能无法满足子类的需求时。

两同两小一大原则：

方法名相同，参数类型相同；

子类返回值类型小于等于父类返回值类型；

子类抛出的异常小于等于父类抛出的异常；

子类访问权限大于等于父类访问权限。

- **String、StringBuffer和StringBuilder:**

效率：StringString(大姐，出生于JDK1.0时代) 不可变字符序列     <StringBuffer(二姐，出生于JDK1.0时代)  线程安全的可变字符序列   <StringBuilder(小妹，出生于JDK1.5时代) 非线程安全的可变字符序列。

Java中的String是一个类，而并非基本数据类型。string是值传入，不是引用传入。 StringBuffer和StringBuilder可以算是双胞胎了，这两者的方法没有很大区别。但在线程安全性方面，StringBuffer允许多线程进行字符操作。 这是因为在源代码中StringBuffer的很多方法都被关键字 synchronized  修饰了，而StringBuilder没有。 StringBuilder的效率比StringBuffer稍高，如果不考虑线程安全，StringBuilder应该是首选。另外，JVM运行程序主要的时间耗费是在创建对象和回收对象上。

- **集合：（重要）**

- **super:**

super可以访问父类的成员变量，成员方法，构造方法。

- **start和run的区别：**

**start方法**

 用 start方法来启动线程，是真正实现了多线程， 通过调用Thread类的start()方法来启动一个线程，这时此线程处于就绪（可运行）状态，并没有运行，一旦得到cpu时间片，就开始执行run()方法。但要注意的是，此时无需等待run()方法执行完毕，即可继续执行下面的代码。所以run()方法并没有实现多线程。

**run方法**

 run()方法只是类的一个普通方法而已，如果直接调用Run方法，程序中依然只有主线程这一个线程，其程序执行路径还是只有一条，还是要顺序执行，还是要等待run方法体执行完毕后才可继续执行下面的代码。

- 流媒体技术是一种可以使音频，视频和其他多媒体信息在   Internet   及   Intranet   上以实时的，无需下载等待的方式进行播放的技术。

流媒体又叫流式媒体，它是指商家用一个视频传送服务器把节目当成数据包发出，传送到网络上。

- **初始化过程：**

1. 初始化父类中的静态成员变量和静态代码块 ； 
2. 初始化子类中的静态成员变量和静态代码块 ； 
3. 初始化父类的普通成员变量和代码块，再执行父类的构造方法；
4. 初始化子类的普通成员变量和代码块，再执行子类的构造方法； 

- **自动转型：**

1. 若参与运算的数据类型不同，则先转换成同一类型，然后进行运算。
2. 转换按数据长度增加的方向进行，以保证精度不降低。例如int型和long型运算时，先把int量转成long型后再进行运算。
3. 所有的浮点运算都是以双精度进行的，即使仅含float单精度量运算的表达式，也要先转换成double型，再作运算。
4. char型和short型参与运算时，必须先转换成int型。
5. 在赋值运算中，赋值号两边的数据类型不同时，需要把右边表达式的类型将转换为左边变量的类型。如果右边表达式的数据类型长度比左边长时，将丢失一部分数据，这样会降低精度。

![Object方法](https://i.imgur.com/62iwODt.png)

- 日志的级别之间的大小关系如右所示：ALL < TRACE < DEBUG < INFO < WARN < ERROR < FATAL < OFF Log4j建议只使用四个级别，优先级从高到低分别是 ERROR > WARN > INFO > DEBUG。 

- 共享数据的所有访问一定要作为临界区，用synchronized标识，这样保证了所有的对共享数据的操作都通过对象锁的机制进行控制。

- **full GC触发的条件**

除直接调用System.gc外，触发Full GC执行的情况有如下四种。

1. 旧生代空间不足

旧生代空间只有在新生代对象转入及创建为大对象、大数组时才会出现不足的现象，当执行Full GC后空间仍然不足，则抛出如下错误：

    java.lang.OutOfMemoryError: Java heap space 
为避免以上两种状况引起的FullGC，调优时应尽量做到让对象在Minor GC阶段被回收、让对象在新生代多存活一段时间及不要创建过大的对象及数组。

2. Permanet Generation空间满

PermanetGeneration中存放的为一些class的信息等，当系统中要加载的类、反射的类和调用的方法较多时，Permanet Generation可能会被占满，在未配置为采用CMS GC的情况下会执行Full GC。如果经过Full GC仍然回收不了，那么JVM会抛出如下错误信息：

    java.lang.OutOfMemoryError: PermGen space 
为避免Perm Gen占满造成Full GC现象，可采用的方法为增大Perm Gen空间或转为使用CMS GC。

3. CMS GC时出现promotion failed和concurrent mode failure

对于采用CMS进行旧生代GC的程序而言，尤其要注意GC日志中是否有promotion failed和concurrent mode failure两种状况，当这两种状况出现时可能会触发Full GC。

promotionfailed是在进行Minor GC时，survivor space放不下、对象只能放入旧生代，而此时旧生代也放不下造成的；concurrent mode failure是在执行CMS GC的过程中同时有对象要放入旧生代，而此时旧生代空间不足造成的。

应对措施为：增大survivorspace、旧生代空间或调低触发并发GC的比率，但在JDK 5.0+、6.0+的版本中有可能会由于JDK的bug29导致CMS在remark完毕后很久才触发sweeping动作。对于这种状况，可通过设置-XX:CMSMaxAbortablePrecleanTime=5（单位为ms）来避免。

4. 统计得到的Minor GC晋升到旧生代的平均大小大于旧生代的剩余空间

这是一个较为复杂的触发情况，Hotspot为了避免由于新生代对象晋升到旧生代导致旧生代空间不足的现象，在进行Minor GC时，做了一个判断，如果之前统计所得到的Minor GC晋升到旧生代的平均大小大于旧生代的剩余空间，那么就直接触发Full GC。

例如程序第一次触发MinorGC后，有6MB的对象晋升到旧生代，那么当下一次Minor GC发生时，首先检查旧生代的剩余空间是否大于6MB，如果小于6MB，则执行Full GC。

当新生代采用PSGC时，方式稍有不同，PS GC是在Minor GC后也会检查，例如上面的例子中第一次Minor GC后，PS GC会检查此时旧生代的剩余空间是否大于6MB，如小于，则触发对旧生代的回收。
除了以上4种状况外，对于使用RMI来进行RPC或管理的Sun JDK应用而言，默认情况下会一小时执行一次Full GC。可通过在启动时通过- java-Dsun.rmi.dgc.client.gcInterval=3600000来设置Full GC执行的间隔时间或通过`-XX:+ DisableExplicitGC`来禁止RMI调用System.gc。

- **堆栈方法区：**

		堆区：只存放类对象，线程共享；
		方法区：又叫静态存储区，存放class文件和静态数据，线程共享;
		栈区：存放方法局部变量，基本类型变量区、执行环境上下文、操作指令区，线程不共享

- **HashTable和HashMap的区别：**

1、继承不同。

		public class Hashtable extends Dictionary implements Map
		public class HashMap extends AbstractMap implements Map

2、Hashtable 中的方法是同步的，而HashMap中的方法在缺省情况下是非同步的。在多线程并发的环境下，可以直接使用Hashtable，但是要使用HashMap的话就要自己增加同步处理了。

3、Hashtable中，key和value都不允许出现null值。

在HashMap中，null可以作为键，这样的键只有一个；可以有一个或多个键所对应的值为null。当get()方法返回null值时，即可以表示 HashMap中没有该键，也可以表示该键所对应的值为null。因此，在HashMap中不能由get()方法来判断HashMap中是否存在某个键， 而应该用containsKey()方法来判断。

4、两个遍历方式的内部实现上不同。

Hashtable、HashMap都使用了 Iterator。而由于历史原因，Hashtable还使用了Enumeration的方式 。

5、哈希值的使用不同，HashTable直接使用对象的hashCode。而HashMap重新计算hash值。

6、Hashtable和HashMap它们两个内部实现方式的数组的初始大小和扩容的方式。HashTable中hash数组默认大小是11，增加的方式是 old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数

![map](https://i.imgur.com/4NUxzkd.png)

![map集合类](https://i.imgur.com/gH0Qv70.png)

- **创建线程的方式有三种：**

		继承 Thread 类，重写 run 方法
		实现 Runnable 接口，并将对象实例作为参数传递给 Thread 类的构造方法
		实现 callable 接口，并实现 call 方法，并且线程执行完毕之后会有返回值

- **static / private**

static修饰某个字段时，肯定会改变字段创建的方式（每个被static修饰的字段对于每一个类来说只有一份存储空间，而非static修饰的字段对于每一个对象来说都有一个存储空间）

static属性是属于类的，所以对象共同拥有，所以既可以通过类名.变量名进行操作，又可以通过对象名.变量名进行操作

- 访问修饰控制符
![访问修饰控制符](https://i.imgur.com/lB5mcAZ.png)

- java程序的种类：

1.Application：Java应用程序，是可以由Java解释器直接运行的程序。

2.Applet：即Java小应用程序，是可随网页下载到客户端由浏览器解释执行的Java程序。

3.Servlet：Java服务器端小程序，由Web服务器(容器)中配置运行的Java程序。

- 从运行层面上来看，从四个选项选出不同的一个。
![引用类型](https://i.imgur.com/rTsbilS.jpg)
强引用，弱引用，动态类型，静态类型

- Java 的跨平台特性是因为JVM的存在，它可以执行 .class字节码文件，而不是 .java源代码。


- 其实当我们在为Integer赋值的时候，java编译器会将其翻译成调用valueOf()方法。比如Integer i=127翻译为Integer i=Integer.valueOf(127)
然后我们来看看valueOf()函数的源码：

		public static Integer valueOf(int i)
		{
		    //high为127
		    if(i >= -128 && i <= IntegerCache.high)
		        return IntegerCache.cache[i + 128];
		    else
		        return new Integer(i);
		}

可以看出，对于-128到127之间的数，Java会对其进行缓存。而超出这个范围则新建一个对象。

- Servlet 的生命周期分
为5个阶段：加载、创建、初始化、处理客户请求、卸载。

		加载：容器使用类加载器使用 servlet 类对应的文件加载 servlet
		创建：通过调用 servlet 构造函数创建一个 servlet 对象
		初始化：调用 init 方法进行初始化
		处理客户请求：每当有一个客户请求，容器就会创建一个线程来处理客户请求。
		卸载：调用 destroy 方法让 servlet 让自己释放其占用的资源

![运算符优先级](https://i.imgur.com/C7fqjpp.jpg)

- CountDownLatch 和 CyclicBarrier
CountDownLatch 是等待一组线程执行完，才执行后面的代码。此时这组线程已经执行完。
CyclicBarrier 是等待一组线程至某个状态后再同时全部继续执行线程。此时这组线程还未执行完。

- **java线程转换状态：**
![java线程状态](https://i.imgur.com/3BglRF6.png)

- inputStream是字节流输入流；而inputStreamReader是对字符流的处理

- 由于x是static的，存贮在类内，而不是对象内，所以++、--操作的是同一个变量。

- HashSet:

HashSet 内部使用 Map 保存数据，即将 HashSet 的数据作为 Map 的 key 值保存，这也是HashSet中元素不能重复的原因。而Map中保存key值前，会去判断当前Map中是否含有该key对象，内部是先通过key的hashCode，确定有相同的hashCode之后，再通过equals方法判断是否相同。

- javac 将源程序编译成 .class 文件，字节码；java 将字节码转为机器码，exe 程序。 

  ```
  javac -d 指定放置生成的类文件的位置
  javac -s 指定放置生成的源文件的位置
  ```
### 运算符
- ~操作运算符

		10原码：0000000000000000,0000000000001010；
		~10： 1111111111111111,1111111111110101  变为负数，计算机用补码存储
		~10反码：10000000000000000,0000000000001010
		~10补码：10000000000000000,0000000000001011，等于 -11

- java 中位运算符：

`>>`表示右移，如果该数为正，则高位补0，若为负数，则高位补1；

`>>>`表示无符号右移，也叫逻辑右移，即若该数为正，则高位补0，而若该数为负数，则右移后高位同样补0。

`<<`表示左移位
`>>`表示带符号右移位
`>>>`表示无符号右移
但是没有`<<<`运算符

	$a & $b	And（按位与）	将把 $a 和 $b 中都为 1 的位设为 1。
	$a | $b	Or（按位或）	将把 $a 和 $b 中任何一个为 1 的位设为 1。
	$a ^ $b	Xor（按位异或）	将把 $a 和 $b 中一个为 1 另一个为 0 的位设为 1。
	~ $a	Not（按位取反）	将 $a 中为 0 的位设为 1，反之亦然。
	$a << $b	Shift left（左移）	将 $a 中的位向左移动 $b 次（每一次移动都表示“乘以 2”）。
	$a >> $b	Shift right（右移）	将 $a 中的位向右移动 $b 次（每一次移动都表示“除以 2”）。

- 逻辑运算符和位移运算符

**逻辑运算符：**&&和|| 是按照“短路”方式求值的。如果第一个操作数已经能够确定表达式的值，第二个操作数就不必计算了

**位移运算符：**&和| 运算符应用于布尔值，得到的结果也是布尔值，不按“短路”方式计算。即在得到计算结果之前，一定要计算两个操作数的值。

---

- **字符流和字节流**

**字节流：**
InputStream 

|-- FileInputStream (基本文件流） 

|-- BufferedInputStream 

|-- DataInputStream 

|-- ObjectInputStream

**字符流：**
Reader 

|-- InputStreamReader (byte->char 桥梁） 

|-- BufferedReader (常用） 

Writer 

|-- OutputStreamWriter (char->byte 桥梁） 

|-- BufferedWriter 

|-- PrintWriter （常用）

- Java一维数组的两种初始化方法

1. 静态初始化


    	int array[] = new int[]{1,2,3,4,5}

或者

    int array[] = {1,2,3,4,5}
需要注意的是，写成如下形式也是错误的

    int array[] = new int[5]{1,2,3,4}

2. 动态初始化

		int array[] = new int[5];
		array[0] = 1;
		array[1] = 2;
		array[2] = 3;
		array[3] = 4;
		array[4] = 5;

静态与动态的区别就是在于，前者的是声明时初始化，后者是声明后初始化

- Java 序列化

Java在序列化时不会实例化static变量和transient修饰的变量，因为static代表类的成员，transient代表对象的临时数据，被声明这两种类型的数据成员不能被序列化

- 循环


1. 普通for循环：可以删除

        注意每次删除之后索引要--
2. Iterator遍历：可以删除

        不过要使用Iterator类中的remove方法，如果用List中的remove方法会报错
3. 增强for循环foreach：不能删除

        强制用List中的remove方法会报错

- Collection 和 Collections

java.util.Collection是一个集合接口。它提供了对集合进行基本操作的通用接口方法。Collection 接口在 java 类中有很多具体的实现。Collection 接口的意义是为各种具体的集合提供了最大化的统一操作方式。List,Set,Queue

java.util.Collections 是一个包装类。它包含有各种有关集合操作的静态多态方法。此类不能实例化，就像一个工具类，服务于 Java 的 Collection 框架。

- 如果两个对象相同，那么他们的 hashCode 应该也相同。如果两个对象的 hashCode 相等，那么这两个对象不一定相同。

- java.lang 包是 java 语言的核心包，lang 是language 的缩写。

java.lang包定义了一些基本的类型，包括Integer，String之类的，是 java 程序必备的包，有解释器自动引入，无需手动导入。

- **封装、继承、多态是 面向对象语言的三大特征。**

如果有四大特征的话，就是：抽象、封装、继承、多态

- Java中，赋值是有返回值的 ，赋什么值，就返回什么值。比如这题，x=y，返回y的值，所以括号里的值是1。

Java跟C的区别，C中赋值后会与0进行比较，如果大于0，就认为是true；而Java不会与0比较，而是直接把赋值后的结果放入括号。

- 当类的字节码文件加载到内存中时，类的实例方法并没有被分配入口地址，只有当该类的对象创建以后，实例方法才分配了入口地址。
- 当类的字节码文件加载到内存，类方法的入口地址就会分配完成，所以类方法不仅可以被该类的对象调用，也可以直接通过类名完成调用。类方法的入口地址只有程序退出时消失。

- instanceof:

instanceof 用来在运行时指出对象是否是特定类的一个实例，instanceof通过返回一个布尔值来指出，这个对象是否是这个特定类或者是它的子类的一个实例

- **Vetor & ArrayList的主要区别**

1. 同步性：Vector 是线程安全的，也就是同步的，而 ArrayList 是线程不安全的
2. 数据增长：当需要增长时，Vector 默认是增长为原来的一倍，而 ArrayList 确实原来的 50%，这样 ArrayList 就有利于节约内存空间。如果涉及到堆栈，队列等操作，应该考虑用 Vector，如果需要快速随机访问元素，应该使用 ArrayList 。

- 反射破坏代码的封装性，破坏原有的修饰符访问权限。
- java中的关键字有哪些？

答：1）48个关键字：abstract、assert、boolean、break、byte、case、catch、char、class、continue、default、do、double、else、enum、extends、final、finally、float、for、if、implements、import、int、interface、instanceof、long、native、new、package、private、protected、public、return、short、static、strictfp、super、switch、synchronized、this、throw、throws、transient、try、void、volatile、while。

2）2个保留字（现在没用以后可能用到作为关键字）：goto、const。

3）3个特殊直接量：true、false、null。 

---

函数递归调用使用栈区来递归，需要额外开销，并且效率不高

---

1、jps：查看本机java进程信息。

2、jstack：打印线程的栈信息，制作线程dump文件。

3、jmap：打印内存映射，制作堆dump文件

4、jstat：性能监控工具

5、jhat：内存分析工具

6、jconsole：简易的可视化控制台

7、jvisualvm：功能强大的控制台

- abstract class表示的是"is-a"关系，interface表示的是"like-a"关系

  ```
  is-a，理解为是一个，代表继承关系。 如果A is-a B，那么B就是A的父类。
  like-a，理解为像一个，代表组合关系。 如果A like a B，那么B就是A的接口。
  has-a，理解为有一个，代表从属关系。 如果A has a B，那么B就是A的组成部分。
  ```

- Java中所有错误和异常的父类是 java.lang.Throwable

- Java语言不支持native或synchronized的构造方法。

- J2EE常用的名词解释：

  ```
  web容器：给处于其中的应用程序组件（JSP，SERVLET）提供一个环境，使 JSP,SERVLET直接更容器中的环境变量接**互，不必关注其它系统问题。主要有WEB服务器来实现。例如：TOMCAT,WEBLOGIC,WEBSPHERE等。该容器提供的接口严格遵守J2EE规范中的WEB APPLICATION 标准。我们把遵守以上标准的WEB服务器就叫做J2EE中的WEB容器。
  
  EJB容器：Enterprise java bean 容器。更具有行业领域特色。他提供给运行在其中的组件EJB各种管理功能。只要满足J2EE规范的EJB放入该容器，马上就会被容器进行高效率的管理。并且可以通过现成的接口来获得系统级别的服务。例如邮件服务、事务管理。
  
  JNDI：（Java Naming & Directory Interface）JAVA命名目录服务。主要提供的功能是：提供一个目录系，让其它各地的应用程序在其上面留下自己的索引，从而满足快速查找和定位分布式应用程序的功能。
  
  JMS：（Java Message Service）JAVA消息服务。主要实现各个应用程序之间的通讯。包括点对点和广播。
  
  JTA：（Java Transaction API）JAVA事务服务。提供各种分布式事务服务。应用程序只需调用其提供的接口即可。
  
  JAF：（Java Action FrameWork）JAVA安全认证框架。提供一些安全控制方面的框架。让开发者通过各种部署和自定义实现自己的个性安全控制策略。
  
  RMI/IIOP:（Remote Method Invocation /internet对象请求中介协议）他们主要用于通过远程调用服务。例如，远程有一台计算机上运行一个程序，它提供股票分析服务，我们可以在本地计算机上实现对其直接调用。当然这是要通过一定的规范才能在异构的系统之间进行通信。RMI是JAVA特有的。
  ```

- Properties类是Hashtable的一个子类

- 抽象类中的方法是可以有方法体的。JDK1.8之后，接口中的方法也可以有方法体，用default关键字修饰方法。

- Garbage Collection/当对象的所有引用都消失后，对象使用的内存将自动回收

- Java   提供的事件处理模型是一种人机交互模型。它有三个基本要素：

  1) 事件源（Event Source）：即事件发生的场所，就是指各个组件，如按钮等，点击按钮其实就是组件上发生的一个事件；

  2) 事件（Event）：事件封装了组件上发生的事情，比如按钮单击、按钮松开等等；

  3) 事件监听器（Event Listener）：负责监听事件源上发生的特定类型的事件，当事件到来时还必须负责处理相应的事件；
  
- 1双字=2字=4字节=32位

  位、字节、字是计算机数据存储的单位。位是最小的存储单位.

## 框架
- DI

所谓依赖注入就是指：在运行期，由外部容器动态地将依赖对象注入到组件中。当spring容器启动后，spring容器初始化，创建并管理bean对象，以及销毁它。所以我们只需从容器直接获取Bean对象就行，而不用编写一句代码来创建bean对象。这种现象就称作控制反转，即应用本身不负责依赖对象的创建及维护，依赖对象的创建及维护是由外部容器负责的。这样控制权就由应用转移到了外部容器，控制权的转移就是所谓反转。虽然平时只需要按要求将bean配置到配置文件中，但是了解其实现过程对理解spring的实现原理是有好处的

``` 
Spring依赖注入（DI）的三种方式，分别为：
1．  接口注入
2．  Setter 方法注入
3．  构造方法注入
```

- DAO

Spring提供的DAO(数据访问对象)支持主要的目的是便于以标准的方式使用不同的数据访问技术。 简化 DAO 组件的开发。 

Spring提供了一套抽象DAO类供你扩展。这些抽象类提供了一些方法，用来简化代码开发。 IoC 容器的使用，提供了 DAO 组件与业务逻辑组件之间的解耦。所有的 DAO 组件，都由容器负责注入到业务逻辑组件中，其业务组件无须关心 DAO 组件的实现。 面向接口编程及 DAO 模式的使用，提高了系统组件之间的解耦，降低了系统重构的成本。 方便的事务管理: Spring的声明式事务管理力度是方法级。 异常包装:Spring能够包装Hibernate异常，把它们从CheckedException变为RuntimeException; 开发者可选择在恰当的层处理数据中不可恢复的异常，从而避免烦琐的 catch/throw 及异常声明。
- Spring IOC 

## 前端
- 客户端要获取一个socket对象通过实例化，而服务器获得一个socket对象则通过getRemoteSocketAddress()方法的返回值
- JSP 的6个基本动作：

		jsp:include：在页面被请求的时候引入一个文件；
		jsp:useBean：寻找或者实例化一个JavaBean。；
		jsp:setProperty：设置 JavaBean 的属性。；
		jsp:getProperty：输出某个 JavaBean 的属性；
		jsp:forward：把请求转到一个新的页面；
		jsp:plugin：根据浏览器类型为 Java 插件生成 OBJECT 或 EMBED 标记。
- **HttpServlet 容器响应 web 客户端**请求流程如下：

		1）Web客户向Servlet容器发出Http请求；
		2）Servlet容器解析Web客户的Http请求；
		3）Servlet容器创建一个HttpRequest对象，在这个对象中封装Http请求信息；
		4）Servlet容器创建一个HttpResponse对象；
		5）Servlet容器调用HttpServlet的service方法，这个方法中会根据request的Method来判断具体是执行doGet还是doPost，把HttpRequest和HttpResponse对象作为service方法的参数传给HttpServlet对象；
		6）HttpServlet调用HttpRequest的有关方法，获取HTTP请求信息；
		7）HttpServlet调用HttpResponse的有关方法，生成响应数据；
		8）Servlet容器把HttpServlet的响应结果传给Web客户。

doGet() 和 doPost（）是创建 HttpServlet 时需要覆盖的方法。

- 转发和重定向
- 默认RMI采用的是TCP/IP通信协议。
- 会话跟踪是一种灵活、轻便的机制，它使Web上的状态编程变为可能。
HTTP是一种无状态协议，每当用户发出请求时，服务器就会做出响应，客户端与服务器之间的联系是离散的、非连续的。当用户在同一网站的多个页面之间转换时，根本无法确定是否是同一个客户，会话跟踪技术就可以解决这个问题。当一个客户在多个页面间切换时，服务器会保存该用户的信息。
有四种方法可以实现会话跟踪技术：URL重写、隐藏表单域、Cookie、Session。

	1）.隐藏表单域：<input type="hidden">，非常适合步需要大量数据存储的会话应用。
	2）.URL 重写:URL 可以在后面附加参数，和服务器的请求一起发送，这些参数为名字/值对。
	3）.Cookie:一个 Cookie 是一个小的，已命名数据元素。服务器使用 SET-Cookie 头标将它作为 HTTP
	响应的一部分传送到客户端，客户端被请求保存 Cookie 值，在对同一服务器的后续请求使用一个
	Cookie 头标将之返回到服务器。与其它技术比较，Cookie 的一个优点是在浏览器会话结束后，甚至
	在客户端计算机重启后它仍可以保留其值
	4）.Session：使用 setAttribute(String str,Object obj)方法将对象捆绑到一个会话

- TCP
![TCp](https://i.imgur.com/lZtqLO6.png)

- exception是JSP九大内置对象之一，其实例代表其他页面的异常和错误。只有当页面是错误处理页面时，即isErroePage为 true时，该对象才可以使用。对于C项，errorPage的实质就是JSP的异常处理机制,发生异常时才会跳转到 errorPage指定的页面，没必要给errorPage再设置一个errorPage。所以当errorPage属性存在时， isErrorPage属性值为false
- session.setAttribute()和session.getAttribute()配对使用，作用域是整个会话期间，在所有的页面都使用这些数据的时候使用。request.getAttribute()表示从request范围取得设置的属性，必须要先setAttribute设置属性，才能通过getAttribute来取得，设置与取得的为Object对象类型。其实表单控件中的Object的 name与value是存放在一个哈希表中的，所以在这里给出Object的name会到哈希表中找出对应它的value。setAttribute()的参数是String和Object。
- HttpServletRequest 类主要处理：

		1.读取和写入HTTP头标
		2.取得和设置cookies
		3.取得路径信息
		4.标识HTTP会话

- [web.xml]
- WebService
	
		Webservice是跨平台，跨语言的远程调用技术;
		它的通信机制实质就是xml数据交换;
		它采用了soap协议（简单对象协议）进行通信
- jsp九大内置对象：request、response、session、application、out、pagecontext、config、page、exception

		内置对象	真实的对象	方法
		request	HttpServletRequest	setAttribute() 、getAttribute()
		response	HttpServletResponse	addCookie()、getWriter()
		session	HttpSession	setAttribute()、getAttribute()
		application	ServletContext	setAttribute()、getAttribute()
		config	ServletConfig	getInitParameter()、getInitParameterNames()
		exception	Throwable	getMessage()
		page	Object	（不使用对象）
		out	JspWriter	write()、print()
		pageContext	PageContext	setAttribute()、getAttribute()

## 数据库
- 使索引失效的几种情况：

(1)条件中有or，即使有条件带索引也不会使用；要想使用or，又想让索引生效，只能将or条件中的每个列都加上索引；

(2)对于多列索引，如果不是使用的第一部分，则不会使用索引；

(3)like查询是以%开头的，不会用到索引；

(4)如果列类型是字符串，那一定要在条件中将数据使用引号引用起来,否则不使用索引；

(5)如果mysql估计使用全表扫描要比使用索引快,则不使用索引；

-  JDBC statement中的PReparedStatement的占位符对应着即将与之对应当值，并且一个占位符只能对应一个值，如果能对应多个就会引起混淆。sql语句是确定的，那么一个占位符必定只能对应一个值



## 其他
- 区分IP地址的方式：

		1. 分四段，每段用“ .”点分割
		2. 每段的数字最大不超过255
		3. 四段不能全为 0

- 由于操作系统对处理器的管理策略不同，其提供的作业处理方式也就不同，例如，批处理方式、分时处理方式、实时处理方式等等 
- 动态RAM会周期性的刷新，静态RAM不进行刷新

		1、静态RAM，指SRAM：只要有供电，它保存的数据就不会丢失，且为高速存储器，如CPU中的高速缓存（cache）
		2、动态RAM，指DRAM：有供电，还要根据它要求的刷新时间参数，才能保持存储的数据不丢失，如电脑中的内存条
- CPU是一台计算机的运算核心和控制核心。主要包括运算器（ALU，Arithmetic and Logic Unit）和控制器（CU，Control Unit）两大部件。此外，还包括若干个寄存器和高速缓冲存储器及实现它们之间联系的数据、控制及状态的总线
	

----

---
---20190715