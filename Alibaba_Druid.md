# 继承自springbootDataSource.md对Druid的一些展开说明

 ## 监控---慢SQL日志

- 系统属性配置（使用 java -d输出）
  - druid.stat.logSlowSql=true
  - druid.stat.slowSqlMillis=3000

- SpringBoot (application.properties)
  - spring.datasource.druid.filter.stat.enabled=true
  - spring.datasource.druid.filter.stat.log-slow-sql=true
  - spring.datasource.druid.filter.stat.slow-sql-millis=3000



