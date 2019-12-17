# Spring 对 Redis 的支持

**Redis是一款开源的内存KV存储，支持多种数据结构**

- https://redis.io

**Spring 对 Redis的支持**

- Spring Data Redis
  - 支持的客户端 Jedis / Lettuce
  - RedisTemplate
  - Repository支持

**Redis的哨兵模式**

**Redis Sentinel 是 Redis 的一种高可用方案**

- 监控、通知、自动故障转移、服务发现
- 使用JedisSentinelPool来处理redis哨兵模式

**Redis的高可用、集群模式**

**Redis Cluster redis集群** 

- 数据自动分片 （分成16384个Hash Slot）
- 在部分节点失效时有一定可用性

**JedisCluster**

- Jedis只从Master读数据，如果想要自动读写分离，可以定制