

# Spring常用注解

## Java Config相关注解：

- @Configuration
- @ImportResource
- @ComponentScan
- @Bean
- @ConfigurationProperties

## 定义相关注解（类）：

- @Component/@Repository/@Serivce
- @Controller/@RestController
- @RequestMapping

## 注入相关注解：

- @Autowired/@Qualifier(具体到类，防止歧义)/@Resource(具体到类，防止歧义)
- @Value（传一些值或者表达式）

# Actuator提供的一些好用的Endpoint

| URL               | 作用                 |
| ----------------- | -------------------- |
| /actuator/health  | 健康检查             |
| /actuator/beans   | 查看容器中所有的Bean |
| /actuator/mapping | 查看Web的URL映射     |
| /actuator/env     | 查看环境信息         |

# 如何解锁Endpoint

默认：

- /actuator/health 和 /actuator/info 可web访问

解锁所有Endpoint：

- application.properties / application.yml
  - Management.endpoints.web.exposure.include=* (health,beans使用逗号分隔)