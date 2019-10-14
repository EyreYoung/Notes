# Think in Java 学习笔记
---
## 一、对象入门
- Java的多项设计思想
- 面向对象的程序设计概念

### 1.1 抽象的进步
`SmallTalk`的五大基本特征：
1. 所有东西都是对象
2. 程序是对象的组合
3. 每个对象都有自己的存储空间，能够容纳其他对象
4. 每个对象都有一种类型
5. 同一类对象能接收相同的东西(对象的可替换性)

### 1.2 对象的接口
对象 类型 接口
**eg**:  
Type Name: `Light`  
Interface: `on()` 
           `off()` 
           `brighten()` 
           `dim()` 
``` java
Light lt = new Light();
lt.on();
```
lt: 句柄

### 1.3 实现方案的隐藏
public：后续的定义任何人可以使用
private：只有自己、类型创建者、类型的内部函数能够访问
friendly：只能在Package范围内使用
protected：继承的类可以访问

### 1.4 方案的重复使用
- 直接使用对象
- 组织对象(通过新类包含)
- 继承(应首先考虑组织，更加简单灵活)

### 1.5 继承：重新使用接口

- 改善基础类
- 等价和类似关系

### 1.6 多形对象的互换使用

![类型继承](https://github.com/EyreYoung/Notes/blob/master/Book/img/1.6-1.png)
``` java
void doStuff(Shape s){
    s.erase();
    // ...
    s.draw();
}

Circle c = new Circle();
Triange t = new Triangle();
Line l = new Line();
doStuff(c);
doStuff(t);
doStuff(l);
```
**Upcasting**：衍生类当作父类处理

#### 1.6.1 动态绑定
**多形性(Polymorphism)**：在不知道具体类型的情况下，将消息发给对象，采取行动仍然正确

#### 1.6.2 抽象的基础类和接口
- `abstract` 关键字
- 无法实际创建对象的类型
- 抽象方法只能在抽象类中创建
- 继承抽象类后必须实现抽象方法，否则自身也是抽象类

- interface禁止所有函数定义

### 1.7 对象的创建和存在时间
- 存储、存在时间在编写程序时决定，对象放置在堆栈或静态存储区域
- 内存池中动态创建对象
- 垃圾收集器

#### 1.7.1 集合与继承器
