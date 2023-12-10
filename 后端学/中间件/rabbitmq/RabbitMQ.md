# RabbitMQ

### 1、MQ基本概念

MQ：Message Queue，消息传输过程中保存消息的容器（中间件）。多用于分布式系统之间进行通信

![image-20231205143126580](https://gitee.com/coi4/test/raw/master/img/image-20231205143126580.png)

分布式系统通信两种方式：

- 直接远程调用
- 借助第三方完成间接通信

MQ优势：

- 应用解耦：提升容错性和可维护性（耦合性越高，容错性越低，可维护性越低）![image-20231205143710068](https://gitee.com/coi4/test/raw/master/img/image-20231205143710068.png)

  ![image-20231205143720427](https://gitee.com/coi4/test/raw/master/img/image-20231205143720427.png)

- 异步提速：提升用户体验和系统吞吐量（单位时间处理请求的数目）![image-20231205143853952](https://gitee.com/coi4/test/raw/master/img/image-20231205143853952.png)

  ![image-20231205143910890](https://gitee.com/coi4/test/raw/master/img/image-20231205143910890.png)

- 削风填谷：提高系统稳定性![image-20231205143959996](https://gitee.com/coi4/test/raw/master/img/image-20231205143959996.png)

  ![image-20231205144048612](https://gitee.com/coi4/test/raw/master/img/image-20231205144048612.png)

MQ劣势：

- 系统可用性降低：系统引入外部依赖越多，系统稳定性越差；一旦宕机，对业务造成影响
- 系统复杂度提高：异步调用（如何保证消息没有被重复消费，怎么处理消息丢失情况，如何保证消息传递的顺序性）
- 一致性问题：A系统处理完业务，通过MQ给B，C，D三个系统发消息数据，BC系统处理成功，D系统失败，如何保证消息数据处理的一致性

常见产品：RabbtMQ、RocketMQ、ActiveMQ、Kafka、ZeroMQ、MetaMQ等，也可以直接使用Redis充当消息队列（RabbitMQ综合能力强）![image-20231205145135893](https://gitee.com/coi4/test/raw/master/img/image-20231205145135893.png)

### 2、RabbitMQ简介

基于AMQP协议使用Erlang语言开发的一款消息队列产品

AMQP（类比HTTP）：Advanced Message Queuing Protocol（高级消息队列协议），网络协议，应用层协议的一个开放标准，为面向消息的中间件设计。

![image-20231205150817882](https://gitee.com/coi4/test/raw/master/img/image-20231205150817882.png)

> Broker：接受和分发消息的应用，RabbitMQ Server就是Message Broker
>
> Virtual host：把AMQP的基本组件划分到一个虚拟分组中，类似于namespace（出于多租户和安全因素设计）；当多个不同的用户使用同一个RabbitMQ Server提供服务时，可以划分出多个vhost，每个用户在自己的vhost创建exchange/queue等
>
> Connection：publisher/consumer和broker之间的TCP连接
>
> Channel：在connection内部建立的逻辑链接（作为轻量级的connection）；应用程序支持多线程，通常每个thread创建单独的channel进行通讯，AMQP method包含了channel id帮助客户端和message broker识别channel，channel之间完全隔离
>
> Exchange：message到达broker的第一站，根据分发规则，匹配查询表中的routing key，分发到queue中去，常用类型有：direct (point-to-point), topic (publish-subscribe) and fanout (multicast)
>
> Queue：消息最终被送到这里等待consumer取走
>
> Binding：exchange和queue之间的虚拟连接，binding中可以包含routing key。Binding信息被保存到exchange中的查询表中，用于message的分发依据

**6种工作模式**：简单模式、work queues、Publish/Subscribe发布与订阅模式、Routing路由模式、Topics 主题模式、RPC 远程调用模式（远程调用，不太算 MQ；暂不作介绍）。

JMS：JavaMessage Service，Java消息服务应用程序接口，是一个Java平台中关于面向消息中间件的API；是JavaEE规范中的一种，类比JDBC，很多消息中间件都实现了JMS规范（API规范接口）

### 3、安装和配置

 RabbitMQ 官方地址：http://www.rabbitmq.com/

安装文档：资料/软件/安装 RabbitMQ.md

### 4、快速入门

使用简单模式完成消息传递

![image-20231205151608781](https://gitee.com/coi4/test/raw/master/img/image-20231205151608781.png)

> P：生产者，发送消息的程序
>
> C：消费者，消息的接收者，会一直等待消息的到来
>
> queue：消息队列（红色部分），相当于邮箱，可以缓存消息；生产者投递，消费者取出

步骤：

- 创建工程（生成者、消费者）
- 分别添加依赖
- 编写生产者发送消息
- 编写消费者接收消息

### 5、工作模式

Work queues工作队列模式：多个消费端共同消费同一个队列中的消息（竞争关系）（对于任务过重或任务较多情况使用可以提高任务处理速度，如短信服务部署多个只需要有一个节点成功发生即可）![image-20231205151855307](https://gitee.com/coi4/test/raw/master/img/image-20231205151855307.png)

- 代码编写：与简单模式几乎一样，多复制一个消费者
- 底层使用默认交换机（和默认交换机绑定）

Pub/Sub订阅模式（发布/订阅）：![image-20231205152248868](https://gitee.com/coi4/test/raw/master/img/image-20231205152248868.png)

- exchange：交换机（X）；一方面接受生产者发送的消息，另一方面知道如何处理消息（要和队列绑定）（只负责转发，不负责存储，如果没有队列与exchange绑定，或者没有符合路由规则的队列，那么消息会丢失），常见以下3种类型
  - Fanout：广播，将消息交给所有绑定到交换机的队列
  - Direct：定向，把消息交给符合指定routing key的队列
  - Topic：通配符，给符合routing pattern（路由模式）的队列

Routing路由模式：与交换机的绑定需要指定一个RoutingKey（路由key）；消息的发送方在向exchange发送消息时，也必须指定消息的RoutingKey；exchange不再把消息交给每一个绑定的队列，而是根据消息的 Routing Key 进行判断，只有队列Routingkey 与消息的 Routing key 完全一致，才会接收到消息![image-20231205153143830](https://gitee.com/coi4/test/raw/master/img/image-20231205153143830.png)

Topics通配符模式：可以实现发布订阅模式和routing路由模式功能；exchange可以让队列在绑定Routing key时使用通配符；routingkey多个单词以.隔开，如 item.insert ![image-20231205153559352](https://gitee.com/coi4/test/raw/master/img/image-20231205153559352.png)

![image-20231205154001148](https://gitee.com/coi4/test/raw/master/img/image-20231205154001148.png)

- 通配符规则：#匹配一个或多个词，*匹配一个词（item.* 只能匹配 item.insert）

### 6、spring整合RabbitMQ

步骤：

- 生产者：

  - 创建生产者工程（springboot）

  - 添加依赖（引入start，依赖坐标）

    ```
    <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
    </dependency>
    ```

  - 配置整合（编写yml配置，基本信息配置）

  - 编写代码发送消息（定义交换机，队列以及绑定关系的配置类；注入RabbitTemplate，调用方法，完成消息发送）

- 消费者：

  - 创建生产者工程
  - 添加依赖
  - 配置整合
  - 编写消息监听器（定义监听类，使用@RabbitListener注解完成队列监听

使用Spring整合RabbitMQ将组建全部配置方式实现，简化编码；spring提供rabbit template简化发送消息API；使用监听机制简化消费者编码

基本信息再yml中配置，队列交互机以及绑定关系在配置类中使用Bean的方式配置；生产端直接注入RabbitTemplate完成消息发送；消费端直接使用@RabbitListener完成消息接收

### 7、高级特性

#### 7.1、消息可靠性投递

rabbitmq消息投递路径：producer--->rabbitmq broker--->exchange--->queue--->consumer

模式：

- confirm确认模式：消息从producer到exchange会返回一个confirmCallback
- return退回模式：消息从exchange到queue投递失败会返回一个returnCallback

设置ConnectionFactory的publisher-confirms=“true”开启确认模式

- 使用rabbitTemplate.setConfirmCallback设置回调函数（发送到exchange后调用confirm方法没方法中判断ack，true则发送成功，false则需要处理）

设置ConnectionFactory的publisher-returns=“true”开启退回模式

- 使用rabbitTemplate.setReturnCallback设置退回函数，失败后，如果设置了rabbitTemplate.setMandatory（true）参数，则会将消息退回给producer。并执行回调函数returnMessage

也提供了事务机制（但性能较差）

- 使用channel下列方法，完成事务控制：
  - txSelect(), 用于将当前channel设置成transaction模式
  - txCommit()，用于提交事务
  - txRollback(),用于回滚事务

#### 7.2、Consumer ACK

Acknowledge，确认；表示消费端收到消息后的确认方式，有三种

- 自动确认：acknowledge=“none”（在rabbit：lisener-container标签中）；确认的同时，将相应的message从RabbitMQ的消息缓存中移除
- 手动确认：acknowledge=“manual”；需要在业务处理成功后，调用channel.basicACK（），如果出现异常，调用channel.basicNack（），让其自动重新发送消息
- 根据异常情况确认：acknowledge=“auto”（麻烦）

消息可靠性总结：

1. 持久化
   - exchange、queue、message要持久化
2. 生产法确认confirm
3. 消费方确认Ack
4. Broker高可用

#### 7.3、消费端限流

在`<rabbit:listener-container>`	配置中prefetch属性设置消费端一次拉取多少消息

消费端的确认模式一定为手动确认

#### 7.4、TTL

Time  To Live（存活时间/过期时间）

当消息到存活时间后，还没有被消费，自动清除

- 使用参数：expiration，（ms），当该消息在队列头部时（消费时），会单独判断是否过期

也可以对整个队列（queue）设置过期时间![image-20231205190730927](https://gitee.com/coi4/test/raw/master/img/image-20231205190730927.png)

- 使用参数：x-message-ttl，单位（ms），会对整个队列消息统一过期

两种都进行了设置，以时间短的为主

#### 7.5、死信队列

DLX，Dead Letter Exchange，当消息成为Dead message后，可以被重新发送到另一个交换机，这个交换机就是DXL![image-20231205191200925](https://gitee.com/coi4/test/raw/master/img/image-20231205191200925.png)

消息成为死信的三种情况：

1. 队列消息长度到达限制
2. 消费者拒绝消费消息，basicNack/basic Reject，并且不把消息重新放入原目标队列，requeue=false
3. 原队列存在消息过期设置并过期

队列绑定死信交换机：

- 给队列设置参数：x-dead-letter-exchange和x-dead-letter-routing-key![image-20231205191554569](https://gitee.com/coi4/test/raw/master/img/image-20231205191554569.png)

#### 7.6、延迟队列

达到指定时间后，才会被消费

需求：下单后，30分钟未支付，取消订单，回滚库存。新用户注册成功7天后，发送短信问候。

实现方式：

1.  定时器
2. 延迟队列

rabbitmq并未提供延迟队列功能，可以使用TTL+死信队列组合![image-20231205191903371](https://gitee.com/coi4/test/raw/master/img/image-20231205191903371.png)

#### 7.7、日志与监控

默认日志存放路径：/var/log/rabbitmq/rabbit@xxx.log

web管控台监控

rabbitmqctl管理和监控

- > 查看队列
  >
  > \# rabbitmqctl list_queues
  >
  > 查看exchanges
  >
  > \# rabbitmqctl list_exchanges
  >
  > 查看用户
  >
  > \# rabbitmqctl list_users
  >
  > 查看连接
  >
  > \# rabbitmqctl list_connections
  >
  > 查看消费者信息
  >
  > \# rabbitmqctl list_consumers
  >
  > 查看环境变量
  >
  > \# rabbitmqctl environment
  >
  > 查看未被确认的队列
  >
  > \# rabbitmqctl list_queues name messages_unacknowledged
  >
  > 查看单个队列的内存使用
  >
  > \# rabbitmqctl list_queues name memory
  >
  > 查看准备就绪的队列
  >
  > \# rabbitmqctl list_queues name messages_ready

#### 7.8、消息可靠性分析与追踪

消息失踪可能是生产者或消费者与rabbitmq断开连接；或者因为交换器与队列之间不同的转发策略；甚至是交换器并没有与任何队列进行绑定，生产者又不感知或者没有采取相应的措施；另外RabbitMQ本身的集群策略也可能导致消息的丢失

RabbitMQ中可以使用Firehose_tracing插件功能实现消息追踪

Firehose：将生产者投递给rabbitmq的消息，rabbitmq投递给消费者的消息按照指定的格式发送到默认的exchange上，这个默认的exchange叫amq.rabbitmq.trace，一个topic类型的exchange，发送到这个exchange的消息的routing key为publish.exchangename 和

deliver.queuename

- 打开trace会影响消息写入功能，适当打开后请关闭
  - rabbitmqctl trace_on：开启Firehose命令
  - rabbitmqctl trace_off：关闭Firehose命令

rabbitmq_tracing比Firehose多了一层GUI包装

- 启用插件：rabbitmq-plugins enable rabbitmq_tracing

#### 7.9、管理

### 8、应用问题

消息可靠性保障：消息补偿机制![image-20231205193317730](https://gitee.com/coi4/test/raw/master/img/image-20231205193317730.png)

消息幂等性处理：乐观锁解决方案![image-20231205193500784](https://gitee.com/coi4/test/raw/master/img/image-20231205193500784.png)

幂等性指一次和多次请求某一个资源，对于资源本身应该具有同样的结果（多次执行对资源本身所产生的影响均与依次执行的影响相同）

需求：100%确保消息发送成功

### 9、集群搭建

9.1、高可用集群