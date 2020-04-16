# Java锁

## `Synchronized` 和 `lock` ？

- `Synchronized` 是Java中的关键字，用来修饰一个代码块或一个方法。

```java
public int synMethod(int m){
  synchronized(m) { // 括号后是变量，一次只有一个线程进入代码块
    //...
  }
}

public synchronized void synMethod() { // 一次只有一个线程进入该方法
   //...
}

public void test() { 
  synchronized (this) { // 括号内放入对象，线程获得对象锁
      //...
  }
}
```

- `Lock` 是接口，有如下方法：

```java
public interface Lock {
  void lock(); // 用来获取锁，必须主动释放锁，发生异常时不自动释放，因此要放在try catch中，释放锁放在finally中，防止死锁
  void lockInterruptibly() throws InterruptedException; // 获取锁时，如果锁被占用，可以响应中断状态
  boolean tryLock(); // 有返回值，获取锁成功返回true，被占用返回false。无论如何立即返回，拿不到锁不会一直等待
  boolean tryLock(long time, TimeUnit unit) throws InterruptedException; // 类似tryLock，等待时间内获取到锁返回true，超时返回false
  void unlock(); // 释放锁，一定要在finally块中
  Condition newCondition();
}
```

- 发生异常时，`Synchronized`会自动释放线程占用的锁。`Lock`假如没有使用 `unlock()` 的话会造成死锁
- `Synchronized`不能响应中断，因此会一直等待。`Lock`可以响应中断状态
- `Lock` 可以知道是否成功获取锁，`Synchronized`不能
- `Synchronized`是非公平锁，无法实现公平锁。`ReentrantLock`两个都可以实现

## `volatile` ？

- 保证变量操作的可见性。一个线程修改了变量值，立刻写入到物理内存中，其他线程中已经写入的值宣布无效，重新从物理内存中加载
- 保证变量操作的有序性。禁止指令重排序。
- 不保证原子性。比如线程1已经计算出了临时变量还未赋值，因此没能写到物理内存，此时线程二修改了变量，线程1之后继续把已计算的临时变量继续赋值
- 加入 `volatile`的变量在汇编代码中加入了`lock`指令，相当于一个内存屏障

## `synchronized` 修饰静态方法和成员方法分别锁住了什么？

- 修饰普通成员方法时，锁是对象锁(this)。
  - 当一个类中多个普通方法被`synchronized`修饰（同步），锁的都是这个类的对象this。多个线程访问同一个类的不同方法也会被阻塞。
  - 如果通过不同对象来调用，锁就是不一样的，不会阻塞。
  - 通过同一个对象调用非同步方法不会被阻塞
- 修饰静态方法时，是类锁。范围比对象锁大。只要是该类的对象，使用的都是同一把锁。

## CAS？

- CompareAndSwap。内存地址v，旧的预期值A，更新目标值B
- **乐观锁**的一种。拿数据时认为别人不会修改。更新数据的时候判断是否被修改过。
- 多个线程更新同一个变量时，一个会成功，其他不成功并重试
- 循环时间长，失败不断重试，给CPU带来压力
- 只能保证一个共享变量的原子操作
- **ABA问题**。修改为B后又修改为A，无法判断中间发生过修改

## Atomic

- 轻量级地保证变量原子性
- 通过无锁化的CAS实现