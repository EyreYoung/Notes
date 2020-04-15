# Java基础

## Java和Php的区别？

- Php的库函数用C实现，Java核心运行时类库用Java编写，Java应用运行时编写的代码、引用的类库、框架都在JVM上解释执行
- Php内置模板引擎，Java Web需要使用外部容器如Tomcat

## 正则表达式？

- 用来查找符合某些复杂规则的字符串
- 记录文本规则的代码
- Java中String类提供正则表达式操作

## 比较Java和JavaScript？

- Java来自Sun Mircosystems公司，是面向对象的程序设计语言。JavaScript来自Netscape公司，是基于对象和时间驱动的解释型语言
- Java源代码执行前必须进行编译，JavaScript代码直接由浏览器解释执行
- Java采用强类型变量检查，JavaScript使用弱类型变量，由解释器在运行时推断类型
- 代码格式不一样

## Java如何跳出多重嵌套循环？

- 最外层循环标记A
- `break A;`
- 避免使用

## `&` 和 `&&` 的区别？

- `&` 的用法有按位与和逻辑与
- `&&` 是短路和运算
- `&&` 是false的话，右边不会进行运算

## `int`和`Integer`的区别？

- 基本类型和包装类型
- Java中，一切皆对象，八种基本类型不是对象
- 基本类型不需要`new`来创建，封装类型需要
- 基本类型直接把变量的值存在堆栈中。封装类型通过引用指向实例，具体实例保存在堆中
- 基本类型初始值为0或者`false`，封装类型初始值为`null`
- Java5引入自动装箱/拆箱机制，可以互相转换

## 如何输出某种编码的字符串？

- `public String​(byte[] bytes,
      Charset charset)`

### `String`和`StringBuffer`的区别？

- 都是`final`类，不能被继承
- `String`长度不可变，每次修改都会生成新的String对象，经常改变长度的话不应使用
- `StringBuffer`会对对象本身进行操作
- `StringBuilder`与`StringBuffer`兼容，用于字符串缓冲区被单个线程使用，比`StringBuffer`快，但不适合多线程
- `String`类的 `+` 拼接性能差，应该使用`StringBuffer`或`StringBuilder`

## 数组Array和列表ArrayList的区别？

- Array不能修改大小，ArrayList可以动态改变大小
- Array可以存储基本类型和对象类型，但必须是同类型，ArrayList只能存储对象类型
- ArrayList提供更多方法，比如`addAll()`

## 值传递和引用传递？

- 值传递传递的是真实内容的一个副本，形参不影响实参
- 引用传递时形参和实参指向同一个对象，形参操作会影响实参对象
- Java中只有值传递，对引用对象传递的是地址的副本，但会指向同一个对象

## Java支持的数据类型？

- `byte/short/int/long/float/double/char/boolean`

## 自动拆装箱？

- Java编译器在基本数据类型和对应对象包装类型之间做的转换，如`int/Integer double/Double`

### `4.0 - 3.6 = 0.40000001`?

- 二进制无法精确表示十进制小数，转换过程中出现误差

## 十进制数在内存中如何存储？

- 补码的形式

## `Lambda`表达式优缺点？

- 简洁
- 方便并行计算
- 不易调试，不易读

## Java8新特性？

- 接口的默认方法和静态方法。解决接口修改与接口的实现类不兼容问题，方便向前兼容
- 函数式接口 `@FunctionalInterface` 和 `lambda` 表达式。
- 方法引用。
- Stream API。`java.util.Stream`
- Optional。
- `Data Time`API。对时间和日期的处理

## `==` 比较？

- 基本类型：直接比较大小
- 引用类型：比较两者在内存中的地址，只有同时`new`出来的对象才会返回`true`

## `Object` 的 `hashCode()` 如何计算？

- 本地方法，使用C/C++实现，一般是返回内存地址，取决于JVM的实现

## 为什么重写了 `equals()` 还要重写 `hashCode()` ?

- HashMap中的比较需要 `equals()` 和 `hashCode()` 同时运行。先用 `hashCode()` 比较，如果相等则进一步使用 `equals()` 进行比较，假如 `hashCode()`不相等，则不会继续比较。

## 静态变量和实例变量的区别？

- 静态变量声明时要加`static`
- 静态变量是类的属性，也叫类变量，只要字节码文件被加载，就会被分配空间。可以直接通过类名使用
- 实例变量是对象的属性，必须创建了实例对象，其中的变量才会被分配空间。必须创建对象后通过对象来引用

## Java中 `final` 关键字怎么用？

- 修饰类。用来表明类不能被继承。final类的成员变量可以根据需要设为final，所有成员方法都被隐式设为final
- 修饰方法。用来禁止方法在子类中被修改。类的`private`方法被隐式设为final
- 修饰变量。如果是基本类型则值不能修改；如果是引用类型则初始化后不能再指向另一个对象