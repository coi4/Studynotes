# ZooKeeper

### 1、初识

Apache Hadoop项目下的一个子项目，是一个树形目录服务；管理Hadoop（大象）、Hive（蜜蜂）、Pig（猪）的管理员，简称zk；分布式、开源的分布式应用程序的协调服务

主要功能：K

- 配置管理
- 分布式锁
- 集群管理

### 2、安装与配置

### 3、命令操作

#### 3.1、数据模型

与Unix的文件系统目录树类似，拥有一个层次化结构

每一个节点都被称为ZNode，每个节点上都会保存自己的数据和节点信息

节点允许少量（1MB）数据存储在该节点下

节点可分为四大类：

- PERSISTENT 持久化节点
- EPHEMERAL 临时节点 ：-e
- PERSISTENT_SEQUENTIAL 持久化顺序节点 ：-s
- EPHEMERAL_SEQUENTIAL 临时顺序节点 ：-es

#### 3.2、服务端常用命令

![image-20231205194601299](https://gitee.com/coi4/test/raw/master/img/image-20231205194601299.png)

启动 ZooKeeper 服务: ./zkServer.sh start

查看 ZooKeeper 服务状态: ./zkServer.sh status

停止 ZooKeeper 服务: ./zkServer.sh stop 

重启 ZooKeeper 服务: ./zkServer.sh restart 

#### 3.3、客户端常用命令

连接ZooKeeper服务端

```
./zkCli.sh –server ip:port
```

断开连接

```
quit
```

查看命令帮助

```
help
```

显示指定目录下节点

```
ls 目录
```

创建节点

```
create /节点path value
```

获取节点值

```
get /节点path
```

设置节点值

```
set /节点path value
```

删除单个节点

```
delete /节点path
```

删除带有子节点的节点

```
deleteall /节点path
```

创建临时节点

```
create -e /节点path value
```

创建顺序节点

```
create -s /节点path value
```

查询节点详细信息

```
ls –s /节点path 
```

> •czxid：节点被创建的事务ID
>
> •ctime: 创建时间 
>
> •mzxid: 最后一次被更新的事务ID 
>
> •mtime: 修改时间 
>
> •pzxid：子节点列表最后一次被更新的事务ID
>
> •cversion：子节点的版本号
>
> •dataversion：数据版本号
>
> •aclversion：权限版本号
>
> •ephemeralOwner：用于临时节点，代表临时节点的事务ID，如果为持久节点则为0
>
> •dataLength：节点存储的数据的长度
>
> •numChildren：当前节点的子节点个数

### 4、JavaAPI操作

Curator：Zookeeper的Java客户端库

常见Zookeeper Java API：

- 原生Java API
- ZkClient
- Curator

Curator项目的目标是简化ZooKeeper客户端的使用

Curator API常用操作

- 建立连接
- 添加节点
- 删除
- 修改
- 查询
- Watch事件监听：
  - 允许用户在指定节点上注册一些Watcher，在一些待定事件触发时，服务端会将时间通知到感兴趣的客户端上，该机制是zk实现分布式协调服务的重要特性；
  - 引入了Watcher机制实现发布/订阅功能，让多个订阅者同时监听某一个对象，当一个对象自身状态变化时，会通知所有订阅者
  - 需要开发者自己反复注册watcher
  - Curator引入了Cache来实现对服务端事件的监听
  - 三种watcher
    - NodeCache : 只是监听某一个特定的节点
    - PathChildrenCache : 监控一个ZNode的子节点. 
    - TreeCache : 可以监控整个树上的所有节点，类似于PathChildrenCache和NodeCache的组合
- 分布式锁实现

分布式锁：分布式集群工作情况，属于多JVM下的工作环境，跨JVM之间无法通过多线程的锁解决同步问题——分布式锁（处理跨机器的进程之间的数据同步问题）![image-20231205200147924](https://gitee.com/coi4/test/raw/master/img/image-20231205200147924.png)

![image-20231205200203480](https://gitee.com/coi4/test/raw/master/img/image-20231205200203480.png)

分布式锁原理：

- 核心思想：客户端要获取锁——创建节点，用完删
- 客户端获取锁，lock节点下创建临时顺序节点；然后获取lock下的所有子节点，客户端获取所有子节点后，发现自己创建的子节点最小，则认为取到了锁，用完删；非最小，需要找到比自己小的那个节点，同时对其注册事件监听器，监听删除事件；如果比自己小的节点被删除，客户端的Watcher会收到通知，再次判断自己创建的节点是否是lock子结点中序号最小的，如果是则取到，不是则重复以上步骤继续获取并注册监听

Curator实现分布式锁API：5种锁方案

- InterProcessSemaphoreMutex：分布式排它锁（非可重入锁）
- InterProcessMutex：分布式可重入排它锁
- InterProcessReadWriteLock：分布式读写锁
- InterProcessMultiLock：将多个锁作为单个实体管理的容器
- InterProcessSemaphoreV2：共享信号量

模拟12306售票系统![image-20231205200847543](https://gitee.com/coi4/test/raw/master/img/image-20231205200847543.png)

### 5、集群搭建

Leader选举：

- Serverid：服务器ID；比如有三台服务器，编号分别是1,2,3。 编号越大在选择算法中的权重越大。

- Zxid：数据ID； 服务器中存放的最大数据ID.值越大说明数据越新，在选举算法中数据越新权重越大。

- 在Leader选举的过程中，如果某台ZooKeeper

    获得了超过半数的选票，则此ZooKeeper就可以成为Leader了。

![image-20231205201046425](https://gitee.com/coi4/test/raw/master/img/image-20231205201046425.png)

### 6、核心理论

集群角色

三个角色：

- eader 领导者 ：     
  - 处理事务请求
  -  集群内部各服务器的调度者
- Follower 跟随者 ：
  - 处理客户端非事务请求，转发事务请求给Leader服务器
  - 参与Leader选举投票
- Observer 观察者：
  -  处理客户端非事务请求，转发事务请求给Leader服务器