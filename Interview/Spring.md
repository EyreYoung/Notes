# Spring

## 事务管理？

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