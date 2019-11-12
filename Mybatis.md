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