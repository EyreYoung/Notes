# Redis学习

## Linux下安装
下载地址：http://redis.io/download
```
$ wget http://download.redis.io/releases/redis-5.0.7.tar.gz
$ tar xzf redis-5.0.7.tar.gz
$ cd redis-5.0.7
$ make
```

## 缓存击穿？避免？

- 某热点key在失效时，刚好有大量并发请求
- 避免：
  - 使用互斥锁。缓存失效时，先用SETNX设置mutex key。返回成功后再load db并回设缓存
  - 提前使用互斥锁。在value内部设置1个超时值(timeout1), timeout1比实际的memcache timeout(timeout2)小。当从cache读取到timeout1发现它已经过期时候，马上延长timeout1并重新设置到cache。然后再从数据库加载数据并设置到cache中。
  - 永远不过期。发现要过期时，通过后台的异步线程进行缓存的构建

## 缓存穿透？避免？

- 恶意请求故意查询不存在的key，系统会去后端系统查找，造成很大压力
- 避免：
  - 对查询结果为空的情况也进行缓存，期限设置短一些，key对应数据insert后清理缓存
  - 对肯定不存在的key过滤，可以通过bitmap过滤。布隆过滤器

## 缓存雪崩？避免？

- 缓存服务器重启、崩溃、集体失效
- 避免：
  - 失效后，通过加锁或者队列控制查询和写缓存的线程数量
  - 做二级缓存。原始缓存设为短期，拷贝缓存设为长期
  - key的失效时间加上随机数，让失效时间尽量均匀

## 常见业务数据？

- 秒杀系统、票务系统、商品系统
- 突发高频访问数据如新闻
- 复杂高频的统计数据如投票、在线人数

## Redis 数据类型？

Redis自身是一个`Map`，所有数据都采用`key:value`的形式存储

- `string` ：类比`String`
  - **存储数据**：单个数据，最简单最常用的数据存储类型
  - **格式**：一个存储空间保存一个数据
  - **存储内容**：字符串，如果字符串是整数的格式，可以作为数字操作使用
- `hash` ：类比`HashMap`
- `list` ：类比`LinkedList`
- `set` ：类比`HashSet`
- `sorted_list` ：类比`TreeSet`

## `string` 操作？

- 添加、修改数据：`set key value`
- 添加、修改多条数据：`mset key1 value1 key2 value2...`
- 获得数据：`get key`
- 获得多条数据：`mget key1 key2`
- 获取字符数据个数：`strlen key`
- 追加信息到原信息尾部（不存在则新建）：`append key value`
- 删除数据：`del key`



- 数据最大存储量：`512MB`
- 数值计算最大范围：9223372036854775807

### `string` 数值操作?

`Redis`用于控制数据库表主键id，为数据库表主键提供生成策略，保障数据库表的主键唯一性，适用于所有数据库，支持数据库集群

- 数值数据自增、自减：`incr key` `decr key`
- 数值数据增加、减少固定值：`incrby key #{增加量}` `decrby key #{减少量}` `increby key #{浮点数}`

- `string`在`redis`内部存储默认为字符串，遇到增减操作(incr decr)时会转成数值型计算
- redis所有操作都是原子性的，使用单线程处理所有业务，命令逐个执行，因此无需考虑并发影响
- 数值操作超过上限会报错，Java中`Long.MAX_VALUE`

### `string` 设置生命周期?

Redis控制数据的生命周期，通过数据是否失效控制业务行为。如限制一定时间内不能再次投票

- 设置数据生命周期

```shell
setex key #{生存秒数} value
psetex key #{生存毫秒数} value
```

### `string` 存储结构性数据？

Redis应用于各种结构型和非结构型高热度数据访问加速

- `set user:id:1001:fans 10000`

- `set user:id:1001 {id:1001, name:张三, fans:10000}`

- 数据库热点数据`key`命名惯例：`#{表名}:#{主键名}:#{主键值}:#{字段名}`



##  `hash`操作？

- `Key->{field1: value1, field2:value2, field3:value3}` 对一系列存储的数据进行编组，方便管理，典型应用存储对象信息

- 一个存储空间保存多个键值对数据

- 底层使用哈希表实现数据存储
- hash存储结构优化：field个数少时存储结构优化为类数组结构；field个数多时使用HashMap结构



- 添加、修改数据：`hset key field value`
- 获取数据：`hget key field`   `hgetall key`
- 删除数据：`hdel key field1 [field2]`

## 持久化

**持久化**：利用永久性存储介质保存数据，在特定时间将保存的数据进行恢复的工作机制。

防止数据意外丢失，确保数据安全性。

### RDB快照(Snapshotting)

- 通过创建快照获得存储在内存中的数据在某个时间点的副本
- 创建快照后，可以对快照进行备份；可以复制到其他服务器来创建具有相同数据的服务器副本；可以将快照留在本地以便在重启服务器时使用

触发方式：

- save指令：阻塞当前Redis服务器，直到持久化完成，线上禁止使用
- bgsave指令：fork一个子进程，子进程负责持久化，阻塞只发生在fork子进程时
- 