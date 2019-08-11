# spring框架基础
## 使用静态和实例工厂方法创建spring bean
1.静态工厂类
```xml
<bean id="dao" class="DaoFactory" factory-method="getFixedDepositDao">
<constructor-arg index="0" value="jdbc"/>
</bean>
```
2.动态工厂类
```xml
<bean id="daoFactory" class="DaoFactory" >
<bean id="dao" factory-bean="daoFactory" factory-method="getFixedDepositDao">
<constructor-arg index="0" value="jdbc"/>
</bean>
```
## 基于构造函数的DI（依赖注入）