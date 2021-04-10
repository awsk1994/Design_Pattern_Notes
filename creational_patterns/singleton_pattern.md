# 单例模式 (Singleton Pattern)
 - 意图：保证一个类仅有一个实例，并提供一个访问它的全局访问点。
 - 主要解决：一个全局使用的类频繁地创建与销毁。
 - 何时使用：当您想控制实例数目，节省系统资源的时候。
 - 关键代码：构造函数是私有的：
   - 一个private constructor(私有构造函数)
     - 使得外面的类不能通过引用来产生对象
   - 一个private static 变量
     - 使得外面的类直接访问对象
   - 一个public static 访问方法
     - 必须提供一个自己的对象以及访问这个对象的静态方法。

<img src="./img/singleton_pattern_diagram.jpeg" height="300px"/>

 - 三种实现：饿汉式, 懒汉式, Double Checked Locking
 - 可分为有状态的和无状态的。
   - **有状态**的单例对象一般也是**可变**的单例对象，多个单态对象在一起就可以作为一个状态仓库一样向外提供服务。
   - **没有状态**的单例对象也就是**不变**单例对象，仅用做提供工具函数。

## 实现
### 1. 饿汉式（Hungry)

```java
public class Singleton1 {
  // 在自己内部定义自己一个实例
  // 注意这是 private 只供内部调用
  private static Singleton1 instance = new Singleton1();

  // 构造函数设置为私有
  private Singleton1(){}

  // 静态工厂方法，提供了一个供外部访问得到对象的静态方法
  public static Singleton1 getInstance(){
    return instance;
  }
}
```
 - 优点：没有加锁，执行效率会提高。（不需要锁因为只是一个get）
 - 缺点：类加载时就初始化，浪费内存。
 - 它基于 classloader 机制避免了多线程的同步问题，不过，instance 在类装载时就实例化，虽然导致类装载的原因有很多种，在单例模式中大多数都是调用 getInstance 方法， 但是也不能确定有其他的方式（或者其他的静态方法）导致类装载，这时候初始化 instance 显然没有达到 lazy loading 的效果。

### 2. 懒汉式(Lazy)
```java
public class Singleton2 {
  private static Singleton2 instance = null;
  private Singleton2(){}

  public synchronized static Singleton2 getInstance(){
    // 这跟饿汉式很相似
    if(instance == null)
      instance = new Singleton2();
    
    return instance;
  } 
}
```
 - 描述：很好的 lazy loading，能够在多线程中很好的工作，但是，效率很低，99% 情况下不需要同步。
 - 优点：第一次调用才初始化，避免内存浪费。
 - 缺点：必须加锁 synchronized 才能保证单例，但加锁会影响效率。（因为在getInstance里，创建并初始化instance）
 - getInstance() 的性能对应用程序不是很关键（该方法使用不太频繁）。

### 3. 双检锁/双重校验锁（DCL，即 double-checked locking）

```java
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getSingleton() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
          if (singleton == null) {  
              singleton = new Singleton();  
          }  
        }
    }  
    return singleton;  
    }  
}
```

 - 描述：这种方式采用双锁机制，安全且在多线程情况下能保持高性能，也具备lazy loading
 - getInstance() 的性能对应用程序很关键。
 - 为何需要双检锁？
   - If only synchronized-if, then we need to acquire lock every time (even when singleton is not null).
   - If only if-synchronized, singleton might be instanted by another thread at the moment between the if and the synchronized.

## 应用实例：
1. 一个班级只有一个班主任。
2. Windows 是多进程多线程的，在操作一个文件的时候，就不可避免地出现多个进程或线程同时操作一个文件的现象，所以所有文件的处理必须通过唯一的实例来进行。
3. 一些设备管理器常常设计为单例模式，比如一个电脑有两台打印机，在输出的时候就要处理不能两台打印机打印同一个文件。

## 优点：
1. 在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例（比如管理学院首页页面缓存）。
2. 避免对资源的多重占用（比如写文件操作）。
缺点：没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。

## 使用场景：
1、要求生产唯一序列号。
2、WEB 中的计数器，不用每次刷新都在数据库里加一次，用单例先缓存起来。
3、创建的一个对象需要消耗的资源过多，比如 I/O 与数据库的连接等。
 - 注意事项：getInstance() 方法中需要使用同步锁 synchronized (Singleton.class) 防止多线程同时进入造成 instance 被多次实例化。
