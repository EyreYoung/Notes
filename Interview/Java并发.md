# Java并发

## 进程和线程？

### 进程

- 进程是代码在数据集合上的一次运行活动
- 系统进行资源分配和调度的基本单位

### 线程

- 进程中的一个实体，本身不会独立存在
- 进程的一个执行路径，一个进程中至少有一个线程
- 进程中多个线程共享进程的资源
- CPU分配的基本单位

### 进程与线程关系

- Java中启动main函数就启动了一个JVM的进程，main函数所在的线程就是这个进程中的一个线程（主线程）
- 一个进程中有多个线程，多个线程共享进程的堆和方法区资源
- 每个线程有自己的栈区域和程序计数器
- **本质区别**：**是否单独占有内存地址空间和其他系统资源**（比如IO）
  - 进程单独占有一定的内存地址空间，所以进程间存在内存隔离，数据分开，数据共享复杂但是同步简单
  - 线程共享所属进程的内存地址空间和资源，数据共享简单但是同步复杂
  - 进程单独占有内存地址空间，一个进程出现问题不会影响其他进程，可靠性高
  - 线程崩溃可能影响整个程序的稳定性，可靠性高
  - 进程的创建和销毁要保存寄存器和栈信息，需要资源的分配回收和页调度，开销大
  - 线程只需保存寄存器和栈信息，开销小
  - **线程是操作系统进行资源分配的基本单位，线程是操作系统进行调度的基本单位（CPU分配时间）**

### 为什么要使用多线程

- 进程间通信比较复杂，线程间通信比较简单，共享资源在线程之间通信比较容易

## 线程的生命周期和状态？

- **New 初始状态**：线程被构建，但还没有调用 `start()` 方法
- **Runnable 运行状态**：Java将操作系统中就绪和运行两个状态叫做 运行中
- **Blocked 阻塞状态**：线程阻塞于锁
- **Waiting 等待状态**：线程需要等待其他线程做一些特定动作，通知或者中断
- **Time_Waiting 超时等待状态**：不同于Waiting，可以在指定时间自行返回
- **Terminated 终止状态**：线程执行完毕

![](img/Java线程状态变化.png)

- 线程创建后处于**New 初始状态**，调用start()方法后开始运行，进入**Ready 就绪状态**
- 就绪状态的线程获得CPU时间片后处于**Runnable 运行状态**
- 线程执行wait()方法后，进入**Waiting 等待状态**，需要依靠其他线程通知才能回到**运行状态**
- **Time_Waiting 超时等待状态**可以通过 `sleep(long millis)` 或 `wait(long millis)` 方法进入，时间到达后线程会返回**Runnable状态**
- 线程调用同步方法时，如果没有获取到锁，线程进入**Blocked 阻塞状态**
- 线程执行 `Runnable` 的 `run()` 方法后会进入**Terminated 终止状态**

## 创建线程方法？

### 继承Thread类

```java
public class Demo {
    public static class MyThread extends Thread {
        @Override
        public void run() {
            System.out.println("MyThread");
        }
    }
    
    public static void main(String[] args) {
        Thread thread = new MyThread();
        thread.start();
    }
}
```

### 实现Runnable接口

```java
@FunctionalInterface
public interface Runnable {
    public abstract void run();
}
```

示例：

```java
public class Demo {
    public static class MyThread implements Runnable {
        @override
        public void run() {
            System.out.println("My Thread");
        }
    }
    
    public static void main(String[] args) {
        new Thread(new MyThread()).start();
        
        // Java8
        new Thread(() -> {
            System.out.println("Java8 匿名内部类");
        }).start();
    }
}
```

### 实现Callable接口

```java
public class CallerTask implements Callable<String> {
    @Override
    public String call() throws Exception {
        System.out.println("Thread.currentThread().getState() = " + Thread.currentThread().getState());
        return "hello";
    }

    public static void main(String[] args) {
        FutureTask<String> futureTask = new FutureTask<>(new CallerTask());
        new Thread(futureTask).start();
        try {
            String result = futureTask.get();
            System.out.println(result);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```

### Thread和Runnable比较？

- Thread只能单继承，Runnable可以多实现
- Thread继承方便传参，可以在子类添加成员变量，通过set设置参数或构造函数传递
- Runnable只能使用主线程中声明为final的变量

## 线程间通信



##  上下文切换？

- 线程个数一般大于CPU核心数，一个CPU核心在某时刻只能被一个线程使用
- CPU为每个线程分配时间片并轮转，线程的时间片用完会回到**Ready 就绪状态**让给其他线程使用
- 当前任务用完时间片在切换任务时，先保存自己的状态，一遍下次切换回这个任务时重新加载这个任务的状态，这个过程叫上下文切换
- 上下文切换消耗大量的CPU时间

## 线程死锁？

必备条件：

- 互斥：一个资源任意时刻只能有一个线程占用
- 请求和保持：一个线程因为请求资源被阻塞时，自身获得的锁不释放
- 不剥夺：线程已获得的资源不能被其他资源强行剥夺，必须使用结束才能释放
- 循环等待：多个线程形成头尾相连的循环等待关系

如何破坏：

- 互斥：不破坏
- 请求与保持：一次性申请所有资源
- 不剥夺：占用部分资源的线程继续申请其他资源时，如果获取不到，主动释放已占有的资源
- 循环等待：按序申请资源

## `sleep()` 和 `wait()` 的区别和共同点？

- 共同点：都可以暂停线程运行
- 区别：`sleep() `没有释放锁，`wait()` 释放了锁。
- `sleep()` 一般用于暂停运行，`wait()` 一般用于线程间交互/通信。
- wait方法调用后，线程不会自动苏醒，需要别的线程调用同一个对象上的 `notify()` 方法或 `notifyAll()` 方法。或者使用 `wait(long timeout)` ，超时后线程自动苏醒
- `sleep()`执行结束线程会自动苏醒

## 为什么调用 `start()` 方法会执行 `run()` 方法，不能直接调用 `run()` 方法？

- `new` 一个 `Thread`，线程进入初始状态，调用 `start()` 方法可以进入运行状态，`start()` 会执行线程的相应准备工作，自动执行 `run()` 方法的代码
- 如果直接使用 `run()` 方法，相当于普通的方法调用，还是在 `main `线程下运行，并没有实现多线程

## 并发编程的特性？

- **原子性**：一个操作或多个操作，要么所有操作全部被执行并且不会被干扰中断，要么都不执行。`synchronized`可以保证代码片段原子性
- **可见性**：当一个变量对变量进行修改，其他线程立刻可以看到修改后的最新值。`volatile` 可以保证共享变量的可见性
- **有序性**：JVM在运行期间会进行优化，对指令重排序，要保证代码执行的先后顺序。`volatile` 可以禁止重排序

## ThreadLocal？

- 让每个线程绑定自己的值，存储每个线程的私有资源
- 创建 `ThreadLocal` 变量后，访问这个变量的每个线程都有这个变量的本地副本
- 变量使用 `get()` 和 `set()` 方法获取默认值或者改为当前线程存的副本的值
- 用来避免两个线程竞争

## 线程池？

- 线程池用来限制和管理资源。维护基本统计信息
- **降低资源消耗**。通过重复利用已创建的线程降低线程创建和销毁造成的消耗
- **提高响应速度**。任务到达时，不用等线程创建就能立即运行
- **提高线程的可管理性**。无限制地创建线程会消耗系统资源，降低稳定性。线程池可以统一分配、调优、监控

## `ThreadPoolExecutor` 构造函数?

- `corePoolSize`：**核心线程数**。最小可以同时运行的线程数
- `maximumPoolSize` ：**最大线程数**。队列中任务达到队列容量时，可同时运行的线程数量变为最大线程数
- **`workQueue`**：

