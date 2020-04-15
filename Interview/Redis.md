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