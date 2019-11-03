# ***spring的JDBC操作类***
## spring-jdbc（包）
- core，jdbcTemplate等相关核心接口和类
- datasource，数据源相关的辅助类
- object，将基本的JDBC操作封装成对象
- support，错误码等其他辅助工具
## 常用的bean注解
通过注解来定义Bean
- @Component：通用注解
- @Repository：dao，数据操作的一个仓库
- @Service：业务的服务，可以使用Service注解
- @Controller：springMVC，使用Controller注解
- @RestController：开发Restful应用
##  jdbc   Template
- query
- queryForObject
- queryForList
- queryForMap
- update（插入，修改，删除）
- execute
- 批量上传 
  - jdbcTemplate.batchUpdate("INSERT INTO FOO(BAR) VALUES (?);", new BatchPreparedStatementSetter(){})
  - List<T> list ; namedParameterJdbcTemplate.batchUpdate("INSERT INTO FOO(BAR) VALUES(: bar);", SqlParameterSourceUtils.createBatch(list));

## spring对于jdbc的异常处理

![](/Volumes/moveDisk/files/markdown/spring_tutorial/images/jdbc_exception.png)

Spring会将数据操作的异常转换为DataAccessException，无论使用何种数据处理方式，都是用一样的处理异常。

Spring 将对不同数据库的处理放在了，sql-error-code.xml文件和sqlErrorCode.java下进行处理。

**定义错误码解析逻辑**

