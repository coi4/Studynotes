# Readis

## 一、Nosql入门+概述

技术的分类

1、解决功能性的问题：Java、Jsp、RDBMS、Tomcat、HTML、Linux、JDBC、SVN

2、解决扩展性的问题：Struts、Spring、SpringMVC、Hibernate、Mybatis

3、解决性能的问题：NoSQL、Java线程、Hadoop、Nginx、MQ、ElasticSearch

打破传统关系型数据库以业务逻辑为依据的存储模式，而针对不同数据结构类型改以性能为最优先的存储方式

原子操作：指不会被线程调度机制打断的操作；这种操作一旦开始，就一直运行到结束，中间不会有任何 context switch （切换到另一个线程）

原子性：有一个失败则都失败

概述

> not only SQL（非关系型数据库）
>
> 不依赖业务逻辑方式存储，以简单的key-value模式存储；大大增加了数据库的扩展能力
>
> - 适用场景：对数据高并发读写；海量数据读写；对数据高可扩展性（用不着sql和用了sql也不行的情况）
> - 不适用：需要事务支持；基于SQL的结构化查询存储，处理复杂的关系，需要即席查询

- Memcache：很早出现的nosql数据库；存储在内存中，不持久；支持简单的key-value，类型单一；作为缓存数据库辅助持久化的数据库
- redis：几乎覆盖了Memcached绝大部分功能；都存在内存中，支持持久化，主要用作备份恢复；还支持多种数据结构存储；作为缓存数据库
- MongoDB：高性能、开源、模式自由的文档型数据库；都在内存中，内存不足把不常用数据保存到硬盘；对value（尤其是json）还提供了丰富的查询功能；可以根据数据的特点替代RDBMS，成为独立数据库/配合RDBMS，存储特定数据

行式存储数据库：

- 行式：![image-20231101103725593](https://gitee.com/coi4/test/raw/master/img/image-20231101103725593.png)
- 列式：![image-20231101103735447](https://gitee.com/coi4/test/raw/master/img/image-20231101103735447.png)
  - Hbase：Hadoop项目中的数据库；用于对大量数据进行随机、实时的读写操作的场景中（目标是处理数据量非常庞大的表，可以用普通计算机处理超过10亿行数据，还可处理有数百万列元素的数据表）
  - Cassandra：免费的开源nosql数据库；目的是在于管理由大量商用服务器构建起来的庞大集群上的海量数据集；长处是对写入及读取操作进行规模调整，不强调主集群的设计思路能够以相对直观的方式简化各集群的创建与扩展流程

图关系型数据库：Neo4j；主要应用于社会关系、公共交通网络、地图etc

![image-20231101104605001](https://gitee.com/coi4/test/raw/master/img/image-20231101104605001.png)

## 二、Redis介绍

简介

使用C语言编写，可基于内存亦可持久化的日志key-value数据库（非关系型），支持多种语言的API；

Redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件；实现主从同步

> * 非关系型数据库  mysql，oracle
> * 关系型数据库sqlserver,db2
> * 关系型数据库在存储之前，必须要定义好所谓的数据字典，后续的存储数据按照存储字典来 存储，而Redis就不需要了。

特性

远程的：分为客户端，服务端。可以分别部署在不同的机器上，通过自定义协议进行 传输和交互的。平时说的Redis通常指的是Redis的服务端。 

基于内存的：所有数据结构存在内存中。所有操作非常高速。性能优越于硬盘存储的 mysql，因为存在内存中，所有也是比较吃内存的。 

非关系型数据库 : 本质是数据库，存储数据，区别于Mysql。

应用场景

配合关系型数据库做高速缓存：当系统的接口数据比较慢的时候，可以把系统数据接口的数据缓存起来，当下次取的时候，可以直接从缓存中取就可以了。

数据存储：redis 有两种非常完备的持久化机制【AOF和RDB】，可以定期将数据持久化硬 盘中，保障数据的完整性，安全性。

![image-20231101105237620](https://gitee.com/coi4/test/raw/master/img/image-20231101105237620.png)

为什么使用redis

性能：将运行结果放入缓存。这样，后面的请求就去缓存中读取，使得请求能够迅速响应。![image-20231031194516561](https://gitee.com/coi4/test/raw/master/img/image-20231031194516561.png)

并发：数据库连接异常---使用redis做一个缓冲操作，让请求先访问到redis， 而不是直接访问数据库。![image-20231031194649355](https://gitee.com/coi4/test/raw/master/img/image-20231031194649355.png)

单线程为什么这么快

(一)纯内存操作 

 (二)单线程操作，避免了频繁的上下文切换  

(三)采用了非阻塞I/O多路复用机制

安装

http://redis.cn/   http://redis.io

安装redis-6.2.1.tar.gz

1. 准备：下载安装最新版gcc编译器

   - 安装c语言的编译环境

     - ```
       yum install centos-release-scl scl-utils-build
       yum install -y devtoolset-8-toolchain
       scl enable devtoolset-8 bash
       ```

   - 测试gcc版本

     - ```
       gcc --version
       ```

2. 下载redis放opt目录

3. 解压命令：tar -zxvf redis-6.2.1.tar.gz

4. 解压完成后进入目录：cd redis-6.2.1

5. 在redis-6.2.1目录下再次执行make命令（没有准备好C语言编译环境会报错）

   - 运行make distclean
   - 再次在，，目录下执行make命令

6. 跳过make test继续执行make install

安装目录：/user/local/bin

> redis-benchmark:性能测试工具，可以在自己本子运行，看看自己本子性能如何
>
> redis-check-aof：修复有问题的AOF文件，rdb和aof后面讲
>
> redis-check-dump：修复有问题的dump.rdb文件
>
> redis-sentinel：Redis集群使用
>
> redis-server：Redis服务器启动命令
>
> redis-cli：客户端，操作入口

后台启动：

1. 备份redis.conf：拷贝到其他目录
2. 修改redis.conf(128行)文件将里面的daemonize no 改成 yes，让服务在后台启动
3. 启动：redis-server/myredis/redis.conf![image-20231101110830024](https://gitee.com/coi4/test/raw/master/img/image-20231101110830024.png)
4. 用客户端访问：redis-cli
5. 多个端口可以：redis-cli -p6379
6. 测试验证：ping![image-20231101111046566](https://gitee.com/coi4/test/raw/master/img/image-20231101111046566.png)
7. 关闭：
   - 单实例关闭：redis-cli shutdown
   - 进入终端关闭：![image-20231101111058486](https://gitee.com/coi4/test/raw/master/img/image-20231101111058486.png)
   - 多实例关闭：指定端口关闭：redis-cli -p 6379 shutdown

## 三、redis数据类型

http://www.redis.cn/commands.html

String：

- 字符串

- 是Redis**最基本**的类型，一个key对 应一个value。
  - String str = “hello”;  redis key – value  String s = new String(“”); 
- 是二进制安全的。意味着Redis的string**可以包含任何数据**。比如jpg图片或者序列化的对象。
- 一个Redis中字符串**value最多可以是512M**。
- 应用：当一个 ip 地址访问网站超过了预定的次数，可以禁止访 问，则这个预定次数就可以使用String来存储

List：

- 列表

- 单键多值
- Redis 列表是简单的字符串列表，按照插入顺序排序。你**可以添加一个元素到列表的 头部（左边）或者尾部（右边）**。 
- 它的底层实际是个双向链表，对两端的操作性能很高，通过索引下标的操作中间的 节点性能会较差。
- 应用：实现最新消息信息排列展示【消息队列】

Set：

- 集合

- Redis set 对外提供的功能与list类似是一个列表的功能，特殊之处在于set是可以**自动排重**的，当你需要存储一个列表数据，又不希望出现重复数据时，set是一个很好的选择。
- 应用：可以自动排重；微博应用中，每个人的好友存在一个集合（set）中，这样求两个人的共同好友的操作，可能就只需要用求交集命令即可。

Hash：

- 散列

- Redis  hash 是一个键值对集合。 
- Redis hash 是一个 string 类型的 field 和 value 的映射表，hash 特别适合用于**存储对 象**。
  - ![image-20231101111921265](https://gitee.com/coi4/test/raw/master/img/image-20231101111921265.png)
- 类似Java里面的Map <String,Object>
- 应用：存储用户信息：key(用户ID) + field(属性标签) 操作对应属 性数据了，既不需要重复存储数据，也不会带来序列化和并发修 改控制的问题。很好的解决了问题

Zset:

- 有序集合

- 与set相似，是没有重复元素的字符串集合；不同：所有成员都关联了一个评分（score），被用来按照从最低分到最高分的方式排序集合中的成员；成员唯一，评分可以重复。

- 底层使用了两个数据结构：hash；跳跃表（跳跃表效率堪比红黑树，实现远比红黑树简单；从第2层开始，1节点比51节点小，向后比较。

  21节点比51节点小，继续向后比较，后面就是NULL了，所以从21节点向下到第1层

  在第1层，41节点比51节点小，继续向后，61节点比51节点大，所以从41向下

  在第0层，51节点为要查找的节点，节点被找到，共查找4次。）![image-20231101112221569](https://gitee.com/coi4/test/raw/master/img/image-20231101112221569.png)

- 可以很快根据评分或者次序来获取一个范围的元素；访问中间元素也非常快；可用来作为一个没有重复成员的只能列表。

- 应用：以某个条件为权重，比如按顶的次数排序。  需要精准设定过期时间的应用    使用sorted set的设置过期时间的时间戳，那么就可以简单地 通过过期时间排序，定时清除过期数据。 

Bitmaps：

- 本身不是一种数据类型， 实际上它就是**字符串**（key-value） ， 但是它可以对字符串的位进行操作；单独提供了一套命令， 所以在Redis中使用Bitmaps和使用字符串的方法不太相同。 可以把Bitmaps想象成一个**以位为单位的数组**（1字节8位）， 数组的每个单元只能存储0和1， **数组的下标**在Bitmaps中叫做偏移量。

- 与set相比：网站每天的独立访问用户很多，用bitmaps更省空间；少，set更合适

- 常用命令：

  - setbit：设置Bitmaps中某个偏移量的值（0或1）setbit<key><offset><value>（offset:偏移量从0开始）

    - setbit unique：users：20201106 1 1（访问了设置1，没有设置为0）

    - 很多应用的用户id以一个指定数字（例如10000） 开头， 直接将用户id和Bitmaps的偏移量对应势必会造成一定的浪费， 通常的做法是每次做setbit操作时将用户id减去这个指定数字。

      在第一次初始化Bitmaps时， 假如偏移量非常大， 那么整个初始化过程执行会比较慢， 可能会造成Redis的阻塞。

  - getbit：获取Bitmaps中某个偏移量的值getbit<key><offset>

    - getbit unique：users：20201106 1
    - 不存在的偏量值，返回0

  - bitcount： 统计字符串从start**字节**到end字节比特值为1的数量bitcount<key>[start end]

    - start 和 end 参数的设置，都可以使用负数值：比如 -1 表示最后一个位，而 -2 表示倒数第二个位

      - K1 【01000001 01000000  00000000 00100001】，对应【0，1，2，3】

      - bitcount K1 0 -2  ： 统计下标0到下标倒数第2，字节组中bit=1的个数，即01000001  01000000  00000000

        --》bitcount K1 0 -2　　--》3

    - bitcount unique：users：20201106 1 3

  - bitop：复合操作， 它可以做多个Bitmaps的and（交集） 、 or（并集） 、 not（非） 、 xor（异或） 操作并将结果保存在destkey中。bitop and(or/not/xor) <destkey> [key…]

    - 计算出两天都访问过网站的用户数量

      bitop and unique:users:and:2020110403

      unique:users:20201103unique:users:20201104

    - 计算出任意一天都访问过网站的用户数量（例如月活跃就是类似这种） ， 可以使用or求并集

HyperLogLog：

- 统计网站PV（PageView页面访问量）,可以使用Redis的incr、incrby轻松实现；UV（UniqueVisitor，独立访客）、独立IP数、搜索记录数等需要去重和计数的问题可以将数据存储在MySQL表中，使用distinct count计算不重复个数/使用Redis提供的hash、set、bitmaps等数据结构来处理----结果精确，占用空间大，对非常大的数据集不切实际

- 降低精度平衡存储空间---heperloglog

- 用来做基数统计的算法，优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定的、并且是很小的。

  在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。

  但是，因为 HyperLogLog 只会根据输入元素来计算基数(没有重复元素的集合元素的个数），而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。

- 常用命令：
  - pfadd：添加指定元素到 HyperLogLog 中pfadd <key>< element> [element ...] 
    - 将所有元素添加到指定HyperLogLog数据结构中。如果执行命令后HLL估计的近似基数发生变化，则返回1，否则返回0。
  - pfcount： 计算HLL的近似基数，可以计算多个HLL，比如用HLL存储每天的UV，计算一周的UV可以使用7天的UV合并计算即可  pfcount<key> [key ...]
    - ![image-20231102001103247](https://gitee.com/coi4/test/raw/master/img/image-20231102001103247.png)
  - pfmerge： 将一个或多个HLL合并后的结果存储在另一个HLL中，比如每月活跃用户可以使用每天的活跃用户来合并计算可得 pfmerge<destkey><sourcekey> [sourcekey ...]
    - ![image-20231102001205367](https://gitee.com/coi4/test/raw/master/img/image-20231102001205367.png)

Geospatial：

- GEO，Geographic，地理信息的缩写。该类型，就是元素的2维坐标，在地图上就是经纬度。redis基于该类型，提供了经纬度设置，查询，范围查询，距离查询，经纬度Hash等常见操作

- 常用命令：

  - geoadd：添加地理位置（经度，纬度，名称）geoadd<key>< longitude><latitude><member> [longitude latitude member...]  

    - ![image-20231102001416307](https://gitee.com/coi4/test/raw/master/img/image-20231102001416307.png)

    - 两极无法直接添加，一般会下载城市数据，直接通过 Java 程序一次性导入。

      有效的经度从 -180 度到 180 度。有效的纬度从 -85.05112878 度到 85.05112878 度。

      当坐标位置超出指定范围时，该命令将会返回一个错误。

      已经添加的数据，是无法再次往里面添加的。

  - geopos：获得指定地区的坐标值 geopos  <key><member> [member...] 

  - geodist： 获取两个位置之间的直线距离 geodist<key><member1><member2>  [m|km|ft|mi ] 

    - mi 表示单位为英里。

      ft 表示单位为英尺。

      如果用户没有显式地指定单位参数， 那么 GEODIST 默认使用米作为单位

  - georadius：以给定的经纬度为中心，找出某一半径内的元素 georadius<key>< longitude><latitude>radius m|km|ft|mi  （经度 纬度 距离 单位)

常用命令：

非数据类型常用命令：

- 切换库：select  0
- 启动服务器，用客户端访问
  - ./redis-server redis.conf 
  - ./redis-cli 
- 测试验证连接是否正常：ping
- 查看当前库的所有键：key *
- 判断key是否存在：exists  <key>
- 查看键的类型: type <key>
- 删除某个键:del <key>
- 设置key的过期时间单位为秒：expre <key> <seconds>
- 查看还有多少秒过期，-1表示永不过期，-2表示已过期: ttl <key>
- 查看当前数据库的key的数量: dbsize
- 清空当前库: flushdb
- 通杀全部库: flushall

String类型常用命令

- 添加键值对：  set  <key>
- 查询对应键值：  get   <key>
- 将给定的 追加到原值的末尾：append <key>  <value>
- 获得值的长度：strlen    <key>
- 只有在 key 不存在时设置 key 的值：setnx  <key>  <value>   
- 将 key 中储存的数字值增1,只能对数字值操作，如果为空，新增值为1  ：incr <key>  
- 将 key 中储存的数字值减1,只能对数字值操作，如果为空，新增值为-1 : decr  <key>
-   将 key 中储存的数字值增减。自定义步长。  : incrby / decrby   <key> <步长> 
-  同时设置一个或多个 key-value对 : mset   <key1> <value1> <key2> <value2>       .....   
- 同时获取一个或多个 value : mget    <key1> <key2>    .....   
- 同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。: msetnx <key1> <value1> <key2> <value2>        .....  
-  获得值的范围: getrange  <key>  <起始位置>  <结束位置>   
-  用   覆写 所储存的字符串值，从<起始位置>开始。: setrange  <key>    <起始位置>     <value>
- 设置键值的同时，设置过期时间，单位秒。  : setex <key>   <过期时间>     <value>
- 以新换旧，设置了新值同时获得旧值 : getset   <key> <value>

List类型常用命令：

- 从左边/右边插入一个或多个值：lpush/rpush          <key> <value1> <value2>....  
- 从左边/右边吐出一个值。值在键在，值光键亡 ：lpop/rpop     <key>
- 按照索引下标获得元素(从左到右) 元素不会丢失！ ：lrange     <key> <start> <stop>
- 获得列表长度 ： llen   <key>
- 在的后面插入 插入值 ： linsert <key> before<value>   <pivot> <newvalue>y

Set类型常用命令：

- 将一个或多个 member 元素加入到集合 key 当中，已经存在于集合的 member 元素 将被忽略。：sadd  <key> <value1> <value2>    .....   
- 取出该集合的所有值 : smembers   <key>
- 判断集合是否为含有该值，有返回1，没有返回0 : sismember     <key> 
- 删除集合中的某个元素: srem  <key> <value1> <value2>  .... 
- 随机从该集合中吐出一个值。: spop  <key>   
- 随机从该集合中取出n个值，不会从集合中删除。: srandmember   <key> <n>
- 返回两个集合的交集元素。: sinter   <key1> <key2>
- 返回两个集合的并集元素。: sunion      <key1> <key2>
- 返回两个集合的差集元素，返回的结果跟key的顺序有关系 : sdiff    <key1> <key2>

Hash常用命令：

- 给集合中的  键赋值: hset     <key>  <filed>  <value> 
- 从集合 取出 value:  hget    <key1> 
- 批量设置hash的值  :hmset  <key1>    <filed1> <value1> <field2>    ...     
- 批量取出hash的值 : hmget  <key1> <filed1><filed2><filed3>    ...     
- 查看哈希表 key 中，给定域 field 是否存在。 有返回1，没有返回0 :hexists key    <field>
- 列出该hash集合的所有field : hkeys   <key>
- 列出该hash集合的所有value : hvals     <key>

Zset常用命令：

- 将一个或多个 member 元素及其 score 值加入到有序集 key 当中。  a)  zadd <key><score1><value1>  <score2><value2>       ...  
- 返回有序集 key 中，下标在 之间的元素带WITHSCORES，可以让分数一起 和值返回到结果集。  a)  zrange <key> <start><stop>     [WITHSCORES]    ①  WITHSCORES 如果在命令行上加上该选项，则将score 和 value 一同取出，如 果不加该选项，则只取value值！ 
- 返回有序集 key 中，所有 score 值介于 min 和 max 之间(包括等于 min 或 max )的 成员。有序集成员按 score 值递增(从小到大)次序排列。 
  - a)  zrangebyscore key min max [withscores] [limit offset count]
  - b) zrevrangebyscore key max min [withscores] [limit offset count] 从大到小  
- 为元素的score加上增量  a)  zincrby     <key><increment><member>
- 删除该集合下，指定值的元素   a)  zrem      <key>  <vallue>  
- 统计该集合，分数区间内的元素个数  a)  zcount <key> <min> <max>
- 返回该值在集合中的排名，从0开始。  a)   zrank<key>  <value>

## 四、redis解析配置文件

自定义目录：/myredis/redis.conf

Units单位：![image-20231101114138983](https://gitee.com/coi4/test/raw/master/img/image-20231101114138983.png)

includes包含：类似jsp中的include，多实例的情况可以把公用的配置文件提取出来![image-20231101114242269](https://gitee.com/coi4/test/raw/master/img/image-20231101114242269.png)

网络相关配置：

- bind：默认情况bind=127.0.0.1只能接受本机的访问请求

  不写的情况下，无限制接受任何ip地址的访问

  生产环境肯定要写你应用服务器的地址；服务器是需要远程访问的，所以需要将其注释掉

  如果开启了protected-mode，那么在没有设定bind ip且没有设密码的情况下，Redis只允许接受本机的响应

  ![image-20231101114534393](https://gitee.com/coi4/test/raw/master/img/image-20231101114534393.png)

  保存配置，停止服务，重启启动查看进程，不再是本机访问了。

  ![image-20231101114600022](https://gitee.com/coi4/test/raw/master/img/image-20231101114600022.png)

- protected-mode：将本机访问保护模式设置no

  ![image-20231101114633325](https://gitee.com/coi4/test/raw/master/img/image-20231101114633325.png)

- Port：端口号，默认 6379

  ![image-20231101114731640](https://gitee.com/coi4/test/raw/master/img/image-20231101114731640.png)

- tep-backlog：设置tcp的backlog，backlog其实是一个连接队列，backlog队列总和=未完成三次握手队列 + 已经完成三次握手队列。

  在高并发环境下你需要一个高backlog值来避免慢客户端连接问题。

  注意Linux内核会将这个值减小到/proc/sys/net/core/somaxconn的值（128），所以需要确认增大/proc/sys/net/core/somaxconn和/proc/sys/net/ipv4/tcp_max_syn_backlog（128）两个值来达到想要的效果

  ![image-20231101114757735](https://gitee.com/coi4/test/raw/master/img/image-20231101114757735.png)

- timeout：一个空闲的客户端维持多少秒会关闭，0表示关闭该功能。即永不关闭。

  ![image-20231101114823425](https://gitee.com/coi4/test/raw/master/img/image-20231101114823425.png)

- tcp-keepalive：对访问客户端的一种心跳检测，每个n秒检测一次。

  单位为秒，如果设置为0，则不会进行Keepalive检测，建议设置成60 

  ![image-20231101114848113](https://gitee.com/coi4/test/raw/master/img/image-20231101114848113.png)

general通用：

- daemonize：是否为后台进程，设置为yes

  守护进程，后台启动![image-20231101115059939](https://gitee.com/coi4/test/raw/master/img/image-20231101115059939.png)

- pidfile：存放pid文件的位置，每个实例会产生一个不同的pid文件![image-20231101115117049](https://gitee.com/coi4/test/raw/master/img/image-20231101115117049.png)

- loglevel：指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为notice

  四个级别根据使用阶段来选择，生产环境选择notice 或者warning

  ![image-20231101115202747](https://gitee.com/coi4/test/raw/master/img/image-20231101115202747.png)

- logfile：日志文件名称![image-20231101115224045](https://gitee.com/coi4/test/raw/master/img/image-20231101115224045.png)

- databases 16：设定库的数量 默认16，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id![image-20231101115241944](https://gitee.com/coi4/test/raw/master/img/image-20231101115241944.png)

安全：

- 设置密码：![image-20231101115308883](https://gitee.com/coi4/test/raw/master/img/image-20231101115308883.png)

  访问密码的查看、设置和取消

  在命令中设置密码，只是临时的。重启redis服务器，密码就还原了。

  永久设置，需要再配置文件中进行设置。

  ![image-20231101115330683](https://gitee.com/coi4/test/raw/master/img/image-20231101115330683.png)

限制：

- maxclients：
  - 设置redis同时可以与多少个客户端进行连接。
  - 默认情况下为10000个客户端。
  - 如果达到了此限制，redis则会拒绝新的连接请求，并且向这些连接请求方发出“max number of clients reached”以作回应。
  - ![image-20231101115524200](https://gitee.com/coi4/test/raw/master/img/image-20231101115524200.png)
- maxmemory
  - 建议***\*必须设置\****，否则，将内存占满，造成服务器宕机
  - 设置redis可以使用的内存量。一旦到达内存使用上限，redis将会试图移除内部数据，移除规则可以通过maxmemory-policy来指定。
  - 如果redis无法根据移除规则来移除内存中的数据，或者设置了“不允许移除”，那么redis则会针对那些需要申请内存的指令返回错误信息，比如SET、LPUSH等。
  - 但是对于无内存申请的指令，仍然会正常响应，比如GET等。如果你的redis是主redis（说明你的redis有从redis），那么在设置内存使用上限时，需要在系统中留出一些内存空间给同步队列缓存，只有在你设置的是“不移除”的情况下，才不用考虑这个因素。
  - ![image-20231101115608703](https://gitee.com/coi4/test/raw/master/img/image-20231101115608703.png)
- maxmemory-policy
  - volatile-lru：使用LRU算法移除key，只对设置了过期时间的键；（最近最少使用）
  - allkeys-lru：在所有集合key中，使用LRU算法移除key
  - volatile-random：在过期集合中移除随机的key，只对设置了过期时间的键
  - allkeys-random：在所有集合key中，移除随机的key
  -  volatile-ttl：移除那些TTL值最小的key，即那些最近要过期的key
  - noeviction：不进行移除。针对写操作，只是返回错误信息
  - ![image-20231101115700935](https://gitee.com/coi4/test/raw/master/img/image-20231101115700935.png)
- maxmemory-samples
  - 设置样本数量，LRU算法和最小TTL算法都并非是精确的算法，而是估算值，所以你可以设置样本的大小，redis默认会检查这么多个key并选择其中LRU的那个。
  - 一般设置3到7的数字，数值越小样本越不准确，但性能消耗越小。
  - ![image-20231101115730180](https://gitee.com/coi4/test/raw/master/img/image-20231101115730180.png)

## 五、redis持久化

![image-20231101091859977](https://gitee.com/coi4/test/raw/master/img/image-20231101091859977.png)

RDB

![image-20231102181942946](https://gitee.com/coi4/test/raw/master/img/image-20231102181942946.png)

在**指定的时间间隔内**将内存中的数据集快照**写入磁盘**，也就是行话讲的Snapshot 快照，它恢复时是将快照文件直接读到内存里。 

工作机制：每隔一段时间，就把内存中的数据保存到硬盘上的指定文件中。

默认开启

Redis 会单独创建（fork）一个**子进程**来进行持久化，会**先将数据写入到一个临时文件**中 【xxx.rdb】（默认为dump.rdb，rdb文件的保存路径，也可以修改（445行）。默认为Redis启动时命令行所在的目录下dir "/myredis/"），待**持久化过程都结束**了，再用这个**临时文件替换上次持久化好的文件**。整个过 程中，主进程是不进行任何IO操作的，这就确保了极高的性能如果需要进行**大规模数据的恢复**，且对于数据恢复的**完整性不是非常敏感**，那RDB方式要比AOF方式更加的高效。  RDB 的缺点是**最后一次持久化后的数据可能丢失**。

保存策略：

- **save** 900 1（900 秒内如果至少有 1 个 key 的值变化，则保存在，以此类推）（默认是1分钟内改了1万次，或5分钟内改了10次，或15分钟内改了1次）；
- **bgsave**：Redis会在后台异步进行快照操作， 快照同时还可以响应客户端请求；可通过**lastsave**命令获取最后一次成功执行快照的时间
- 常用属性配置：![image-20231101092636783](https://gitee.com/coi4/test/raw/master/img/image-20231101092636783.png)
- rdb的备份：先通过config get dir  查询rdb文件的目录 将*.rdb的文件拷贝到别的地方
- rdb的恢复：
  - 关闭Redis
  -  先把备份的文件拷贝到工作目录下 cp dump2.rdb dump.rdb
  -  启动Redis, 备份数据会直接加载
- 动态停止RDB：redis-cli config set save ""#save后给空值，表示禁用保存策略

两次保存的时间间隔内，服务器宕机，或者断电，数据丢失

![image-20231101092946230](https://gitee.com/coi4/test/raw/master/img/image-20231101092946230.png)

优点：

- 适合大规模的数据恢复
- 对数据完整性和一致性要求不高
- 节省磁盘空间
- 恢复速度快

缺点：

- fork时，数据被克隆，大致2倍的膨胀性需要考虑
- 虽然fork时使用了写时拷贝技术，但如果数据庞大还是比较消耗性能
- 在备份周期在一定间隔时间做一次备份，所以如果Redis意外down掉的话，就会丢失最后一次快照后的所有修改。

AOF

![image-20231102182159704](https://gitee.com/coi4/test/raw/master/img/image-20231102182159704.png)![image-20231102182318740](https://gitee.com/coi4/test/raw/master/img/image-20231102182318740.png)

是以**日志的形式**来记录每个写操作，将每一次对数据进行修改，都把新建、修 改数据的命令保存到指定文件中， 只许追加文件但不可以改写文件。Redis**重新启动时读取这个文件，重新执行新建、 修改数据的命令恢复数据**。（实时备份，更耐久，文件大小应该比rdb大）

需要手动开启：可以在redis.conf中配置文件名称，默认为 appendonly.aof AOF文件的保存路径，同RDB的路径一致。

保存命令时，只会保存对数据有修改的命令（写操作）

当RDB和AOF存的不一致的情况下，按照AOF来恢复。因为AOF是对RDB的补 充。备份周期更短，也就更可靠。 

保存策略：appendfsync always/everyday/no（每次产生新的修改命令都执行保存操作（效率低，安全）/每秒执行一次保存操作，为保存当前秒内操作时断电，部分数据丢失（1秒的数据）/从不保存，将数据交给操作系统处理（更快，更不安全）推荐（默认）的操作是每秒fsync一次，这种fsync兼顾速度与安全）

常用属性：![image-20231101093843728](https://gitee.com/coi4/test/raw/master/img/image-20231101093843728.png)

![image-20231101093855957](https://gitee.com/coi4/test/raw/master/img/image-20231101093855957.png)

文件修复：![image-20231101094024171](https://gitee.com/coi4/test/raw/master/img/image-20231101094024171.png)

优点：

- 备份机制更稳健，丢失数据概率更低。
- 可读的日志文本，通过操作AOF稳健，可以处理误操作。

缺点：

- 比起RDB占用更多的磁盘空间。
- 恢复备份速度要慢。
- 每次读写都同步的话，有一定的性能压力
- 存在个别Bug，造成恢复不能。

## 六、redis事务

Redis事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，**不会被其他客户端发送来的命令请求所打断**。

Redis事务的主要作用就是**串联多个命令防止别的命令插队**。

从输入Multi命令开始，输入的命令都会依次进入命令队列中，但不会执行，直到输入Exec后，Redis会将之前的命令队列中的命令依次执行。

组队的过程中可以通过discard来放弃组队。

![image-20231102003422638](https://gitee.com/coi4/test/raw/master/img/image-20231102003422638.png)

组队成功，提交成功：

![image-20231102003431574](https://gitee.com/coi4/test/raw/master/img/image-20231102003431574.png)

组队阶段报错，提交失败：

![image-20231102003532957](https://gitee.com/coi4/test/raw/master/img/image-20231102003532957.png)

组队成功，提交有成功有失败情况：

![image-20231102003601499](https://gitee.com/coi4/test/raw/master/img/image-20231102003601499.png)

事物的错误处理：

- 组队中某个命令出现了报告错误，执行时整个的所有队列都会被取消。

- 如果执行阶段某个命令报出了错误，则只有报错的命令不会被执行，而其他的命令都会执行，不会回滚。

事务冲突问题：

- **悲观锁(Pessimistic Lock)**, 顾名思义，就是很悲观，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会block直到它拿到锁。**传统的关系型数据库里边就用到了很多这种锁机制**，比如**行锁**，**表锁**等，**读锁**，**写锁**等，都是在做操作之前先上锁。
- **乐观锁(Optimistic Lock),** 顾名思义，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制。**乐观锁适用于多读的应用类型，这样可以提高吞吐量**。Redis就是利用这种check-and-set机制实现事务的。
- 在执行multi之前，先执行watch key1 [key2],可以监视一个(或多个) key ，如果在事务***\*执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断。\****
- unwatch：取消 WATCH 命令对所有 key 的监视。如果在执行 WATCH 命令之后，EXEC 命令或DISCARD 命令先被执行了的话，那么就不需要再执行UNWATCH 了。

事务三特性：

- 单独的隔离操作 
  -  事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。 

- 没有隔离级别的概念 
  -  队列中的命令没有提交之前都不会实际被执行，因为事务提交前任何指令都不会被实际执行

- 不保证原子性 
  -  事务中如果有一条命令执行失败，其后的命令仍然会被执行，没有回滚 

秒杀案例：

- 解决计数器和人员记录的事务操作：![image-20231102004919971](https://gitee.com/coi4/test/raw/master/img/image-20231102004919971.png)

- Redis事务--秒杀并发模拟：使用工具ab模拟测试（会出现超卖情况。查看库存会出现负数。）、CentOS6 默认安装、CentOS7需要手动安装

  - **联网：**yum install httpd-tools

  - **无网络**：进入cd  /run/media/root/CentOS 7 x86_64/Packages（路径跟centos6不同），顺序安装

    ```
    apr-1.4.8-3.el7.x86_64.rpm
    apr-util-1.5.2-6.el7.x86_64.rpm
    httpd-tools-2.4.6-67.el7.centos.x86_64.rpm 
    ```

  - **测试及结果**：

    - 通过ab测试：vim postfile 模拟表单提交参数,以&符号结尾;存放当前目录。内容：prodid=0101&。ab -n 2000 -c 200 -k -p ~/postfile -T application/x-www-form-urlencoded http://192.168.2.115:8081/Seckill/doseckill
    - 超卖：![image-20231102005516645](https://gitee.com/coi4/test/raw/master/img/image-20231102005516645.png)

- 超卖问题：![image-20231102005534191](https://gitee.com/coi4/test/raw/master/img/image-20231102005534191.png)

- 利用乐观锁淘汰用户，解决超卖问题（出现遗留库存和链接超时）：

  ```
  //增加乐观锁
  jedis.watch(qtkey);
   
  //3.判断库存
  String qtkeystr = jedis.get(qtkey);
  if(qtkeystr==null || "".equals(qtkeystr.trim())) {
  System.out.println("未初始化库存");
  jedis.close();
  return false ;
  }
   
  int qt = Integer.parseInt(qtkeystr);
  if(qt<=0) {
  System.err.println("已经秒光");
  jedis.close();
  return false;
  }
  
  //增加事务
  Transaction multi = jedis.multi();
   
  //4.减少库存
  //jedis.decr(qtkey);
  multi.decr(qtkey);
   
  //5.加人
  //jedis.sadd(usrkey, uid);
  multi.sadd(usrkey, uid);
   
  //执行事务
  List<Object> list = multi.exec();
   
  //判断事务提交是否失败
  if(list==null || list.size()==0) {
  System.out.println("秒杀失败");
  jedis.close();
  return false;
  }
  System.err.println("秒杀成功");
  jedis.close();
  ```

  ![image-20231102005551834](https://gitee.com/coi4/test/raw/master/img/image-20231102005551834.png)

  ![image-20231102005642443](https://gitee.com/coi4/test/raw/master/img/image-20231102005642443.png)

- 继续增加并发测试：

  - 连接有限制：ab -n 2000 -c 200 -k -p postfile -T 'application/x-www-form-urlencoded' http://192.168.140.1:8080/seckill/doseckill

    - 增加-r参数，-r  Don't exit on socket receive errors.

      ab -n 2000 -c 100 -r -p postfile -T 'application/x-www-form-urlencoded'http://192.168.140.1:8080/seckill/doseckill(http://192.168.140.1:8080/seckill/doseckill）

  - 已经秒光，可是还有库存：ab -n 2000 -c 100 -p postfile -T 'application/x-www-form-urlencoded' http://192.168.137.1:8080/seckill/doseckill

    - 原因，就是乐观锁导致很多请求都失败。先点的没秒到，后点的可能秒到了。

  - 连接超时，通过连接池解决：![image-20231102175041739](https://gitee.com/coi4/test/raw/master/img/image-20231102175041739.png)

  - 连接池：节省每次连接redis服务带来的消耗，把连接好的实例反复利用；通过参数管理连接的行为

    - 链接池参数
      - MaxTotal：控制一个pool可分配多少个jedis实例，通过pool.getResource()来获取；如果赋值为-1，则表示不限制；如果pool已经分配了MaxTotal个jedis实例，则此时pool的状态为exhausted。
      - maxIdle：控制一个pool最多有多少个状态为idle(空闲)的jedis实例；
      -  MaxWaitMillis：表示当borrow一个jedis实例时，最大的等待毫秒数，如果超过等待时间，则直接抛JedisConnectionException；
      - testOnBorrow：获得一个jedis实例的时候是否检查连接可用性（ping()）；如果为true，则得到的jedis实例均是可用的；

- 解决库存遗留问题

  - LUA脚本：嵌入式脚本语言，实现可配置性、可扩展性；https://www.w3cschool.cn/lua/

    - ```
      local userid=KEYS[1]; 
      local prodid=KEYS[2];
      local qtkey="sk:"..prodid..":qt";
      local usersKey="sk:"..prodid.":usr'; 
      local userExists=redis.call("sismember",usersKey,userid);
      if tonumber(userExists)==1 then 
        return 2;
      end
      local num= redis.call("get" ,qtkey);
      if tonumber(num)<=0 then 
        return 0; 
      else 
        redis.call("decr",qtkey);
        redis.call("sadd",usersKey,userid);
      end
      return 1;
      ```

      

    - 将复杂的或者多步的redis操作，写为一个脚本，一次提交给redis执行，减少反复连接redis的次数。提升性能。（类似事务，不会被插队，可用来淘汰用户，解决超卖问题，或解决争抢问题，实际上是**redis 利用其单线程的特性，用任务队列的方式解决多任务并发问题**。）

    - ![image-20231102175620630](https://gitee.com/coi4/test/raw/master/img/image-20231102175620630.png)

- 代码：![image-20231102175642653](https://gitee.com/coi4/test/raw/master/img/image-20231102175642653.png)

  - 

## 七、redis发布订阅

发布订阅 (pub/sub) 是一种消息通信模式：发送者 (pub) 发送消息，订阅者 (sub) 接收消息。

Redis 客户端可以订阅任意数量的频道。

实现：

1.  打开一个客户端订阅channel1

   SUBSCRIBE channel1

   - ![image-20231101115922846](https://gitee.com/coi4/test/raw/master/img/image-20231101115922846.png)

2. 打开另一个客户端，给channel1发布消息hello

   - publish channel1 hello

   - ![image-20231101120006456](https://gitee.com/coi4/test/raw/master/img/image-20231101120006456.png)

     返回的1是订阅者数量

3. 打开第一个客户端可以看到发送的消息

   - ![image-20231101120040980](https://gitee.com/coi4/test/raw/master/img/image-20231101120040980.png)

   注：发布的消息没有持久化，如果在订阅的客户端收不到hello，只能收到订阅后发布的消息

## 八、redis复制

主机数据更新后根据配置和策略， 自动同步到备机的master/slaver机制，Master以写为主，Slave以读为主

![image-20231103080423641](https://gitee.com/coi4/test/raw/master/img/image-20231103080423641.png)

读写分离，性能扩展；容灾快速恢复

操作：

拷贝多个redis.conf文件include(写绝对路径)

开启daemonize yes

Pid文件名字pidfile

指定端口port

Log文件名字

dump.rdb名字dbfilename

Appendonly 关掉或者换名字

- 新建redis6379.conf，填写以下内容：

  ```
  include /myredis/redis.conf
  pidfile /var/run/redis_6379.pid
  port 6379
  dbfilename dump6379.rdb
  ```

- 新建redis6380.conf，填写以下内容：![image-20231103080724249](https://gitee.com/coi4/test/raw/master/img/image-20231103080724249.png)

- 新建redis6381.conf，填写以下内容：![image-20231103080750320](https://gitee.com/coi4/test/raw/master/img/image-20231103080750320.png)

  slave-priority 10

  设置从机的优先级，值越小，优先级越高，用于选举主机时使用。默认100

- 启动三台redis服务器：![image-20231103080837710](https://gitee.com/coi4/test/raw/master/img/image-20231103080837710.png)

- 查看系统进程，看看三台服务器是否启动：![image-20231103080911336](https://gitee.com/coi4/test/raw/master/img/image-20231103080911336.png)

- 查看三台主机运行情况：info replication

  打印主从复制的相关信息![image-20231103081015148](https://gitee.com/coi4/test/raw/master/img/image-20231103081015148.png)

- 配从(库)不配主(库)：slaveof  <ip><port>

  成为某个实例的从服务器

  - 在6380和6381上执行: slaveof 127.0.0.1 6379
  - 在主机上写，在从机上可以读取数据：在从机上写数据报错![image-20231103081509212](https://gitee.com/coi4/test/raw/master/img/image-20231103081509212.png)
  - 主机挂掉，重启就行，一切如初
  - 从机重启需重设：slaveof 127.0.0.1 6379：可以将配置增加到文件中。永久生效。![image-20231103081519239](https://gitee.com/coi4/test/raw/master/img/image-20231103081519239.png)

常用：

- 一主二仆：![image-20231103081630983](https://gitee.com/coi4/test/raw/master/img/image-20231103081630983.png)

- 薪火相传：上一个Slave可以是下一个slave的Master，Slave同样可以接收其他 slaves的连接和同步请求，那么该slave作为了链条中下一个的master, 可以有效减轻master的写压力,去中心化降低风险。

  - 用 slaveof  <ip><port>

    中途变更转向:会清除之前的数据，重新建立拷贝最新的

    风险是一旦某个slave宕机，后面的slave都没法备份

    主机挂了，从机还是从机，无法写数据了

- 反客为主：当一个master宕机后，后面的slave可以立刻升为master，其后面的slave不用做任何修改。

  用 slaveof  no one  将从机变为主机。

原理：![image-20231103081847198](https://gitee.com/coi4/test/raw/master/img/image-20231103081847198.png)

哨兵模式(sentinel)：***\*反客为主的自动版\****，能够后台监控主机是否故障，如果故障了根据投票数自动将从库转换为主库

步骤：

- ***\*调整为一主二仆模式，\*******\*6379\*******\*带着\*******\*6380\*******\*、\*******\*6381\****

- ***\*自定义的\*******\*/myredis\*******\*目录下新建\*******\*sentinel.conf\*******\*文件，名字绝不能错\****

- ***\*配置哨兵\*******\*,\*******\*填写内容\****

  - sentinel monitor mymaster 127.0.0.1 6379 1

    其中mymaster为监控对象起的服务器名称， 1 为至少有多少个哨兵同意迁移的数量。 

- ***\*启动哨兵\****

  - /usr/local/bin

    （redis做压测可以用自带的redis-benchmark工具）

    执行redis-sentinel  /myredis/sentinel.conf 

- ***\*当主机挂掉，从机选举中产生新的主机\****

  - (大概10秒左右可以看到哨兵窗口日志，切换了新的主机)

    哪个从机会被选举为主机呢？根据优先级别：slave-priority 

    原主机重启后会变为从机。

- ***\*复制延时\****

  - 由于所有的写操作都是先在Master上操作，然后同步更新到Slave上，所以从Master同步到Slave机器有一定的延迟，当系统很繁忙的时候，延迟问题会更加严重，Slave机器数量的增加也会使这个问题更加严重。

***\*故障恢复\****：![image-20231103082451502](https://gitee.com/coi4/test/raw/master/img/image-20231103082451502.png)优先级在redis.conf中默认：slave-priority 100，值越小优先级越高

偏移量是指获得原主机数据最全的

每个redis实例启动后都会随机生成一个40位的runid

主从复制：

```
private static JedisSentinelPool jedisSentinelPool=null;

public static  Jedis getJedisFromSentinel(){
if(jedisSentinelPool==null){
            Set<String> sentinelSet=new HashSet<>();
            sentinelSet.add("192.168.11.103:26379");

            JedisPoolConfig jedisPoolConfig =new JedisPoolConfig();
            jedisPoolConfig.setMaxTotal(10); //最大可用连接数
jedisPoolConfig.setMaxIdle(5); //最大闲置连接数
jedisPoolConfig.setMinIdle(5); //最小闲置连接数
jedisPoolConfig.setBlockWhenExhausted(true); //连接耗尽是否等待
jedisPoolConfig.setMaxWaitMillis(2000); //等待时间
jedisPoolConfig.setTestOnBorrow(true); //取连接的时候进行一下测试 ping pong

jedisSentinelPool=new JedisSentinelPool("mymaster",sentinelSet,jedisPoolConfig);
return jedisSentinelPool.getResource();
        }else{
return jedisSentinelPool.getResource();
        }
}
```



## 九、redis集群

主从模式，薪火相传模式，主机宕机，导致ip地址发生变化，应用程序中配置需要修改对应的主机地址、端口等信息。

之前通过代理主机来解决，但是redis3.0中提供了解决方案。就是无中心化集群配置（实现扩容，并发写操作进行分摊（分摊压力））。

不足：多键操作是不被支持的 ；多键的Redis事务是不被支持的。lua脚本不被支持；由于集群方案出现较晚，很多公司已经采用了其他的集群方案，而代理或者客户端分片的方案想要迁移至redis cluster，需要整体迁移而不是逐步过渡，复杂度较大。

 Redis 集群实现了对Redis的水平扩容，即启动N个redis节点，将整个数据库分布存储在这N个节点中，每个节点存储总数据的1/N。

Redis 集群通过分区（partition）来提供一定程度的可用性（availability）： 即使集群中有一部分节点失效或者无法进行通讯， 集群也可以继续处理命令请求。

操作：

- 将rdb,aof文件都删除掉。

- ***\*制作\*******\*6\*******\*个实例，\*******\*6379,6380,6381,6389,6390,6391\****

  - ***\*配置基本信息\****

    - 开启daemonize yes

      Pid文件名字

      指定端口

      Log文件名字

      Dump.rdb名字

      Appendonly 关掉或者换名字

  - ***\*redis cluster配置修改\****

    - cluster-enabled yes  打开集群模式

      cluster-config-file nodes-6379.conf 设定节点配置文件名

      cluster-node-timeout 15000  设定节点失联时间，超过该时间（毫秒），集群自动进行主从切换。

      ```
      include /home/bigdata/redis.conf
      port 6379
      pidfile "/var/run/redis_6379.pid"
      dbfilename "dump6379.rdb"
      dir "/home/bigdata/redis_cluster"
      logfile "/home/bigdata/redis_cluster/redis_err_6379.log"
      cluster-enabled yes
      cluster-config-file nodes-6379.conf
      cluster-node-timeout 15000
      ```

  - ***\*修改好redis6379\*******\*.conf\*******\*文件\*******\*，拷贝多个redis.conf文件\****![image-20231103082954524](https://gitee.com/coi4/test/raw/master/img/image-20231103082954524.png)

  - ***\*使用查找替换修改另外\*******\*5\*******\*个文件\****（%s/6379/6380 )

  - ***\*启动\*******\*6个\*******\*redis\*******\*服务\****:![image-20231103083034938](https://gitee.com/coi4/test/raw/master/img/image-20231103083034938.png)

- ***\*将六个节点合成一个集群\****

  - 组合之前，请确保所有redis实例启动后，nodes-xxxx.conf文件都生成正常。![image-20231103083130824](https://gitee.com/coi4/test/raw/master/img/image-20231103083130824.png)

  - 合体：

    cd  /opt/redis-6.2.1/src（用真实ip地址）

    ```
    redis-cli --cluster create --cluster-replicas 1 192.168.11.101:6379 192.168.11.101:6380 192.168.11.101:6381 192.168.11.101:6389 192.168.11.101:6390 192.168.11.101:6391
    ```

  - 普通方式登录：可能直接进入读主机，存储数据时，会出现MOVED重定向操作。所以，应该以集群方式登录。![image-20231103083338685](https://gitee.com/coi4/test/raw/master/img/image-20231103083338685.png)

- ***\*-c 采用集群策略连接，设置数据会自动切换到相应的写主机\****![image-20231103083409438](https://gitee.com/coi4/test/raw/master/img/image-20231103083409438.png)

- ***\*通过 cluster nodes 命令查看集群信息\****![image-20231103083425267](https://gitee.com/coi4/test/raw/master/img/image-20231103083425267.png)

- 如何分配：一个集群至少要有三个主节点。

  选项 --cluster-replicas 1 表示我们希望为集群中的每个主节点创建一个从节点。

  分配原则尽量保证每个主数据库运行在不同的IP地址，每个从库和主库不在一个IP地址上。

- slost：

  ```
  [OK] All nodes agree about slots configuration.
  >>> Check for open slots...
  >>> Check slots coverage...
  [OK] All 16384 slots covered.
  ```

  一个 Redis 集群包含 16384 个插槽（hash slot）， 数据库中的每个键都属于这 16384 个插槽的其中一个， 

  集群使用公式 CRC16(key) % 16384 来计算键 key 属于哪个槽， 其中 CRC16(key) 语句用于计算键 key 的 CRC16 校验和 。

  集群中的每个节点负责处理一部分插槽。 举个例子， 如果一个集群可以有主节点， 其中：

  节点 A 负责处理 0 号至 5460 号插槽。

  节点 B 负责处理 5461 号至 10922 号插槽。

  节点 C 负责处理 10923 号至 16383 号插槽。

- ***\*在集群中录入值\****

  - 在redis-cli每次录入、查询键值，redis都会计算出该key应该送往的插槽，如果不是该客户端对应服务器的插槽，redis会报错，并告知应前往的redis实例地址和端口。

    redis-cli客户端提供了 –c 参数实现自动重定向。

    如 redis-cli  -c –p 6379 登入后，再录入、查询键值对可以自动重定向。

    不在一个slot下的键值，是不能使用mget,mset等多键操作。

    可以通过{}来定义组的概念，从而使key中{}内相同内容的键值对放到一个slot中去。![image-20231103083901912](https://gitee.com/coi4/test/raw/master/img/image-20231103083901912.png)

- ***\*查询集群中的值\****：CLUSTER GETKEYSINSLOT <slot><count> 返回 count 个 slot 槽中的键。![image-20231103083941897](https://gitee.com/coi4/test/raw/master/img/image-20231103083941897.png)

- ***\*故障恢复\****：如果某一段插槽的主从都挂掉，而cluster-require-full-coverage 为yes ，那么 ，整个集群都挂掉

  如果某一段插槽的主从都挂掉，而cluster-require-full-coverage 为no ，那么，该插槽数据全都不能使用，也无法存储。

  redis.conf中的参数  cluster-require-full-coverage

- ***\*集群的\*******\*Jedis\*******\*开发\****：即使连接的不是主机，集群会自动切换主机存储。主机写，从机读。

  无中心化主从集群。无论从哪台主机写的数据，其他主机上都能读到数据。

  ```
  public class JedisClusterTest {
    public static void main(String[] args) { 
       Set<HostAndPort>set =new HashSet<HostAndPort>();
       set.add(new HostAndPort("192.168.31.211",6379));
       JedisCluster jedisCluster=new JedisCluster(set);
       jedisCluster.set("k1", "v1");
       System.out.println(jedisCluster.get("k1"));
    }
  }
  ```

  

## 九、Jedis

需要的jar包：

```
<dependency>
<groupId>redis.clients</groupId>
<artifactId>jedis</artifactId>
<version>3.2.0</version>
</dependency>
```

连接redis注意事项：

禁用Linux的防火墙：Linux(CentOS7)里执行命令

systemctl stop/disable firewalld.service 

redis.conf中注释掉bind 127.0.0.1 ,然后 protected-mode no

常用操作：

创建动态的工程

创建测试程序：

```
package com.atguigu.jedis;
import redis.clients.jedis.Jedis;
public class Demo01 {
public static void main(String[] args) {
Jedis jedis = new Jedis("192.168.137.3",6379);
String pong = jedis.ping();
System.out.println("连接成功："+pong);jedis.close();
 }
}
```

测试相关数据类型：

- api---Key：

  ```
  jedis.set("k1", "v1");
  jedis.set("k2", "v2");
  jedis.set("k3", "v3");
  Set<String> keys = jedis.keys("*");
  System.out.println(keys.size());
  for (String key : keys) {
  System.out.println(key);
  }
  System.out.println(jedis.exists("k1"));
  System.out.println(jedis.ttl("k1"));                
  System.out.println(jedis.get("k1"));
  ```

- String：

  ```
  jedis.mset("str1","v1","str2","v2","str3","v3");
  System.out.println(jedis.mget("str1","str2","str3"));
  ```

- List：

  ```
  List<String> list = jedis.lrange("mylist",0,-1);
  for (String element : list) {
  System.out.println(element);
  }
  ```

- set：

  ```
  jedis.sadd("orders", "order01");
  jedis.sadd("orders", "order02");
  jedis.sadd("orders", "order03");
  jedis.sadd("orders", "order04");
  Set<String> smembers = jedis.smembers("orders");
  for (String order : smembers) {
  System.out.println(order);
  }
  jedis.srem("orders", "order02");
  ```

- hash：

  ```
  jedis.hset("hash1","userName","lisi");
  System.out.println(jedis.hget("hash1","userName"));
  Map<String,String> map = new HashMap<String,String>();
  map.put("telphone","13810169999");
  map.put("address","atguigu");
  map.put("email","abc@163.com");
  jedis.hmset("hash2",map);
  List<String> result = jedis.hmget("hash2", "telphone","email");
  for (String element : result) {
  System.out.println(element);
  }
  ```

- zset：

  ```
  jedis.zadd("zset01", 100d, "z3");
  jedis.zadd("zset01", 90d, "l4");
  jedis.zadd("zset01", 80d, "w5");
  jedis.zadd("zset01", 70d, "z6");
   
  Set<String> zrange = jedis.zrange("zset01", 0, -1);
  for (String e : zrange) {
  System.out.println(e);
  }
  ```

实例：

完成一个手机验证码功能

> 要求：
>
> 1、输入手机号，点击发送后随机生成6位数字码，2分钟有效
>
> 2、输入验证码，点击验证，返回成功或失败
>
> 3、每个手机号每天只能输入3次

## 十、与spring boot整合

步骤：

1.  在pom.xml文件中引入redis相关依赖

   - ```
     <!-- redis -->
     <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-data-redis</artifactId>
     </dependency>
     
     <!-- spring2.X集成redis所需common-pool2-->
     <dependency>
     <groupId>org.apache.commons</groupId>
     <artifactId>commons-pool2</artifactId>
     <version>2.6.0</version>
     </dependency>
     ```

     

2.  application.properties配置redis配置

   - ```
     #Redis服务器地址
     spring.redis.host=192.168.140.136
     #Redis服务器连接端口
     spring.redis.port=6379
     #Redis数据库索引（默认为0）
     spring.redis.database= 0
     #连接超时时间（毫秒）
     spring.redis.timeout=1800000
     #连接池最大连接数（使用负值表示没有限制）
     spring.redis.lettuce.pool.max-active=20
     #最大阻塞等待时间(负数表示没限制)
     spring.redis.lettuce.pool.max-wait=-1
     #连接池中的最大空闲连接
     spring.redis.lettuce.pool.max-idle=5
     #连接池中的最小空闲连接
     spring.redis.lettuce.pool.min-idle=0
     ```

3. 添加redis配置类

   - ```
     @EnableCaching
     @Configuration
     public class RedisConfig extends CachingConfigurerSupport {
     
         @Bean
         public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
             RedisTemplate<String, Object> template = new RedisTemplate<>();
             RedisSerializer<String> redisSerializer = new StringRedisSerializer();
             Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
             ObjectMapper om = new ObjectMapper();
             om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
             om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
             jackson2JsonRedisSerializer.setObjectMapper(om);
             template.setConnectionFactory(factory);
     //key序列化方式
             template.setKeySerializer(redisSerializer);
     //value序列化
             template.setValueSerializer(jackson2JsonRedisSerializer);
     //value hashmap序列化
             template.setHashValueSerializer(jackson2JsonRedisSerializer);
             return template;
         }
     
         @Bean
         public CacheManager cacheManager(RedisConnectionFactory factory) {
             RedisSerializer<String> redisSerializer = new StringRedisSerializer();
             Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
     //解决查询缓存转换异常的问题
             ObjectMapper om = new ObjectMapper();
             om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
             om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
             jackson2JsonRedisSerializer.setObjectMapper(om);
     // 配置序列化（解决乱码的问题）,过期时间600秒
             RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
                     .entryTtl(Duration.ofSeconds(600))
                     .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(redisSerializer))
                     .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(jackson2JsonRedisSerializer))
                     .disableCachingNullValues();
             RedisCacheManager cacheManager = RedisCacheManager.builder(factory)
                     .cacheDefaults(config)
                     .build();
             return cacheManager;
         }
     }
     ```

     

4. 测试一下

   RedisTestController中添加测试方法

   - ```
     @RestController
     @RequestMapping("/redisTest")
     public class RedisTestController {
         @Autowired
         private RedisTemplate redisTemplate;
     
         @GetMapping
         public String testRedis() {
             //设置值到redis
             redisTemplate.opsForValue().set("name","lucy");
             //从redis获取值
             String name = (String)redisTemplate.opsForValue().get("name");
             return name;
         }
     }
     ```

     

## 十一、应用问题解决

***\*缓存穿透\****：key对应的数据在数据源并不存在，每次针对此key的请求从缓存获取不到，请求都会压到数据源，从而可能压垮数据源。比如用一个不存在的用户id获取用户信息，不论缓存还是数据库都没有，若黑客利用此漏洞进行攻击可能压垮数据库![image-20231103084317872](https://gitee.com/coi4/test/raw/master/img/image-20231103084317872.png)

- **对空值缓存：**如果一个查询返回的数据为空（不管是数据是否不存在），我们仍然把这个空结果（null）进行缓存，设置空结果的过期时间会很短，最长不超过五分钟

- **设置可访问的名单（白名单）：**

  使用bitmaps类型定义一个可以访问的名单，名单id作为bitmaps的偏移量，每次访问和bitmap里面的id进行比较，如果访问id不在bitmaps里面，进行拦截，不允许访问。

- **采用布隆过滤器**：(布隆过滤器（Bloom Filter）是1970年由布隆提出的。它实际上是一个很长的二进制向量(位图)和一系列随机映射函数（哈希函数）。

  布隆过滤器可以用于检索一个元素是否在一个集合中。它的优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。)

  将所有可能存在的数据哈希到一个足够大的bitmaps中，一个一定不存在的数据会被 这个bitmaps拦截掉，从而避免了对底层存储系统的查询压力。

- **进行实时监控：**当发现Redis的命中率开始急速降低，需要排查访问对象和访问的数据，和运维人员配合，可以设置黑名单限制服务

***\*缓存击穿\****：key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。![image-20231103084451993](https://gitee.com/coi4/test/raw/master/img/image-20231103084451993.png)

- 预先设置热门数据：**在redis高峰访问之前，把一些热门数据提前存入到redis里面，加大这些热门数据key的时长**

- **实时调整：**现场监控哪些数据热门，实时调整key的过期时长

- 使用锁：

  （1） 就是在缓存失效的时候（判断拿出来的值为空），不是立即去load db。

  （2） 先使用缓存工具的某些带成功操作返回值的操作（比如Redis的SETNX）去set一个mutex key

  （3） 当操作返回成功时，再进行load db的操作，并回设缓存,最后删除mutex key；

  （4） 当操作返回失败，证明有线程在load db，当前线程睡眠一段时间再重试整个get缓存的方法。

***\*缓存雪崩\**** ：key对应的数据存在，但在redis中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端DB加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端DB压垮。

缓存雪崩与缓存击穿的区别在于这里针对很多key缓存，前者则是某一个key；![image-20231103084636265](https://gitee.com/coi4/test/raw/master/img/image-20231103084636265.png)

- **构建多级缓存架构：**nginx缓存 + redis缓存 +其他缓存（ehcache等）

- **使用锁或队列****：**

  用加锁或者队列的方式保证来保证不会有大量的线程对数据库一次性进行读写，从而避免失效时大量的并发请求落到底层存储系统上。不适用高并发情况

-  **设置过期标志更新缓存：**

  记录缓存数据是否过期（设置提前量），如果过期会触发通知另外的线程在后台去更新实际key的缓存。

- **将缓存失效时间分散开：**

  比如我们可以在原有的失效时间基础上增加一个随机值，比如1-5分钟随机，这样每一个缓存的过期时间的重复率就会降低，就很难引发集体失效的事件。

***\*分布式锁\****：随着业务发展的需要，原单体单机部署的系统被演化成分布式集群系统后，由于分布式系统多线程、多进程并且分布在不同机器上，这将使原单机部署情况下的并发控制锁策略失效，单纯的Java API并不能提供分布式锁的能力。为了解决这个问题就需要一种跨JVM的互斥机制来控制共享资源的访问，这就是分布式锁要解决的问题！

- ***\*解决方案：使用redis实现分布式锁\****

  - redis:命令

    \# set sku:1:info “OK” NX PX 10000

    EX second ：设置键的过期时间为 second 秒。 SET key value EX second 效果等同于 SETEX key second value 。

    PX millisecond ：设置键的过期时间为 millisecond 毫秒。 SET key value PX millisecond 效果等同于 PSETEX key millisecond value 。

    NX ：只在键不存在时，才对键进行设置操作。 SET key value NX 效果等同于 SETNX key value 。

    XX ：只在键已经存在时，才对键进行设置操作。

- ```
  @GetMapping("testLock")
  public void testLock(){
      //1获取锁，setne
      Boolean lock = redisTemplate.opsForValue().setIfAbsent("lock", "111");
      //2获取锁成功、查询num的值
      if(lock){
          Object value = redisTemplate.opsForValue().get("num");
          //2.1判断num为空return
          if(StringUtils.isEmpty(value)){
              return;
          }
          //2.2有值就转成成int
          int num = Integer.parseInt(value+"");
          //2.3把redis的num加1
          redisTemplate.opsForValue().set("num", ++num);
          //2.4释放锁，del
          redisTemplate.delete("lock");
  
      }else{
          //3获取锁失败、每隔0.1秒再获取
          try {
              Thread.sleep(100);
              testLock();
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  - 重启，服务集群，通过网关压力测试：

    ab -n 1000 -c 100 http://192.168.140.1:8080/test/testLock

  - 查看redis中num的值：

- ***\*优化之设置锁的过期时间\****：：setnx刚好获取到锁，业务逻辑出现异常，导致锁无法释放；解决：设置过期时间，自动释放锁。

  -  首先想到通过expire设置过期时间（缺乏原子性：如果在setnx和expire之间出现异常，锁也无法释放）![img](https://gitee.com/coi4/test/raw/master/img/wps3.jpg)
  - 在set时指定过期时间（推荐）![image-20231103085319045](https://gitee.com/coi4/test/raw/master/img/image-20231103085319045.png)
    - 可能会释放其他服务器的锁。最终等于没锁的情况。
      - 解决：setnx获取锁时，设置一个指定的唯一值（例如：uuid）；释放前获取这个值，判断是否自己的锁

- ***\*优化之UUID防误删\****： ![image-20231103085435799](https://gitee.com/coi4/test/raw/master/img/image-20231103085435799.png)

  - 删除操作缺乏原子性。

- ***\*优化之LUA脚本保证删除的原子性\****

  ```
  @GetMapping("testLockLua")
  public void testLockLua() {
      //1 声明一个uuid ,将做为一个value 放入我们的key所对应的值中
      String uuid = UUID.randomUUID().toString();
      //2 定义一个锁：lua 脚本可以使用同一把锁，来实现删除！
      String skuId = "25"; // 访问skuId 为25号的商品 100008348542
      String locKey = "lock:" + skuId; // 锁住的是每个商品的数据
  
      // 3 获取锁
      Boolean lock = redisTemplate.opsForValue().setIfAbsent(locKey, uuid, 3, TimeUnit.SECONDS);
  
      // 第一种： lock 与过期时间中间不写任何的代码。
      // redisTemplate.expire("lock",10, TimeUnit.SECONDS);//设置过期时间
      // 如果true
      if (lock) {
          // 执行的业务逻辑开始
          // 获取缓存中的num 数据
          Object value = redisTemplate.opsForValue().get("num");
          // 如果是空直接返回
          if (StringUtils.isEmpty(value)) {
              return;
          }
          // 不是空 如果说在这出现了异常！ 那么delete 就删除失败！ 也就是说锁永远存在！
          int num = Integer.parseInt(value + "");
          // 使num 每次+1 放入缓存
          redisTemplate.opsForValue().set("num", String.valueOf(++num));
          /*使用lua脚本来锁*/
          // 定义lua 脚本
          String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
          // 使用redis执行lua执行
          DefaultRedisScript<Long> redisScript = new DefaultRedisScript<>();
          redisScript.setScriptText(script);
          // 设置一下返回值类型 为Long
          // 因为删除判断的时候，返回的0,给其封装为数据类型。如果不封装那么默认返回String 类型，
          // 那么返回字符串与0 会有发生错误。
          redisScript.setResultType(Long.class);
          // 第一个要是script 脚本 ，第二个需要判断的key，第三个就是key所对应的值。
          redisTemplate.execute(redisScript, Arrays.asList(locKey), uuid);
      } else {
          // 其他线程等待
          try {
              // 睡眠
              Thread.sleep(1000);
              // 睡醒了之后，调用方法。
              testLockLua();
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  ![image-20231103085555908](https://gitee.com/coi4/test/raw/master/img/image-20231103085555908.png)

  ```
  1.定义key，key应该是为每个sku定义的，也就是每个sku有一把锁。
  String locKey ="lock:"+skuId; // 锁住的是每个商品的数据
  Boolean lock = redisTemplate.opsForValue().setIfAbsent(locKey, uuid,3,TimeUnit.SECONDS);
  ```

  ![image-20231103085639912](https://gitee.com/coi4/test/raw/master/img/image-20231103085639912.png)

- 加锁

  ```
  // 1. 从redis中获取锁,set k1 v1 px 20000 nx
  String uuid = UUID.randomUUID().toString();
  Boolean lock = this.redisTemplate.opsForValue()
        .setIfAbsent("lock", uuid, 2, TimeUnit.SECONDS);
  ```

  使用lua释放锁

  ```
  // 2. 释放锁 del
  String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
  // 设置lua脚本返回的数据类型
  DefaultRedisScript<Long> redisScript = new DefaultRedisScript<>();
  // 设置lua脚本返回类型为Long
  redisScript.setResultType(Long.class);
  redisScript.setScriptText(script);
  redisTemplate.execute(redisScript, Arrays.asList("lock"),uuid);
  ```

  重试

  ```
  Thread.sleep(500);
  testLock();
  ```

- 确保分布式锁可用，我们至少要确保锁的实现同时**满足以下四个条件**：

  \- 互斥性。在任意时刻，只有一个客户端能持有锁。

  \- 不会发生死锁。即使有一个客户端在持有锁的期间崩溃而没有主动解锁，也能保证后续其他客户端能加锁。

  \- 解铃还须系铃人。加锁和解锁必须是同一个客户端，客户端自己不能把别人加的锁给解了。

  \- 加锁和解锁必须具有原子性。

## 十二、新功能

ACL：Access Control List（访问控制列表），允许根据可以执行的命令和可以访问的键来限制某些连接。

命令：

- 使用acl list命令展现用户权限列表![image-20231103090037115](https://gitee.com/coi4/test/raw/master/img/image-20231103090037115.png)

- 使用acl cat命令：查看添加权限指令类别；加参数类型名可以查看类型下具体命令

- 使用acl whoami命令查看当前用户

- 使用aclsetuser命令创建和编辑用户ACL

  - | ACL规则                |                                                              |                                                    |
    | ---------------------- | ------------------------------------------------------------ | -------------------------------------------------- |
    | 类型                   | 参数                                                         | 说明                                               |
    | 启动和禁用用户         | ***\*on\****                                                 | 激活某用户账号                                     |
    | ***\*off\****          | 禁用某用户账号。注意，已验证的连接仍然可以工作。如果默认用户被标记为off，则新连接将在未进行身份验证的情况下启动，并要求用户使用AUTH选项发送AUTH或HELLO，以便以某种方式进行身份验证。 |                                                    |
    | 权限的添加删除         | ***\*+<command>\****                                         | 将指令添加到用户可以调用的指令列表中               |
    | ***\*-<command>\****   | 从用户可执行指令列表移除指令                                 |                                                    |
    | ***\*+@<category>\**** | 添加该类别中用户要调用的所有指令，有效类别为@admin、@set、@sortedset…等，通过调用ACL CAT命令查看完整列表。特殊类别@all表示所有命令，包括当前存在于服务器中的命令，以及将来将通过模块加载的命令。 |                                                    |
    | -@<actegory>           | 从用户可调用指令中移除类别                                   |                                                    |
    | ***\*allcommands\****  | +@all的别名                                                  |                                                    |
    | ***\*nocommand\****    | -@all的别名                                                  |                                                    |
    | 可操作键的添加或删除   | ***\*~<pattern>\****                                         | 添加可作为用户可操作的键的模式。例如~*允许所有的键 |

  - 通过命令创建新用户默认权限acl setuser user1

  - 设置有用户名、密码、ACL权限、并启用的用户acl setuser user2 on >password ~cached:* +get

  - 切换用户，验证权限![image-20231103090521853](https://gitee.com/coi4/test/raw/master/img/image-20231103090521853.png)

IO多线程：IO多线程其实指***\*客户端交互部分\****的***\*网络IO\****交互处理模块***\*多线程\****，而非***\*执行命令多线程\****。Redis6执行命令依然是单线程。

Redis 的多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程。之所以这么设计是不想因为多线程而变得复杂，需要去控制 key、lua、事务，LPUSH/LPOP 等等的并发问题。

多线程IO默认也是不开启的，需要再配置文件中配置io-threads-do-reads  yes    io-threads 4

***\*工具支持 Cluster\****：通过多线程的方式对多个分片进行压测。![image-20231103090715957](https://gitee.com/coi4/test/raw/master/img/image-20231103090715957.png)