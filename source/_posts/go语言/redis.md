### 全局命令

-----

1、```keys *```  	

查看所有键，遍历所有键，线上禁止使用

2、```dbsize```      

键总数，直接读取redis内置变量

3、```exists key```

检查键是否存在，1代表存在，0不存在。

4、```del key [key ...]```

删除键，可删除多个。返回结果为删除成功键的个数，键不存在时返回0。

5、```expire key seconds```

对键添加过期时间。单位为秒。```ttl key``` 可观察键hello的剩余过期时间。

6、```type key```

键的数据结构类型。返回```string```(字符串)、```hash```(哈希)、```list```(列表)、```set```(集合)、```zset```(有序集 合)等类型。

7、```object encoding key```

查看内部编码类型。



### 类型

-------

#### 字符串

> redis键都是字符串类型。

常用命令：

- ```set key value [ex seconds] [px milliseconds] [nx|xx]```，ex seconds: 为键设置秒级过期时间，px milliseconds:为键设置毫秒级过期时间。nx: 键必须不存在，才能设置成功，用于添加。xx:与nx相反，键必须存在，才可以设置成功，用于更新。

- ```mset key value```，批量设置值。

- ```mget key```，批量获取值。

- ```incr key```，key值为整数或不存在，加1，key值不为整数，返回错误。类似有```decr、decrby、incrby```等命令。



#### 哈希

#####常用命令：

- ```hset key field value```，设置值。
- ```hget key field```，获取值。
- ```hdel key field [field ...]```，删除值。
- ```hlen key```，计算field个数。
- ```hmset key field、hmget key field```，批量设置、获取。

- ```hexists key field```，判断field是否存在。
- ```hkeys key```，获取所有的field。
- ```hvals key```，获取所有的value。

#####内部编码：

- ziplist(压缩列表)。

> 哈希类型field个数小于hash-max-ziplist-entries 配置(默认512个)、同时所有值都小于hash-max-ziplist-value配置(默认64 字节)时，Redis会使用ziplist作为哈希的内部实现。ziplist使用更加紧凑的结构实现多个元素的连续存储，所以在节省内存方面比hashtable更加优秀。

- hashtable(哈希表)

> 当哈希类型无法满足ziplist的条件时，Redis会使 用hashtable作为哈希的内部实现，因为此时ziplist的读写效率会下降，而 hashtable的读写时间复杂度为O(1)。



#### 列表

> 列表(list)类型是用来存储多个有序的字符串。



#####常用命令：

1、添加：

- ```rpush key value [value]```
- ```lpush key value [value]```
- ```linsert key before|after pivot value```

2、查找

- ```lrange key start end```
- ```lindex key index```
- ```llen key```

3、删除

- ```lpop key```
- ```rpop key```
- ```lrem count value```
- ```ltrim key start end```

4、修改

- ```lset key index value```

5、阻塞操作

- ```blpop、 brpop```

#####内部编码

- ziplist(压缩列表):当列表的元素个数小于list-max-ziplist-entries配置 (默认512个)，同时列表中每个元素的值都小于list-max-ziplist-value配置时 (默认64字节)，Redis会选用ziplist来作为列表的内部实现来减少内存的使用。

- linkedlist(链表):当列表类型无法满足ziplist的条件时，Redis会使用 linkedlist作为列表的内部实现。



#### 集合

> 集合(set)类型也是用来保存多个的字符串元素，但和列表类型不一 样的是，集合中不允许有重复元素，并且集合中的元素是无序的，不能通过 索引下标获取元素。

##### 常用命令

- ```sadd key element [element]```	返回结果为添加成功的元素的个数

- ```srem key element [element]```    返回结果为删除成功的元素的个数
- ```scard key```                                      计算元素个数
- ```sismember key element```              判断元素是否在集合中，在返回1，否则返回0
- ```srandmember key [count]```          随机返回集合中的count个元素
- ```spop key```                                        随机弹出一个元素
- ```smembers key```                                获取所有元素
- ```sinter key [key ...]```                求多个集合的交集
- ```sunion key [key ...]```                求多个集合的并集
- ```sdiff key [key ...]```                  求多个集合的差集

##### 内部编码

- intset(整数集合):当集合中的元素都是整数且元素个数小于set-max- intset-entries配置(默认512个)时，Redis会选用intset来作为集合的内部实现，从而减少内存的使用。

- hashtable(哈希表):当集合类型无法满足intset的条件时，Redis会使 用hashtable作为集合的内部实现。



#### 有序集合

##### 常用命令

- ```zadd key score member [score member ...]```   添加成员。

  参数：

  - nx: member必须不存在，才可以设置成功，用于添加。 
  - xx: member必须存在，才可以设置成功，用于更新。 
  - ch: 返回此次操作后，有序集合元素和分数发生变化的个数。
  - incr: 对score做增加，相当于后面介绍的zincrby。

- ```zcard key```   计算成员个数。

- ```zscore key member   ```   计算某个成员的分数，key不存在返回nil。

- ```zrank key member```   计算成员的排名，```zrevrank key member```反之。

- ```zrem key member [member ...]```   删除成员。

- ```zincrby key increment member```   增加成员的分数。

- ```zrange key start end [withscores]```   返回指定排名范围的成员。如果加上withscores选项，同时会返 回成员的分数。

- ```zcount key min max```   返回指定分数范围成员个数。

- ```zremrangebyrank key start end```   删除指定排名内的升序元素。

- ```zremrangebyscore key min max```   删除指定分数范围的成员。

##### 内部编码

- ziplist(压缩列表):当有序集合的元素个数小于zset-max-ziplist- entries配置(默认128个)，同时每个元素的值都小于zset-max-ziplist-value配 置(默认64字节)时，Redis会用ziplist来作为有序集合的内部实现，ziplist 可以有效减少内存的使用。

- skiplist(跳跃表):当ziplist条件不满足时，有序集合会使用skiplist作 为内部实现，因为此时ziplist的读写效率会下降。



### 键管理

------

##### 单个键管理

- ```rename key newkey```   键重命名。

#####键过期

- ```expire key seconds```   键在seconds秒后过期。
- ```expireat key timestamp```   键在秒级时间戳timestamp后过期。

- ```ttl key```   查询键的剩余过期时间。  

  有3种返回值:

  - 大于等于0的整数: 键剩余的过期时间(ttl是秒，pttl是毫秒)。

  - -1: 键没有设置过期时间。
  - -2: 键不存在。

注意：

（1）如果expire key的键不存在，返回结果为0。

（2）如果过期时间为负值，键会立即被删除，犹如使用del命令一样。

（3）persist命令可以将键的过期时间清除。

（4）对于字符串类型键，执行set命令会去掉过期时间。

（5）Redis不支持二级数据结构(例如哈希、列表)内部元素的过期功 能，例如不能对列表类型的一个元素做过期时间设置。

##### 键迁移

```migrate target_ip target_port [key...] destination-db timeout [copy|replace] ```

