# 面试准备

## Java基础

### Java和Php的区别？

- Php的库函数用C实现，Java核心运行时类库用Java编写，Java应用运行时编写的代码、引用的类库、框架都在JVM上解释执行
- Php内置模板引擎，Java Web需要使用外部容器如Tomcat

### 正则表达式？

- 用来查找符合某些复杂规则的字符串
- 记录文本规则的代码
- Java中String类提供正则表达式操作

### 比较Java和JavaScript？

- Java来自Sun Mircosystems公司，是面向对象的程序设计语言。JavaScript来自Netscape公司，是基于对象和时间驱动的解释型语言
- Java源代码执行前必须进行编译，JavaScript代码直接由浏览器解释执行
- Java采用强类型变量检查，JavaScript使用弱类型变量，由解释器在运行时推断类型
- 代码格式不一样

### Java如何跳出多重嵌套循环？
- 最外层循环标记A
- `break A;`
- 避免使用

### `&` 和 `&&` 的区别？
- `&` 的用法有按位与和逻辑与
- `&&` 是短路和运算
- `&&` 是false的话，右边不会进行运算

### `int`和`Integer`的区别？
- 基本类型和包装类型
- Java中，一切皆对象，八种基本类型不是对象
- 基本类型不需要`new`来创建，封装类型需要
- 基本类型直接把变量的值存在堆栈中。封装类型通过引用指向实例，具体实例保存在堆中
- 基本类型初始值为0或者`false`，封装类型初始值为`null`
- Java5引入自动装箱/拆箱机制，可以互相转换

### 如何输出某种编码的字符串？
- `public String​(byte[] bytes, Charset charset)`

### `String`和`StringBuffer`的区别？
- 都是`final`类，不能被继承
- `String`长度不可变，每次修改都会生成新的String对象，经常改变长度的话不应使用
- `StringBuffer`会对对象本身进行操作
- `StringBuilder`与`StringBuffer`兼容，用于字符串缓冲区被单个线程使用，比`StringBuffer`快，但不适合多线程
- `String`类的 `+` 拼接性能差，应该使用`StringBuffer`或`StringBuilder`

### 数组Array和列表ArrayList的区别？
- Array不能修改大小，ArrayList可以动态改变大小
- Array可以存储基本类型和对象类型，但必须是同类型，ArrayList只能存储对象类型
- ArrayList提供更多方法，比如`addAll()`

### 值传递和引用传递？
- 值传递传递的是真实内容的一个副本，形参不影响实参
- 引用传递时形参和实参指向同一个对象，形参操作会影响实参对象
- Java中只有值传递，对引用对象传递的是地址的副本，但会指向同一个对象

### Java支持的数据类型？
- `byte/short/int/long/float/double/char/boolean`

### 自动拆装箱？
- Java编译器在基本数据类型和对应对象包装类型之间做的转换，如`int/Integer double/Double`

### `4.0 - 3.6 = 0.40000001`?
- 二进制无法精确表示十进制小数，转换过程中出现误差

### 十进制数在内存中如何存储？

- 补码的形式

### `Lambda`表达式优缺点？

- 简洁
- 方便并行计算
- 不易调试，不易读

### Java8新特性？

- 接口的默认方法和静态方法。解决接口修改与接口的实现类不兼容问题，方便向前兼容
- 函数式接口 `@FunctionalInterface` 和 `lambda` 表达式。
- 方法引用。
- Stream API。`java.util.Stream`
- Optional。
- `Data Time`API。对时间和日期的处理

### `==` 比较？

- 基本类型：直接比较大小
- 引用类型：比较两者在内存中的地址，只有同时`new`出来的对象才会返回`true`

### `Object` 的 `hashCode()` 如何计算？

- 本地方法，使用C/C++实现，一般是返回内存地址，取决于JVM的实现

### 为什么重写了 `equals()` 还要重写 `hashCode()` ?

- HashMap中的比较需要 `equals()` 和 `hashCode()` 同时运行。先用 `hashCode()` 比较，如果相等则进一步使用 `equals()` 进行比较，假如 `hashCode()`不相等，则不会继续比较。

### Map的分类和常见情况？

- Java为数据结构中的**映射**定义了一个接口 `java.util.Map` ，有四个实现类：`HashMap` `Hashtable` `LinkedHashMap` `TreeMap`
- `HashMap`：最常用的Map；访问速度快；遍历时顺序随机；不支持线程同步；只允许一个键为null
- `Hashtable`：类似HashMap；不允许键为null；支持线程同步，同时只能有一个线程写入；写入较慢
- `LinkedHashMap`：`HashMap`的子类；保留写入顺序；遍历按顺序输出；可以在构造时加上参数，按使用次数排序；遍历时慢于HashMap，除非HashMap实际数据远小于容量
- `TreeMap`：实现SortMap接口；按键的升序排列；可以指定排序的比较器

## 关键字

### Java中 `final` 关键字怎么用？

- 修饰类。用来表明类不能被继承。final类的成员变量可以根据需要设为final，所有成员方法都被隐式设为final
- 修饰方法。用来禁止方法在子类中被修改。类的`private`方法被隐式设为final
- 修饰变量。如果是基本类型则值不能修改；如果是引用类型则初始化后不能再指向另一个对象

### `Synchronized` 和 `lock` ？

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

### `volatile` ？

- 保证变量操作的可见性。一个线程修改了变量值，立刻写入到物理内存中，其他线程中已经写入的值宣布无效，重新从物理内存中加载
- 保证变量操作的有序性。禁止指令重排序。
- 不保证原子性。比如线程1已经计算出了临时变量还未赋值，因此没能写到物理内存，此时线程二修改了变量，线程1之后继续把已计算的临时变量继续赋值
- 加入 `volatile`的变量在汇编代码中加入了`lock`指令，相当于一个内存屏障

### `synchronized` 修饰静态方法和成员方法分别锁住了什么？

- 修饰普通成员方法时，锁是对象锁(this)。
  - 当一个类中多个普通方法被`synchronized`修饰（同步），锁的都是这个类的对象this。多个线程访问同一个类的不同方法也会被阻塞。
  - 如果通过不同对象来调用，锁就是不一样的，不会阻塞。
  - 通过同一个对象调用非同步方法不会被阻塞
- 修饰静态方法时，是类锁。范围比对象锁大。只要是该类的对象，使用的都是同一把锁。

### 静态变量和实例变量的区别？

- 静态变量声明时要加`static`
- 静态变量是类的属性，也叫类变量，只要字节码文件被加载，就会被分配空间。可以直接通过类名使用
- 实例变量是对象的属性，必须创建了实例对象，其中的变量才会被分配空间。必须创建对象后通过对象来引用

## 锁

https://zhuanlan.zhihu.com/p/84109815

### CAS？

- CompareAndSwap。内存地址v，旧的预期值A，更新目标值B
- 乐观锁的一种。拿数据时认为别人不会修改。更新数据的时候判断是否被修改过。
- 多个线程更新同一个变量时，一个会成功，其他不成功并重试
- 循环时间长，失败不断重试，给CPU带来压力
- 只能保证一个共享变量的原子操作
- ABA问题。修改为B后又修改为A，无法判断中间发生过修改

### Atomic

- 轻量级地保证变量原子性
- 通过无锁化的CAS实现



## 面向对象

### IOC？

### 反射？
- 反射（Reflection）是Java的特征之一。允许运行中的Java程序获得自身信息，操作类或对象的内部属性
- 反射通过Java编译后生成的`.class`文件找到类、方法和属性
- 四个类：`Class // 类 Constructor // 类的构造方法 Field // 类的属性对象 Method // 类的方法`
- 主要用途是配置化的通用框架，需要根据配置文件加载不同的对象和类，在运行中动态加载


## 集合

### HashMap？

基于哈希表，实现Map接口的双列集合。数据结构是数组加列表。

Key唯一；Value可以重复；允许`null`键`null`值

- 哈希表
  - 基于数组实现
  - Java 8中散列函数：`hashCode`右移16位与自身异或的值。位置是散列值对散列表长度取模使用与运算，所以散列表长度必须是2的整数幂
- 哈希冲突
  - 散列函数得到了相同的地址
  - 要求散列函数计算简单、分布均匀
  - HashMap使用链地址法。长度小于8使用链表，大于8使用红黑树；数组大于8使用红黑树；容量小于64且一个桶的元素大于等于8时，数组容量翻倍
- 数据结构
  - 底层是一个数组，每个元素都是一个Entry，包括key、value、next。
  - 构造函数有两个参数，容量和负载参数。容量必须是2的整数幂，默认16
- HashMap存储
  - 使用`put()`方法，如果存在key值，覆盖对应value；没有key值则新增一个Entry
  - 根据key计算出散列值，对应下标没有值则写入
  - 对应下标有值则对比key值是否相同，相同则写入；不同则找下一个节点是否相同

- HashMap扩容
  - 元素变多时，数组出现碰撞概率变大，需要及时扩容
  - 触发条件是元素数量 > 数组容量 * 装载因子(load factor)
  - 数组每次扩大一倍，重新计算元素位置

### Hashtable？

- 线程安全的遗留类，类似HashMap
- Hashtable与HashMap的相同点
  - Hashtable和HashMap相同都是基于哈希表实现的，同样每个元素都是一个key-value对，内部也是通过单链表来解决冲突问题，容量不足时，同样会自动增长。
  -  Hashtable同样实现了Serializable接口，它支持序列化，实现Cloneable接口，能被克隆，实现了Map接口。
- Hashtable与HashMap的不同点
  - 继承父类不同：Hashtable继承自Dictionary类，而HashMap继承自AbstractMap类。
  - 线程安全不同：Hashtable中的方法是Synchronize的，而HashMap中的方法在缺省的情况下是非Synchronize的，在多线程的环境下，可以直接使用Hashtable
  - 是否提供contains方法：HashMap把Hashtable中的contains方法去掉了，改成了containsValue和containsKey，因为contains方法容易引起误解。
  - key和value是否允许null值：Hashtable中，key和value都不允许null值，而HashMap则都允许。
    遍历方式不同：都使用Iterator，但Hashtable还是用了Enumeration的方式。
  - hash不同：Hashtable使用了对象的hashCode，而HashMap重新计算了hash值。
    内部实现使用的数组初始化和扩容方式不同：Hashtable默认容量为11，而HashMap为16，Hashtable扩容是，变为原来的两倍加1，HashMap变为两倍。

### LinkedHashMap？

- LinkedHashMap是HashMap类的一个子类，它拥有HashMap的一切特性，HashMap中的元素是无序存储的，而LinkedHashMap使用双向链表来保证它的迭代顺序。可以说LinkedHashMap=HashMap+LinkedList。除了维护一个Entry数组，还定义了双向链表的头尾节点来保证迭代顺序，在Entry类中还新增了每个节点的前后节点（before，after）。
-  LinkedHashMap支持两种顺序：插入顺序和访问顺序
        1.插入顺序：先添加的在前面，后添加的在后面，修改操作不印象顺序。
        2.访问顺序：访问指的是get/put，对一个键执行get/put操作后，其对应的键值对会移到链表的末尾，所以最末尾的时最近访问的，最开始的是最久没有被访问的，这就是访问顺序。

### TreeMap？

- 实现对存储元素自动排序
- 存储结构
  - 红黑树。二叉树：一个节点最多两个子节点；排序二叉树：大于左子节点，小于右子节点；平衡二叉树：左右子树高度差小于等于1
  - 节点为红色或者黑色；根节点和叶子节点都是黑色；红色不重复，黑色可重复；任意节点到所有叶子节点经过的黑色节点数量相同。通过变色或旋转保证
- 排序方式
  - 构造时未传入比较器：按key的自然顺序排列，如果key不是基本类型，必须实现了Comparable接口，否则抛出异常。
- 插入方法
  - 调用put方法，首先判断红黑树是否建立，未建立则先创建红黑树，赋值给root。
  - 遍历所有节点，如果找到key相同节点，更新value；没找到则将最后遍历到的节点作为父节点插入子节点，调整结构。

### ConcurrentHashMap?

- 线程安全的HashMap
- 基于数组加链表/红黑树实现
- CAS+synchronized保证并发性（不再使用segment）
- 不允许null值null键
- 插入：
  - 判断Node数组是否初始化，没有则进行初始化
  - 通过hash定位数组的索引坐标，判断是否有Node节点，没有则使用CAS添加。失败则重试
  - 如果内部正在扩容，则帮助一起扩容
  - 如果有node节点，用synchronized锁住头元素。如果是链表节点，执行链表添加操作，红黑树则执行红黑树插入操作。

## JVM

### JVM调优

如果CPU使用率较高，GC频繁且GC时间长，可能就需要JVM调优了。
 基本思路就是让每一次GC都回收尽可能多的对象，
 对于CMS来说，要合理设置年轻代和年老代的大小。该如何确定它们的大小呢？这是一个迭代的过程，可以先采用JVM的默认值，然后通过压测分析GC日志。

如果看年轻代的内存使用率处在高位，导致频繁的Minor GC，而频繁GC的效率又不高，说明对象没那么快能被回收，这时年轻代可以适当调大一点。

如果看年老代的内存使用率处在高位，导致频繁的Full GC，这样分两种情况：如果每次Full GC后年老代的内存占用率没有下来，可以怀疑是内存泄漏；如果Full GC后年老代的内存占用率下来了，说明不是内存泄漏，要考虑调大年老代。

对于G1收集器来说，可以适当调大Java堆，因为G1收集器采用了局部区域收集策略，单次垃圾收集的时间可控，可以管理较大的Java堆。

## GC

### GC算法

- 引用计数法。对于对象A，任何对象引用了A，它的引用计数器+1，引用失效-1。引用计数器变成0的时候，不能再使用
- 标记-清除算法（Mark-Sweep）。标记阶段通过根节点标记可达对象。未被标记则是垃圾对象。容易造成内存碎片化
- 复制算法。内存分为两块，一半放数据，另一半不放。GC时将正在使用的内存的存活对象拷贝到未使用的内存块，清楚原来的所有对象。有内存浪费
- 标记-压缩。先标记对象，把不可回收的对象放到已回收的对象的位置。没有内存浪费

### 老生代和新生代？

- 新生代分为eden、survivor1、survivor2。new的对象非常大则放入老生代，否则放入edan，GC一次后仍有引用，放入survivor1，再经历一次放入survivor2.一定次数后放入老生代。

## Java缓存

### LRU？

Least Recent Used

- 缓存思想：
  - 缓存大小固定
  - 每次读取会刷新缓存使用时间
  - 缓存满后，删除最久未使用的缓存，再添加新缓存

### FIFO？

First In First Out



### LFU？



## Redis

### 缓存击穿？避免？

- 某热点key在失效时，刚好有大量并发请求
- 避免：
  - 使用互斥锁。缓存失效时，先用SETNX设置mutex key。返回成功后再load db并回设缓存
  - 提前使用互斥锁。在value内部设置1个超时值(timeout1), timeout1比实际的memcache timeout(timeout2)小。当从cache读取到timeout1发现它已经过期时候，马上延长timeout1并重新设置到cache。然后再从数据库加载数据并设置到cache中。
  - 永远不过期。发现要过期时，通过后台的异步线程进行缓存的构建

### 缓存穿透？避免？

- 恶意请求故意查询不存在的key，系统会去后端系统查找，造成很大压力
- 避免：
  - 对查询结果为空的情况也进行缓存，期限设置短一些，key对应数据insert后清理缓存
  - 对肯定不存在的key过滤，可以通过bitmap过滤。布隆过滤器

### 缓存雪崩？避免？

- 缓存服务器重启、崩溃、集体失效
- 避免：
  - 失效后，通过加锁或者队列控制查询和写缓存的线程数量
  - 做二级缓存。原始缓存设为短期，拷贝缓存设为长期
  - key的失效时间加上随机数，让失效时间尽量均匀

## Spring

### 事务管理？

- 事务：
  - 原子性。事务是最小的单位，不允许分割。
  - 隔离性。执行完事务后，数据保持一致。
  - 一致性。并发访问数据库时，一个用户的事务不被其他事务干扰，并发事务之间数据库是独立的。
  - 持久性。事务提交后，在数据库中的数据改变应该是持久的，数据库故障也不应该影响。
  
- Spring事务管理API

  事务管理就是按照给定的事务规则来执行提交和回滚操作

  - `PlatformTransactionManager` 接口

  ```java
  // 与事务策略分离的接口
  
  public interface PlatformTransactionManager {
  
      // 平台无关的获得事务的方法
    	// 根据一个TransactionDefinition参数，返回一个TransactionStatus对象，可能是已存在的事务对象，也可能是新的事务对象
      TransactionStatus getTransaction(TransactionDefinition definition) throws TransactionException;
  
      // 平台无关的事务提交方法
      void commit(TransactionStatus status) throws TransactionException;
  
      // 平台无关的事务回滚方法
      void rollback(TransactionStatus status) throws TransactionException;
  }
  ```

  - `TransactionDefinition` 接口

  ```java
  // 用于定义一个事务的规则
  // 默认的实现类：DefaultTransactionDefinition
  // 定义的事务规则：事务隔离级别、事务传播行为、事务超时、事务的只读属性、事务的回滚规则
  
  public interface TransactionDefinition{
      int getIsolationLevel();
      int getPropagationBehavior();
      int getTimeout();
      boolean isReadOnly();
  }
  
  /**
  事务隔离级别:
  	TransactionDefinition.ISOLATION_DEFAULT：使用底层数据库默认隔离级别
  	TransactionDefinition.ISOLATION_READ_UNCOMMITTED：读未提交。很少使用
  	TransactionDefinition.ISOLATION_READ_COMMITTED：读提交。防止脏读
  	TransactionDefinition.ISOLATION_REPEATABLE_READ：重复读。防止脏读和不可重复读
  	TransactionDefinition.ISOLATION_SERIALIZABLE：串行化。严重影响性能
  	
  事务传播行为（解决业务层方法互相调用的问题）：
  
  事务超时属性
  
  事务只读属性
  
  回滚规则
  */
  ```

  - `TransactionStatus` 接口

  ```java
  // 返回一个Transaction对象，代表一个新的或者已存在的事务
  
  public interface TransactionStatus{
      boolean isNewTransaction(); // 是否是新的事物
      boolean hasSavepoint(); // 是否有恢复点
      void setRollbackOnly();  // 设置为只回滚
      boolean isRollbackOnly(); // 是否为只回滚
      boolean isCompleted; // 是否已完成
  }
  ```

- 编程式事务管理（基于底层API）

```java
public class BankServiceImpl implements BankService {
    private BankDao bankDao;
    private TransactionDefinition txDefinition;
    private PlatformTransactionManager txManager;
    ......

    public boolean transfer(Long fromId， Long toId， double amount) {
        // 获取一个事务
        TransactionStatus txStatus = txManager.getTransaction(txDefinition);
        boolean result = false;
        try {
            result = bankDao.transfer(fromId， toId， amount);
            txManager.commit(txStatus);    // 事务提交
        } catch (Exception e) {
            result = false;
            txManager.rollback(txStatus);      // 事务回滚
            System.out.println("Transfer Error!");
        }
        return result;
    }
}
```

相应配置文件

```XML
<bean id="bankService" class="footmark.spring.core.tx.programmatic.origin.BankServiceImpl">
    <property name="bankDao" ref="bankDao"/>
    <property name="txManager" ref="transactionManager"/>
    <property name="txDefinition">
    <bean class="org.springframework.transaction.support.DefaultTransactionDefinition">
        <property name="propagationBehaviorName" value="PROPAGATION_REQUIRED"/>
    </bean>
    </property>
</bean>
```

- 编程式事务管理（基于`TransactionTemplate`）

```java
public class BankServiceImpl implements BankService {
    private BankDao bankDao;
    private TransactionTemplate transactionTemplate;
    ......
    public boolean transfer(final Long fromId， final Long toId， final double amount) {
        return (Boolean) transactionTemplate.execute(new TransactionCallback(){ // 匿名内部类
            public Object doInTransaction(TransactionStatus status) {
                Object result;
                try {
                        result = bankDao.transfer(fromId， toId， amount);
                    } catch (Exception e) {
                        status.setRollbackOnly(); // 执行事务回滚
                        result = false;
                        System.out.println("Transfer Error!");
                }
                return result;
            }
        });
    }
}
```

相应配置文件：

```xml
<bean id="bankService" class="footmark.spring.core.tx.programmatic.template.BankServiceImpl">
    <property name="bankDao" ref="bankDao"/>
    <property name="transactionTemplate" ref="transactionTemplate"/>
</bean>
```

- Spring声明式事务管理

建立在AOP机制上，本质是对目标方法前后进行拦截。在目标方法开始前创建或加入一个事务，执行完目标方法后根据执行情况提交或回滚事务。

优点：只需在配置文件进行事务规则声明。

## 数据库

### 事务隔离级别？

主要在多个事务并发的情况下。解决脏读、不可重复读、幻读等问题。

- Read uncommitted 读未提交
  - 脏读：事务B读取了事务A尚未提交的数据，即事务A还未结束就回滚的数据被事务B读到。
- Read committed 读提交
  - 不会出现脏读，但会出现不可重复读。
  - 不可重复读：事务A读取数据后，事务B紧接更新了数据并提交事务，事务A再次读取的时候，数据已经被修改。
  - SQL Server、Oracle默认级别
- Repeatable read 重复读
  - 避免不可重复读。一个事务中重复读取数据，不会发生变化，除非提交了数据，再次进行读取
  - 幻读：事务A查询了数据，此时事务B新增一条数据。事务A继续新增这条数据时发现冲突，或者更新时影响的行数跟刚刚读取的不一致。
- Serializable 串行化
  - 最高的事务隔离级别。
  - 事务顺序执行，避免脏读、不可重复读、幻读。
  - 性能很低，很少使用。

## 未分类

### 消息队列？

https://blog.csdn.net/songfeihu0810232/article/details/78648706

### 布隆过滤器

https://zhuanlan.zhihu.com/p/43263751