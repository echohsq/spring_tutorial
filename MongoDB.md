# Spring与MongoDB

## Spring对MongoDB的支持

**MongoDB是一款开源的文档型数据库**

- https://www.mongodb.com

**Spring对MongoDB的支持**

- Spring Data MongoDB
  - MongoTemplate
  - Repository支持

**注解**

- @Document
- @Id

**MongoTemplate**

- save / remove
- Criteria / Query / Update

**在docker中创建MongoDB容器**

- docker pull 镜像

- docker run --name mongodb -p 27017:27017 -v ~/docker-data/mongo:/data/db -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=admin -d mongo

- docker ps 查询当前正在运行的容器

- MongoDB创建文件存储库， 命令： use 名称

  db.createUser(

  ​    {

  ​      user: "springbucks",

  ​      pwd: "springbucks",

  ​      roles: [

  ​               { role: "readWrite", db: "springbucks" }

  ​     ]

  }

  )

**properties文件配置**

```java
spring.data.mongodb.uri=mongodb://springbucks:springbucks@localhost:27017/springbucks
```

前两个springbucks分别指向用户名和密码。

## spring Data MongoDB 的 Repository

@EnableMongoRepositories

**对应接口**

- MongoRepository<T, ID>
- PagingAndSortingRepository<T, ID>
- CrudRepository<T, ID>

