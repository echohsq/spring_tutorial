# ***SpringBoot事务***
## ***事务抽象的核心接口***
1. PlatformTransactionManager
- DataSourceTransactionManager
- HibernateTransactionManager
- JtaTransactionManager
- 
2. TransactionDefinition
- Propagation
- Isolation
- Timeout
- Read-only status
3. 代码示例：
```java
void commit(TransactionStatus status) throws TransactionException;
void rollback(TransactionStatus status) throws TransactionException;
TransactionStatus getTransaction(@Nullable TransactionDefinition definition) throws TransactionException;
```
## ***事务传播特性***
传播性 | 值 | 描述
----------| ----| -----
PROPAGATION_REQUIRED | 0 | 当前有事务就用当前的，没有就用最新的
PROPAGATION_SUPPORTS | 1 | 事务可有可无，不是必须的
PROPAGATION_MANDATORY | 2 | 当前一定要有事务，不然就抛异常
PROPAGATION_REQUIRES_NEW | 3 | 无论是否有事务，都起个新的事务
PROPAGATION_NOT_SUPPORTED | 4 | 不支持事务，按非事务方式运行
PROPAGATION_NEVER | 5 | 不支持事务，如果有事务则抛异常
PROPAGATION_NESTED | 6 | 当前有事务就在当前事务里再起一个事务