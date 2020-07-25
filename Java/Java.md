```
char 在java中是2个字节。java采用unicode，2个字节（16位）来表示一个字符

printf主要是继承了C语言的printf的一些特性，可以进行格式化输出

print就是一般的标准输出，但是不换行

println和print基本没什么差别，就是最后会换行

System.out.printf("the number is: d",t);
     	参照JAVA API的定义如下：
   	  'd' 整数 结果被格式化为十进制整数
   	  'o' 整数 结果被格式化为八进制整数
   	  'x', 'X' 整数 结果被格式化为十六进制整数
   	  'e', 'E' 浮点 结果被格式化为用计算机科学记数法表示的十进制数
    	 'f' 浮点 结果被格式化为十进制数
   	  'g', 'G' 浮点 根据精度和舍入运算后的值，使用计算机科学记数形式或十进制格式对结果进行格式化。
   	  'a', 'A' 浮点 结果被格式化为带有效位数和指数的十六进制浮点数

println("test")相当于print("test\n")就是一般的输出字符串
```



```java
static：静态修饰符，被static修饰的变量和方法类似于全局变量和全局方法，可以在不创建对象时调用，当然也可以在创建对象之后调用。常见的可以用于工具类的工具方法中等，譬如：Math类中的绝大多数方法都是静态方法，他们扮演了工具方法的作用。
public：声明当前被修饰的对象、方法、变量为公有的。这里的公有指的是可以被公有访问，举个例子：一个类就像是一台电脑，公有的部分就是除去电脑本身之外用户可见的部分，譬如:你知道点击哪里可以登录QQ，摁哪里可以开关机，等等，你可以使用这个类所有的可见的东西都是被声明为public的，公有可见且公有可被访问的。
private：声明当前被修饰的变量、方法为私有的。这里的私有指的是仅仅可以被私有访问，举个例子：一个类就像是一台电脑，私用的部分就是除去电脑本身之外用户不可见的部分，譬如：你知道点击哪里可以登录QQ，但是内部到底是怎么登录的QQ你是不知道的，你知道摁哪里可以开关机，但是内部是怎么开关机的你是不知道的，等等，你在使用这个类时那些这个类的确有但是你访问是非法的方法或者变量是被声明为private的，私有不可见且不可访问的。
    
    static是静态函数，用了static就说明这个函数是属于类的，在调用时不需要再创建对象。
    public说明这个函数是属于对象的，在调用时要先new一个对象。
    
    首先要明确java中没有全局变量，但是可以通过静态变量  static声明 来达到同样的目的
```

```JAVA
==号在比较基本数据类型时比较的是值，而用==号比较两个对象时比较的是两个对象的地址值
```

一个很棒的关于Java传值和传引用的解释：

https://blog.csdn.net/jiangnan2014/article/details/22944075



方法中声明的基本数据类型等一般存放在栈中，类的成员变量一般存放在堆中。

final static必须在对象创建前赋值，不可以在构造函数赋值

因为是**static**的，会在对象创建前分配空间

因为是**final**的，必须在分配空间的时候赋值

final可以在构造函数赋值

![image-20200327142419009](C:\Users\syz\AppData\Roaming\Typora\typora-user-images\image-20200327142419009.png)

不加public等的不同package都不能import

String 字符串常量，字符串长度不可变。重新赋值修改字符串**其实是创建了新的对象，所指向的内存空间不同**。（用于存放字符的数组被声明为final的，因此只能赋值一次，不可再更改）

```
继承、重载、多态

package com.demo;

class A {
    void print() {
        System.out.println("A");
    }
}

class B extends A {
    void print() {
        System.out.println("B");
    }
    void print2() {
        System.out.println("B2");
    }
}

class C extends A {
    void print() {
        System.out.println("C");
    }
}

public class Test {
    public static void main(String[] args) {
        A b = new B();
        b.print();    // 输出B
	    ((B)b).print2();
    }
}
因为B继承A，所以B可以看成是一个A对象，这样写b指向B，父类中的一个方法只有在在父类中定义而在子类中没有重写的情况下，才可以被父类类型的引用调用;对于父类中定义的方法，如果子类中重写了该方法，那么父类类型的引用将会调用子类中的这个方法，这就是动态连接。
子类直接视为父类，父类变成子类需要显式的类型转换 
    
这样既有父类的共性，又有子类的特性

子类所有的构造函数 默认调用父类的无参构造函数（其实是默认省略掉了一行代码：super();）;
```

```Java
要想使用new生成一个内部类的实例，需要先指向一个外部类的实例，也就是先生成外部类的实例，
    
因为内部类可以调用外部类的成员，当没有外部类实例的时候也就没有这些成员的内存空间，
内部类在实例化的时候，调用外部类的成员就会出错，
所以需要使用外部类的实例 + 点 + new 的方式实例化一个新的内部类

Outer outer = new Outer(); 
Outer.Inner inner = outer.new Inner();
```

#### String Buffer和String Builder

StringBuffer对象则代表一个字符序列可变的字符串，当一个StringBuffer被创建以后，通过StringBuffer提供的append()、insert()、reverse()、setCharAt()、setLength()等方法可以改变这个字符串对象的字符序列。一旦通过StringBuffer生成了最终想要的字符串，就可以调用它的toString()方法将其转换为一个String对象。

StringBuilder类也代表可变字符串对象。实际上，StringBuilder和StringBuffer基本相似，两个类的构造器和方法也基本相同。不同的是：**StringBuffer是线程安全的，而StringBuilder则没有实现线程安全功能，所以性能略高。**

#### Handler、Looper

#### 内部类

###### 普通内部类

作为外部类的一个成员存在，不能定义静态变量,但可以访问外部类的所有成员。

static类型的属性和方法，在类加载的时候就会存在于内存中。

要想使用某个类的static属性和方法，那么这个类必须要加载到虚拟机中。

非静态内部类并不随外部类一起加载，只有在实例化外部类之后才会加载。

###### 静态内部类

只能访问外部类的static变量和方法

不能直接访问外部类的非static变量和方法

###### 局部内部类

定义在程序块中，只在块内有效

###### 匿名内部类

一个类用于继承其他类或是实现接口，并不需要增加额外的方法，只是对继承方法的事先或是覆盖。
 	只是为了获得一个对象实例，不需要知道其实际类型。
 	类名没有意义，也就是不需要使用到。

#### **静态代码块**

静态代码块是由static和{}组成的代码片段

静态代码块使用时有如下注意事项：

- 如果需要通过计算来初始化静态变量，可以声明一个静态块。
- **静态块仅在该类被加载时执行一次**。
- 只能初始化类的静态数据成员

#### 接口

接口是隐式抽象的，当声明一个接口的时候，不必使用**abstract**关键字。

接口中每一个方法也是隐式抽象的，声明时同样不需要**abstract**关键字。

接口中的方法都是公有的。

抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。

接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。

**注**：JDK 1.8 以后，接口里可以有静态方法和方法体了。

#### 泛型（模板类）

静态方法不允许用类的泛型

因为泛型类中的泛型参数的实例化是在定义对象的时候指定的，而静态变量和静态方法不需要使用对象来调用。对象都没有创建，如何确定这个泛型参数是何种类型，所以当然是错误的。

```
public static void print (T var) {
    System.out.println(var);
}
```

如果静态方法操作的类型不确定，必须要将泛型定义在方法上。

这是一个泛型方法，在泛型方法中使用的T是自己在方法中定义的T，而不是泛型类中的T。

```
public static <T> void test(T k) {

}
```

**不能创建**(new)泛型变量和数组

#### Java File类

File file = new File(filePath+ *File.separator* + fileName);

*File.separator* 分隔符

![image-20200424151334861](C:\Users\syz\AppData\Roaming\Typora\typora-user-images\image-20200424151334861.png)

FileinputStream：每次从硬盘读入一个字到中转站， 再写入目的文件（硬盘）

BufferedInputStream:一次读入n个字节到输入缓冲区，接着经中转站一个个写入到输出缓冲区，输入缓冲区为空时再次从硬盘读入批量数据，同理输出缓冲区满了以后再批量写入到目的文件（硬盘）。是从buffer里读数据的，肯定比从影盘里读快了。

read(bytes[])时返回读入缓冲的字节总数，如果因为已经到达文件末尾而没有更多的数据，则返回-1。

java在使用流时,都会有一个缓冲区,按一种它认为比较高效的方法来发数据:把要发的数据先放到缓冲区,缓冲区放满以后再一次性发过去,而不是分开一次一次地发。而flush()表示强制将缓冲区中的数据发送出去,不必等到缓冲区满.

[getPath](https://blog.csdn.net/u013041642/article/details/72953906)

为了可靠和安全，我们计算机的软件系统一般被分为两个部分，操作系统的Kernel Space和应用程序的user space，主要区别是权限吧。用户空间的程序要访问内核空间管理的数据、资源，一般要通过系统调用（syscall）来实现。

##### 多重 catch 语句中，异常类型必须子类在前父类在后

多重 catch 语句中，异常类型必须子类在前父类在后，如果你把父类放前面就执行不到后边的了， 比如你把Exception放到第一位，那么后面的就不会得到执行了，

发生这种情况，是由Java的“**异常匹配**”机制决定的。异常匹配就是指，抛出的异常到底由哪个异常处理单元(handler)处理。主要有两大原则：

1. **就近匹配原则**：找到离异常异常抛出点最近的处理单元，叫被**“捕获”**，然后就不再往下找。
2. **向上转型原则**：一个特定类型的异常处理单元，可以捕捉它**本身**以及所有从它**派生**的异常。

### Java并发24:Atomic系列-原子类型数组AtomicXxxxArray学习笔记

#### 原子类型数组

在java.util.concurrent.atomic中，原子类型数组有以下三种：

- AtomicLongArray：提供对int[]数组元素的原子性更新操作。-
- AtomicIntegerArray：提供对long[]数组元素的原子性更新操作。
- AtomicReferenceArray：提供对引用类型[]数组元素的原子性更新操作。

#### 原子类型数组的通用方法

首先学习上述三种原子类型数组的通用方法，这些方法如下：

构造器：分为初始长度构造器和初始数组构造器，不提供无参构造器。

- get(index)：取值，具有原子性和可见性。
- set(index)：赋值，具有原子性和可见性。
- lazySet(index,newValue)：赋值，具有原子性，不具备可见性。
- getAndSet(index,newValue)：赋值并返回旧值，具有原子性和可见性。
- compareAndSet(index,expect,newValue)：如果当前是期望值则赋值并返回赋值成功与否，具有原子性和可见性。
- weakCompareAndSet(index,expect,newValuee)：与compareAndSet(index,expect,newValue)类似。

### notify和notifyAll

先说两个概念：锁池和等待池

锁池:假设线程A已经拥有了某个对象(注意:不是类)的锁，而其它的线程想要调用这个对象的某个synchronized方法(或者synchronized块)，由于这些线程在进入对象的synchronized方法之前必须先获得该对象的锁的拥有权，但是该对象的锁目前正被线程A拥有，所以这些线程就进入了该对象的锁池中。

等待池:假设一个线程A调用了某个对象的wait()方法，线程A就会释放该对象的锁后，进入到了该对象的等待池中

> Reference：[java中的锁池和等待池](https://link.zhihu.com/?target=http%3A//blog.csdn.net/emailed/article/details/4689220)

然后再来说notify和notifyAll的区别

- 如果线程调用了对象的 wait()方法，那么线程便会处于该对象的等待池中，等待池中的线程不会去竞争该对象的锁。
- 当有线程调用了对象的 notifyAll()方法（唤醒所有 wait 线程）或 notify()方法（只随机唤醒一个 wait 线程），被唤醒的的线程便会进入该对象的锁池中，锁池中的线程会去竞争该对象锁。也就是说，调用了notify后只要一个线程会由等待池进入锁池，而notifyAll会将该对象等待池内的所有线程移动到锁池中，等待锁竞争。
- 优先级高的线程竞争到对象锁的概率大，假若某线程没有竞争到该对象锁，它还会留在锁池中，唯有线程再次调用 wait()方法，它才会重新回到等待池中。而竞争到对象锁的线程则继续往下执行，直到执行完了 synchronized 代码块，它会释放掉该对象锁，这时锁池中的线程会继续竞争该对象锁。

> Reference：[线程间协作：wait、notify、notifyAll](https://link.zhihu.com/?target=http%3A//wiki.jikexueyuan.com/project/java-concurrency/collaboration-between-threads.html)

综上，所谓唤醒线程，另一种解释可以说是将线程由等待池移动到锁池，notifyAll调用后，会将全部线程由等待池移到锁池，然后参与锁的竞争，竞争成功则继续执行，如果不成功则留在锁池等待锁被释放后再次参与竞争。而notify只会唤醒一个线程。

### Java 反射

**Class**类是一种**Object**

- **Object**是所有类的继承根源

**当一个类被加载，**JVM **便自动产生一个**Class**对象**

```Java
//获取Test这个类的Class对象的引用
Class myClass = Test.class;  
//获取Test对象test对应的Class对象的引用
Test test = new Test();
Class myClass = test.getClass();

```

**Class类的构造函数是私有的**

- **只允许 JVM 创建**

- **程序不能 Class a = new Class();**

**可用于实现插件**

- **插件实现规定的Interface**

- **插件编译成 jar 包**

- **运行时根据信息（如配置文件）获得插件类名**

- **创建对象**

- **cast成规定的Interface，并调用interface规定的接口**

**插件的作用**

- **方便（第三方）扩展程序**

- **升级**

- **针对需求（数据格式、用户需求等）改变程序行为**

- **选择性加载（避免主程序过慢）**

### instanceof关键字

**布尔计算(boolean)**

**用法 object  instanceof  Class**

**a** **instanceof** **B**

- **判断 a 是不是 B 这个类或者接口的实例**

- **返回 true**

  - **如果B是a对应的类** **a = new B();**
  - **或者，是 a 对应的类的父类**
  - **或者，是a对应的类实现的接口**


### Java集合类

#### Collection接口

##### List接口

- ArrayList
- LinkedList

##### Set接口

- HashSet
- TreeSet

AVL树、RB树

#### Map接口

- HashMap
- TreeMap



### Native优缺点

#### 优点

> 1. 由于so库反编译比较困难，因此提高代码的安全性。
> 2. 可以方便地使用目前已有的C/C++开源库。
> 3. 方便移植到其它平台。
> 4. 在Native中创建的资源存在于Native Heap上，需要主动去释放它，对于应用而言没有OOM的问题，并且也不需要考虑GC时锁线程带来的掉帧。如Facebook的Fresco框架就是将图片缓存到Native Heap上。
> 5. 在Dalvik虚拟机中，会省去由JIT编译期转为本地代码的步骤

#### 缺点

> 1. 在JDK1.6版本时，Java调用JNI的耗时是Java调用Java的5倍。随着JDK版本升级，差距慢慢减小。
> 2. Java与Native通信，需要多出一些系统开销。
> 3. 需要对不同的处理器架构进行支持，存在明显的兼容性问题。



因为一旦使用JNI，JAVA程序就丧失了JAVA平台的两个优点：
1、程序不再跨平台。要想跨平台，必须在不同的系统环境下重新编译本地语言部分。
2、程序不再是绝对安全的，本地代码的不当使用可能导致整个程序崩溃。一个通用规则是，你应该让本地方法集中在少数几个类当中。这样就降低了JAVA和C/C++之间的耦合性。