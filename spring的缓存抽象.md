# spring的缓存抽象

## 为不同的缓存提供一层抽象

- 为java方法增加缓存，缓存执行结果
- 支持ConcurrentMap、EhCache、Caffeine、JCache（JSR-107）
- 接口
  - org.springframework.cache.Cache
  - org.springframework.cache.CacheManager

## 基于注解的缓存

**@EnableCaching**

- @Cacheable 缓存注入
- @CacheEvict 缓存清理
- @CachePut 不管方法执行情况，进行缓存设置
- Caching 对缓存进行打包
- CacheConfig 设置缓存名字

## 通过Spring Boot配置Redis缓存

```xml
<dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
<dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-date-redis</artifactId>
</dependency>
```

```java
spring.cache.type=redis
spring.cache.cache-names=coffee
spring.cache.redis.time-to-live=5000
spring.cahce.redis.cache-null-values=false
spring.redis.host=localhost
```

```java
@Slf4j
@service
@CacheConfig(cacheName = "coffee")
public class CoffeeService {
  @AutoWired
  private CoffeeRepository coffeeRepository;
  @Cacheable
  public List<Coffee> findAllCoffee() {
    return coffeeRepository.findAll();
  }
  @CacheEvict
  // 删除缓存
  public void reloadCoffee() {
    
  }
}
```

# 与Redis建立连接

**配置连接工厂**

- LettuceConnectionFactory 与 JedisConnectionFactory
  - RedisStandaloneConfiguration
  - RedisSentinelConfiguration
  - RedisClusterConfiguration

**读写分离**

Lettuce内置支持读写分离

- 只读主、只读从
- 优先读主，优先读从

LettuceClientConfiguration

LettucePoolingClientConfiguration

LettuceClientConfigurationBuilderCustomizer

**RedisTemplate[一定要记得设置过期时间]**

RedisTemplate<K, V>

- opsForXxx() ---> opsForHash()

StringRedisTemplate

## Redis Repository

**实体注解**

- @RedisHash
- @Id
- @Indexed