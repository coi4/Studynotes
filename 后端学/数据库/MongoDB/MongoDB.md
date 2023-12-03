### MongoDB

## 一、基础

### 1、相关概念

MySQL在数据操作的“三高”需求和对应的Web 2.0网站需求面前，力不从心

三高需求:**高并发（对数据库的高并发读写的要求）, 高性能（对海量数据的高效率存储和访问的需求）, 高可用（对数据的高扩展性和高可用性的需求)**

#### 1.1、场景

- 社交场景, 使用 MongoDB 存储存储用户信息, 以及用户发表的朋友圈信息, 通过地理位置索引实现附近的人, 地点等功能.
- 游戏场景, 使用 MongoDB 存储游戏用户信息, 用户的装备, 积分等直接以内嵌文档的形式存储, 方便查询, 高效率存储和访问.
- 物流场景, 使用 MongoDB 存储订单信息, 订单状态在运送过程中会不断更新, 以 MongoDB 内嵌数组的形式来存储, 一次查询就能将订单所有的变更读取出来.
- 物联网场景, 使用 MongoDB 存储所有接入的智能设备信息, 以及设备汇报的日志信息, 并对这些信息进行多维度的分析.
- 视频直播, 使用 MongoDB 存储用户信息, 点赞互动信息等.

共同点：

1. 数据量大
2. 写入操作频繁
3. 价值较低的数据, 对**事务性**要求不高

什么时候使用：有一个符合，可以考虑，2个及以上，绝对使用（可以以更低的成本解决问题（包括学习, 开发, 运维等成本））

- 应用不需要事务及复杂 JOIN 支持
- 新应用, 需求会变, 数据模型无法确定, 想快速迭代开发
- 应用需要 2000 - 3000 以上的读写QPS（更高也可以）
- 应用需要 TB 甚至 PB 级别数据存储
- 应用发展迅速, 需要能快速水平扩展
- 应用要求存储的数据不丢失
- 应用需要 `99.999%` 高可用
- 应用需要大量的地理位置查询, 文本查询

#### 1.2、简介

文档型数据库（开源, 高性能, 无模式），最像关系型数据库（MySQL）的非关系型数据库；支持的数据结构非常松散, 是一种类似于 JSON 的 格式叫BSON，既可以存储比较复杂的数据类型, 又相当的灵活；由字段和值对（ﬁeld:value）组成的数据结构；一个文档认 为就是一个对象，字段的数据类型是字符型, 它的值除了使用基本的一些类型外, 还可以包括其他文档, 普通数组和文档数组.

![image-20231108104222167](https://gitee.com/coi4/test/raw/master/img/image-20231108104222167.png)

![image-20231108102952292](https://gitee.com/coi4/test/raw/master/img/image-20231108102952292.png)

MongoDB 数据库中存在的是各种各样的JSON（BSON）

- 数据库 (database)
  - 数据库是一个仓库, 存储集合 (collection)
- 集合 (collection)
  - 类似于数组, 在集合中存放文档
- 文档 (document)
  - 文档型数据库的最小单位, 通常情况, 我们存储和操作的内容都是文档

MongoDB 中, 数据库和集合都不需要手动创建, 当我们创建文档时, 如果文档所在的集合或者数据库不存在, **则会自动创建数据库或者集合**

数据库管理语法：

![image-20231108103335551](https://gitee.com/coi4/test/raw/master/img/image-20231108103335551.png)

集合管理语法：

![image-20231108103402753](https://gitee.com/coi4/test/raw/master/img/image-20231108103402753.png)

#### 1.3、数据模型

<img src="https://gitee.com/coi4/test/raw/master/img/image-20231108103523921.png" alt="image-20231108103523921" style="zoom:200%;" />

#### 1.4、特点

高性能：

- 提供高性能的数据持久化：
  - 嵌入式数据模型的支持减少了数据库系统上的 I/O 活动
  - 索引支持更快的查询, 并且可以包含来自嵌入式文档和数组的键 (文本索引解决搜索的需求, TTL 索引解决历史数据自动过期的需求, 地理位置索引可以用于构件各种 O2O 应用)
  - mmapv1, wiredtiger, mongorocks (rocksdb) in-memory 等多引擎支持满足各种场景需求
  - Gridfs 解决文件存储需求

高可用：

- 复制工具称作**副本集** (replica set) 可以提供自动故障转移和数据冗余

高扩展：

- 水平扩展是其核心功能一部分
- 分片将数据分布在一组集群的机器上 (海量数据存储, 服务能力水平扩展)
- 支持基于**片键**创建数据区域, 在一个平衡的集群当中,将一个区域所覆盖的读写**只定向**到该区域的那些片

支持丰富的查询语言, 支持读和写操作(CRUD), 比如数据聚合, 文本搜索和地理空间查询等. 无模式（动态模式）, 灵活的文档模型

### 2、单机部署

安装启动：

- 下载：https://www.mongodb.com/download-center#community![image-20231108105027305](https://gitee.com/coi4/test/raw/master/img/image-20231108105027305.png)
  - 版本的选择：
    - MongoDB的版本命名规范如：x.y.z；
    - y为奇数时表示当前版本为开发版，如：1.5.2、4.1.13；
    - y为偶数时表示当前版本为稳定版，如：1.6.3、4.0.10；
    - z是修正版本号，数字越大越好。

- 解压安装：在解压目录中手动建立一个目录用于存放数据文件，如data/db

  - 命令行参数方式启动服务：在bin目录中打开命令行提示符，输入

    ```
    mongod --dbpath=..\data\db
    ```

    - 指定窗口：-port
    - bin下mongo启动服务用的，mongo客户端连接服务用的
    - 可以将bin设置到换金发变量的path中

  - 配置文件方式：解压目录中新建config文件夹，该文件夹中新建配置文件mongo.conf

    ```
    storage:
    #The directory where the mongod instance stores its data.Default Value is "\data\db" on Windows.
    dbPath: D:\02_Server\DBServer\mongodb-win32-x86_64-2008plus-ssl-4.0.1\dat
    ```

    - 使用双引号，自动将双引号的内容转义，如果不转义报错

      - 解决：\换成/或\\\
      - 路径中没有空格无需加引号

    - 不能以tab分割字段

      - 将其转换成空格

      - 启动方式

        ```
        mongod -f ../config/mongod.conf
        或
        mongod --config ../config/mongod.conf
        ```

    - 更多参数配置![image-20231109091125551](https://gitee.com/coi4/test/raw/master/img/image-20231109091125551.png)

shell连接

- 命令行输入以下shell命令即可完成登录

  ```
  mongo
  或
  mongo --host=127.0.0.1 --port=27017
  ```

- 查看已有数据库

  ```
  >show databases
  ```

- 退出mongodb

  ```
  exit
  ```

- 更多参数查看

  ```
  mongo --help
  ```

compass-图形化界面客户端

- 下载：https://www.mongodb.com/download-center/v2/compass?initial=true
- 解压执行MongoDBCompassCommunity.exe![image-20231109091605780](https://gitee.com/coi4/test/raw/master/img/image-20231109091605780.png)

### 3、常用命令

#### 3.1、数据库操作

**选择和创建**：use 数据库名称

- 数据库不存在则自动创建：use articledb
- 集合只有在内容插入后才会创建，创建集合（数据表）后要再插入一个文档（记录），集合才会真正创建

**查看有权限查看的**所有数据库**命令**：show dbs/show databases

**查看当前正在使用的数据库命令**：db

默认的数据库为test，如果没有选择数据库，集合将放在test数据库中

数据库名

- 不能是空字符串
- 不能含‘ ’、$、/\和\0
-  应全部小写
- 最多64字节

默认数据库名，可以直接访问这些有特殊作用的数据库

- **admin**: 从权限角度考虑, 这是 `root` 数据库, 如果将一个用户添加到这个数据库, 这个用户自动继承所有数据库的权限, 一些特定的服务器端命令也只能从这个数据库运行, 比如列出所有的数据库或者关闭服务器
- **local**: 数据永远不会被复制, 可以用来存储限于本地的单台服务器的集合 (部署集群, 分片等)
- **config**: Mongo 用于分片设置时, `config` 数据库在内部使用, 用来保存分片的相关信息

数据库的删除：db.dropDatabase()（主要用来删除已经持久化的数据库）

#### 3.2、集合操作

隐式创建：当向集合中插入一个文档时，如果集合不存在，会自动创建集合

集合删除：db.collection.drop()/db.集合.drop()（删除成功返回true）

#### 3.3、文档基本CRUD

文档的插入：

- 单个文档插入：insert（）或save（）

  ```
  db.collection.insert(
  <document or array of documents>,
  {
  writeConcern: <document>,
  ordered: <boolean>
  }
  )
  ```

  ![image-20231109230938612](https://gitee.com/coi4/test/raw/master/img/image-20231109230938612.png)

  ```
  //要向comment的集合(表)中插入一条测试数据：
  db.comment.insert({"articleid":"100000","content":"今天天气真好，阳光明
  媚","userid":"1001","nickname":"Rose","createdatetime":new Date(),"likenum":NumberInt(10),"state":null})
  //comment不在，会隐式创建
  //）mongo中的数字，默认情况下是double类型，如果要存整型，必须使用函数NumberInt(整型数字)，否则取出来就有问题了
  //插入当前日期使用 new Date()
  //插入的数据没有指定 _id ，会自动生成主键值
  //如果某字段没值，可以赋值为null，或不写该字段。
  //显示WriteResult({ "nInserted" : 1 })表示插入数据成功
  ```

- 文档键命名规范：

  - 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
  - .和$有特别的意义，只有在特定环境下才能使用。
  - 以下划线"_"开头的键是保留的(不是严格要求的)。

- 批量插入：

  ```
  db.collection.insertMany(
      [ <document 1> , <document 2>, ... ],
      {
           writeConcern: <document>,
           ordered: <boolean>
       }
  )
  ```

  ```
  db.comment.insertMany([
  {"_id":"1","articleid":"100001","content":"我们不应该把清晨浪费在手机上，健康很重要，一杯温水幸福你我
  他。","userid":"1002","nickname":"相忘于江湖","createdatetime":new Date("2019-08-
  05T22:08:15.522Z"),"likenum":NumberInt(1000),"state":"1"},
  {"_id":"2","articleid":"100001","content":"我夏天空腹喝凉开水，冬天喝温开水","userid":"1005","nickname":"伊人憔
  悴","createdatetime":new Date("2019-08-05T23:58:51.485Z"),"likenum":NumberInt(888),"state":"1"},
  {"_id":"3","articleid":"100001","content":"我一直喝凉开水，冬天夏天都喝。","userid":"1004","nickname":"杰克船
  长","createdatetime":new Date("2019-08-06T01:05:06.321Z"),"likenum":NumberInt(666),"state":"1"},
  {"_id":"4","articleid":"100001","content":"专家说不能空腹吃饭，影响健康。","userid":"1003","nickname":"凯
  撒","createdatetime":new Date("2019-08-06T08:18:35.288Z"),"likenum":NumberInt(2000),"state":"1"},
  {"_id":"5","articleid":"100001","content":"研究表明，刚烧开的水千万不能喝，因为烫
  嘴。","userid":"1003","nickname":"凯撒","createdatetime":new Date("2019-08-
  06T11:01:02.521Z"),"likenum":NumberInt(3000),"state":"1"}
  ]);
  ```

  如果某条数据插入失败，将会终止插入，但已经插入成功的数据不会回滚掉。

  因为批量插入由于数据较多容易出现失败，因此，可以使用try catch进行异常捕捉处理，测试的时候可以不处理。

文档的基本查询：

```
db.collection.find(<query>, [projection])
```

![image-20231109232046624](https://gitee.com/coi4/test/raw/master/img/image-20231109232046624.png)

- 查询所有：db.comment.find()/db.comment.find({})

  - 加条件：db.comment.find({userid:'1003'})
  - 只需要返回符合条件的第一条数据：db.comment.findOne({userid:'1003'})

- 投影查询：查询结果返回部分字段

  - 只显示 _id、userid、nickname :

    ```
    >db.comment.find({userid:"1003"},{userid:1,nickname:1})
    { "_id" : "4", "userid" : "1003", "nickname" : "凯撒" }
    { "_id" : "5", "userid" : "1003", "nickname" : "凯撒" }
    ```

  - 查询所有数据，但只显示 _id、userid、nickname :

    ```
    >db.comment.find({},{userid:1,nickname:1})
    ```

文档的更新：

![image-20231109232547964](https://gitee.com/coi4/test/raw/master/img/image-20231109232547964.png)

![image-20231109232647830](https://gitee.com/coi4/test/raw/master/img/image-20231109232647830.png)

- 覆盖的修改：

  ```
  //修改_id为1的记录，点赞量为1001
  db.comment.update({_id:"1"},{likenum:NumberInt(1001)})
  ```

- 局部修改

  ```
  db.comment.update({_id:"2"},{$set:{likenum:NumberInt(889)}})
  ```

- 批量的修改

  ```
  //默认只修改第一条数据
  db.comment.update({userid:"1003"},{$set:{nickname:"凯撒2"}})
  //修改所有符合条件的数据
  db.comment.update({userid:"1003"},{$set:{nickname:"凯撒大帝"}},{multi:true})
  ```

- 列值增长的修改：

  ```
  //对3号数据的点赞数，每次递增1
  db.comment.update({_id:"3"},{$inc:{likenum:NumberInt(1)}})
  ```

删除文档：

```
db.集合名称.remove(条件)
//删除所有数据
db.comment.remove({})
```

#### 3.4、文档的分页查询

统计查询：db.collection.count(query, options)

![image-20231109233528811](https://gitee.com/coi4/test/raw/master/img/image-20231109233528811.png)

- 统计所有记录数：db.comment.count()

分页列表查询：\>db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)

- 返回指定条数的记录，可以在fifind方法后调用limit来返回结果(TopN)，默认值20
- skip方法同样接受一个数字参数作为跳过的记录条数。（前N个不要）,默认值是0

```
//需求：每页2个，第二页开始：跳过前两条数据，接着值显示3和4条数据
//第一页
db.comment.find().skip(0).limit(2)
//第二页
db.comment.find().skip(2).limit(2)
//第三页
db.comment.find().skip(4).limit(2)
```

排序查询：db.COLLECTION_NAME.find().sort({KEY:1})/db.集合名称.find().sort(排序方式)

- 1为升序，-1降序
- 先执行sort（），然后是skip（），最后是limit（）

正则的复杂条件查询：模糊查询：db.collection.find({field:/正则表达式/})/db.集合.find({字段:/正则表达式/})

- 查询以“专家”开头的：db.comment.find({content:/^专家/})

比较查询：

```
db.集合名称.find({ "field" : { $gt: value }}) // 大于: field > value

db.集合名称.find({ "field" : { $lt: value }}) // 小于: field < value

db.集合名称.find({ "field" : { $gte: value }}) // 大于等于: field >= value

db.集合名称.find({ "field" : { $lte: value }}) // 小于等于: field <= value

db.集合名称.find({ "field" : { $ne: value }}) // 不等于: field != value
```

- 例如：

  ```
  //查询评论点赞数量大于700的记录
  db.comment.find({likenum:{$gt:NumberInt(700)}})
  ```

包含查询：db.comment.find({userid:{$in:["1003","1004"]}})

- 不包含使用$nin操作符

条件连接查询：

- 同时满足两个以上条件：$and:[ { },{ },{ } ]

```
db.comment.find({$and:[{likenum:{$gte:NumberInt(700)}},{likenum:{$lt:NumberInt(2000)}}]})
```

- 或者关系：$or:[ { },{ },{ } ]

总结

> 选择切换数据库：use articledb
>
> 插入数据：db.comment.insert({bson数据})
>
> 查询所有数据：db.comment.find();
>
> 条件查询数据：db.comment.find({条件})
>
> 查询符合条件的第一条记录：db.comment.findOne({条件})
>
> 查询符合条件的前几条记录：db.comment.find({条件}).limit(条数)
>
> 查询符合条件的跳过的记录：db.comment.find({条件}).skip(条数)
>
> 修改数据：db.comment.update({条件},{修改后的数据}) 或db.comment.update({条件},{$set:{要修改部分的字段:数据})
>
> 修改数据并自增某字段值：db.comment.update({条件},{$inc:{自增的字段:步进值}})
>
> 删除数据：db.comment.remove({条件})
>
> 统计查询：db.comment.count({条件})
>
> 模糊查询：db.comment.find({字段名:/正则表达式/})
>
> 条件比较运算：db.comment.find({字段名:{$gt:值}})
>
> 包含查询：db.comment.find({字段名:{$in:[值1，值2]}})或db.comment.find({字段名:{$nin:[值1，值2]}})
>
> 条件连接查询：db.comment.find({$and:[{条件1},{条件2}]})或db.comment.find({$or:[{条件1},{条件2}]})

### 4、索引

#### 4.1、概述

MongoDB索引使用B树数据结构（B-Tree）（MySQL是B+Tree)

#### 4.2、类型

单字段索引：支持在文档的单个字段上创建用户定义的升序/降序索引，称为单字段索引（Single Field Index）；MongoDB可以在任何方向上遍历索引

复合索引：支持多个字段的用户定义索引，即复合索引（Compound Index）；如果复合索引由 { userid: 1, score: -1 } 组成，则索引首先按userid正序排序，然后在每个userid的值内，再在按score倒序排序。

其他：

地理空间索引：返回结果时使用平面几何的二维索引和返回结果时使用球面几何的二维球面索引。

文本：支持在集合中搜索字符串内容。这些文本索引不存储特定于语言的停止词（例如“the”、“a”、“or”），而将集合中的词作为词干，只存储根词。

哈希：散列索引类型，它对字段值的散列进行索引。这些索引在其范围内的值分布更加随机，但只支持相等匹配，不支持基于范围的查询。

#### 4.3、索引管理操作

查看：返回一个集合中所有索引的数组；db.collection.getIndexes()

- 结果中显示的是默认 _id 索引。
- 该索引可防止客户端插入两个具有相同值的文档；不能在_id字段上删除此索引。
- 该索引是唯一索引，因此值不能重复，即 _id 值不能重复的。在分片集群中，通常使用 _id 作为片键。

创建：db.collection.createIndex(keys, options)

![image-20231114102011563](https://gitee.com/coi4/test/raw/master/img/image-20231114102011563.png)

![image-20231114102025966](https://gitee.com/coi4/test/raw/master/img/image-20231114102025966.png)

移除：db.collection.dropIndex(index)![image-20231114102356686](https://gitee.com/coi4/test/raw/master/img/image-20231114102356686.png)

- 所有索引的移除：db.collection.dropIndexes()
  - _id 的字段的索引是无法删除的，只能删除非 _id 字段的索引。

#### 4.4、使用

分析查询性能（Analyze Query Performance）通常使用执行计划（解释计划、Explain Plan）来查看查询的情况

想知道，建立的索引是否有效，效果如何，都需要通过执行计划查看。

db.collection.find(query,options).explain(options)

 "stage" : "COLLSCAN", 表示全集合扫描

![image-20231114103041655](https://gitee.com/coi4/test/raw/master/img/image-20231114103041655.png)

创建索引，再看执行计划： "stage" : "IXSCAN" ,基于索引的扫描![image-20231114103130581](https://gitee.com/coi4/test/raw/master/img/image-20231114103130581.png)

涵盖的查询：当查询条件和查询的投影仅包含索引字段时，MongoDB直接从索引返回结果，而不扫描任何文档或将文档带入内存。

![image-20231114103341864](https://gitee.com/coi4/test/raw/master/img/image-20231114103341864.png)

![image-20231114103359316](https://gitee.com/coi4/test/raw/master/img/image-20231114103359316.png)

### 5、在Nodejs中使用MongoDB-mongoose

#### 5.1、mongoose提供的新对象类型

#### 5.2、简单使用

#### 5.3、Mongoose的CRUD

### 6、使用Mocha编写测试“TestDriven Development”

### 7、文章评论

> 文章示例参考：早晨空腹喝水，是对还是错？https://www.toutiao.com/a6721476546088927748/
>
> 需要实现以下功能：
>
> 1）基本增删改查API
>
> 2）根据文章id查询评论
>
> 3）评论点赞

1. 表结构分析

   ![image-20231114104252485](https://gitee.com/coi4/test/raw/master/img/image-20231114104252485.png)

2. 技术选型：SpringDataMongoDB

   - 用于操作MongoDB的持久层框架，封装了底层的mongodb-driver。
   - https://projects.spring.io/spring-data-mongodb/

3. 文章微服务模块搭建

   - 引入依赖

   - 创建application.yml

     ```
     spring:
     #数据源配置
     data:
     mongodb:
     # 主机地址
     host: 192.168.40.141
     # 数据库
     database: articledb
     # 默认端口是27017
     port: 27017
     #也可以使用uri连接
     #uri: mongodb://192.168.40.134:27017/articledb
     ```

   - 创建启动类:![image-20231114104537813](https://gitee.com/coi4/test/raw/master/img/image-20231114104537813.png)

4. 文章评论实体类编写

5. 基本增删改查

6. 根据上级ID查询文章评论的分页列表

7. 实现评论点赞

## 二、进阶

### 1、副本集

#### 1.1、简介

MongoDB中的副本集（Replica Set）是一组维护相同数据集的mongod服务。 副本集可提供冗余和高可用性，是所有生产部署的基础;集类似于有自动故障恢复功能的主从集群。通俗的讲就是用多台机器进行同一数据的异步同步，从而使多台机器拥有同一数据的多个副本，并且当主库当掉时在不需要用户干预的情况下自动切换其他备份服务器做主库。而且还可以利用副本服务器做只读服务器，实现读写分离，提高负载。

#### 1.2、两种类型三个角色

类型:

- 主节点(Primary): 数据操作的主要连接点，可读写。
- 次要节点(Secondaries)：数据冗余备份节点，可以读或选举。

角色:

- 主要成员(Primary):主要接收所有写操作。就是主节点。

- 副本成员(Replicate):从主节点通过复制操作以维护相同的数据集，即备份数据，不可写操作，但可

  以读操作（但需要配置）。是默认的一种从节点类型。

- 仲裁者(Arbiter):不保留任何数据的副本，只具有投票选举作用。当然也可以将仲裁服务器维护为副本集的一部分，即副本成员同时也可以是仲裁者。也是一种从节点类型。

  - 可以将额外的mongod实例添加到副本集作为仲裁者;不维护数据集,目的是通过响应其他副本集成员的心跳和选举请求来维护副本集中的仲裁; 因为不存储数据集，所以仲裁器可以是提供副本集仲裁功能的好方法，其资源成本比具有数据集的全功能副本集成员更便宜。
  - 副本集具有偶数个成员,添加仲裁者以获得主要选举中的“大多数”投票。

![image-20231114105124630](https://gitee.com/coi4/test/raw/master/img/image-20231114105124630.png)

副本集架构目标:一主一副本一仲裁

#### 1.3、副本集的创建

1. 创建主节点
2. 创建副本节点
3. .创建仲裁节点
4. 初始化配置副本集和主节点
5. 查看副本集配置内容
6. 查看副本集状态
7. 添加副本从节点
8. 添加仲裁节点

#### 1.4、数据读写操作

登录主节点27017,写如何读取数据

![image-20231114105845032](https://gitee.com/coi4/test/raw/master/img/image-20231114105845032.png)

从节点默认情况下,没有读写权限:

- 设置读操作权限：rs.slaveOk() /  rs.slaveOk(true)(取消false)

- ```
  在27018上设置作为奴隶节点权限，具备读权限
  rs:SECONDARY> rs.slaveOk()
  ```

  但仍然不可插入:主插入,从来读取![image-20231114110134773](https://gitee.com/coi4/test/raw/master/img/image-20231114110134773.png)

仲裁节点:不存放任何业务数据可以登陆查看,只存放副本集配置等数据![image-20231114110248743](https://gitee.com/coi4/test/raw/master/img/image-20231114110248743.png)

#### 1.5、主节点的选举原则

MongoDB在副本集中，会自动进行主节点的选举，主节点选举的触发条件：

1. 主节点故障
2. 主节点网络不可达（默认心跳信息为1秒）
3. 人工干预（rs.stepDown(600)）

当复制集内存活成员数量不足大多数时，整个复制集将无法选举出Primary，复制集将无法提供写服务，处于只读状态。

票数相同,数据新的节点获胜

可以通过设置优先级（priority）来设置额外票数。优先级即权重，取值为0-1000，相当于可额外增加0-1000的票数，优先级的值越大，就越可能获得多数成员的投票（votes）数。指定较高的值可使成员更有资格成为主要成员，更低的值可使成员更不符合条件。

- 默认情况下,优先级的值是1
- 查看:re.conf()
- 主节点和副本节点的优先级各为1，即，默认可以认为都已经有了一票。但选举节点，优先级是0，（选举节点的优先级必须是0，不能是别的值。即不具备选举权，但具有投票权）

#### 1.6、故障测试

副本节点:

关闭27018副本节点：发现，主节点和仲裁节点对27018的心跳失败。因为主节点还在，因此，没有触发投票选举。如果此时，在主节点写入数据。再启动从节点，会发现，主节点写入的数据，会自动同步给从节点。

```
db.comment.insert({"_id":"1","articleid":"100001","content":"我们不应该把清晨浪费在
手机上，健康很重要，一杯温水幸福你我他。","userid":"1002","nickname":"相忘于江
湖","createdatetime":new Date("2019-08-
05T22:08:15.522Z"),"likenum":NumberInt(1000),"state":"1"})
```

主节点:

关闭27017节点发现，从节点和仲裁节点对27017的心跳失败，当失败超过10秒，此时因为没有主节点了，会自动发起投票。而副本节点只有27018，因此，候选人只有一个就是27018，开始投票。27019向27018投了一票，27018本身自带一票，因此共两票，超过了“大多数”27019是仲裁节点，没有选举权，27018不向其投票，其票数是0.最终结果，27018成为主节点。具备读写功能。在27018写入数据查看。再启动27017节点，发现27017变成了从节点，27018仍保持主节点。登录27017节点，发现是从节点了，数据自动从27018同步。从而实现了高可用。

```
db.comment.insert({"_id":"2","articleid":"100001","content":"我夏天空腹喝凉开水，冬
天喝温开水","userid":"1005","nickname":"伊人憔悴","createdatetime":new Date("2019-
08-05T23:58:51.485Z"),"likenum":NumberInt(888),"state":"1"})
```

仲裁节点和主节点:

先关掉仲裁节点27019，关掉现在的主节点27018

登录27017后，发现，27017仍然是从节点，副本集中没有主节点了，导致此时，副本集是只读状态，无法写入。27017的票数，没有获得大多数，即没有大于等于2，它只有默认的一票（优先级是1）,所以不选举。 

如果要触发选举，随便加入一个成员即可。

- 如果只加入27019仲裁节点成员，则主节点一定是27017，因为没得选了，仲裁节点不参与选举，但参与投票。（不演示）

- 如果只加入27018节点，会发起选举。因为27017和27018都是两票，则按照谁数据新，谁当主节点

仲裁节点和从节点：

先关掉仲裁节点27019，关掉现在的副本节点2701810秒后，27017主节点自动降级为副本节点。（服务降级）副本集不可写数据了，已经故障了。

#### 1.7、Compass连接副本集

**使用云服务器需要修改配置中的主节点**ip

```
var config = rs.config();
config.members[0].host="180.76.159.126:27017";rs.reconfig(config)
```

![image-20231114111804554](https://gitee.com/coi4/test/raw/master/img/image-20231114111804554.png)

![image-20231114111820057](https://gitee.com/coi4/test/raw/master/img/image-20231114111820057.png)

#### 1.8、SpringDataMongoDB连接副本集

```
mongodb://host1,host2,host3/articledb?
connect=replicaSet&slaveOk=true&replicaSet=副本集名字
```

slaveOk=true：开启副本节点读的功能，可实现读写分离。

connect=replicaSet：自动到副本集中选择读写的主机。如果slaveOK是打开的，则实现了读写分

离

示例：连接 replica set 三台服务器 (端口 27017, 27018, 和27019)，直接连接第一个服务器，无论是replica set一部分或者主服务器或者从服务器，写入操作应用在主服务器 并且分布查询到从服务器。修改配置文件application.yml

![image-20231114112044800](https://gitee.com/coi4/test/raw/master/img/image-20231114112044800.png)

### 2、分片集群

#### 2.1、分片概念

分片（sharding）是一种跨多台机器分布数据的方法， MongoDB使用分片来支持具有非常大的数据集和高吞吐量操作的部署。指将数据拆分，将其分散存在不同的机器上的过程。

具有大型数据集或高吞吐量应用程序的数据库系统可以会挑战单个服务器的容量。例如，高查询率会耗尽服务器的CPU容量。工作集大小大于系统的RAM会强调磁盘驱动器的I / O容量。

有两种解决系统增长的方法：垂直扩展和水平扩展。

- 垂直扩展意味着增加单个服务器的容量，例如使用更强大的CPU，添加更多RAM或增加存储空间量。可用技术的局限性可能会限制单个机器对于给定工作负载而言足够强大。此外，基于云的提供商基于可用的硬件配置具有硬性上限。结果，垂直缩放有实际的最大值。
- 水平扩展意味着划分系统数据集并加载多个服务器，添加其他服务器以根据需要增加容量。虽然单个机器的总体速度或容量可能不高，但每台机器处理整个工作负载的子集，可能提供比单个高速大容量服务器更高的效率。扩展部署容量只需要根据需要添加额外的服务器，这可能比单个机器的高端硬件的总体成本更低。权衡是基础架构和部署维护的复杂性增加。

MonggoDB支持通过分片进行水平扩展

#### 2.2、分片集群包含的组件

分片（存储）：每个分片包含分片数据的子集。 每个分片都可以部署为副本集。

mongos（路由）：mongos充当查询路由器，在客户端应用程序和分片集群之间提供接口。

confifig servers（“调度”的配置）：配置服务器存储群集的元数据和配置设置。 从MongoDB 3.4开始，必须将配置服务器部署为副本（CSRS）。

![image-20231114112326551](https://gitee.com/coi4/test/raw/master/img/image-20231114112326551.png)

#### 2.3、分片集群架构目标

两个分片节点副本集（3+3）+一个配置节点副本集（3）+两个路由节点（2），共11个服务节点。

#### 2.4、分片（存储）节点副本集的创建

所有的的配置文件都直接放到 sharded_cluster 的相应的子目录下面，默认配置文件名字：mongod.conf

##### 2.4.1、第一套副本集

一主一副本一仲裁：

准备存放数据和日志的目录

新建或修改配置文件

依次启动三个mongod服务

查看是否启动：

- 初始化副本集和创建主节点
- 主节点配置查看
- 添加副本节点
- 添加仲裁节点

##### 2.4.2、第二套

一主一副本一仲裁

同上

#### 2.5、配置节点副本集的创建

同上

#### 2.6、路由节点的创建和操作

##### 2.6.1、第一个路由节点的创建和连接：

准备存放数据和日志的目录

新建或修改配置文件

启动mongos

客户端登录mongos

##### 2.6.2、在路由节点上进行分片配置操作

使用命令添加分片：

- 添加分片：sh.addShard("IP:Port")

  - 将第一套副本集加进来
  - 查看分片状态情况
  - 将第二套加进来
  - 查看

- 开启分片功能：sh.enableSharding("库名")、sh.shardCollection("库名.集合名",{"key":1})

  - 在mongos上的articledb数据库配置sharding
  - 查看

- 集合分片：sh.shardCollection(namespace, key, unique)![image-20231114113853066](https://gitee.com/coi4/test/raw/master/img/image-20231114113853066.png)

  - 查看：sh.status()

  - 显示集群详细信息：mongos> db.printShardingStatus()

  - 查看均衡器是否工作：mongos> sh.isBalancerRunning()

    false

  - 查看当前Balancer状态：mongos> sh.getBalancerState()

    true

  - 分片规则：

    - 哈希策略
    - 范围策略
    - 基于范围的分片方式与基于哈希的分片方式性能对比：

##### 2.6.3、分片后插入数据测试

测试一：哈希规则

- 登录mongos后，向comment循环插入1000条数据做测试![image-20231114114628629](https://gitee.com/coi4/test/raw/master/img/image-20231114114628629.png)

- 分别登录两个片的主节点，统计文档数量![image-20231114114647565](https://gitee.com/coi4/test/raw/master/img/image-20231114114647565.png)

  ![image-20231114114655596](https://gitee.com/coi4/test/raw/master/img/image-20231114114655596.png)

测试二：范围规则

- 循环插入
- 查看

#### 2.7、Compass连接分片集群

![image-20231114114759619](https://gitee.com/coi4/test/raw/master/img/image-20231114114759619.png)

![image-20231114114812209](https://gitee.com/coi4/test/raw/master/img/image-20231114114812209.png)

#### 2.8、SpringDataMongoDB连接分片集群

配置和单机mongod的配置一样![image-20231114114854118](https://gitee.com/coi4/test/raw/master/img/image-20231114114854118.png)

#### 2.9、清除所有节点数据

### 3、安全认证

#### 3.1、MongoDB的用户和角色权限简介

默认情况下，MongoDB实例启动运行时没有启用用户访问权限控制

为了强制开启用户访问控制(用户验证)，则需要在MongoDB实例启动时使用选项 --auth 或在指定启动配置文件中添加选项 auth=true 。

启用访问控制：MongoDB使用的是基于角色的访问控制(Role-Based Access Control,RBAC)来管理用户对实例的访问。通过对用户授予一个或多个角色来控制用户访问数据库资源的权限和数据库操作的权限，在对用户分配角色之前，用户无法访问实例。在实例启动时添加选项 --auth 或指定启动配置文件中添加选项 auth=true 。

角色：在MongoDB中通过角色对用户授予相应数据库资源的操作权限，每个角色当中的权限可以显式指定，也可以通过继承其他角色的权限，或者两都都存在的权限。![image-20231114115131469](https://gitee.com/coi4/test/raw/master/img/image-20231114115131469.png)

权限：权限由指定的数据库资源(resource)以及允许在指定资源上进行的操作(action)组成。

1. 资源(resource)包括：数据库、集合、部分集合和集群；

2. 操作(action)包括：对资源进行的增、删、改、查(CRUD)操作。

#### 3.2、单实例环境

对单实例的MongoDB服务开启安全认证，这里的单实例指的是未开启副本集或分片的MongoDB实例。

关闭已开启的服务：增加mongod的单实例的安全认证功能，可以在服务搭建的时候直接添加，也可以在之前搭建好的服务上添加。使用之前搭建好的服务，先停止之前的服务

- 快速关闭方法（快速，简单，数据可能会出错）：通过系统的kill命令直接杀死进程；杀完要检查一下，避免有的没有杀掉

  ```
  #通过进程编号关闭节点
  kill -2 54410
  ```

  如果一旦是因为数据损坏，则需要进行如下操作：

  - 删除lock文件：rm -f /mongodb/single/data/db/*.lock
  - 修复数据：/usr/local/mongodb/bin/mongod --repair --dbpath=/mongodb/single/data/db

- 标准的关闭方法（数据不容易出错，但麻烦）：通过mongo客户端中的shutdownServer命令来关闭服务

  - ![image-20231114115512456](https://gitee.com/coi4/test/raw/master/img/image-20231114115512456.png)

添加用户和权限：

- 先按照普通无授权认证的配置，来配置服务端的配置文件 /mongodb/single/mongod.conf 

- 按之前未开启认证的方式（不添加 --auth 参数）来启动MongoDB服务（在操作用户时，启动mongod服务时尽量不要开启授权。）

- 使用Mongo客户端登录：

- 创建两个管理员用户，一个是系统的超级管理员 myroot ，一个是admin库的管理用户

  myadmin （对安全要求很高，防止超管泄漏，则不要创建超管用户）

- 认证测试

- 创建普通用户

服务端开启认证和客户端连接登录：

- 关闭已经启动的服务
- 以开启认证的方式启动服务
  - 参数方式：
  - 配置文件方式
- 开启了认证的情况下的客户端登录
  - 先连接再认证
  - 连接时直接认证

SpringDataMongoDB连接认证：使用用户bobo使用密码 123456 连接到MongoDB 服务上。

- application.yml：![image-20231114120003398](https://gitee.com/coi4/test/raw/master/img/image-20231114120003398.png)

#### 3.3、副本集环境

![image-20231114120021509](https://gitee.com/coi4/test/raw/master/img/image-20231114120021509.png)

对副本集执行访问控制需要配置两个方面:

- 副本集和共享集群的各个节点成员之间使用内部身份验证，可以使用密钥文件或x.509证书。密钥文件比较简单，本文使用密钥文件，官方推荐如果是测试环境可以使用密钥文件，但是正式环境，官方推荐x.509证书。原理就是，集群中每一个实例彼此连接的时候都检验彼此使用的证书的内容是否相同。只有证书相同的实例彼此才可以访问
- 使用客户端连接到mongodb集群时，开启访问授权。对于集群外部的访问。如通过可视化客户端，或者通过代码连接的时候，需要开启授权。

在keyfifile身份验证中，副本集中的每个mongod实例都使用keyfifile的内容作为共享密码，只有具有正确密钥文件的mongod或者mongos实例可以连接到副本集。密钥文件的内容必须在6到1024个字符之间，并且在unix/linux系统中文件所有者必须有对文件至少有读的权限。

1. 关闭已开启的副本集服务：

2. 通过主节点添加一个管理员账号：只需要在主节点上添加用户，副本集会自动同步

3. 创建副本集认证的key文件

   - 生成一个key文件到当前文件夹中。

     - 使用openssl生成密码文件，然后使用chmod来更改文件权限，仅为文件所有者提供读取权限![image-20231114120327148](https://gitee.com/coi4/test/raw/master/img/image-20231114120327148.png)

   - 所有副本集节点都必须要用同一份keyfifile，一般是在一台机器上生成，然后拷贝到其他机器上，且必须有读的权限，否则将来会报错：permissions on

     /mongodb/replica_sets/myrs_27017/mongo.keyfile are too open

   - 一定要保证密钥文件一致，文件位置随便。但是为了方便查找，建议每台机器都放到一个固定的位置，都放到和配置文件一起的目录中。

     ```
     //将该文件分别拷贝到多个目录中
     [root@bobohost ~]# cp mongo.keyfile /mongodb/replica_sets/myrs_27017
     [root@bobohost ~]# cp mongo.keyfile /mongodb/replica_sets/myrs_27018
     [root@bobohost ~]# cp mongo.keyfile /mongodb/replica_sets/myrs_27019
     ```

4. 修改配置文件指定keyfile：![image-20231114120551000](https://gitee.com/coi4/test/raw/master/img/image-20231114120551000.png)

   ![image-20231114120603585](https://gitee.com/coi4/test/raw/master/img/image-20231114120603585.png)

   ![image-20231114120613761](https://gitee.com/coi4/test/raw/master/img/image-20231114120613761.png)

5. 重新启动副本集：如果副本集是开启状态，则先分别关闭关闭复本集中的每个mongod，从次节点开始。直到副本集的所有成员都离线，包括任何仲裁者。主节点必须是最后一个成员关闭以避免潜在的回滚。![image-20231114120711517](https://gitee.com/coi4/test/raw/master/img/image-20231114120711517.png)

6. 在主节点上添加普通账号：重新连接，使用普通用户bobo重新登录，查看数据。![image-20231114120748493](https://gitee.com/coi4/test/raw/master/img/image-20231114120748493.png)

7. SpringDtaMongoDB连接副本集

#### 3.4、分片集群环境