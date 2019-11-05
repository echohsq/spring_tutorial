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

### 常用JPA注解：

**实体**

- @Entity（实体标注） @MappedSuperclass（父类标注）
- @Table（name)

**主键**

- @Id
  - @GeneratedValue（strategy，generator）（主键生成策略）
  - @SequenceGenerator（name，sequenceName）（主键序列类型）

**举例**

```java
@Entity(name = "Product")
public static class Product {
  @Id
  @GeneratedValue(
          strategy = GenerationType.SEQUENCE,
          generator = "sequence-generator"
  )
  @SequenceGenerator(
          name = "sequence-generator",
          sequenceName = "product_sequence"
  )
  private Long id;
  
  @Column(name = "product_name")
  private String name;
}
```

**映射**

- @Column（name, nullable, length, insertable, updatable)
- @JoinTable(name), @JoinColumn(name)

**关系**

- @OneToOne, @OneToMany, @ManyToOne, @ManyToMany
- @OrderBy

## 使用Lombok

**常用功能**

- @Getter / @Setter
- @ToString
- @NoArgsConstructor / @RequiredArgsConstructor / @AllArgsConstructor
- @Data (混合注解包括getter和setter)
- @Builder
- @Slf4j / @CommonsLog / @Log4j2