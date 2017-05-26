# <a name="top">Java笔记</a>
* [一、Struts2](#anchor1)
* [二、Java接口](#anchor2)
* [三、多线程](#anchor3)
* [四、反射](#anchor4)
* [五、序列化和反序列化](#anchor5)
* [六、动态代理](#anchor6)
* [七、Socket通信](#anchor7)

## <a name="anchor1">一、Struts2</a>[【TOP】](#top)
1. 禁用的（disabled）的表单元素的值不会被传至Action中。
2. 
3. 

## <a name="anchor2">二、Java接口</a>[【TOP】](#top)
1. 常用接口
```java
java.lang.Cloneable
java.lang.Comparable<T>
java.lang.Iterable<T>
java.lang.Runnable
java.io.Serializable
java.util.Iterator<E>
```
2. 观察者模式
```java
java.util.Observable
java.util.Observer
```
3. 生产者/消费者模式
```java
// 阻塞队列
java.util.concurrent.BlockingQueue
java.util.concurrent.BlockingDeque
```

## <a name="anchor3">三、多线程</a>[【TOP】](#top)
1. 一些重要概念
* 并发与并行

【并发】
```
当有多个线程在操作时，如果系统只有一个CPU，则它根本不可能真正同时进行一个以上的线程，它只能把CPU运行时间划分成若干个时间段，再将时间段分配给各个线程执行，在一个时间段的线程代码运行时，其它线程处于挂起状。这种方式我们称之为并发（Concurrent）。
```
【并行】
```
当系统有一个以上CPU时，则线程的操作有可能非并发。当一个CPU执行一个线程时，另一个CPU可以执行另一个线程，两个线程互不抢占CPU资源，可以同时进行，这种方式我们称之为并行（Parallel）。
```
【并发与并行的区别】
```
并发和并行是即相似又有区别的两个概念，并行是指两个或者多个事件在同一时刻发生；而并发是指两个或多个事件在同一时间间隔内发生。
在多道程序环境下，并发性是指在一段时间内宏观上有多个程序在同时运行，但在单处理机系统中，每一时刻却仅能有一道程序执行，故微观上这些程序只能是分时地交替执行。
倘若在计算机系统中有多个处理机，则这些可以并发执行的程序便可被分配到多个处理机上，实现并行执行，即利用每个处理机来处理一个可并发执行的程序，这样，多个程序便可以同时执行。
```
在操作系统中，若干个程序段同时在系统中运行，这些程序的执行在时间上是重叠的，一个程序段的执行尚未结束，另一个程序段的执行已经开始，无论从微观还是宏观，程序都是一起执行的。对比地，并发是指在同一个时间段内，两个或多个程序执行，有时间上的重叠（宏观上是同时，微观上仍是顺序执行）。
* 线程状态
```
NEW           → 未启动的线程
RUNNABLE      → 启动后未被阻塞的线程
BLOCKED       → 等待对象锁的线程，处于对象的等待队列中
WAITING       → 无限期等待条件的线程，处于对象的条件队列中（调用无参的wait、join方法）
TIMED_WAITING → 有限期等待条件的线程，处于对象的条件队列中（调用sleep或带时间参数的wait、join方法）
TERMINATED    → 运行结束的线程
```
2. 线程同步
* volatile
* 原子变量
* synchronized
* 显示锁
3. 线程协作（wait/notify）
* 生产者/消费者协作模式
```java
java.util.concurrent.BlockingQueue
java.util.concurrent.BlockingDeque
```
* 同时开始
* 等待结束
```java
java.util.concurrent.CountDownLatch
```
* 异步结果
```java
java.util.concurrent.Callable
java.util.concurrent.Future
    → java.util.concurrent.FutureTask
java.util.concurrent.Executor
    → java.util.concurrent.ExecutorService
java.util.concurrent.Executors
```
* 集合点
```java
java.util.concurrent.CyclicBarrier
```
* 线程中断
```java
interrupt()
isInterrupted()
Thread.interrupted()
```
* 显示锁
```java
java.util.concurrent.locks.Lock
    → java.util.concurrent.locks.ReentrantLock
java.util.concurrent.locks.ReadWriteLock
    → java.util.concurrent.locks.ReentrantReadWriteLock
```

## <a name="anchor4">四、反射</a>[【TOP】](#top)
```java
instanceof
java.lang.Class
java.lang.annotation.Annotation
java.lang.ClassLoader
java.lang.reflect.Constructor
java.lang.reflect.Field
java.lang.reflect.Method
java.lang.reflect.Type
java.lang.Package
```

## <a name="anchor5">五、序列化和反序列化</a>[【TOP】](#top)
```

```

## <a name="anchor6">六、动态代理</a>[【TOP】](#top)
```

```

## <a name="anchor7">七、Socket通信</a>[【TOP】](#top)
```

```
