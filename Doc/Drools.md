# Drools Documentation
https://docs.jboss.org/drools/release/7.27.0.Final/drools-docs/html_single/index.html

## Introduction
KIE(Knowledge Is Everything)包含：
- **Drools**是一个业务规则管理系统，具有基于前向链接和后向链接的推理规则引擎，可对业务规则和复杂的事件处理进行快速可靠的评估。
- **jBPM**是一种灵活的业务流程管理套件，允许您通过描述实现这些目标所需执行的步骤来对业务目标进行建模。
- **OptaPlanner**是一个约束解决方案，可以优化用例，例如员工排班，车辆路线，任务分配和云优化。
- **Business Central**是一个功能全面的Web应用程序，用于可视化组成自定义业务规则和流程。
- **UberFire**是一个基于Web的工作台框架，其灵感来自Eclipse Rich Client Platform。

Libraries：
- **`knowledge-api.jar`**：提供了接口和工厂。用户API，引擎API。
- **`knowledge-internal-api.jar`**：这提供了内部接口和工厂。
- **`drools-core.jar`**：Drools引擎的核心，运行组件。包含RETE引擎和LEAPS引擎。如果要预编译规则（并通过Package或RuleBase对象进行部署），则这是唯一的运行时依赖项。
- **`drools-compiler.jar`**：包含用于获取规则源和构建可执行规则库的编译器/生成器组件。应用程序的运行时依赖项，但是如果您正在预编译规则，则不必如此。依赖`drools-core`
- **`drools-jsr94.jar`**：这是符合JSR-94的实现，这实际上是drools-compiler组件上的一层。请注意，由于JSR-94规范的性质，并非所有功能都可以通过此接口轻松公开。在某些情况下，直接进入Drools API会更容易，但是在某些环境中，必须使用JSR-94。
- **`drools-decisiontables.jar`**：决策表的“编译器”组件，使用了`drools-compiler`组件。支持`excel`和`CSV`输入格式。

使用`Maven`：
```XML
​<dependencyManagement>
   ​<dependencies>
     ​<dependency>
       ​<groupId>org.drools</groupId>
       ​<artifactId>drools-bom</artifactId>
       ​<type>pom</type>
       ​<version>...</version>
       ​<scope>import</scope>
     ​</dependency>
     ​...
   ​</dependencies>
 ​</dependencyManagement>
 ​<dependencies>
   ​<dependency>
     ​<groupId>org.kie</groupId>
     ​<artifactId>kie-api</artifactId>
   ​</dependency>
   ​<dependency>
     ​<groupId>org.drools</groupId>
     ​<artifactId>drools-compiler</artifactId>
     ​<scope>runtime</scope>
   ​</dependency>
   ​...
 ​<dependencies
```

## KIE
