

# 1.什么是JUC

源码+官方文档

java.util.concurrent

高频问答

并发编程

```
java.util.concurrent
java.util.concurrent.atomic //原子性
java.util.concurrent.locks  //lock锁
```

java.util是java的工具包（屏蔽同名）

包、分类

**业务：普通的线程代码 Thread**

Runable 没有返回值、效率比callable相对较低！

# 2、线程和进程

线程、进程



线程：一个程序 QQ.exe 程序的集合:

一个进程往往可以包含多个线程，至少包含一个！

java默认有个线程？2个  一个是main  另一个做垃圾回收的GC线程



线程：开了一个进程Typora，写字，自动保存（线程负责的）

对于java而言：Thread、Runable、Callable

**进程就是运行了的程序，是操作系统进行资源分配和调度的基本单位**

**进程是CPU分配资源的基本单位**



**线程就是操作系统中进行运算调度的最小单位**

**线程是CPU执行的基本单位**



java真的可以开启线程吗？开不了



并发

# 3、并发、并行

并发编程：并发、并行

并发（多线程操作同一个资源）

- CPU一核，模拟出来多条线程，天下武功唯快不破，快速交替

并行（多个人一起行走）

- CPU多核，多个线程可以同时执行；线程池

  ```java
  public class Test1 {
      public static void main(String[] args) {
          //获得CPU的核数
          //CPU密集型，IO密集型
          System.out.println(Runtime.getRuntime().availableProcessors());
      }
  }
  ```

并发编程的本质：**充分利用CPU的资源**

所有的公司都很看重！

企业，为了挣钱=>提高效率，裁员，找一个厉害的人顶替三个不怎么样的人；



## 线程有几个状态

```java
public enum State {
  	//新生
    NEW,

    //运行
    RUNNABLE,

    //阻塞
    BLOCKED,

    //等待，死死地等
    WAITING,

   	//超时等待
    TIMED_WAITING,

    //终止
    TERMINATED;
}
```



## wait/sleep的区别

1. **来自不同的**

   wait=>Object

   sleep=>Thread

2. **关于锁的释放**

   wait会释放锁

   sleep睡觉了，抱着锁睡觉，不会释放！

3. **使用的范围是不同的**

   wait必须在同步代码块中（同时运行的代码块）

   sleep可以在任何地方睡

4. **是否需要捕获异常**

   wait必须要捕获异常

   sleep必须要捕获异常

# 3、LOCK锁（重点）

**传统synchronized**

```java
//真正的多线程开发，公司中的开发,降低耦合性
//线程就是一个单独的资源类，没有任何附属的操作！
//1、属性、方法
public class Test2 {
    public static void main(String[] args) {
        //并发 多个线程操作同一个资源类
        Ticket ticket=new Ticket();
        //@FunctionalInterface 函数式接口 jdk1.8 lambda表达式
        new Thread(()->{ for (int i = 0; i < 20; i++) { ticket.sale(); } },"a").start();
        new Thread(()->{ for (int i = 0; i < 40; i++) { ticket.sale(); } },"b").start();
        new Thread(()->{ for (int i = 0; i < 60; i++) { ticket.sale(); } },"c").start();


    }
}

//资源类
class Ticket  {
    //属性、方法
    private int number=50;
    //卖票的方式
//    synchronized本质就是锁
    public synchronized void sale(){
        if (number>0){
            System.out.println(Thread.currentThread().getName()+"卖出了"+number--+"票，剩余"+number);
        }
    }
}
```

**Lock接口**

可重复锁 读写锁

![image-20210302100055578](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210302100055578.png)

![image-20210302100352471](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210302100352471.png)

公平锁：十分公平 先来后到

**非公平锁：十分不公平 可以插队（默认）**

```java
public class Test3 {
    public static void main(String[] args) {
        //并发 多个线程操作同一个资源类
        Ticket2 ticket=new Ticket2();
        new Thread(()->{ for (int i = 0; i < 20; i++) { ticket.sale(); } },"a").start();
        new Thread(()->{ for (int i = 0; i < 40; i++) { ticket.sale(); } },"b").start();
        new Thread(()->{ for (int i = 0; i < 60; i++) { ticket.sale(); } },"c").start();


    }
}

//Lock三部曲
//1.new ReentrantLock();
//2.lock.lock();//加锁
//3.finally->lock.unlock();//解锁
class Ticket2  {
    //属性、方法
    private int number=50;
    //卖票的方式
    Lock lock=new ReentrantLock();
    public void sale(){
        lock.lock();//加锁
        try {
            if (number>0){
                System.out.println(Thread.currentThread().getName()+"卖出了"+number--+"票，剩余"+number);
            }
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }

    }
}
```

## Synchronized和Lock区别

1.Synchronized内置的java关键字，Lock是一个java类

2.Synchronized无法判断获取锁的状态，Lock可以判断是否获得了锁

3.Synchronized会自动释放锁，lock必须要手动释放锁！然后不释放锁，就是**死锁**

4.Synchronized线程1（获得锁、阻塞）、线程2（等待，一直等）；Lock就不一定会等待下去；lock.trylock

5.Synchronized可重入锁，不可以中断，非公平；Lock，可重入锁，可以判断锁，非公平（可以自己设置）

6.Synchronized适合锁少量的代码同步问题，Lock适合锁大量的代码



**锁是什么，如何判断锁的是谁！**

# 4、生产者和消费者问题

Synchronized wait notify

面试的：单例模式、排序算法、生产者和消费者、死锁

**生产者和消费者问题Synchronized**

```java
package JUC;
//线程之间的通信问题：生产者和消费者问题！ 等待唤醒，通知唤醒
//线程交替执行 A B操作同一个变量 num=0
//A num+1
//B num-1
public class Test4 {
    public static void main(String[] args) {
        Data data=new Data();
        new Thread(()->{
            try {
                for (int i = 0; i < 10; i++) {
                    data.increment();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"A").start();
        new Thread(()->{
            try {
                for (int i = 0; i < 10; i++) {
                    data.decrement();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"B").start();
    }
}
class Data{
    //数字 资源类
    private int number=0;
    //+1
    public synchronized void increment() throws InterruptedException {
        if (number!=0){
            //等待
            this.wait();
        }
        number++;
        System.out.println(Thread.currentThread().getName()+"=>"+number);
        this.notifyAll();
//        通知其他线程，我+1完毕了
    }
    //-1
    public synchronized void decrement() throws InterruptedException {
        if (number==0){
            //等待
            this.wait();
        }
        number--;
        System.out.println(Thread.currentThread().getName()+"=>"+number);
        this.notifyAll();
        //通知其他线程，我-1完毕了

    }
}
```

问题存在，ABCD4个线程！产生虚假唤醒

![image-20210302213539050](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210302213539050.png)

  **等待应该总是出现在循环中**

将if改成while

```java
package JUC;
//线程之间的通信问题：生产者和消费者问题！ 等待唤醒，通知唤醒
//线程交替执行 A B操作同一个变量 num=0
//A num+1
//B num-1
public class Test4 {
    public static void main(String[] args) {
        Data data=new Data();
        new Thread(()->{
            try {
                for (int i = 0; i < 10; i++) {
                    data.increment();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"A").start();
        new Thread(()->{
            try {
                for (int i = 0; i < 10; i++) {
                    data.decrement();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"B").start();
        new Thread(()->{
            try {
                for (int i = 0; i < 10; i++) {
                    data.increment();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"C").start();
        new Thread(()->{
            try {
                for (int i = 0; i < 10; i++) {
                    data.decrement();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"D").start();
    }
}

class Data{
    //数字 资源类
    private int number=0;
    //+1
    public synchronized void increment() throws InterruptedException {
        while (number!=0){
            //等待
            this.wait();
        }
        number++;
        System.out.println(Thread.currentThread().getName()+"=>"+number);
        this.notifyAll();
//        通知其他线程，我+1完毕了
    }
    //-1
    public synchronized void decrement() throws InterruptedException {
        while (number==0){
            //等待
            this.wait();
        }
        number--;
        System.out.println(Thread.currentThread().getName()+"=>"+number);
        this.notifyAll();
        //通知其他线程，我-1完毕了
    }
}
```

JUC的生产者与消费者问题

通过Lock可以找到Condition

![image-20210302214443106](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210302214443106.png)

代码 实现：

```java
package JUC;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

//线程之间的通信问题：生产者和消费者问题！ 等待唤醒，通知唤醒
//线程交替执行 A B操作同一个变量 num=0
//A num+1
//B num-1
public class Test5 {
    public static void main(String[] args) {
        Data2 data2 = new Data2();
        new Thread(()->{ for (int i = 0; i < 10; i++) { try { data2.increment(); } catch (InterruptedException e) { e.printStackTrace(); } } },"A").start();
        new Thread(()->{ for (int i = 0; i < 10; i++) { try { data2.decrement(); } catch (InterruptedException e) { e.printStackTrace(); } } },"B").start();
        new Thread(()->{ for (int i = 0; i < 10; i++) { try { data2.increment(); } catch (InterruptedException e) { e.printStackTrace(); } } },"C").start();
        new Thread(()->{ for (int i = 0; i < 10; i++) { try { data2.decrement(); } catch (InterruptedException e) { e.printStackTrace(); } } },"D").start();
    }
}

class Data2{
    //数字 资源类
    private int number=0;
    Lock lock=new ReentrantLock();
    Condition condition = lock.newCondition();
    //condition.await();
    //condition.signalAll();
    //+1
    public  void increment() throws InterruptedException {
        lock.lock();
        try {
            while (number!=0){
                //等待
                condition.await();
            }
            number++;
            System.out.println(Thread.currentThread().getName()+"=>"+number);
            condition.signalAll();
            // 通知其他线程，我+1完毕了
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }

    }
    //-1
    public  void decrement() throws InterruptedException {
        lock.lock();
        try {
            while (number==0){
                //等待
                condition.await();
            }
            number--;
            System.out.println(Thread.currentThread().getName()+"=>"+number);
            condition.signalAll();
            // 通知其他线程，我-1完毕了
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }

    }
}
```

**任何一个 新的技术绝对不是仅仅覆盖了原来的技术，他一定有优势和补充**

Condition 精准的通知和唤醒线程



代码测试：

```java
package JUC;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
//A执行完 调用B B执行完调用C C执行完调用D
public class Test6 {
    public static void main(String[] args) {
        Data3 data3 = new Data3();
        new Thread(()->{ for (int i = 0; i < 20; i++) { data3.printA(); } },"A").start();
        new Thread(()->{ for (int i = 0; i < 20; i++) { data3.printB(); } },"B").start();
        new Thread(()->{ for (int i = 0; i < 20; i++) { data3.printC(); } },"C").start();
    }
}
//资源类
class Data3{

    private Lock lock=new ReentrantLock();
    private Condition condition1 = lock.newCondition();
    private Condition condition2 = lock.newCondition();
    private Condition condition3 = lock.newCondition();
    private int number=1;
    public void printA(){
        lock.lock();
        try {
            //业务，判断-> 执行-> 通知
                while (number!=1){
                    //等待
                    condition1.await();
                }
            System.out.println(Thread.currentThread().getName()+"=>AAAA");
            //唤醒，唤醒指定的人，B
            number=2;
            condition2.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
    public void printB(){
        lock.lock();
        try {
            //业务，判断-> 执行-> 通知
            while (number!=2){
                condition2.await();
            }
            System.out.println(Thread.currentThread().getName()+"=>BBBBB");
            number=3;
            condition3.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
    public void printC(){
        lock.lock();
        try {
            //业务，判断-> 执行-> 通知
            while (number!=3){
                condition3.await();
            }
            System.out.println(Thread.currentThread().getName()+"=>CCCCC");
            number=1;
            condition1.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
    //生产线： 下单->支付->交易->物流
}
```

# 5、8锁现象

如何判断锁的是谁！永远的知道什么锁，锁到底锁的是谁！

对象，class

**深刻理解我们的锁**

小结

new this 具体的一个对象

static 	Class的唯一的一个模板



# 6、集合类不安全

**List不安全**

并发

```java
package JUC.UNSAFE;


import java.util.*;
import java.util.concurrent.CopyOnWriteArrayList;

//java.util.ConcurrentModificationException
public class ListTest {
    public static void main(String[] args) {
//        List<String> list= Arrays.asList("1","2","3");
//        list.forEach(System.out::println);
//        单线程十分的安全
//        //并发下ArrayList是不安全的
//        List<String> list = new ArrayList<>();
//        for (int i = 0; i < 100; i++) {
//            new Thread(()->{list.add(UUID.randomUUID().toString().substring(0,5));System.out.println(list);},String.valueOf(i)).start();
//        }
//        解决方案：
//        1、List<String> list = new Vector<>();
//        2、List<String> list = Collections.synchronizedList(new ArrayList<>());
//        3、List<String> list = new CopyOnWriteArrayList<>();
//        CopyOnWrite 写入时复制 COW 计算机程序设计领域的一种优化策略；
//        多线程调用的时候， 比如同时使用list，读取的时候，固定的，写入（覆盖） 该怎么解决
//        在写入的时候 不仅写入 而且复制一份 最后再整合
//        在写入的时候避免覆盖造成数据问题
//        读写分离
//        CopyOnWriteArrayList 比 Vector 厉害的地方
//        Vector 使用了synchronized方法
//        CopyOnWriteArrayList 使用了 lock 方法


        List<String> list = new CopyOnWriteArrayList<>();

        for (int i = 0; i < 100; i++) {
            new Thread(()->{list.add(UUID.randomUUID().toString().substring(0,5));System.out.println(list);},String.valueOf(i)).start();
        }
    }
}
```

学习方法：1、先会用	2、货比三家，寻找其他的解决方案	3、分析源码

collection的实现类 list set	 **blockingquene**

Set不安全

```java
package JUC.UNSAFE;

import java.util.*;
import java.util.concurrent.CopyOnWriteArraySet;

//java.util.ConcurrentModificationException
//1、Set<String> set = Collections.synchronizedSet(new HashSet<>());
//2、Set<String> set = new CopyOnWriteArraySet<>();
public class SETTEST {
    public static void main(String[] args) {
//        Set<String> set = new HashSet<>();
//        Set<String> set = Collections.synchronizedSet(new HashSet<>());
        Set<String> set = new CopyOnWriteArraySet<>();
        for (int i = 0; i < 100; i++) {
            new Thread(()->{set.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(set);},String.valueOf(i)).start();
        }
    }
}
```

HashSet底层是什么？

```java
public HashSet() {
    map = new HashMap<>();
}
//add set的本质就是map key 是无法重复的
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
    private static final Object PRESENT = new Object();//不变的值 
```

HashMap

```java
package JUC.UNSAFE;

import java.util.Collections;
import java.util.HashMap;
import java.util.Map;
import java.util.UUID;
import java.util.concurrent.ConcurrentHashMap;

public class MAPTEST {
    public static void main(String[] args) {
        //MAP 是这样用的吗？ 默认等价于什么？
//        Map<String, String> map = new HashMap<>();
        //加载因子loadFactor 默认0.75 初始容量initialCapacity 默认16
        //研究ConcurrentHashMap的原理
        Map<String, String> map = new ConcurrentHashMap<>();
        for (int i = 0; i < 100; i++) {
            new Thread(()->{
                map.put(Thread.currentThread().getName(), UUID.randomUUID().toString().substring(0,5));
                System.out.println(map);
            },String.valueOf(i)).start();
        }
    }
}
```

# 7、callable

1、callable可以有返回值

2、callable可以抛出异常

3、callable方法不同run/call

```java
package JUC.UNSAFE;

import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

//1、探究原理
//2、觉得自己
public class CALLABLETEST {
    public static void main(String[] args) throws ExecutionException, InterruptedException {

//      new Thread(new Runnable()).start();
//      new Thread(new FutureTask<V>()).start();
//      new Thread(new FutureTask<V>(callable)).start();
        new Thread().start();//启动callable
        MyThread myThread = new MyThread();
        FutureTask futureTask = new FutureTask(myThread);
        //适配类
        new Thread(futureTask,"A").start();

        String o = (String)futureTask.get();//获取callable的返回结果
        System.out.println(o);
    }
}

class MyThread implements Callable<String> {
    @Override
    public String call() throws Exception {
        System.out.println("ssws");
        return "123";
    }
}
```

细节：

1、有缓存

2、结果可能需要等待，会阻塞！

# 8、常用辅助类（必会）

CyclicBarrier:指定个数线程执行完毕再执行操作

Semaphore：同一时间只能有指定数量个得到线程

**8.1、CountDownLatch**

```java
package JUC.ADD;

import java.util.concurrent.CountDownLatch;

//计数器
public class CountDownLatchTEST {
    public static void main(String[] args) throws InterruptedException {
        //总数是6
        CountDownLatch countDownLatch = new CountDownLatch(6);
        for (int i = 0; i < 6; i++) {
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"gone");
                countDownLatch.countDown();},String.valueOf(i)).start();
        }
        countDownLatch.await();//等待计数器归零，再向下执行
        System.out.println("关门");
    }
}
```

原理

```java
countDownLatch.countDown();//数量-1
countDownLatch.await();//等待计数器归零，再向下执行;//等待计数器归零，再向下执行
```

每次有线程调用countdown（）数量-1，假设计数器变为0，countDownLatch.await()就会被唤醒 继续执行！

**8.2、CyclicBarrier**

加法计数器

```java
package JUC.ADD;

import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierTEST {
    public static void main(String[] args) {
//        集齐7颗龙珠召唤神龙
//        召唤龙珠的线程
        CyclicBarrier cyclicBarrier = new CyclicBarrier(7,()->{
            System.out.println("召唤成功");
        });
        for (int i = 0; i < 7; i++) {
            //lambda能操作到i吗 不能
            final int finalI = i;
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"收集"+finalI+"个龙珠");//默认是需要final的 但是 jdk1.8可以不写 jvm会默认加上去
                try {
                    cyclicBarrier.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (BrokenBarrierException e) {
                    e.printStackTrace();
                }
            }).start();
        }
    }
}
```

**8.3、Semaphore**

Semaphore：信号量

抢车位！

6车--三个停车位

```java
package JUC.ADD;

import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

public class SemaphoreTEST {
    public static void main(String[] args) {
        //线程数量：停车位！限流！
        Semaphore semaphore = new Semaphore(3);
        for (int i = 0; i < 6; i++) {
            new Thread(()->{
                //acquire()得到
                try {
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getName()+"抢到车位");
                    TimeUnit.SECONDS.sleep(1);
                    System.out.println(Thread.currentThread().getName()+"离开车位");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }finally {
                    semaphore.release();//release()释放
                }
                //release()释放
            },String.valueOf(i)).start();
        }
    }
}
```

原理：

semaphore.acquire();获得，假设如果已经满了 等待 等待被释放为止

semaphore.release();释放，会将当前的信号量释放+1，然后唤醒等待的线程！

作用：多个共享资源的互斥的使用！并发限制，控制最大的线程数！

# 9、读写锁

ReadWriteLock

读的时候可以多线程去读

写只能一个线程去写

volatile只能保证可见性不能保证原子性（同生同死）

读不加锁可能脏读

```java
package JUC.READWRITE;

import java.util.HashMap;
import java.util.Map;
import java.util.Timer;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

//独占锁(写锁)   一次只能被一个线程占有
//共享锁(读锁)   多个线程可以同时占有
//ReadWriteLock
//读和读   可以共存
//读和写   不可以共存
//写和写   不可以共存
public class ReadWriteLockTEST {
    public static void main(String[] args) {
        MyCacheLock myCache = new MyCacheLock();

        //写入
        for (int i = 0; i <5; i++) {
            int finalI = i;
            new Thread(()->{myCache.put(finalI+"",finalI+"");},String.valueOf(i)).start();
        }
        //获取
        for (int i = 0; i <5; i++) {
            int finalI = i;
            new Thread(()->{myCache.get(finalI+"");},String.valueOf(i)).start();
        }

    }
}

class MyCache{
    private volatile Map<String,Object> map=new HashMap<>();

    //存、写入的时候，只希望同时只有一个线程写
    public void put(String key,Object value){
        System.out.println(Thread.currentThread().getName()+"写入"+key);
        map.put(key,value);
        System.out.println(Thread.currentThread().getName()+"写入成功");
    }

    //取、读，所有人都可以去读
    public void get(String key){
        System.out.println(Thread.currentThread().getName()+"读取"+key);
        Object o=map.get(key);
        System.out.println(Thread.currentThread().getName()+"读取成功");
    }
}

class MyCacheLock{
    private volatile Map<String,Object> map=new HashMap<>();
    //读写锁，更加
    private ReadWriteLock readwriteLock=new ReentrantReadWriteLock();
    //存、写
    public void put(String key,Object value){
        readwriteLock.writeLock().lock();
        try {
            System.out.println(Thread.currentThread().getName()+"写入"+key);
            map.put(key,value);
            System.out.println(Thread.currentThread().getName()+"写入成功");
        } catch (Exception e) {
            e.printStackTrace();
        }finally {
            readwriteLock.writeLock().unlock();
        }
    }

    //取、读
    public void get(String key){
        readwriteLock.readLock().lock();
        try {
            System.out.println(Thread.currentThread().getName()+"读取"+key);
            Object o=map.get(key);
            System.out.println(Thread.currentThread().getName()+"读取成功");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            readwriteLock.readLock().unlock();
        }
    }
}
```

# 10、阻塞队列

阻塞

队列

写入：如果队列满了，就必须阻塞等待

取：如果队列是空的，必须阻塞等待生产

阻塞队列：

**BlockingQuene**



![image-20210303173030546](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210303173030546.png)

什么情况下我们会使用阻塞队列：多线程并发处理，线程池！

**学会使用队列**

添加 、移除

**四组API**

| 方式         | 抛出异常 | 不会抛出异常，有返回值 | 阻塞等待 | 超时等待  |
| ------------ | -------- | ---------------------- | -------- | --------- |
| 添加         | add      | offer()                | put()    | offer(,,) |
| 移除         | remove   | poll()                 | take()   | poll(,)   |
| 检测队首元素 | element  | peek                   | -        | -         |

1、抛出异常

2、不会抛出异常

3、阻塞等待

4、超时等待

```java
package JUC.BQ;

import java.util.List;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.TimeUnit;

public class BLOCKINGQUENE {
    public static void main(String[] args) throws InterruptedException {
//    test1();
//    test2();
//    test3();
//    test4();
    }
    //抛出异常
    public static void test1(){
//        队列的大小
        ArrayBlockingQueue BlockingQueue = new ArrayBlockingQueue<>(3);
        System.out.println(BlockingQueue.add("a"));
        System.out.println(BlockingQueue.add("b"));
        System.out.println(BlockingQueue.add("c"));
        System.out.println("====================");

        //java.lang.IllegalStateException: Queue full 队列满了
        //System.out.println(BlockingQueue.add("a"));

        System.out.println(BlockingQueue.remove());
        System.out.println(BlockingQueue.element());//查看队首元素是谁
        System.out.println(BlockingQueue.remove());
        System.out.println(BlockingQueue.remove());

        //java.util.NoSuchElementException 队列当中没有元素
        //System.out.println(BlockingQueue.remove());
    }
    //有返回值，没有异常
    public static void test2(){
        //队列大小
        ArrayBlockingQueue BlockingQueue = new ArrayBlockingQueue<>(3);

        System.out.println(BlockingQueue.offer("a"));
        System.out.println(BlockingQueue.offer("a"));
        System.out.println(BlockingQueue.offer("a"));

        System.out.println(BlockingQueue.offer("a"));//返回一个boolen值 不抛出异常

        System.out.println(BlockingQueue.poll());
        System.out.println(BlockingQueue.poll());
        System.out.println(BlockingQueue.poll());
        System.out.println(BlockingQueue.poll());//返回一个null 也不抛出异常！


    }
    //等待，阻塞（一直阻塞）
    public static void test3() throws InterruptedException {
        //队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);
        //一直阻塞
        blockingQueue.put("a");
        blockingQueue.put("a");
        blockingQueue.put("a");
        //blockingQueue.put("a");//队列没有位置了，就会一直阻塞
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());//没有这个元素，也会一直阻塞
    }
    //等待，阻塞（等待超时）
    public static void test4() throws InterruptedException {
        //队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);
        System.out.println(blockingQueue.offer("a"));
        System.out.println(blockingQueue.offer("a"));
        System.out.println(blockingQueue.offer("a"));
        System.out.println(blockingQueue.offer("a", 1,TimeUnit.SECONDS));//等待超过1秒就退出
        System.out.println("==========");
        System.out.println(blockingQueue.poll(1, TimeUnit.SECONDS));
        System.out.println(blockingQueue.poll(1, TimeUnit.SECONDS));
        System.out.println(blockingQueue.poll(1, TimeUnit.SECONDS));
        System.out.println(blockingQueue.poll(1, TimeUnit.SECONDS));
    }
}
```

SynchronousQueue同步队列

没有容量，

进去一个元素，必须取出来之后才能继续插入

```
package JUC.BQ;

import java.util.concurrent.BlockingQueue;
import java.util.concurrent.SynchronousQueue;
import java.util.concurrent.TimeUnit;

//同步队列
//和其他的BlockingQueue不一样，SynchronousQueue不存储元素
//put了一个元素，必须从里面先take出来，否则不能在put进去
public class SynchronousQueueTEST {
    public static void main(String[] args) throws InterruptedException {
        BlockingQueue<String> blockingQueue = new SynchronousQueue<>();//同步队列
        new Thread(()->{
            try {
                blockingQueue.put("1");
                System.out.println(Thread.currentThread().getName()+"put 1");
                blockingQueue.put("2");
                System.out.println(Thread.currentThread().getName()+"put 2");
                blockingQueue.put("3");
                System.out.println(Thread.currentThread().getName()+"put 3");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"T1").start();

        new Thread(()->{
            try {
                System.out.println(Thread.currentThread().getName()+"=>"+blockingQueue.take());
                System.out.println(Thread.currentThread().getName()+"=>"+blockingQueue.take());
                System.out.println(Thread.currentThread().getName()+"=>"+blockingQueue.take());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        },"T2").start();
    }
}
```

# 11、线程池（重点）

线程池：三大方法、7大参数、4种拒绝策略

**池化技术**

程序的运行，本质：占用系统的资源！优化资源的使用！

线程池，jdbc的连接池，内存池，对象池....

池化技术：开和关消耗资源 ，所以事先准备好一些资源，有人要用的时候，就来这里拿，用完之后还给我。



**线程池的好处：**

1、降低资源的消耗。

2、提高响应的速度。

3、方便管理。

**线程可以复用，可以控制最大并发数、管理线程**



线程池

```java
package JUC.POOL;


import java.util.concurrent.Executor;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

//Executors工具类、3大方法
public class POOLTEST {
    public static void main(String[] args) {
//        ExecutorService service = Executors.newSingleThreadExecutor();//单个线程
//        ExecutorService service = Executors.newFixedThreadPool(5);//创建一个固定的线程池的大小
        ExecutorService service = Executors.newCachedThreadPool();//可伸缩的，遇强则强，遇弱则弱
        try {
            for (int i = 0; i < 100; i++) {
                //使用了线程池之后，使用线程池来创建线程
                service.execute(()->{
                    System.out.println(Thread.currentThread().getName()+"=>OK");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池使用完，程序结束，关闭线程池
            service.shutdown();
        }

    }
}
```

7大参数

源码分析

```java
public static ExecutorService newSingleThreadExecutor() {
    return new FinalizableDelegatedExecutorService
        (new ThreadPoolExecutor(1, 1,
                                0L, TimeUnit.MILLISECONDS,
                                new LinkedBlockingQueue<Runnable>()));
}
    public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>());
    }
    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }
//本质：ThreadPoolExecutor
        public ThreadPoolExecutor(int corePoolSize,//核心线程池大小
                              int maximumPoolSize,//最大核心线程池大小
                              long keepAliveTime,//超时了 没有人调用就会释放
                              TimeUnit unit,//超时单位
                              BlockingQueue<Runnable> workQueue,//阻塞队列
                              ThreadFactory threadFactory,//线程工厂，创建线程的，一般不动
                              RejectedExecutionHandler handler//拒绝策略) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```

手动创建一个线程池



4种拒绝策略

![image-20210303194237315](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210303194237315.png)

```java
package JUC.POOL;


import java.util.concurrent.*;

//Executors工具类、3大方法
//new ThreadPoolExecutor.AbortPolicy());//银行满了，还有人进来，就不处理这个人，并且抛出异常。
//new ThreadPoolExecutor.CallerRunsPolicy());//哪来的去哪里 main
//new ThreadPoolExecutor.DiscardPolicy());//队列满了，丢掉任务，不会抛出异常！
//new ThreadPoolExecutor.DiscardOldestPolicy());//队列满了，尝试和最早的竞争
public class POOLTEST {
    public static void main(String[] args) {
//       ExecutorService service = Executors.newSingleThreadExecutor();//单个线程
//       ExecutorService service = Executors.newFixedThreadPool(5);//创建一个固定的线程池的大小
//       ExecutorService service = Executors.newCachedThreadPool();//可伸缩的，遇强则强，遇弱则弱
//        new ThreadPoolExecutor(
//                2,
//                5,
//                2,
//                TimeUnit.SECONDS,
//                new LinkedBlockingQueue<>(3),
//                Executors.defaultThreadFactory(),
//                new ThreadPoolExecutor.AbortPolicy());//银行满了，还有人进来，就不处理这个人，并且抛出异常。
//        ThreadPoolExecutor service = new ThreadPoolExecutor(
//                2,
//                5,
//                2,
//                TimeUnit.SECONDS,
//                new LinkedBlockingQueue<>(3),
//                Executors.defaultThreadFactory(),
//                new ThreadPoolExecutor.CallerRunsPolicy());//哪来的去哪里 main
//        ThreadPoolExecutor service = new ThreadPoolExecutor(
//                2,
//                5,
//                2,
//                TimeUnit.SECONDS,
//                new LinkedBlockingQueue<>(3),
//                Executors.defaultThreadFactory(),
//                new ThreadPoolExecutor.DiscardPolicy());//队列满了，丢掉任务，不会抛出异常！
        ThreadPoolExecutor service = new ThreadPoolExecutor(
                2,
                5,
                2,
                TimeUnit.SECONDS,
                new LinkedBlockingQueue<>(3),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.DiscardOldestPolicy());//队列满了，尝试和最早的竞争
        try {
            for (int i = 0; i < 100; i++) {
                //使用了线程池之后，使用线程池来创建线程
                service.execute(()->{
                    System.out.println(Thread.currentThread().getName()+"=>OK");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池使用完，程序结束，关闭线程池
            service.shutdown();
        }

    }
}
```

小结和拓展

最大线程到底该如何定义

1、CPU 密集型	几核，就是几，可以保持CPU的效率最高

2、IO 密集型 判断你的程序中十分耗IO的线程，只要大于这个数就可以 一般设置两倍

池的最大的大小该怎么设置

```java
package JUC.POOL;


import java.util.concurrent.*;

//Executors工具类、3大方法
//new ThreadPoolExecutor.AbortPolicy());//银行满了，还有人进来，就不处理这个人，并且抛出异常。
//new ThreadPoolExecutor.CallerRunsPolicy());//哪来的去哪里 main
//new ThreadPoolExecutor.DiscardPolicy());//队列满了，丢掉任务，不会抛出异常！
//new ThreadPoolExecutor.DiscardOldestPolicy());//队列满了，尝试和最早的竞争
public class POOLTEST {
    public static void main(String[] args) {
//        最大线程到底该如何定义
//        1、CPU 密集型    几核，就是几，可以保持CPU的效率最高
//        2、IO 密集型 判断你的程序中十分耗IO的线程，只要大于这个数就可以 一般设置两倍
//        程序 15个大型任务 io十分占用资源！
        //获取CPU的核数
        System.out.println(Runtime.getRuntime().availableProcessors());
        ThreadPoolExecutor service = new ThreadPoolExecutor(
                2,
                Runtime.getRuntime().availableProcessors(),
                2,
                TimeUnit.SECONDS,
                new LinkedBlockingQueue<>(3),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.DiscardOldestPolicy());//队列满了，尝试和最早的竞争
        try {
            for (int i = 0; i < 100; i++) {
                //使用了线程池之后，使用线程池来创建线程
                service.execute(()->{
                    System.out.println(Thread.currentThread().getName()+"=>OK");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池使用完，程序结束，关闭线程池
            service.shutdown();
        }

    }
}
```

# 12、四大函数式接口（重点必须掌握）

Consumer	Function	Predicate	Supplier

## **Function接口**

lambda表达式、链式编程、函数式接口、stream流式计算

函数式接口：只有一个方法的接口	例如Runable

```java
@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
//泛型、枚举、反射
//lambda表达式、链式编程、函数式接口、Steam流式计算
//超级多FunctionalInterface
//简化编程模型，在新版本的框架底层大量应用
//foreach（消费者类的函数式接口）
```

**代码测试：**

```java
package JUC.FUNCTION;

import java.util.function.Function;

//Function 函数型接口,有一个输入参数，有一个输出
//只要是函数式接口就可以用lambda表达式简化
public class FUNCTIONTEST {
    public static void main(String[] args) {
        //Function<T,R>传入参数T返回参数R

//        //工具类 输出传入的值
//        Function function = new Function<String,String>() {
//            @Override
//            public String apply(String s) {
//                return  s;
//            }
//        };
//        Function<String,String> function=(str)->{return str;};
//        Function function=(str)->{return str;};
        Function function=str->str;
        System.out.println(function.apply("sdadw"));
    }
}
```

## Predicate接口

只有一个输入参数，返回值为boolen值

```java
package JUC.INTERFACE;


import java.util.function.Predicate;

//断定型接口：有一个输入参数 返回值只能是BOOLEN值
public class PredicateTEST {
    public static void main(String[] args) {
        //判断字符串是否为空
//        Predicate<String> predicate = new Predicate<String>() {
//            @Override
//            public boolean test(String str) {
//                return str.isEmpty();
//            }
//        };
        Predicate<String> predicate=(str)->str.isEmpty();
        System.out.println(predicate.test(""));
    }
}
```

## Consumer接口

消费型接口

```java
package JUC.INTERFACE;

import java.util.function.Consumer;

//Consumer 消费型接口：只有输入，没有返回值

public class CONSUMERTEST {
    public static void main(String[] args) {
        //打印字符串
//        Consumer<String> consumer = new Consumer<String>() {
//            @Override
//            public void accept(String str) {
//                System.out.println(str);
//            }
//        };
        Consumer<String> consumer=(str)->{
            System.out.println(str);
        };
        consumer.accept("2232322");
    }

}
```

## Supplier接口

供给型接口

```java
package JUC.INTERFACE;

import java.util.function.Supplier;

//Supplier 供给型接口:没有参数 只有返回值
public class SUPPLIERTEST {
    public static void main(String[] args) {
//        Supplier<String> supplier = new Supplier<>() {
//            @Override
//            public String get() {
//                return "GET";
//            }
//        };
        Supplier<String> supplier=()-> "GET";
        System.out.println(supplier.get());
    }
}
```

# 13、Stream流式计算

什么是Stream流式计算

大数据：存储+计算

集合、MySQL 本质就是存储东西的；

计算都应该交给流来做！

```java
package JUC.STREAM;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Locale;

//现在有五个用户！筛选：
//1、ID必须是偶数
//2、年龄必须大于23岁
//3、用户名转为大写字母
//4、用户名字母倒着排序
//5、只输出一个用户！
public class TEST {
    public static void main(String[] args) {
        USER user1 = new USER(1, "a", 21);
        USER user2 = new USER(2, "b", 22);
        USER user3 = new USER(3, "c", 23);
        USER user4 = new USER(4, "d", 24);
        USER user5 = new USER(6, "e", 25);
        //集合就是存储
        List<USER> list=Arrays.asList(user1, user2, user3, user4, user5);

        //计算交给Stream流
        //lambda表达式、链式编程、函数式接口、stream流式计算
        list.stream()
                .filter(u->{return u.getId()%2==0;})
                .filter(u->{return u.getAge()>23;})
                .map(user -> {return user.getName().toUpperCase();})
                .sorted((x1,x2)->{return x2.compareTo(x1);})
                .limit(1)
                .forEach(System.out::println);
    }
}
```

## 14、Forkjoin

分支合并

并行执行任务！提高效率。大数据量

大数据：Map Reduce（把大任务拆分成小任务）

Forkjoin特点：工作窃取

一个线程执行完成之后，会帮助其他线程完成。

这个里面维护的都是双端队列 为了方便窃取

Forkjoin

```java
package JUC.FORKJOIN;

import java.util.concurrent.RecursiveTask;

//求和计算任务！
//3 6FockJoin 9Stream并行流
//如何使用forkjoin
//1、forkjoinPool通过它来执行
//2、计算任务   forkJoinPool.execute(ForkJoinTask task);
//3、计算类要继承ForkJoinTask

public class FOCKJOINTEST extends RecursiveTask<Long> {
    private long start;
    private long end;

    //临界值
    private long temp=10000L;

    public FOCKJOINTEST(long start, long end) {
        this.start = start;//1
        this.end = end;//2000000000
    }

    //计算方法
    @Override
    protected Long compute() {
        if ((end-start)<temp){
            Long sum=0L;
            for (long i = start; i < end; i++) {
                sum+=i;
            }
            return sum;
        }else {
            //分支合并计算
            long middle = (start + end) / 2;//中间值
            FOCKJOINTEST fockjointest1 = new FOCKJOINTEST(start, middle);
            fockjointest1.fork();//拆分任务，把任务压入线程队列
            FOCKJOINTEST fockjointest2 = new FOCKJOINTEST(middle+1, end);
            fockjointest2.fork();//拆分任务，把任务压入线程队列
            return fockjointest1.join()+fockjointest2.join();
        }
    }
}
```

```java
package JUC.FORKJOIN;


import java.util.concurrent.ExecutionException;
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.ForkJoinTask;
import java.util.stream.LongStream;

public class TEST {
    public static void main(String[] args) {

            test3();

    }

    //普通程序员
    public static void test1(){
        Long sum=0L;
        long start=System.currentTimeMillis();
        for (Long i = 1L; i <= 10_0000_0000; i++) {
            sum+=i;
        }
        long end=System.currentTimeMillis();
        System.out.println("sum="+sum+"时间："+(end-start));
    }

    //会用ForkJoin
    public static void test2() throws ExecutionException, InterruptedException {
        long start=System.currentTimeMillis();
        ForkJoinPool forkJoinPool = new ForkJoinPool();
        ForkJoinTask<Long> test = new FOCKJOINTEST(0L, 10_0000_0000L);
        ForkJoinTask<Long> submit = forkJoinPool.submit(test);//提交任务
        Long sum = submit.get();
        long end=System.currentTimeMillis();
        System.out.println("sum="+sum+"时间："+(end-start));
    }

    //会Steam并行流
    public static void test3(){
        long start=System.currentTimeMillis();
        //range表示() 左右都不包含
        //rangeClosed表示(] 右包含
        long sum = LongStream.rangeClosed(0L, 10_0000_0000L).parallel().reduce(0, Long::sum);
        long end=System.currentTimeMillis();
        System.out.println("sum="+sum+"时间："+(end-start));
    }
}
```

## 15、异步回调

Future设计的初衷：对将来的某个时间的结果进行建模

```java
package JUC.FUTURE;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.Future;
import java.util.concurrent.TimeUnit;

//异步调用CompletableFuture
//成功回调
//失败回调
public class FUTURETEST {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
//        //发起一个请求 没有返回值的异步回调
//        CompletableFuture<Void> future = CompletableFuture.runAsync(()->{
//            try {
//                TimeUnit.SECONDS.sleep(1);
//            } catch (InterruptedException e) {
//                e.printStackTrace();
//            }finally {
//                System.out.println(Thread.currentThread().getName()+"sync");
//            }
//        });
//
//        future.get();//获取执行结果
        //有返回值的异步回调
        //ajax,成功和失败的回调
        //失败返回的是错误信息
        CompletableFuture<Integer> future = CompletableFuture.supplyAsync(()->{
            System.out.println(Thread.currentThread().getName()+"work");
            int i=10/0;
            return 1;
        });
        System.out.println(future.whenComplete((u, y) -> {
            System.out.println("t=>"+u);//正常的返回结果
            System.out.println("y=>"+y);//错误的信息java.util.concurrent.CompletionException: java.lang.ArithmeticException: / by zero
        }).exceptionally((e) -> {
            System.out.println(e.getMessage());
            return 233;//可以获取到错误的返回结果
        }).get());
        //sucess code 200
        //error code 404 500
    }
}
```

异步任务

## 16、JMM

请你探探你对volatile的理解

volatile是java虚拟机提供的**轻量级的同步机制**

1、保证可见性

2、不保证原子性

3、禁止指令重排



**JMM**

什么是JMM

JVM：java虚拟机

JMM：java内存模型 不存在的东西 概念 约定

关于JMM的一些同步 的约定：

1、线程解锁前，必须把共享表量**立刻**刷回主存。volatile干的事（MESI缓存一致性协议）

2、线程加锁前，必须读取主存中的最新值到工作内存中!

3、加锁和解锁是同一把锁

volatile标注的共享变量被修改之后，线程会重新读取

线程 **工作内存、主内存**

8种操作

主存 -> read -> 缓存 -> load -> 工作内存 -> use -> 执行引擎 -> assign -> 工作内存 -> store -> 缓存 -> write -> 主存

还有lock和unlock

![image-20210305095722578](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210305095722578.png)

![image-20210305095910529](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210305095910529.png)

## 内存交互操作

 　**内存交互操作有8种，虚拟机实现必须保证每一个操作都是原子的，不可在分的（对于double和long类型的变量来说，load、store、read和write操作在某些平台上允许例外）**

- lock   （锁定）：作用于主内存的变量，把一个变量标识为线程独占状态

- unlock （解锁）：作用于主内存的变量，它把一个处于锁定状态的变量释放出来，释放后的变量才可以被其他线程锁定
- read  （读取）：作用于主内存变量，它把一个变量的值从主内存传输到线程的工作内存中，以便随后的load动作使用
- load   （载入）：作用于工作内存的变量，它把read操作从主存中变量放入工作内存中
- use   （使用）：作用于工作内存中的变量，它把工作内存中的变量传输给执行引擎，每当虚拟机遇到一个需要使用到变量的值，就会使用到这个指令
- assign （赋值）：作用于工作内存中的变量，它把一个从执行引擎中接受到的值放入工作内存的变量副本中
- store  （存储）：作用于主内存中的变量，它把一个从工作内存中一个变量的值传送到主内存中，以便后续的write使用
- write 　（写入）：作用于主内存中的变量，它把store操作从工作内存中得到的变量的值放入主内存的变量中

　　**JMM对这八种指令的使用，制定了如下规则：**

- 不允许read和load、store和write操作之一单独出现。即使用了read必须load，使用了store必须write

- 不允许线程丢弃他最近的assign操作，即工作变量的数据改变了之后，必须告知主存

- 不允许一个线程将没有assign的数据从工作内存同步回主内存

- 一个新的变量必须在主内存中诞生，不允许工作内存直接使用一个未被初始化的变量。就是怼变量实施use、store操作之前，必须经过assign和load操作

- 一个变量同一时间只有一个线程能对其进行lock。多次lock后，必须执行相同次数的unlock才能解锁

- 如果对一个变量进行lock操作，会清空所有工作内存中此变量的值，在执行引擎使用这个变量前，必须重新load或assign操作初始化变量的值

- 如果一个变量没有被lock，就不能对其进行unlock操作。也不能unlock一个被其他线程锁住的变量

- 对一个变量进行unlock操作之前，必须把此变量同步回主内存

  程序不知道主内存的值已经发生变化了

## 17、Volatile

1、保证可见性

```java
package JUC.VOLATILE;

import java.util.concurrent.TimeUnit;

public class JMMTEST {
    //不加volatile程序就会死循环！
    //加volatile可以保证可见性
    private static volatile int num=0;
    public static void main(String[] args) {
        new Thread(()->{//线程1 对主内存的变化不知道
            while (num==0){

            }
        }).start();
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        num=1;
        System.out.println(num);
    }
}
```

2、不保证原子性

原子性：ACID原则 不可分割

线程A在执行任务的时候，不能被打扰，也不能被分割。

要么同时成功，要么同时失败。

```java
package JUC.VOLATILE;

//不保证原子性
public class VOLATILETEST2 {

    //不保证原子性
    private volatile static int num=0;

    public  static void add(){
        num++;
    }
    public static void main(String[] args) {
        //理论上结果应该为20000
        for (int i = 0; i < 20; i++) {
            new Thread(()->{
                for (int j = 0; j < 1000; j++) {
                    add();
                }
            }).start();
        }
        while (Thread.activeCount()>2){
            //main gc
            Thread.yield();
        }
        System.out.println(Thread.currentThread().getName()+num);

    }
}
```

如果不加lock和synchronized，怎么样保证原子性

![image-20210305103119503](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210305103119503.png)

使用原子类，解决原子性问题

![image-20210305103150209](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210305103150209.png)

原子类为什么这么高级

```java
package JUC.VOLATILE;

import java.util.concurrent.atomic.AtomicInteger;

//不保证原子性
public class VOLATILETEST2 {

    //volatile 不保证原子性
    //原子类的 int
    private volatile static AtomicInteger num=new AtomicInteger();

    public  static void add(){
        //num++;//不是一个原子性操作
        num.getAndIncrement( );//AtomicInteger的加一方法 CAS
    }
    public static void main(String[] args) {
        //理论上结果应该为20000
        for (int i = 0; i < 20; i++) {
            new Thread(()->{
                for (int j = 0; j < 1000; j++) {
                    add();
                }
            }).start();
        }
        while (Thread.activeCount()>2){
            //main gc
            Thread.yield();
        }
        System.out.println(Thread.currentThread().getName()+num);

    }
}
```

这些类的底层都是直接和操作系统挂钩！

在内存中修改值！

Unsafe类是一个很特殊的存在！

**指令重排**

什么是指令重排：

你写的程序，计算机并不是按照你写的那样去执行的。

源代码-->编译器优化的重排-->指令并行也可能会重排-->执行 

处理器在进行指令重排的时候，考虑：数据之间的依赖性！

```java
int x = 1;//1
int y = 2;//2
x = x + 5;//3
y = x * x;//4
我们所期望的是：1234 但是可能执行的时候会变成：2134 1324
可不可能是  4123！
```

可能造成影响的结果

 假设a b x y

| 线程a | 线程b |
| ----- | ----- |
| x=a   | y=b   |
| b=1   | a=2   |

正常的结果X=0,Y=0  但是可能由于指令重排

| 线程a | 线程b |
| ----- | ----- |
| b=1   | a=2   |
| x=a   | y=b   |

异常的结果X=2，Y=1



**非计算机专业**

**volatile可以避免指令重排：**

内存屏障。CPU指令。作用：

1、保证特定的操作的执行顺序

2、可以保证某些变量的内存可见性（利用这些特性、就可以保证volatile实现了可见性）

![image-20210305110201499](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210305110201499.png)



volatile是可以保持可见性。不能保证原子性，由于内存屏障，可以保证避免指令重排的现象产生！

## 18、彻底玩转单例模式

饿汉式 	DCL懒汉式

```java
package JUC.SINGLE;

//饿汉式单例子
public class HUNGRY {

    //可能会浪费空间
    private byte[] data1=new byte[1024*1024];
    private byte[] data2=new byte[1024*1024];
    private byte[] data3=new byte[1024*1024];
    private byte[] data4=new byte[1024*1024];

    private HUNGRY(){

    }
    private final static HUNGRY hungry=new HUNGRY();

    public static HUNGRY main(String[] args) {
        return hungry;
    }
}
```

DCL懒汉式

```java
package JUC.SINGLE;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;

//懒汉式单例
//道高一尺魔高一丈！
public class LAZYMAN {

    private static boolean flag=false;

    private LAZYMAN() {
        synchronized (LAZYMAN.class){
            if (flag==false){
                flag=true;
            }
            else {
                throw new RuntimeException("不要试图使用反射");
            }
        }
        System.out.println(Thread.currentThread().getName()+"ok");
    }

    private volatile static LAZYMAN lazyman;

    //双重检测锁模式 懒汉式单例 DCL懒汉式
    public static LAZYMAN getInstance(){
        //加锁
        if (lazyman==null){
            synchronized (LAZYMAN.class){
                if (lazyman==null){
                    lazyman=new LAZYMAN();//不是原子性操作
                    //1、分配内存空间
                    //2、执行构造方法，初始化对象
                    //3、把这个对象指向这个空间
                }
            }
        }
        return lazyman;//此时lazyman还没有完成构造
    }

//    //多线程并发
//    public static void main(String[] args) {
//        for (int i = 0; i < 10; i++) {
//            new Thread(()->{lazyman.getInstance();}).start();
//        }
//    }
    //反射！
    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException, NoSuchFieldException {
//        LAZYMAN instance = LAZYMAN.getInstance();
        Field flag = LAZYMAN.class.getDeclaredField("flag");
        flag.setAccessible(true);
        Constructor<LAZYMAN> declaredConstructor = LAZYMAN.class.getDeclaredConstructor(null);
        declaredConstructor.setAccessible(true);
        LAZYMAN lazyman1 = declaredConstructor.newInstance();
        flag.set(lazyman1,false);
        LAZYMAN lazyman2 = declaredConstructor.newInstance();
        System.out.println(lazyman1);
        System.out.println(lazyman2);
    }
}
```

静态内部类

```java
package JUC.SINGLE;

//静态内部类
public class HOLDER {
    private HOLDER() {
    }

    public static  class InnerClass{
        private static final HOLDER holder=new HOLDER();
    }
}
```

单例不安全，因为有反射

枚举

```java
package JUC.SINGLE;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

//enum是一个什么？ 本身也是一个class的类
public enum ENUMSINGLE {
    INSTANCE;

    private ENUMSINGLE() {
    }

    @Override
    public String toString() {
        return "ENUMSINGLE{}";
    }

    public ENUMSINGLE getInstance(){
        return INSTANCE;
    }

}
class test{
    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        ENUMSINGLE instance1 = ENUMSINGLE.INSTANCE;
//        Constructor<ENUMSINGLE> declaredConstructor = ENUMSINGLE.class.getDeclaredConstructor(String.class,int.class);
        Constructor<?>[] declaredConstructors = ENUMSINGLE.class.getDeclaredConstructors();
//        declaredConstructor.setAccessible(true);
//        ENUMSINGLE instance2 = declaredConstructor.newInstance();
        //java.lang.NoSuchMethodException: JUC.SINGLE.ENUMSINGLE.<init>()
        System.out.println(declaredConstructors.toString());

    }
}
```

枚举没有无参构造，只有有参构造，而且枚举天生单例。

枚举类型的最终反编译源码；



## 19、深入理解CAS

UNSAFE

什么是CAS

大厂必须要深入研究底层！有所突破！

**修内功！操作系统，计算机网络原理！**

UNsafe相当于java的后面，可以通过这个类调用native操作内存

![image-20210306152313865](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210306152313865.png)

CAS：比较当然工作内存中的值，如果这个值是期望的，那么则执行操作！如果不是就一直循环！

缺点：

1、由于底层是自旋锁循环会耗时

2、一次性只能保证一个共享变量的原子性

3、会存在ABA问题



**CAS:ABA问题（狸猫换太子）**

![image-20210306153002034](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210306153002034.png)

```java
package JUC.CAS;

import java.util.concurrent.atomic.AtomicInteger;

public class CAS1 {

    //CAS compareAndExchange
    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger(2020);
        //对于我们平时写的SQL:乐观锁！
        //期望、更新
        //public final boolean compareAndSet(int expectedValue, int newValue)
        //如果我期望的值达到了，那么就更新，否则，就不更新
        //捣乱的线程
        atomicInteger.compareAndSet(2020,2021);
        System.out.println(atomicInteger.get());
        atomicInteger.compareAndSet(2021,2020);
        System.out.println(atomicInteger.get());
        //期望的线程
        atomicInteger.compareAndSet(2020,6666);
        System.out.println(atomicInteger.get());

    }
}
```



## **20、原子引用**

解决ABA问题，主需要引入原子引用！对应的思想：乐观锁

带版本号的原子操作

**注意**

**Integer使用了对象缓存机制，默认范围是-128~127，推荐使用静态工厂方法valueof获取对象实例，而不是new，因为valueof缓存，而new一定会创建新的对象分配新的内存空间；**

```java
package JUC.CAS;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicInteger;
import java.util.concurrent.atomic.AtomicStampedReference;

public class CAS1 {

    //CAS compareAndExchange
    public static void main(String[] args) {
//        AtomicInteger atomicInteger = new AtomicInteger(2020);
        //AtomicStampedReference注意，如果泛型是包装类，要注意对象引用问题
        //蒸菜子啊业务操作，这里面比较的都是一个个对象
        AtomicStampedReference<Integer> atomicInteger = new AtomicStampedReference<>(1,1);
        //对于我们平时写的SQL:乐观锁！
        //期望、更新
        //public final boolean compareAndSet(int expectedValue, int newValue)
        //如果我期望的值达到了，那么就更新，否则，就不更新
        //乐观锁的原理
        new Thread(()->{
            int stamp = atomicInteger.getStamp();//获得版本号
            System.out.println("a1=>"+stamp);
            try {
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            //Version+1
            System.out.println(atomicInteger.compareAndSet(1, 2, atomicInteger.getStamp(), atomicInteger.getStamp() + 1));
            System.out.println("a2=>"+atomicInteger.getStamp());
            System.out.println(atomicInteger.compareAndSet(2, 1, atomicInteger.getStamp(), atomicInteger.getStamp() + 1));
            System.out.println("a3=>"+atomicInteger.getStamp());
        },"a").start();

        new Thread(()->{
            int stamp = atomicInteger.getStamp();//获得版本号
            System.out.println("b1=>"+stamp);

            try {
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(atomicInteger.compareAndSet(1, 6, atomicInteger.getStamp(), atomicInteger.getStamp() + 1));
            System.out.println("b2=>"+atomicInteger.getStamp());
        },"b").start();
        //期望的线程


    }
}
```

## 21、各种锁的理解

### 1、公平锁、非公平锁

公平锁：非常公平，不能插队，必须先来后到！

非公平锁：非常不公平，可以插队，（默认都是非公平的）

synchronized

```java
package JUC.LOCK;

//synchronized
public class LOCK1 {
    public static void main(String[] args) {
        Phone phone = new Phone();
        new Thread(()->{phone.sms();},"A").start();
        new Thread(()->{phone.sms();},"B").start();
    }
}

class Phone{
    public synchronized void sms(){
        System.out.println(Thread.currentThread().getName()+"sms");
        call();
    }
    private synchronized void call(){
        System.out.println(Thread.currentThread().getName()+"call");
    }
}
```



### 2、可重入锁

可重入锁(递归锁)

lock

```java
package JUC.LOCK;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

//synchronized
public class LOCK2 {
    public static void main(String[] args) {
        Phone2 phone = new Phone2();
        new Thread(()->{phone.sms();},"A").start();
        new Thread(()->{phone.sms();},"B").start();
    }
}

class Phone2{
    Lock lock=new ReentrantLock();
    public  void sms(){
        lock.lock();//细节问题
        //lock锁必须配对，否则会死锁
        try {
            System.out.println(Thread.currentThread().getName()+"sms");
            call();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    private  void call(){
        lock.lock();
        try {
            System.out.println(Thread.currentThread().getName()+"call");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}
```



### 3、自旋锁

spinlock

```java
package JUC.LOCK;

import java.util.concurrent.atomic.AtomicReference;

/*
* 自旋锁
* */
public class SPINLOCK {

    //int 0
    //Thread null
    AtomicReference<Thread> reference = new AtomicReference<>();

    //加锁
    public void mylock(){
        Thread thread = Thread.currentThread();
        System.out.println(Thread.currentThread().getName()+"=>mylock");
        //自旋锁
        while (!reference.compareAndSet(null,thread)){

        }
    }

    //解锁
    public void myunlock(){
        Thread thread = Thread.currentThread();
        System.out.println(Thread.currentThread().getName()+"=>myunlock");
        //解锁
        reference.compareAndSet(thread,null);
    }
}
```



### 4、死锁

死锁是什么

![image-20210306162839285](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210306162839285.png)

```java
package JUC.LOCK;


import java.util.concurrent.TimeUnit;

public class DEADLOCK {
    public static void main(String[] args) {
        String A="LOCKA";
        String B="LOCKB";

        new Thread(new MyThread(A,B),"A").start();
        new Thread(new MyThread(B,A),"B").start();


    }
}

class MyThread implements Runnable{
    private String lockA;
    private String lockB;

    public MyThread(String lockA, String lockB) {
        this.lockA = lockA;
        this.lockB = lockB;
    }

    @Override
    public void run() {
        synchronized (lockA){
            System.out.println(Thread.currentThread().getName()+"GETA"+lockA+"=>getB");
            try {
                TimeUnit.SECONDS.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (lockB){
                System.out.println(Thread.currentThread().getName()+"GETB"+lockA+"=>getA");
            }
        }
    }
}
```

解决问题

1、使用**JPS -l**定位进程号

2、使用**jstack**进程号找到死锁问题

面试，工作中！排查问题

1、日志

2、堆栈

