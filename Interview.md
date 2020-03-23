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

### `int`和`integer`的区别？
- 基本类型和包装类型
- Java中，一切皆对象，八种基本类型不是对象
- 基本类型不需要`new`来创建，封装类型需要
- 基本类型直接把变量的值存在堆栈中。封装类型通过引用指向实例，具体实例保存在堆中
- 基本类型初始值为0或者`false`，封装类型初始值为`null`
- Java5引入自动装箱/拆箱机制，可以互相转换

### 如何输出某种编码的字符串？
- `public String​(byte[] bytes,
              Charset charset)`

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