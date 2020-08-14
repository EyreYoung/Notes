# Java集合

## Map的分类和常见情况？

- Java为数据结构中的**映射**定义了一个接口 `java.util.Map` ，有四个实现类：`HashMap` `Hashtable` `LinkedHashMap` `TreeMap`
- `HashMap`：最常用的Map；访问速度快；遍历时顺序随机；不支持线程同步；只允许一个键为null
- `Hashtable`：类似HashMap；不允许键为null；支持线程同步，同时只能有一个线程写入；写入较慢
- `LinkedHashMap`：`HashMap`的子类；保留写入顺序；遍历按顺序输出；可以在构造时加上参数，按使用次数排序；遍历时慢于HashMap，除非HashMap实际数据远小于容量
- `TreeMap`：实现SortMap接口；按键的升序排列；可以指定排序的比较器

## HashMap？

[HashMap? ConcurrentHashMap? 相信看完这篇没人能难住你！](https://crossoverjie.top/2018/07/23/java-senior/ConcurrentHashMap/)

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

## Hashtable？

- 线程安全的遗留类，类似HashMap
- Hashtable与HashMap的相同点
  - Hashtable和HashMap相同都是基于哈希表实现的，同样每个元素都是一个key-value对，内部也是通过单链表来解决冲突问题，容量不足时，同样会自动增长。
  - Hashtable同样实现了Serializable接口，它支持序列化，实现Cloneable接口，能被克隆，实现了Map接口。
- Hashtable与HashMap的不同点
  - 继承父类不同：Hashtable继承自Dictionary类，而HashMap继承自AbstractMap类。
  - 线程安全不同：Hashtable中的方法是Synchronize的，而HashMap中的方法在缺省的情况下是非Synchronize的，在多线程的环境下，可以直接使用Hashtable
  - 是否提供contains方法：HashMap把Hashtable中的contains方法去掉了，改成了containsValue和containsKey，因为contains方法容易引起误解。
  - key和value是否允许null值：Hashtable中，key和value都不允许null值，而HashMap则都允许。
    遍历方式不同：都使用Iterator，但Hashtable还是用了Enumeration的方式。
  - hash不同：Hashtable使用了对象的hashCode，而HashMap重新计算了hash值。
    内部实现使用的数组初始化和扩容方式不同：Hashtable默认容量为11，而HashMap为16，Hashtable扩容是，变为原来的两倍加1，HashMap变为两倍。

## LinkedHashMap？

- LinkedHashMap是HashMap类的一个子类，它拥有HashMap的一切特性，HashMap中的元素是无序存储的，而LinkedHashMap使用双向链表来保证它的迭代顺序。可以说LinkedHashMap=HashMap+LinkedList。除了维护一个Entry数组，还定义了双向链表的头尾节点来保证迭代顺序，在Entry类中还新增了每个节点的前后节点（before，after）。
- LinkedHashMap支持两种顺序：插入顺序和访问顺序
      1.插入顺序：先添加的在前面，后添加的在后面，修改操作不印象顺序。
      2.访问顺序：访问指的是get/put，对一个键执行get/put操作后，其对应的键值对会移到链表的末尾，所以最末尾的时最近访问的，最开始的是最久没有被访问的，这就是访问顺序。

## TreeMap？

- 实现对存储元素自动排序
- 存储结构
  - 红黑树。二叉树：一个节点最多两个子节点；排序二叉树：大于左子节点，小于右子节点；平衡二叉树：左右子树高度差小于等于1
  - 节点为红色或者黑色；根节点和叶子节点都是黑色；红色不重复，黑色可重复；任意节点到所有叶子节点经过的黑色节点数量相同。通过变色或旋转保证
- 排序方式
  - 构造时未传入比较器：按key的自然顺序排列，如果key不是基本类型，必须实现了Comparable接口，否则抛出异常。
- 插入方法
  - 调用put方法，首先判断红黑树是否建立，未建立则先创建红黑树，赋值给root。
  - 遍历所有节点，如果找到key相同节点，更新value；没找到则将最后遍历到的节点作为父节点插入子节点，调整结构。

## ConcurrentHashMap?

- 线程安全的HashMap
- 基于数组加链表/红黑树实现
- CAS+synchronized保证并发性（不再使用segment）
- 不允许null值null键
- 插入：
  - 判断Node数组是否初始化，没有则进行初始化
  - 通过hash定位数组的索引坐标，判断是否有Node节点，没有则使用CAS添加。失败则重试
  - 如果内部正在扩容，则帮助一起扩容
  - 如果有node节点，用synchronized锁住头元素。如果是链表节点，执行链表添加操作，红黑树则执行红黑树插入操作。