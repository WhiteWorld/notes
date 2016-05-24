# Redis

## Links

命令：http://redis.io/commands
Try：http://try.redis.io/

Redis in Action: https://redislabs.com/ebook/redis-in-action/part-1-getting-started
Redis 实战： http://redisinaction.com/preview


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
SINTER	SINTER key-name [key-name ...]——返回那些同时存在于所有集合中的元素（数学上的交集运算）
SINTERSTORE	SINTERSTORE dest-key key-name [key-name ...]——将那些同时存在于所有集合的元素（数学上的交集运算）保存到键dest-key
SUNION	SUNION key-name [key-name ...]——返回那些至少存在于一个集合中的元素（数学上的并集计算）
SUNIONSTORE	SUNIONSTORE dest-key key-name [key-name ...]——将那些至少存在于一个集合中的元素（数学上的并集计算）存储到dest-key中