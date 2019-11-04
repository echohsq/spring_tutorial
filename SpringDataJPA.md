 # Spring Data

在保留底层存储特性的同时，提供相对一致的、基于Spring的编程模型

## 主要模块

- Spring Data Commons
- Spring Data JDBC
- Spring Data JPA
- Spring Data Redis
- ...

### 使用spring配置：

```xml
<dependencyManagement>
     <dependencies>
       <dependency>
         <groupId>org.springframework.data</groupId>
         <artifactId>spring-data-releasetrain</artifactId>
         <version>Lovelace-SR4</version>
         <scope>import</scope>
         <type>pom</type>
       </dependency>
     </dependencies>
</dependencyManagement>
```

### 使用springboot设置：

```xml
<dependency>
    <groudId>org.springframe.boot</groudId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

