# Redis

## Links

命令：http://redis.io/commands
Try：http://try.redis.io/

Redis in Action: https://redislabs.com/ebook/redis-in-action/part-1-getting-started
Redis 实战： http://redisinaction.com/preview


## 常用命令

### 字符串

字符串可以保存： 字节串 (byte string)   整数  浮点数

自增和自减 INCR DECR

当用户将一个值存储到Redis字符串里面的时候，如果这个值可以被解释（interpret）为十进制整数或者浮点数，那么Redis会察觉到这一点，并允许用户对这个字符串执行各种INCR*和DECR*操作。如果用户对一个不存在的键或者一个保存了空串的键执行自增或者自减操作，那么Redis在执行操作时会将这个键的值当作是0来处理。如果用户尝试对一个值无法被解释为整数或者浮点数的字符串键执行自增或者自减操作，那么Redis将向用户返回一个错误。

供Redis处理子串和二进制位的命令 APPEND   APPEND  SETRANGE GETBIT SETBIT BITCOUNT BITOP


Redis中的自增命令和自减命令

| 命令 | 用例和描述 |
| -- | -- |
| INCR | INCR key-name——将键存储的值加上1 |
| DECR | DECR key-name——将键存储的值减去1 |
| INCRBY | INCRBY key-name amount——将键存储的值加上整数amount |
| DECRBY | DECRBY key-name amount——将键存储的值减去整数amount |
| INCRBYFLOAT | INCRBYFLOAT key-name amount——将键存储的值加上浮点数amount，这个命令在Redis 2.6或以上的版本可用 |



供Redis处理子串和二进制位的命令

| 命令 | 用例和描述 |
| -- | -- |
|APPEND|APPEND key-name value——将提供的值value追加到给定键key-name当前存储的值的末尾|
|GETRANGE|GETRANGE key-name start end——获取一个由偏移量start至偏移量end范围内所有字符组成的子串，包括start和end在内
|SETRANGE|	SETRANGE key-name offset value——将从start偏移量开始的子串设置为给定value
|GETBIT|	GETBIT key-name offset——将字节串看作是二进制位串（bit string），并返回位串中偏移量为offset的二进制位的值
|SETBIT|	SETBIT key-name offset value——将字节串看作是二进制位串，并将位串中偏移量为offset的二进制位的值设置为value
|BITCOUNT|	BITCOUNT key-name [start end]——统计二进制位串里面值为1的二进制位的数量，如果给定了可选的start偏移量和end偏移量，那么只对偏移量指定范围内的二进制位进行统计
|BITOP|	BITOP operation dest-key key-name [key-name ...]——对一个或多个二进制位串执行包括并（AND）、或（OR）、异或（XOR）、 非（NOT）在内的任意一种按位运算操作（bitwise operation），并将计算得出的结果保存在dest-key键里面


### 列表

Redis的列表允许用户从序列的两端推入或者弹出元素、获取元素，执行各种常见的列表操作

一些常用的列表命令

|命令|用例和描述|
|--|--|
|RPUSH|	RPUSH key-name value [value ...]——将一个或多个值推入到列表的右端|
|LPUSH|	LPUSH key-name value [value ...]——将一个或多个值推入到列表的左端|
|RPOP|	RPOP key-name——移除并返回列表最右端的元素
|LPOP|	LPOP key-name——移除并返回列表最左端的元素
|LINDEX|	LINDEX key-name offset——返回列表中偏移量为offset的元素
|LRANGE|	LRANGE key-name start end——返回列表从start偏移量到end偏移量范围内的所有元素，包括start和end
|LTRIM|	LTRIM key-name start end——对列表进行修剪，只保留从start偏移量到end偏移量范围内的元素，包括start和end

阻塞式的列表弹出命令以及在列表之间移动元素的命令

|命令|用例和描述|
|--|--|
|BLPOP|	BLPOP key-name [key-name ...] timeout——从第一个非空列表中弹出位于最左端的元素，或者在timeout秒之内阻塞并等待可弹出的元素出现
|BRPOP|	BRPOP key-name [key-name ...] timeout——从第一个非空列表中弹出位于最右端的元素，或者在timeout秒之内阻塞并等待可弹出的元素出现
|RPOPLPUSH|	RPOPLPUSH source-key dest-key——从source-key列表中弹出位于最右端的元素，然后将这个元素推入到dest-key列表的最左端，并向用户返回这个元素
|BRPOPLPUSH|	BRPOPLPUSH source-key dest-key timeout——从source-key列表中弹出位于最右端的元素，然后将这个元素推入到dest-key列表的最左端， 并向用户返回这个元素；如果source-key为空，那么在timeout秒之内阻塞并等待可弹出的元素出现

### 集合

一些常用的集合命令

|命令|	用例和描述|
|--|--|
|SADD|	SADD key-name item [item ...]——将一个或多个元素添加到集合里面，并返回被添加元素当中原本并不存在于集合里面的元素数量
|SREM|	SREM key-name item [item ...]——从集合里面移除一个或多个元素，并返回被移除元素的数量
|SISMEMBER|	SISMEMBER key-name item——检查元素item是否存在于集合key-name里
|SCARD|	SCARD key-name——返回集合包含的元素的数量
|SMEMBERS|	SMEMBERS key-name——返回集合包含的所有元素
|SRANDMEMBER|	SRANDMEMBER key-name [count]——从集合里面随机地返回一个或多个元素。当count为正数时，命令返回的随机元素不会重复； 当count为负数时，命令返回的随机元素可能会出现重复
|SPOP|	SPOP key-name——从集合里面移除并返回一个随机元素
|SMOVE|	SMOVE source-key dest-key item——如果集合source-key包含元素item， 那么从集合source-key里面移除元素item，并将元素item添加到集合dest-key中； 如果item被成功移除，那么命令返回1，否则返回0

用于组合和处理多个集合的Redis命令

|命令|	用例和描述|
|--|--|
|SDIFF|	SDIFF key-name [key-name ...]——返回那些存在于第一个集合、但不存在于其他集合中的元素（数学上的差集运算）
|SDIFFSTORE|	SDIFFSTORE dest-key key-name [key-name ...]——将那些存在于第一个集合、但并不存在于其他集合中的元素（数学上的差集运算）存储到dest-key中
|SINTER|	SINTER key-name [key-name ...]——返回那些同时存在于所有集合中的元素（数学上的交集运算）
|SINTERSTORE|	SINTERSTORE dest-key key-name [key-name ...]——将那些同时存在于所有集合的元素（数学上的交集运算）保存到键dest-key
|SUNION|	SUNION key-name [key-name ...]——返回那些至少存在于一个集合中的元素（数学上的并集计算）
|SUNIONSTORE|	SUNIONSTORE dest-key key-name [key-name ...]——将那些至少存在于一个集合中的元素（数学上的并集计算）存储到dest-key中

### 散列

用于添加和删除键值对的散列操作

|命令|	用例和描述
|--|--|
|HMGET|	HMGET key-name key [key ...]——从散列里面获取一个或多个键的值
|HMSET|	HMSET key-name key value [key value ...]——为散列里面的一个或多个键设置值
|HDEL|	HDEL key-name key [key ...]——删除散列里面的一个或多个键值对，返回成功找到并删除的键值对数量
|HLEN|	HLEN key-name——返回散列包含的键值对数量|

展示Redis散列的更高级特性

|命令|	用例和描述
|--|--|
|HEXISTS|	HEXISTS key-name key——检查给定键是否存在于散列中
|HKEYS|	HKEYS key-name——获取散列包含的所有键
|HVALS|	HVALS key-name——获取散列包含的所有值
|HGETALL|	HGETALL key-name——获取散列包含的所有键值对
|HINCRBY|	HINCRBY key-name key increment——将键key保存的值加上整数increment
|HINCRBYFLOAT|	HINCRBYFLOAT key-name key increment——将键key保存的值加上浮点数increment

### 有序集合

一些常用的有序集合命令

|命令|	用例和描述
|--|--|
|ZADD|	ZADD key-name score member [score member ...]——将带有给定分值的成员添加到有序集合里面
|ZREM|	ZREM key-name member [member ...]——从有序集合里面移除给定的成员，并返回被移除成员的数量
|ZCARD|	ZCARD key-name——返回有序集合包含的成员数量
|ZINCRBY|	ZINCRBY key-name increment member——将member成员的分值加上increment
|ZCOUNT|	ZCOUNT key-name min max——返回分值介于min和max之间的成员数量
|ZRANK|	ZRANK key-name member——返回成员member在key-name中的排名
|ZSCORE|	ZSCORE key-name member——返回成员member的分值
|ZRANGE|	ZRANGE key-name start stop [WITHSCORES]——返回有序集合中排名介于start和stop之间的成员，如果给定了可选的WITHSCORES选项，那么命令会将成员的分值也一并返回

有序集合的范围型数据获取命令和范围型数据删除命令，以及并集命令和交集命令

|命令|	用例和描述
|--|--|
|ZREVRANK|	ZREVRANK key-name member——返回有序集合里成员member所处的位置，成员按照分值从大到小排列
|ZREVRANGE|	ZREVRANGE key-name start stop [WITHSCORES]——返回有序集合给定排名范围内的成员，成员按照分值从大到小排列
|ZRANGEBYSCORE|	ZRANGEBYSCORE key min max [WITHSCORES] [LIMIT offset count]——返回有序集合中，分值介于min和max之间的所有成员
|ZREVRANGEBYSCORE|	ZREVRANGEBYSCORE key max min [WITHSCORES] [LIMIT offset count]——获取有序集合中分值介于min和max之间的所有成员，并按照分值从大到小的顺序来返回它们
|ZREMRANGEBYRANK|	ZREMRANGEBYRANK key-name start stop——移除有序集合中排名介于start和stop之间的所有成员
|ZREMRANGEBYSCORE|	ZREMRANGEBYSCORE key-name min max——移除有序集合中分值介于min和max之间的所有成员
|ZINTERSTORE|	ZINTERSTORE dest-key key-count key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX]——对给定的有序集合执行类似于集合的交集运算
|ZUNIONSTORE|	ZUNIONSTORE dest-key key-count key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX]——对给定的有序集合执行类似于集合的并集运算

### 发布和订阅

Redis提供的发布与订阅命令

|命令|	用例和描述
|--|--|
|SUBSCRIBE|	SUBSCRIBE channel [channel ...]——订阅给定的一个或多个频道
|UNSUBSCRIBE|	UNSUBSCRIBE [channel [channel ...]]——退订给定的一个或多个频道，如果执行时没有给定任何频道，那么退订所有频道
|PUBLISH|	PUBLISH channel message——向给定频道发送消息
|PSUBSCRIBE|	PSUBSCRIBE pattern [pattern ...]——订阅与给定模式相匹配的所有频道
|PUNSUBSCRIBE|	PUNSUBSCRIBE [pattern [pattern ...]]——退订给定的模式，如果执行时没有给定任何模式，那么退订所有模式

### 其他命令

排序

基本事务

键的过期时间

用于处理过期时间的Redis命令
![](http://image.webreader.duokan.com/mfsv2/download/s010/p01xfjITuKmc/KJ70C96G8kFB40.jpg)
|命令|	示例和描述
|--|--|
|PERSIST|	PERSIST key-name——移除键的过期时间
|TTL|	TTL key-name——返回给定键距离过期还有多少秒
|EXPIRE|	EXPIRE key-name seconds——让键key-name在给定的seconds秒之后过期
|EXPIREAT|	EXPIREAT key-name timestamp——将给定键的过期时间设置为给定的UNIX时间戳
|PTTL|	PTTL key-name——返回给定键距离过期时间还有多少毫秒，这个命令在Redis 2.6或以上版本可用
|PEXPIRE|	PEXPIRE key-name milliseconds——让键key-name在milliseconds毫秒之后过期，这个命令在Redis 2.6或以上版本可用
|PEXPIREAT|	PEXPIREAT key-name timestamp-milliseconds——将一个毫秒级精度的UNIX时间戳设置为给定键的过期时间，这个命令在Redis 2.6或以上版本可用

### 持久化

Snapshotting

AOF

Replication


What happens when a slave connects to a master

|Step|Master operations|Slave operations
|--|--|--|
|1|(waiting for a command)|(Re-)connects to the master;issues the SYNC command 
|2|Starts BGSAVE operation; keeps a backlog of all write commands sent after BGSAVE|Serves old data (if any), or returns errors to commands (depending on configuration)
|3|Finishes BGSAVE; starts sending the snapshot to the slave; continues holding a backlog of write commands|Discards all old data (if any); starts load- ing the dump as it’s received
|4|Finishes sending the snapshot to the slave; starts sending the write command backlog to the slave|Finishes parsing the dump; starts responding to commands normally again
|5|Finishes sending the backlog; starts live stream- ing of write commands as they happe|Finishes executing backlog of write com- mands from the master; continues execut- ing commands as they happen

### Transactions

WATCH MULTI EXEC DISCARD



## 设计实现

### 简单动态字符串 Simple dynamic string SDS

保存字符串值、缓冲区

SDS与C字符串区别

- 常数复杂度获取字符串长度
- 杜绝缓冲区溢出
- 减少修改字符串时带来的内存重分配次数
  - 空间预分配（len < 1M, free = len; len >= 1M. free = 1M）
  - 惰性空间释放
- 二进制安全，字符串里可以包含空格
- 兼容部分C字符串函数

![](http://image.webreader.duokan.com/mfsv2/download/s010/p010v4xnWs6S/JouBfRJ4WFHuCl.jpg)


API

![](http://image.webreader.duokan.com/mfsv2/download/s010/p01xfjITuKmc/KJ70C96G8kFB40.jpg)

![](http://image.webreader.duokan.com/mfsv2/download/s010/p01oDab2gaYj/NyztOLV0Whk1lO.jpg)

### 链表

![](http://image.webreader.duokan.com/mfsv2/download/s010/p01RJP5dpzIa/6mOyLELYEQyZ4L.jpg?thumb=1024x&scale=auto)
双端 无环 带表头指针和表尾指针 带链表长度计数器 多态

### 字典

![](http://image.webreader.duokan.com/mfsv2/download/s010/p01AMW8EM5GU/c2DhIJrE6xc9fo.jpg?thumb=1024x&scale=auto)

渐进式rehash，把操作均摊在每个操作上

### 跳跃表
![](http://image.webreader.duokan.com/mfsv2/download/s010/p01sK2Lei0nP/J0nSWjKdeVKegx.jpg?thumb=1024x&scale=auto)

使用在有序集合、集群节点内部

### 压缩列表
压缩列表（ziplist）是列表键和哈希键的底层实现之一。当一个列表键只包含少量列表项，并且每个列表项要么就是小整数值，要么就是长度比较短的字符串，那么Redis就会使用压缩列表来做列表键的底层实现。

