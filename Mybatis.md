# 认识MyBatis

## MyBatis

- 一款优秀的持久层框架
- 支持定制化SQL、存储过程和高级映射

## 在Spring中使用MyBatis

- MyBatis Spring Adapter
- MyBatis Spring-Boot-Starter

## 在application.properties中对MyBatis进行简单配置

- ```properties
  mybatis.mapper-locations = classpath*:mapper/**/*.xml //指定xml映射文件
  mybatis.type-aliases-package = 类型别名的包名  //包名下的类使用时可以直接写类名
  mybatis.type-handlers-package = TypeHandler 扫描包名  //类型转换的辅助类
  mybatis.configuration.map-underscore-to-camel-case = true  //将下划线转换为驼峰规则
  ```

  

## Mapper的定义与扫描

- @MapperScan 配置扫描位置
- @Mapper 定义接口
- 映射的定义： --XML和注解

# 让MyBatis更好用的工具

## 认识MyBatis Generator

MyBatis Generator（http://www.mybatis.org/generator）

- MyBatis代码生成器
- 根据数据库表生成相关代码
  - POJO
  - Mapper接口
  - SQL Map XML

## 运行MyBatis Generator

命令行

- java -jar mybatis-generator-core-x.x.x.jar -configfile generatorConfig.xml

Maven Plugin (mybatis-generator-maven-plugin)

- mvn mybatis-generator:generate
- ${basedir}/src/main/resources/generatorConfig.xml

java程序

## 配置MyBatis Generator

**generator Configuration**

**context**

- jdbcConnection
- javaModelGenerator
- sqlMapGenerator
- javaClientGenerator (ANOTATEDMAPPER / XMLMAPPER / MIXDEAPPER)
- table 

## 生成时可以使用的插件

### 内置插件都在org.mybatis.generator.plugins包中：

- FluentBuilderMethodsPlugin
- ToStringPlugin
- SerializablePlugin
- RowBoundsPlugin //提供分页方法
- ......

### 使用生成的对象

- 简单操作，直接使用生成的xxxMapper的方法。
- 复杂查询，使用生成的xxxExample对象。



```java
Coffee latte = new Coffee() // FluentBuilderMethodsPlugin方法实现withxxx
                 .withName("latte")
                 .withPrice(Money.of(CurrencyUnit.of("CNY"), 30.0))
                 .withCreateTime(new Date())
                 .withUpdateTime(new Date());
coffeeMapper.insert(latte);

Coffee s = coffeeMapper.selectByPrimaryKey(1L);
log.into("Coffee {}", s);

CoffeeExample example = new CoffeeExample();
example.createCriteria().andNameEqualTo("latte"); //创建查找条件  
List<Coffee> list = coffeeMapper.selectByExample(example);
list.foreach(e -> log.info("selectByExample: {}", e));
```

## 认识Page Helper

**Mybatis PageHelper(https://pagehelper.github.io)**

- 支持多种数据库
- 支持多种分页方式
- SpringBoot支持（https://github.com/pagehelper/pagehelper-spring-boot）
  - Pagehelper-spring-boot-starter