 # Spring Data

在保留底层存储特性的同时，提供相对一致的、基于Spring的编程模型

## （一）主要模块

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

## （二）使用Lombok

**常用功能**

- @Getter / @Setter
- @ToString
- @NoArgsConstructor / @RequiredArgsConstructor / @AllArgsConstructor
- @Data (混合注解包括getter和setter)
- @Builder
- @Slf4j / @CommonsLog / @Log4j2

## （三）使用Spring JPA来操作数据库

### Repository:

**开启注解**

@EnableJpaRepositories

**定义接口继承以下接口即可使用，无需定义实现类**

- CrudRepository<T, ID>
- PagingAndSortingRepository<T, ID>
- JpaRepository<T, ID>

### 定义查询：

**根据方法名定义查询**

- find...By... / read...By... / query...By... / get...By...
- Count...By...
- ...OrderBy... [Asc / Desc]
- And / Or / IgnoreCase
- Top / First / Distinct

### 分页查询：

- PagingAndSortingRepository<T, ID>
- Pageable / Sort
- Slice\<T\> / Page\<T\>



