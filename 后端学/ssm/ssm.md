# ssm

## 一、Spring

Spring技术是JavaEE开发必备技能

### 1、相关概念

**Spring**是一款非常优秀而且功能强大的框架；简化开发；框架整合

Spring能做什么:用以开发web、微服务以及分布式系统等（可以完全使用Spring技术完成整个项目的构建、设计与开发）

核心技术：

- **IOC**
- **AOP**
  - **事务处理**

Spring的简化操作都是基于这两块内容；事务处理属于Spring中AOP的具体应用，可以简化项目中的事务管理

核心概念：IOC/DI、IOC容器和Bean

- **IOC****（****Inversion of Control****）控制反转**：使用对象时，由主动new产生对象转换为由**外部**提供对象
  - Spring提供了一个容器，称为**IOC****容器**，用来充当IOC思想中的"外部"
  - 作用：IOC容器负责对象的创建、初始化等一系列工作，其中包含了数据层和业务层的类对象；被创建或被管理的对象在IOC容器中统称为**Bean**；IOC容器中放的就是一个个的Bean对象
-  **DI****（****Dependency Injection****）依赖注入**：在容器中建立bean与bean之间的依赖关系的整个过程，称为依赖注入
  - 根据业务需求提前建立好关系
- Spring的IOC和DI的概念后，我们会发现这两个概念的最终目标就是:**充分解耦**

主要学习四块内容:

1. IOC
2. 整合Mybatis(IOC的具体应用)
3. AOP
4. 声明式事务(AOP的具体应用)

学：Spring框架设计思想；基础操作；案例

官网：https://spring.io（需要重点关注Spring Framework、SpringBoot和SpringCloud )

- Spring Framework:Spring框架，是Spring中最早最核心的技术，也是所有其他技术的

  基础（Spring其实指的是**Spring Framework**)。

- SpringBoot:Spring是来简化开发，而SpringBoot是来帮助Spring在简化的基础上能更快速进行开发

- SpringCloud:这个是用来做分布式之微服务架构的相关开发。

Spring系统架构：![image-20231105103000452](https://gitee.com/coi4/test/raw/master/img/image-20231105103000452.png)

- (1)核心层

  - Core Container:核心容器，这个模块是Spring最核心的模块，其他的都需要依赖该模块

- (2)AOP层

  - AOP:面向切面编程，它依赖核心层容器，目的是**在不改变原有代码的前提下对其进行功能增强**

  - Aspects:AOP是思想,Aspects是对AOP思想的具体实现

- (3)数据层

  - Data Access:数据访问，Spring全家桶中有对数据访问的具体实现技术Data Integration:数据集成，Spring支持整合其他的数据层解决方案，比如Mybatis

  - Transactions:事务，Spring中事务管理是Spring AOP的一个具体实现，也是后期学习的重点内容

- (4)Web层

  - 这一层的内容将在SpringMVC框架具体学习

- (5)Test层

  - Spring主要整合了Junit来完成单元测试和集成测试

### 2、入门案例

Spring到底是如何来实现IOC和DI：先分析思路然后再代码实现

IOC入门案例

思路：

- 管什么：主要管理项目中所使用到的类对象，比如(Service和Dao)
- 怎么将被管理对象告知IOC容器：使用配置文件
- 如何获取IOC容器：接口
- 如何获取bean：调用接口中的方法
- 使用Spring导入哪些坐标：在pom.xml中添加相应的依赖

实现：

- 创建maven项目

- 添加Spring依赖的jar包：

  ```
  <dependencies>
  <dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>5.2.10.RELEASE</version>
  </dependency>
  <dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
  </dependency>
  </dependencies>
  ```

- 添加需要的类

- 添加配置文件：resources下添加spring配置文件applicationContext.xml，并完成bean的配置![image-20231106114939626](https://gitee.com/coi4/test/raw/master/img/image-20231106114939626.png)

- 完成bean的配置：**bean****定义时****id****属性在同一个上下文中****(****配置文件****)****不能重复**

  ```
  beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans.xsd">
  <!--bean标签标示配置bean
  id属性标示给bean起名字
  class属性表示给bean定义类型
  -->
  <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
  <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl"/>
  </beans>
  ```

- 获取IOC容器：使用Spring提供的接口完成IOC容器的创建，创建App类，编写main方法![image-20231106115047080](https://gitee.com/coi4/test/raw/master/img/image-20231106115047080.png)

- **从容器中获取对象进行方法调用**![image-20231106115106439](https://gitee.com/coi4/test/raw/master/img/image-20231106115106439.png)

DI入门案例：

思路：

- DI的入门案例要依赖于前面IOC的入门案例
- Service中使用new形式创建的Dao对象如何保留：删除掉，最终要使用IOC容器中的bean对象
- Dao对象如何进入IOC容器：在Service中提供方法，让Spring的IOC容器可以通过该方法传入bean对象
- Service与Dao间的关系如何描述：使用配置文件

实现：

- 去除代码中的new：在BookServiceImpl类中，删除业务层中使用new的方式创建的dao对象
- 为属性提供setter方法：在BookServiceImpl类中,为BookDao提供setter方法
- 修改配置完成注入：在配置文件中添加依赖注入的配置；**配置中的两个****bookDao****的含义是不一样的**![image-20231106115651522](https://gitee.com/coi4/test/raw/master/img/image-20231106115651522.png)
  - name="bookDao"中bookDao的作用是让Spring的IOC容器在获取到名称后，将首字母大写，前面加set找对应的setBookDao()方法进行对象注入
  - ref="bookDao"中bookDao的作用是让Spring能在IOC容器中找到id为bookDao的Bean对象给bookService进行注入

### 3、IOC相关内容

bean基础配置：

- bean基础配置**(id****与****class)：

  ![image-20231106115935425](https://gitee.com/coi4/test/raw/master/img/image-20231106115935425.png)

  ```
  <bean id="" class=""/>
  ```

- bean的别名配置

-  bean的作用范围配置(重点)

4、DI相关 内容

5、IOC/DI配置管理第三方

6、核心容器

7、IOC/DI注解开发

8、IOC/DI注解开发管理第三方bean

9、Spring整合

 Spring 整合 junit：![image-20231104093404574](https://gitee.com/coi4/test/raw/master/img/image-20231104093404574.png)

 @RunWith 注解指定运行器，使用 @ContextConfiguration 注解来指定配置类或者配置文件

10、AOP简介

11、AOP入门案例

12、AOP工作流程

13、AOP配置管理

14、AOP事务管理

## 二、SpringMVC

### 1、简介

SpringMVC与Servlet技术功能等同，均属于web层或者说表现层开发技术；SpringMVC与Servlet相比，开发起来更简单快捷，用更少的代码完成表现层代码的开发

#### 1.1、概述

WEB程序的工作流程:三层架构

- web程序通过浏览器访问前端页面，发送异步请求到后端服务器

- 后台服务器采用三层架构进行功能开发
  - 表现层负责接收请求和数据然后将数据转交给业务层
  - 业务层负责调用数据层完成数据库表的增删改查，并将结果返给表现层
  - 表现层将数据转换成json格式返回给前端

- 前端页面将数据进行解析最终展示给用户。

表现层与数据层的技术选型:

- 数据层采用Mybatis框架

- 变现层采用SpringMVC框架，SpringMVC**主要**负责的内容有：
  - controller如何接收请求和数据
  - 如何将请求和数据转发给业务层
  - 如何将响应数据转换成json发回到前端

SpringMVC是一种基于Java实现MVC模型的轻量级Web框架

优点：使用简单、开发便捷(相比于Servlet)；灵活性强

### 2、入门案例

Servlet开发过程：

1. 浏览器发送请求到Tomcat服务器
2. Tomcat服务器接收到请求后，会根据请求路径来匹配对应的Servlet,并将请求交给对应的Servlet来处理

SpringMVC的：

1. 浏览器发送请求到Tomcat服务器
2. Tomcat服务器接收到请求后，会将请求交给SpringMVC中的**DispatcherServlet[**前端控制器]来处理请求
3. DispatcherServlet不真正处理请求，只是按照对应的规则将请求分发到对应的Bean对象
4. Bean对象是有我们自己编写来处理不同的请求，每个Bean中可以处理一个或多个不同的请求url
5. DispatcherServlet和Bean对象都需要交给Spring容器来进行管理

编写的内容：

- Bean对象的编写
- 请求url和Bean对象对应关系的配置
- 构建Spring容器，将DispatcherServlet和Bean对象交给容器管理
- 配置Tomcat服务器，使其能够识别Spring容器，并将请求交给容器中的DispatcherServlet来分发请求

实现步骤：

1.创建web工程(Maven结构)并在工程的pom.xml添加SpringMVC和Servlet坐标

- 打开IDEA,创建一个新的web项目![image-20231104103327343](https://gitee.com/coi4/test/raw/master/img/image-20231104103327343.png)
- 使用骨架创建的项目结构不完整，需要手动补全![image-20231104103542276](https://gitee.com/coi4/test/raw/master/img/image-20231104103542276.png)
- 将pom.xml中多余的内容删除掉，再添加SpringMVC需要的依赖![image-20231104103438915](https://gitee.com/coi4/test/raw/master/img/image-20231104103438915.png)

2.*创建SpringMVC控制器类(等同于Servlet功能)![image-20231104103611765](https://gitee.com/coi4/test/raw/master/img/image-20231104103611765.png)

3.初始化SpringMVC环境(同Spring环境)，设定SpringMVC加载对应的bean![image-20231104103619703](https://gitee.com/coi4/test/raw/master/img/image-20231104103619703.png)

4.初始化Servlet容器，加载SpringMVC环境，并设置SpringMVC技术处理的请求![image-20231104103637883](https://gitee.com/coi4/test/raw/master/img/image-20231104103637883.png)

5.配置Tomcat环境![image-20231104103746397](https://gitee.com/coi4/test/raw/master/img/image-20231104103746397.png)

6.启动，浏览器访问：浏览器输入http://localhost/save

启动服务器初始化过程+单次请求过程

- AbstractDispatcherServletInitializer类是SpringMVC提供的快速初始化Web3.0容器的抽象类

- AbstractDispatcherServletInitializer提供三个接口方法供用户实现
  - createRootApplicationContext()方法，如果创建Servlet容器时需要加载非SpringMVC对应的bean，使用当前方法进行，使用方式同createServletApplicationContext()
  - createServletApplicationContext()方法，创建Servlet容器时，加载SpringMVC对应的bean并放入WebApplicationContext对象范围中，而WebApplicationContext的作用范围为ServletContext范围，即整个web容器范围
  - ngetServletMappings()方法，设定SpringMVC对应的请求映射路径，设置为/表示拦截所有请求，任意请求都将转入到SpringMVC进行处理
  - createServletApplicationContext用来加载SpringMVC环境
  - createRootApplicationContext用来加载Spring环境

![image-20231104204417221](https://gitee.com/coi4/test/raw/master/img/image-20231104204417221.png)

config目录存入的是配置类,写过的配置类有:

- ServletContainersInitConfig

- SpringConfig

- SpringMvcConfig

- JdbcConfig

- MybatisConfig

controller目录存放的是SpringMVC的controller类

service目录存放的是service接口和实现类

dao目录存放的是dao/Mapper接口

- SpringMVC加载其相关bean(表现层bean),也就是controller包下的类

- Spring控制的bean
  - 业务bean(Service)
  - 功能bean(DataSource,SqlSessionFactoryBean,MapperScannerConfigurer等)

让Spring和SpringMVC分开加载各自的内容：

- 在SpringMVC的配置类SpringMvcConfig中使用注解@ComponentScan，我们只需要将其扫描范围设置到controller即可![image-20231104204733432](https://gitee.com/coi4/test/raw/master/img/image-20231104204733432.png)
- 在Spring的配置类SpringConfig中使用注解@ComponentScan ,当时扫描的范围中其实是已经包含了controller![image-20231104204744218](https://gitee.com/coi4/test/raw/master/img/image-20231104204744218.png)

- 因为功能不同，如何避免Spring错误加载到SpringMVC的bean：加载Spring控制的bean的时候排除掉SpringMVC控制的备案
  - 方式一:Spring加载的bean设定扫描范围为com.itheima,排除掉controller包中的bean![image-20231104205210920](https://gitee.com/coi4/test/raw/master/img/image-20231104205210920.png)
    - excludeFilters属性：设置扫描加载bean时，排除的过滤规则
    - type属性：设置排除规则，当前使用按照bean定义时的注解类型进行排除
      - ANNOTATION：按照注解排除
    - classes属性：设置排除的具体注解类，当前设置排除@Controller定义的bean
    - 会报bean未被定义的错误：把SpringMVC的配置类移出Spring配置类的扫描范围
  - 方式二:Spring加载的bean设定扫描范围为精准范围，例如service包、dao包等
  - 方式三:不区分Spring与SpringMVC的环境，加载到同一个环境中[了解即可]

想在tomcat服务器启动将Spring配置类加载：修改ServletContainersInitConfig![image-20231104205640672](https://gitee.com/coi4/test/raw/master/img/image-20231104205640672.png)

### 3、PostMan工具的使用

详情看JavaWeb

对于PostMan如何觉得字小不好看，可以使用ctrl+=调大，ctrl+-调小。

### 4、*请求与响应

#### 4.1、设置请求映射路径

团队多人开发，每人设置不同的请求路径---可能产生冲突：为不同模块设置模块名作为请求路径前置

- 对于Book模块的save,将其访问路径设置http://localhost/book/save
- 对于User模块的save,将其访问路径设置http://localhost/user/save

设置映射路径：

- **修改****Controller**：![image-20231104210811213](https://gitee.com/coi4/test/raw/master/img/image-20231104210811213.png)

#### 4.2、请求参数

接收到请求后，如何接收页面传递的参数？

请求方式：

- GET
- POST

参数传递：

- **GET**发送单个参数

  - 发送请求与参数![image-20231104211229455](https://gitee.com/coi4/test/raw/master/img/image-20231104211229455.png)
  - 接收参数![image-20231104211244592](https://gitee.com/coi4/test/raw/master/img/image-20231104211244592.png)

- **GET**发送多个参数![image-20231104211303784](https://gitee.com/coi4/test/raw/master/img/image-20231104211303784.png)

  ![image-20231104211322418](https://gitee.com/coi4/test/raw/master/img/image-20231104211322418.png)

  如果我们传递的参数中有中文，接收到的参数会出现中文乱码问题；需要修改pom.xml来解决GET请求中文乱码问题![image-20231104211426890](https://gitee.com/coi4/test/raw/master/img/image-20231104211426890.png)

- **POST**发送参数![image-20231104211445775](https://gitee.com/coi4/test/raw/master/img/image-20231104211445775.png)

- POST接收参数与GET一样；中文乱码![image-20231104211545368](https://gitee.com/coi4/test/raw/master/img/image-20231104211545368.png)

  CharacterEncodingFilter是在spring-web包中，所以用之前需要导入对应的jar包。

#### 4.3、五种类型参数传递

普通参数

POJO数据类型

嵌套POJO类型参数

数组类型参数

集合类型

详情看JavaWeb

#### 4.4、JSON数据传输参数

现在比较流行的开发方式为异步调用。前后台以异步方式进行交换，传输的数据使用的是**JSON**,所以前端如果发送的是JSON数据，后端该如何接收?

JSON数据类型

- 普通数组
  - **pom.xml**添加依赖：SpringMVC默认使用的是jackson来处理json的转换，所以需要在pom.xml添加jackson依赖![image-20231105075156778](https://gitee.com/coi4/test/raw/master/img/image-20231105075156778.png)
  - **PostMan**发送JSON数据：![image-20231105075334840](https://gitee.com/coi4/test/raw/master/img/image-20231105075334840.png)
  - **开启****SpringMVC****注解支持**![image-20231105075359226](https://gitee.com/coi4/test/raw/master/img/image-20231105075359226.png)
  - **参数前添加****@RequestBody**![image-20231105075423299](https://gitee.com/coi4/test/raw/master/img/image-20231105075423299.png)

- 对象数据

  - 请求和数据的发送![image-20231105075600834](https://gitee.com/coi4/test/raw/master/img/image-20231105075600834.png)

    ![image-20231105075729344](https://gitee.com/coi4/test/raw/master/img/image-20231105075729344.png)

  - 后端接受![image-20231105075742992](https://gitee.com/coi4/test/raw/master/img/image-20231105075742992.png)

- 对象数组

  - ![image-20231105075816027](https://gitee.com/coi4/test/raw/master/img/image-20231105075816027.png)

    ![image-20231105075828489](https://gitee.com/coi4/test/raw/master/img/image-20231105075828489.png)

  - ![image-20231105075842006](https://gitee.com/coi4/test/raw/master/img/image-20231105075842006.png)

**@RequestBody****与****@RequestParam****区别**

- 区别：
  - @RequestParam用于接收url地址传参，表单传参【application/x-www-form-urlencoded】
  - @RequestBody用于接收json数据【application/json】

- 应用
  - 后期开发中，发送json格式数据为主，@RequestBody应用较广
  - 如果发送非json格式数据，选用@RequestParam接收请求参数

#### 4.5、日期类型

**编写方法接收日期数据**：![image-20231105080336637](https://gitee.com/coi4/test/raw/master/img/image-20231105080336637.png)

**启动****Tomcat****服务器**

******使用****PostMan****发送请求**![image-20231105080426766](https://gitee.com/coi4/test/raw/master/img/image-20231105080426766.png)

**更换日期格式**：SpringMVC默认支持的字符串转日期的格式为yyyy/MM/dd：使用@DateTimeFormat![image-20231105080618882](https://gitee.com/coi4/test/raw/master/img/image-20231105080618882.png)

**携带时间的日期**：![image-20231105080731576](https://gitee.com/coi4/test/raw/master/img/image-20231105080731576.png)![image-20231105080749070](https://gitee.com/coi4/test/raw/master/img/image-20231105080749070.png)

#### 4.6、响应

响应页面

响应数据：

- 文本数据

- json数据

  - POJO对象：![image-20231105081107959](https://gitee.com/coi4/test/raw/master/img/image-20231105081107959.png)

    需要依赖

    **@ResponseBody**注解和**@EnableWebMvc**注解

    ![image-20231105081212585](https://gitee.com/coi4/test/raw/master/img/image-20231105081212585.png)

  - **响应****POJO****集合对象**![image-20231105081238535](https://gitee.com/coi4/test/raw/master/img/image-20231105081238535.png)

    ![image-20231105081258364](https://gitee.com/coi4/test/raw/master/img/image-20231105081258364.png)

### 5、*Rest风格

一种软件架构风格，可以降低开发的复杂性，提高系统的可伸缩性，在以后开发中非常重要和常用

#### 5.1、简介

- 传统风格资源描述形式
  - http://localhost/user/getById?id=1 查询id为1的用户信息
  - http://localhost/user/saveUser 保存用户信息

- REST风格描述形式
  - http://localhost/user/1
  - http://localhost/user

优点：隐藏资源的访问行为，无法通过地址得知对资源是何种操作；书写简化

按照REST风格访问资源时使用**行为动作**区分对资源进行了何种操作

请求方式：GET , POST , PUT , DELETE

按照不同的请求方式代表不同的操作类型（可以变）：

- 发送GET请求是用来做查询

- 发送POST请求是用来做新增
- 发送PUT请求是用来做修改

- 发送DELETE请求是用来做删除

描述模块的名称通常使用复数，也就是加s的格式描述，表示此类资源，而非单个资源，例如:users、books、accounts......

根据REST风格对资源进行访问称为**RESTful**

后期开发都是基于RESTful来进行开发的。

#### 5.2、入门案例

环境准备

思路分析

> 需求:将之前的增删改查替换成RESTful的开发方式。
>
> 1.之前不同的请求有不同的路径,现在要将其修改为统一的请求路径
>
> 修改前: 新增: /save ,修改: /update,删除 /delete...
>
> 修改后: 增删改查: /users
>
> 2.根据GET查询、POST新增、PUT修改、DELETE删除对方法的请求方式进行限定
>
> 3.发送请求的过程中如何设置请求参数?

修改RESTful风格：

新增![image-20231105082303356](https://gitee.com/coi4/test/raw/master/img/image-20231105082303356.png)

删除![image-20231105082421629](https://gitee.com/coi4/test/raw/master/img/image-20231105082421629.png)

- 方法形参的名称和路径{}中的值不一致![image-20231105082539563](https://gitee.com/coi4/test/raw/master/img/image-20231105082539563.png)
- 有多个参数需要传递![image-20231105082553203](https://gitee.com/coi4/test/raw/master/img/image-20231105082553203.png)

修改![image-20231105082635553](https://gitee.com/coi4/test/raw/master/img/image-20231105082635553.png)

![image-20231105082654650](https://gitee.com/coi4/test/raw/master/img/image-20231105082654650.png)

**根据****ID****查询**![image-20231105082713285](https://gitee.com/coi4/test/raw/master/img/image-20231105082713285.png)

**查询所有**![image-20231105082730768](https://gitee.com/coi4/test/raw/master/img/image-20231105082730768.png)

@RequestBody、@RequestParam、@PathVariable ,这三个注解之间的区别和应用分别是什么?

- 区别：
  - @RequestParam用于接收url地址传参或表单传参
  - @RequestBody用于接收json数据
  - @PathVariable用于接收路径参数，使用{参数名称}描述路径参数

- 应用
  - 后期开发中，发送请求参数超过1个时，以json格式为主，@RequestBody应用较广
  - 如果发送非json格式数据，选用@RequestParam接收请求参数
  - 采用RESTful进行开发，当参数数量较少时，例如1个，可以采用@PathVariable接收请求路径变量，通常用于传递id值

#### 5.3、快速开发

每个方法的@RequestMapping注解中都定义了访问路径/books，重复性太高

- 将@RequestMapping提到类上面，用来定义所有方法共同的访问路径。

 每个方法的@RequestMapping注解中都要使用method属性定义请求方式，重复性太高。

- 使用@GetMapping @PostMapping @PutMapping @DeleteMapping代替

每个方法响应json都需要加上@ResponseBody注解，重复性太高

- 将ResponseBody提到类上面，让所有的方法都有@ResponseBody的功能
- 使用@RestController注解替换@Controller与@ResponseBody注解，简化书写

#### 5.4、案例

基于RESTful页面数据交互

##### 5.4.1、需求分析

> 需求一:图片列表查询，从后台返回数据，将数据展示在页面上
>
> 需求二:新增图片，将新增图书的数据传递到后台，并在控制台打印

步骤分析:

> 1.搭建项目导入jar包
>
> 2.编写Controller类，提供两个方法，一个用来做列表查询，一个用来做新增
>
> 3.在方法上使用RESTful进行路径设置
>
> 4.完成请求、参数的接收和结果的响应
>
> 5.使用PostMan进行测试6.将前端页面拷贝到项目中
>
> 7.页面发送ajax请求
>
> 8.完成页面数据的展示

环境准备

##### 5.4.2、后台接口开发

- **编写****Controller****类并使用****RESTful****进行配置**![image-20231105083425946](https://gitee.com/coi4/test/raw/master/img/image-20231105083425946.png)
- **使用****PostMan****进行测试**
  - 测试新增![image-20231105083505756](https://gitee.com/coi4/test/raw/master/img/image-20231105083505756.png)
  - 测试查询![image-20231105083616064](https://gitee.com/coi4/test/raw/master/img/image-20231105083616064.png)

##### 5.4.3、页面访问处理

- **拷贝静态页面**：将资料\功能页面下的所有内容拷贝到项目的webapp目录下
- **访问****pages目录下的books.html**：SpringMVC拦截了静态资源，报错
  - 将静态资源进行放行：![image-20231105083824206](https://gitee.com/coi4/test/raw/master/img/image-20231105083824206.png)
  - 该配置类是在config目录下，SpringMVC扫描的是controller包，所以该配置类还未生效，要想生效需要将SpringMvcConfig配置类进行修改![image-20231105083949431](https://gitee.com/coi4/test/raw/master/img/image-20231105083949431.png)

- **修改****books.html****页面**

### 6、*SSM整合

SpringMVC+Spring+Mybatis整合在一起来完成业务开发

#### 6.1、流程分析

(1) 创建工程

- 创建一个Maven的web工程

- pom.xml添加SSM需要的依赖jar包

- 编写Web项目的入口配置类，实现AbstractAnnotationConfigDispatcherServletInitializer重写以下方法
  - getRootConfigClasses() ：返回Spring的配置类->需要**SpringConfig**配置类
  - getServletConfigClasses() ：返回SpringMVC的配置类->需要**SpringMvcConfig**配置类
  - getServletMappings() : 设置SpringMVC请求拦截路径规则
  - getServletFilters() ：设置过滤器，解决POST请求中文乱码问题

(2)SSM整合[**重点是各个配置的编写**]

- SpringConfig
  - 标识该类为配置类 @Configuration
  - 扫描Service所在的包 @ComponentScan
  - 在Service层要管理事务 @EnableTransactionManagement
  - 读取外部的properties配置文件 @PropertySource
  - 整合Mybatis需要引入Mybatis相关配置类 @Import
    - 第三方数据源配置类 JdbcConfig
      - 构建DataSource数据源，DruidDataSouroce,需要注入数据库连接四要素， @Bean@Value
      - 构建平台事务管理器，DataSourceTransactionManag，@Bean
      - Mybatis配置类 MybatisConfig
        - 构建SqlSessionFactoryBean并设置别名扫描与数据源，@Bean
        - 构建MapperScannerConfigurer并设置DAO层的包扫描
      - - 构建MapperScannerConfigurer并设置DAO层的包扫描

- SpringMvcConfig
  - 标识该类为配置类 @Configuration
  - 扫描Controller所在的包 @ComponentScan
  - 开启SpringMVC注解支持 @EnableWebMvc

(3)功能模块[与具体的业务模块有关]

- 创建数据库表
- 根据数据库表创建对应的模型类
- 通过Dao层完成数据库表的增删改查(接口+自动代理)
- 编写Service层[Service接口+实现类]
  - @Service
  - @Transactional
  - 整合Junit对业务层进行单元测试
    - @RunWith
    - @ContextConfiguration
    - @Test

- 编写Controller层
  - 接收请求 @RequestMapping @GetMapping @PostMapping @PutMapping@DeleteMapping
  - 接收数据 简单、POJO、嵌套POJO、集合、数组、JSON数据类型
    - @RequestParam
    - @PathVariable
    - @RequestBody
  - 转发业务层
    - @Autowired
  - 响应结果
    - @ResponseBody

#### 6.2、整合配置

依赖：

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>com.itheima</groupId>
<artifactId>springmvc_08_ssm</artifactId>
<version>1.0-SNAPSHOT</version>
 <packaging>war</packaging>

 <dependencies>
 <dependency>
 <groupId>org.springframework</groupId>
 <artifactId>spring-webmvc</artifactId>
 <version>5.2.10.RELEASE</version>
 </dependency>

 <dependency>
 <groupId>org.springframework</groupId>
 <artifactId>spring-jdbc</artifactId>
 <version>5.2.10.RELEASE</version>
 </dependency>

 <dependency>
 <groupId>org.springframework</groupId>
 <artifactId>spring-test</artifactId>
 <version>5.2.10.RELEASE</version>
 </dependency>

 <dependency>
 <groupId>org.mybatis</groupId>
 <artifactId>mybatis</artifactId>
 <version>3.5.6</version>
 </dependency>

 <dependency>
 <groupId>org.mybatis</groupId>
 <artifactId>mybatis-spring</artifactId>
 <version>1.3.0</version>
 </dependency>

 <dependency>
 <groupId>mysql</groupId>
 <artifactId>mysql-connector-java</artifactId>
 <version>5.1.47</version>
 </dependency>

 <dependency>
 <groupId>com.alibaba</groupId>
 <artifactId>druid</artifactId>
 <version>1.1.16</version>
 </dependency>

 <dependency>
步骤3:创建项目包结构
<groupId>junit</groupId>
<artifactId>junit</artifactId>
<version>4.12</version>
<scope>test</scope>
</dependency>
<dependency>
<groupId>javax.servlet</groupId>
<artifactId>javax.servlet-api</artifactId>
<version>3.1.0</version>
<scope>provided</scope>
</dependency>
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-databind</artifactId>
<version>2.9.0</version>
</dependency>
</dependencies>
<build>
<plugins>
<plugin>
<groupId>org.apache.tomcat.maven</groupId>
<artifactId>tomcat7-maven-plugin</artifactId>
<version>2.1</version>
<configuration>
<port>80</port>
<path>/</path>
</configuration>
</plugin>
</plugins>
</build>
</project>
```

![image-20231105091440884](https://gitee.com/coi4/test/raw/master/img/image-20231105091440884.png)

config目录存放的是相关的配置类

controller编写的是Controller类

dao存放的是Dao接口，因为使用的是Mapper接口代理方式，所以没有实现类包

service存的是Service接口，impl存放的是Service实现类

resources:存入的是配置文件，如Jdbc.properties

webapp:目录可以存放静态资源

test/java:存放的是测试类

- **创建****SpringConfig****配置类**![image-20231105091516074](https://gitee.com/coi4/test/raw/master/img/image-20231105091516074.png)
- **创建****JdbcConfig****配置类**![image-20231105091548651](https://gitee.com/coi4/test/raw/master/img/image-20231105091548651.png)
- **创建****MybatisConfig****配置类**![image-20231105091605865](https://gitee.com/coi4/test/raw/master/img/image-20231105091605865.png)
- **创建****jdbc.properties**![image-20231105091626816](https://gitee.com/coi4/test/raw/master/img/image-20231105091626816.png)
- **创建****SpringMVC****配置类**![image-20231105091645996](https://gitee.com/coi4/test/raw/master/img/image-20231105091645996.png)
- **创建****Web****项目入口配置类**![image-20231105091705724](https://gitee.com/coi4/test/raw/master/img/image-20231105091705724.png)

#Spring步骤：

- **创建工程，并在** pom.xml **配置文件中配置所依赖的坐标**![image-20231104020439007](https://gitee.com/coi4/test/raw/master/img/image-20231104020439007.png)
- **编写** web3.0 **的配置类**![image-20231104020452016](https://gitee.com/coi4/test/raw/master/img/image-20231104020452016.png)
-  **编写** SpringMVC **的配置类**![image-20231104020504344](https://gitee.com/coi4/test/raw/master/img/image-20231104020504344.png)
-  **编写** Controller **类**![image-20231104020518716](https://gitee.com/coi4/test/raw/master/img/image-20231104020518716.png)

#### 6.3、功能模块开发

新增、修改、删除、根据ID查询和查询所有

- **创建数据库及表**

  ```
  create database ssm_db character set utf8;
  use ssm_db;
  create table tbl_book(
  id int primary key auto_increment,
  type varchar(20),
  name varchar(50),
  description varchar(255)
  )
  insert into `tbl_book`(`id`,`type`,`name`,`description`) values (1,'计算机理
  论','Spring实战 第五版','Spring入门经典教程，深入理解Spring原理技术内幕'),(2,'计算机理
  论','Spring 5核心原理与30个类手写实践','十年沉淀之作，手写Spring精华思想'),(3,'计算机理
  论','Spring 5设计模式','深入Spring源码刨析Spring源码中蕴含的10大设计模式'),(4,'计算机
  理论','Spring MVC+Mybatis开发从入门到项目实战','全方位解析面向Web应用的轻量级框架，带你
  成为Spring MVC开发高手'),(5,'计算机理论','轻量级Java Web企业应用实战','源码级刨析
  Spring框架，适合已掌握Java基础的读者'),(6,'计算机理论','Java核心技术 卷Ⅰ 基础知识(原书
  第11版)','Core Java第11版，Jolt大奖获奖作品，针对Java SE9、10、11全面更新'),(7,'计算
  机理论','深入理解Java虚拟机','5个纬度全面刨析JVM,大厂面试知识点全覆盖'),(8,'计算机理
  论','Java编程思想(第4版)','Java学习必读经典，殿堂级著作！赢得了全球程序员的广泛赞誉'),
  (9,'计算机理论','零基础学Java(全彩版)','零基础自学编程的入门图书，由浅入深，详解Java语言
  的编程思想和核心技术'),(10,'市场营销','直播就这么做:主播高效沟通实战指南','李子柒、李佳
  奇、薇娅成长为网红的秘密都在书中'),(11,'市场营销','直播销讲实战一本通','和秋叶一起学系列网
  络营销书籍'),(12,'市场营销','直播带货:淘宝、天猫直播从新手到高手','一本教你如何玩转直播的
  书，10堂课轻松实现带货月入3W+')
  ```

- **编写模型类**![image-20231105091827201](https://gitee.com/coi4/test/raw/master/img/image-20231105091827201.png)

- **编写****Dao****接口**![image-20231105091846627](https://gitee.com/coi4/test/raw/master/img/image-20231105091846627.png)

- **编写****Service****接口和实现类**![image-20231105091920339](https://gitee.com/coi4/test/raw/master/img/image-20231105091920339.png)

  ![image-20231105091935038](https://gitee.com/coi4/test/raw/master/img/image-20231105091935038.png)
  - bookDao在Service中注入的会提示一个红线提示
    - 可以不用理会，因为运行是正常的
    - 设置错误提示级别![image-20231105092052210](https://gitee.com/coi4/test/raw/master/img/image-20231105092052210.png)

- **编写****Contorller****类**![image-20231105092149711](https://gitee.com/coi4/test/raw/master/img/image-20231105092149711.png)

#### 6.4、单元测试

- **新建测试类**

  ```
  @RunWith(SpringJUnit4ClassRunner.class)
  @ContextConfiguration(classes = SpringConfig.class)
  public class BookServiceTest {
  }
  ```

- **注入****Service****类**

  ```
  @RunWith(SpringJUnit4ClassRunner.class)
  @ContextConfiguration(classes = SpringConfig.class)
  public class BookServiceTest {
  @Autowired
  private BookService bookService;
  }
  ```

- **编写测试方法**![image-20231105092338608](https://gitee.com/coi4/test/raw/master/img/image-20231105092338608.png)

#### 6.5、PostMan测试

新增![image-20231105092447669](https://gitee.com/coi4/test/raw/master/img/image-20231105092447669.png)

**修改**![image-20231105092515862](https://gitee.com/coi4/test/raw/master/img/image-20231105092515862.png)

**删除**![image-20231105092538062](https://gitee.com/coi4/test/raw/master/img/image-20231105092538062.png)

**查询单个**![image-20231105092607498](https://gitee.com/coi4/test/raw/master/img/image-20231105092607498.png)

**查询所有**![image-20231105092631211](https://gitee.com/coi4/test/raw/master/img/image-20231105092631211.png)

### 7、统一结果封装

#### 7.1、**表现层与前端数据传输协议定义**

随着业务的增长，我们需要返回的数据类型会越来越多。对于前端开发人员在解析数据的时候就比较凌乱了，所以对于前端来说，如果后台能够返回一个统一的数据结果，前端在解析的时候就可以按照一种方式进行解析。开发就会变得更加简单。

将返回结果的数据进行统一：

- 为了封装返回的结果数据:**创建结果模型类，封装数据到****data属性中
- 为了封装返回的数据是何种操作及是否操作成功:**封装操作结果到code属性中**
- 操作失败后为了封装返回的错误信息:**封装特殊消息到message(msg)属性中****

设置统一数据返回结果类：![image-20231105092916009](https://gitee.com/coi4/test/raw/master/img/image-20231105092916009.png)

#### 7.2、**表现层与前端数据传输协议实现**

环境准备

结果封装：对于结果封装，我们应该是在表现层进行处理，所以我们把结果类放在controller包下，当然你也可以放在domain包

- **创建****Result****类**![image-20231105093112336](https://gitee.com/coi4/test/raw/master/img/image-20231105093112336.png)
- **定义返回码****Code类**：code类中的常量设计也不是固定的，可以根据需要自行增减，例如将查询再进行细分为GET_OK,GET_ALL_OK,GET_PAGE_OK等![image-20231105093124952](https://gitee.com/coi4/test/raw/master/img/image-20231105093124952.png)

- **修改****Controller****类的返回值**![image-20231105093256230](https://gitee.com/coi4/test/raw/master/img/image-20231105093256230.png)

  ![image-20231105093313548](https://gitee.com/coi4/test/raw/master/img/image-20231105093313548.png)

- **启动服务测试**

### 8、统一异常处理

#### 8.1、问题描述

框架内部抛出的异常：因使用不合规导致

数据层抛出的异常：因外部服务器故障导致（例如：服务器访问超时）

业务层抛出的异常：因业务逻辑书写错误导致（例如：遍历业务书写操作，导致索引异常等）

表现层抛出的异常：因数据收集、校验等规则导致（例如：不匹配的数据类型间导致异常）

工具类抛出的异常：因工具类书写不严谨不够健壮导致（例如：必要释放的连接长期未释放等）

**所有的异常均抛出到表现层进行处理**

- 表现层如何将所有的异常都处理到：**异常分类**
-  表现层处理异常，每个方法中单独书写，代码书写量巨大且意义不强，如何解决：**AOP**

SpringMVC用异常处理器

#### 8.2、异常处理器的使用

异常处理器:

- 集中的、统一的处理项目中出现的异常。

步骤：

- **创建异常处理器类**：**确保****SpringMvcConfig****能够扫描到异常处理器类**![image-20231105093802673](https://gitee.com/coi4/test/raw/master/img/image-20231105093802673.png)
- **让程序抛出异常**：自己创建（添加int i = 1/0 ）
- **运行程序，测试**：异常已经被拦截并执行了doException方法。
- **异常处理器类返回结果给前端**![image-20231105094025900](https://gitee.com/coi4/test/raw/master/img/image-20231105094025900.png)
- postman测试：能按照我们和前端约定好的格式返回给前端。

#**@RestControllerAdvice**自带@ResponseBody注解与@Component注解，具备对应的功能

#### 8.3、项目异常处理方案

在项目中该如何来处理异常

**异常分类**：

- 业务异常（BusinessException）
  - 规范的用户行为产生的异常
    - 用户在页面输入内容的时候未按照指定格式进行数据填写，如在年龄框输入的是字符串
  - 不规范的用户行为操作产生的异常
    - 如用户故意传递错误数据

- 系统异常（SystemException）
  - 项目运行过程中可预计但无法避免的异常
    - 比如数据库或服务器宕机
- 其他异常（Exception）
  - 编程人员未预期到的异常，如:用到的文件不存在

 **异常解决方案**：

- 业务异常（BusinessException）

  - 发送对应消息传递给用户，提醒规范操作
    - 大家常见的就是提示用户名已存在或密码格式不正确等

- 系统异常（SystemException）

  - 发送固定消息传递给用户，安抚用户
    - 系统繁忙，请稍后再试
    - 系统正在维护升级，请稍后再试
    - 系统出问题，请联系系统管理员等

  - 发送特定消息给运维人员，提醒维护
    - 可以发送短信、邮箱或者是公司内部通信软件

  - 记录日志
    - 发消息和记录日志对用户来说是不可见的，属于后台程序

- 其他异常（Exception）

  - 发送固定消息传递给用户，安抚用户

  - 发送特定消息给编程人员，提醒维护（纳入预期范围内）
    - 一般是程序没有考虑全，比如未做非空校验等

  - 记录日志

具体实现：

- **自定义异常类**![image-20231105094648898](https://gitee.com/coi4/test/raw/master/img/image-20231105094648898.png)

  ![image-20231105094700957](https://gitee.com/coi4/test/raw/master/img/image-20231105094700957.png)

  - 让自定义异常类继承RuntimeException的好处是，后期在抛出这两个异常的时候，就不用在try...catch...或throws了

  - 自定义异常类中添加code属性的原因是为了更好的区分异常是来自哪个业务的

- **将其他异常包成自定义异常**：假如在BookServiceImpl的getById方法抛异常了![image-20231105094804176](https://gitee.com/coi4/test/raw/master/img/image-20231105094804176.png)

  - 具体的包装方式有：

    方式一: try{}catch(){}在catch中重新throw我们自定义异常即可。

    方式二:直接throw自定义异常即可

  - 在Code类中再新增需要的属性![image-20231105094906849](https://gitee.com/coi4/test/raw/master/img/image-20231105094906849.png)

- **处理器类中处理自定义异常**![image-20231105094931980](https://gitee.com/coi4/test/raw/master/img/image-20231105094931980.png)
- **运行程序**
  - 根据ID查询，如果传入的参数为1，会报BusinessException
  - 如果传入的是其他参数，会报SystemException

以后项目中的异常处理方式为:![image-20231105095104809](https://gitee.com/coi4/test/raw/master/img/image-20231105095104809.png)

### 9、前后台协议联调

环境准备：

- 创建一个Web的Maven项目
- pom.xml添加SSM整合所需jar包
- 创建对应的配置类
- 编写Controller、Service接口、Service实现类、Dao接口和模型类
- resources下提供jdbc.properties配置文件
-  将资料\SSM功能页面下面的静态资源拷贝到webapp下
- 因为添加了静态资源，SpringMVC会拦截，所有需要在SpringConfig的配置类中将静态资源进行放行。

将所有的列表查询、新增、修改、删除等功能一个个来实现

**列表功能**：

> 需求:页面加载完后发送异步请求到后台获取列表数据进行展示。
>
> 1.找到页面的钩子函数，created()
>
> \2. created()方法中调用了this.getAll()方法
>
> 3.在getAll()方法中使用axios发送异步请求从后台获取数据
>
> 4.访问的路径为http://localhost/books
>
> 5.返回数据

返回数据res.data的内容如下:![image-20231105095758847](https://gitee.com/coi4/test/raw/master/img/image-20231105095758847.png)

发送方式:![image-20231105095645622](https://gitee.com/coi4/test/raw/master/img/image-20231105095645622.png)

 **添加功能**：

> 需求:完成图片的新增功能模块
>
> 1.找到页面上的新建按钮，按钮上绑定了@click="handleCreate()"方法
>
> 2.在method中找到handleCreate方法，方法中打开新增面板
>
> 3.新增面板中找到确定按钮,按钮上绑定了@click="handleAdd()"方法
>
> 4.在method中找到handleAdd方法
>
> 5.在方法中发送请求和数据，响应成功后将新增面板关闭并重新查询数据

handleCreate打开新增面板：![image-20231105095909377](https://gitee.com/coi4/test/raw/master/img/image-20231105095909377.png)

handleAdd方法发送异步请求并携带数据：![image-20231105095933682](https://gitee.com/coi4/test/raw/master/img/image-20231105095933682.png)

**添加功能状态处理**：

> 需求:新增成功是关闭面板，重新查询数据，那么新增失败以后该如何处理?、
>
> 1.在handlerAdd方法中根据后台返回的数据来进行不同的处理
>
> 2.如果后台返回的是成功，则提示成功信息，并关闭面板
>
> 3.如果后台返回的是失败，则提示错误信息

(1)修改前端页面![image-20231105100039468](https://gitee.com/coi4/test/raw/master/img/image-20231105100039468.png)

(2)后台返回操作结果，将Dao层的增删改方法返回值从void改成int

![image-20231105100104715](https://gitee.com/coi4/test/raw/master/img/image-20231105100104715.png)

(3)在BookServiceImpl中，增删改方法根据DAO的返回值来决定返回true/false![image-20231105100207172](https://gitee.com/coi4/test/raw/master/img/image-20231105100207172.png)

(4)测试错误情况，将图书类别长度设置超出范围即可![image-20231105100234017](https://gitee.com/coi4/test/raw/master/img/image-20231105100234017.png)

新增成功后，再次点击新增按钮会发现之前的数据还存在，这个时候就需要在新增的时候将表单内容清空。![image-20231105100253975](https://gitee.com/coi4/test/raw/master/img/image-20231105100253975.png)

 **修改功能**：

> 需求:完成图书信息的修改功能
>
> 1.找到页面中的编辑按钮，该按钮绑定了@click="handleUpdate(scope.row)"
>
> 2.在method的handleUpdate方法中发送异步请求根据ID查询图书信息
>
> 3.根据后台返回的结果，判断是否查询成功
>
> 如果查询成功打开修改面板回显数据，如果失败提示错误信息
>
> 4.修改完成后找到修改面板的确定按钮，该按钮绑定了@click="handleEdit()"
>
> 5.在method的handleEdit方法中发送异步请求提交修改数据
>
> 6.根据后台返回的结果，判断是否修改成功
>
> 如果成功提示错误信息，关闭修改面板，重新查询数据，如果失败提示错误信息

scope.row代表的是当前行的行数据，也就是说,scope.row就是选中行对应的json数据，如下![image-20231105100430440](https://gitee.com/coi4/test/raw/master/img/image-20231105100430440.png)

修改handleUpdate方法![image-20231105100450467](https://gitee.com/coi4/test/raw/master/img/image-20231105100450467.png)

修改handleEdit方法![image-20231105100513774](https://gitee.com/coi4/test/raw/master/img/image-20231105100513774.png)

 **删除功能**：

> 需求:完成页面的删除功能。
>
> 1.找到页面的删除按钮，按钮上绑定了@click="handleDelete(scope.row)"
>
> 2.method的handleDelete方法弹出提示框
>
> 3.用户点击取消,提示操作已经被取消。
>
> 4.用户点击确定，发送异步请求并携带需要删除数据的主键ID
>
> 5.根据后台返回结果做不同的操作
>
> 如果返回成功，提示成功信息，并重新查询数据
>
> 如果返回失败，提示错误信息，并重新查询数据

修改handleDelete方法![image-20231105100556504](https://gitee.com/coi4/test/raw/master/img/image-20231105100556504.png)

### 10、拦截器

#### 10.1、概念

拦截器（Interceptor）是一种动态拦截方法调用的机制，在SpringMVC中动态拦截控制器方法的执行

作用:

- 在指定的方法调用前后执行预先设定的代码

- 阻止原始方法的执行

- 总结：拦截器就是用来做增强

拦截器和过滤器之间的区别：

- 归属不同：Filter属于Servlet技术，Interceptor属于SpringMVC技术
- 拦截内容不同：Filter对所有访问进行增强，Interceptor仅针对SpringMVC的访问进行增强

#### 10.2、入门案例

- **创建拦截器类**：让类实现HandlerInterceptor接口，重写接口中的三个方法。![image-20231105100916662](https://gitee.com/coi4/test/raw/master/img/image-20231105100916662.png)

- **配置拦截器类**![image-20231105101115445](https://gitee.com/coi4/test/raw/master/img/image-20231105101115445.png)

  拦截器中的preHandler方法，如果返回true,则代表放行，会执行原始Controller类中要请求的方法，如果返回false，则代表拦截，后面的就不会再执行了。

- **SpringMVC****添加****SpringMvcSupport****包扫描**![image-20231105101014606](https://gitee.com/coi4/test/raw/master/img/image-20231105101014606.png)
- **运行程序测试**
- **简化****SpringMvcSupport****的编写**：不用再写SpringMvcSupport类![image-20231105101222447](https://gitee.com/coi4/test/raw/master/img/image-20231105101222447.png)

#### 10.3、拦截器参数

-  **前置处理方法**：

  - 原始方法之前运行preHandle![image-20231105101352803](https://gitee.com/coi4/test/raw/master/img/image-20231105101352803.png)

    - request:请求对象

      response:响应对象

      handler:被调用的处理器对象，本质上是一个方法对象，对反射中的Method对象进行了再包装

  - 使用request对象可以获取请求数据中的内容，如获取请求头的Content-Type![image-20231105101459924](https://gitee.com/coi4/test/raw/master/img/image-20231105101459924.png)

  - 使用handler参数，可以获取方法的相关信息![image-20231105101510014](https://gitee.com/coi4/test/raw/master/img/image-20231105101510014.png)

- **后置处理方法**：
  - 原始方法运行后运行，如果原始方法被拦截，则不执行![image-20231105101558964](https://gitee.com/coi4/test/raw/master/img/image-20231105101558964.png)
    - modelAndView:如果处理器执行完成具有返回结果，可以读取到对应数据与页面信息，并进行调整
    - 因为现在都是返回json数据，所以该参数的使用率不高。

-  **完成处理方法**：拦截器最后执行的方法，无论原始方法是否执行![image-20231105101640721](https://gitee.com/coi4/test/raw/master/img/image-20231105101640721.png)

  - ex:如果处理器执行过程中出现异常对象，可以针对异常情况进行单独处理

    因为现在已经有全局异常处理器类，所以该参数的使用率也不高。

最常用的是**preHandle**

#### 10.4、拦截器链配置

多个拦截器如何配置，执行顺序？

- **配置多个拦截器**

  - **创建拦截器类**![image-20231105101847916](https://gitee.com/coi4/test/raw/master/img/image-20231105101847916.png)

  - **配置拦截器类**![image-20231105101900819](https://gitee.com/coi4/test/raw/master/img/image-20231105101900819.png)

  - 运行测试

    - preHandle：与配置顺序相同，必定运行

      postHandle:与配置顺序相反，可能不运行

      afterCompletion:与配置顺序相反，可能不运行。

拦截器执行的顺序是和配置顺序有关。就和前面所提到的运维人员进入机房的案例，先进后出。

- 当配置多个拦截器时，形成拦截器链
- 拦截器链的运行顺序参照拦截器添加顺序为准
- 当拦截器中出现对原始处理器的拦截，后面的拦截器均终止运行
- 当拦截器运行中断，仅运行配置在前面的拦截器的afterCompletion操作

![image-20231105101956631](https://gitee.com/coi4/test/raw/master/img/image-20231105101956631.png)

## 三、maven

## 四、springboot

### 1、简介

**简化** Spring 应用的**初始搭建**以及**开发过程**；SpringBoot 是对 Spring 开发进行简化的

#### 1.1、快速入门

##### 1.1.1、开发步骤

需要联网

-  **创建新模块**![image-20231104021744564](https://gitee.com/coi4/test/raw/master/img/image-20231104021744564.png)

  ![image-20231104021815718](https://gitee.com/coi4/test/raw/master/img/image-20231104021815718.png)

  ![image-20231104021833394](https://gitee.com/coi4/test/raw/master/img/image-20231104021833394.png)

  ![image-20231104021852916](https://gitee.com/coi4/test/raw/master/img/image-20231104021852916.png)

  ![image-20231104021909284](https://gitee.com/coi4/test/raw/master/img/image-20231104021909284.png)

  - 在创建好的工程中不需要创建配置类

  - 创建好的项目会自动生成其他的一些文件，而这些文件目前对我们来说没有任何作用，所以可以将这些文件删除。

    可以删除的目录和文件如下：

    .mvn

    .gitignore

    HELP.md

    mvnw

    mvnw.cmd

- **创建** Controller：在 com.itheima.controller 包下创建 BookController ，代码如下

  ```
  @RestController
  @RequestMapping("/books")
  public class BookController {
  @GetMapping("/{id}")
  public String getById(@PathVariable Integer id){
  System.out.println("id ==> "+id);
  return "hello , spring boot!";
  }
  }
  ```

- **启动服务器**：运行 SpringBoot 工程不需要使用本地的 Tomcat 和 插件，只运行项目 com.itheima 包下的 Application 类

- **进行测试**![image-20231104022111385](https://gitee.com/coi4/test/raw/master/img/image-20231104022111385.png)

SpringBoot 程序中的坐标是我们在创建工程时进行勾选自动生成的；SpringBoot 程序不需要我们自己书写配置类；

##### 1.1.2、**官网构建工程**

- https://spring.io/projects/spring-boot，拖到最下方，点击 Spring Initializr 超链接

- **选择依赖**：点击上图右上角的 ADD DEPENDENCIES... CTRL + B 按钮![image-20231104022520795](https://gitee.com/coi4/test/raw/master/img/image-20231104022520795.png)

- **生成工程**：在页面的最下方点击 GENERATE CTRL + 回车 按钮生成工程并下载到本

  地

##### 1.1.3、SpringBoot工程快速启动

后端可以将 SpringBoot 工程打成 jar 包，该 jar 包运行不依赖于 Tomcat 和 Idea 这些工具也可以正常运行，只是这个 jar 包在运行过程中连接和我们自己程序相同的 Mysql 数据库即可

打包：使用 Maven 的 package 指令打包就会在 target 目录下生成对应的 Jar 包。

启动：进入 jar 包所在位置，在 命令提示符 中输入如下命令

```
jar -jar springboot_01_quickstart-0.0.1-SNAPSHOT.jar
```

#### 1.2 SpringBoot概述

SpringBoot 程序优点恰巧就是针对 Spring 的缺点

- 自动配置。这个是用来解决 Spring 程序配置繁琐的问题
- 起步依赖。这个是用来解决 Spring 程序依赖设置繁琐的问题
- 辅助功能（内置服务器,...）。我们在启动 SpringBoot 程序时既没有使用本地的 tomcat 也没有使用 tomcat 插件，而是使用 SpringBoot 内置的服务器。

##### 1.2.1、起步依赖

**starter**

- SpringBoot 中常见项目名称，定义了当前项目使用的所有项目坐标，以达到减少依赖配置的目的

**parent**

- 所有 SpringBoot 项目要继承的项目，定义了若干个坐标版本号（依赖管理，而非依赖），以达到减少依赖冲突的目的
- spring-boot-starter-parent （2.5.0）与 spring-boot-starter-parent （2.4.6）共计57处坐标版本不同

实际开发

- 使用任意坐标时，仅书写GAV中的G和A，V由SpringBoot提供
- 如发生坐标错误，再指定version（要小心版本冲突）

##### 1.2.2、程序启动

Springboot01QuickstartApplication：引导类

SpringBoot 在创建项目时，采用jar的打包方式

SpringBoot 的引导类是项目的入口，运行 main 方法就可以启动项目

##### 1.2.3、切换web服务器

- 切换 web 服务器就需要将默认的 tomcat 服务器给排除掉：exclusion 标签

```
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-web</artifactId>
<exclusions>
<exclusion>
<artifactId>spring-boot-starter-tomcat</artifactId>
<groupId>org.springframework.boot</groupId>
</exclusion>
</exclusions>
</dependency>
```

- 引入 jetty 服务器

  ```
  <dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-jetty</artifactId>
  </dependency>
  ```

### 2、配置文件

#### 2.1、格式

将端口号改为 80 ，这样在访问的时候就可以不写端口号了：http://localhost/books/1 

配合文件必须放在 resources 目录下

配置方式：

- application.properties：server.port=80 （在该配置文件中书写 port ， Idea 就会提示)

- application.yml：server:

  port: 81（**在** : **后，数据前一定要加空格。**port ， Idea ）

- application.yaml：server:

  port: 82

  - **在配合文件中如果没有提示**![image-20231104085155265](https://gitee.com/coi4/test/raw/master/img/image-20231104085155265.png)

  - ![image-20231104085209776](https://gitee.com/coi4/test/raw/master/img/image-20231104085209776.png)

    弹出窗口点加号

    ![image-20231104085309203](https://gitee.com/coi4/test/raw/master/img/image-20231104085309203.png)

- 优先级：application.properties **>** application.yml **>** application.yaml

#### 2.2、yaml

**一种数据序列化格式**：提示键+关键词

xml：

![image-20231104085645980](https://gitee.com/coi4/test/raw/master/img/image-20231104085645980.png)

优点：

- 容易阅读

  yaml 类型的配置文件比 xml 类型的配置文件更容易阅读，结构更加清晰

- 容易与脚本语言交互

- 以数据为核心，重数据轻格式

  yaml 更注重数据，而 xml 更注重格式

**YAML** **文件扩展名：**

- .yml (主流)
- .yaml

语法规则：

- 大小写敏感
- 属性层级关系使用多行描述，每行结尾使用冒号结束
- 使用缩进表示层级关系，同层级左侧对齐，只允许使用空格（不允许使用Tab键）
- 空格的个数并不重要，只要保证同层级的左侧对齐即可。
- #表示注释
- 属性值前面添加空格（属性名与属性值之间使用冒号+空格作为分隔）（核心规则：**数据前面要加空格与冒号隔开**）
- 数组数据在数据书写位置的下方使用减号作为数据开始符号，每行书写一个数据，减号与数据间空格分隔![image-20231104090038113](https://gitee.com/coi4/test/raw/master/img/image-20231104090038113.png)

配置文件数据读取：

- 新创建一个名为 springboot_03_read_data 的 SpringBoot 工程![image-20231104090204827](https://gitee.com/coi4/test/raw/master/img/image-20231104090204827.png)

- 在 com.itheima.controller 包写创建名为 BookController 的控制器![image-20231104090308164](https://gitee.com/coi4/test/raw/master/img/image-20231104090308164.png)

- 在 com.itheima.domain 包下创建一个名为 Enterprise 的实体类等会用来封装数据![image-20231104090315395](https://gitee.com/coi4/test/raw/master/img/image-20231104090315395.png)

- 在 resources 下创建一个名为 application.yml 的配置文件，里面配置了不同的数据![image-20231104090418013](https://gitee.com/coi4/test/raw/master/img/image-20231104090418013.png)

- 读取配置数据：

  - **使用** **@Value**注解： 

    @Value("表达式") 注解可以从配合文件中读取数据，注解中用于读取属性名引用方式是： ${一级属性名.二级属性名……}![image-20231104090703896](https://gitee.com/coi4/test/raw/master/img/image-20231104090703896.png)

  -  **Environment**对象（开发中很少使用）：使用 @Autowired 注解注入 Environment 对象的方式读取数据，如果需要使用哪个数据只需要通过调用Environment 对象的 getProperty(String name) 方法获取![image-20231104090811884](https://gitee.com/coi4/test/raw/master/img/image-20231104090811884.png)

  - **自定义对象**：

    - 将实体类 bean 的创建交给 Spring 管理。在类上添加 @Component 注解![image-20231104091041322](https://gitee.com/coi4/test/raw/master/img/image-20231104091041322.png)

      ![image-20231104091056619](https://gitee.com/coi4/test/raw/master/img/image-20231104091056619.png)

    - 使用 @ConfigurationProperties 注解表示加载配置文件；在该注解中也可以使用 prefix 属性指定只加载指定前缀的数据

    - 在 BookController 中进行注入![image-20231104091133594](https://gitee.com/coi4/test/raw/master/img/image-20231104091133594.png)

    - 警告提示：解决---在 pom.xml 中添加如下依赖即可![image-20231104091330824](https://gitee.com/coi4/test/raw/master/img/image-20231104091330824.png)

#### 2.3、多环境配置

项目开发完毕后要上线就需要该配置，将环境的配置改为线上环境的![image-20231104091442657](https://gitee.com/coi4/test/raw/master/img/image-20231104091442657.png)

 SpringBoot 给开发者提供了多环境的快捷配置，需要切换环境时只需要改一个配置即可，不同类型的配置文件多环境开发的配置都不相同

yaml文件：

在 application.yml 中使用 --- 来分割不同的配置![image-20231104091652520](https://gitee.com/coi4/test/raw/master/img/image-20231104091652520.png)

最新用来起名字的配置项：![image-20231104091924050](https://gitee.com/coi4/test/raw/master/img/image-20231104091924050.png)

告知 SpringBoot 使用哪段配置：![image-20231104091732838](https://gitee.com/coi4/test/raw/master/img/image-20231104091732838.png)

**properties**文件：

properties 类型的配置文件配置多环境需要定义不同的配置文件

- application-dev.properties 是开发环境的配置文件：server.port=80 
- application-test.properties 是测试环境的配置文件
- application-pro.properties 是生产环境的配置文件
- 以需要在 application.properties 配置文件中设置启用哪个配置文件：spring.profiles.active=pro

命令行启动参数设置：配置文件打到的jar包，通过 java -jar xxx.jar 的方式启动服务的，如何切换环境

SpringBoot 提供了在运行 jar 时设置开启指定的环境的方式：java –jar xxx.jar –-spring.profiles.active=test 

- 修改端口号：java –jar xxx.jar –-server.port=88 
- 同时设置多个配置，比如即指定启用哪个环境配置，又临时指定端口：java –jar springboot.jar –-server.port=88 –-spring.profiles.active=test 

命令行设置的端口号优先级高

#### 2.4、**配置文件分类**

于测试环境和开发环境的很多配置都不相同，所以测试人员在运行我们的工程时需要临时修改很多配置

SpringBoot 定义了配置文件不同的放置的位置；而放在不同位置的优先级是不同的（级别越高优先级越高）：

- 1级：classpath：application.yml

- 2级：classpath：config/application.yml（在 resources 下创建一个名为 config 的目录，在该目录中创建 application.yml 配置文件）

- 3级：file ：application.yml

- 4级：file ：config/application.yml（将工程打成 jar 包---点击工程的 package 来打 jar 包![image-20231104093125843](https://gitee.com/coi4/test/raw/master/img/image-20231104093125843.png)

  在硬盘上找到 jar 包所在位置![image-20231104093249752](https://gitee.com/coi4/test/raw/master/img/image-20231104093249752.png)

  在 jar 包所在位置创建 config 文件夹，在该文件夹下创建 application.yml 配置文件，而在该配合文件中将端口号设置为 82

  在命令行使用以下命令运行程序：java -jar springboot_06_config_file-0.0.1-SNAPSHOT.jar ）

### 3、SpringBoot整合junit

SpringBoot 整合junit 特别简单，分为以下三步完成

- 在测试类上添加 SpringBootTest 注解
- 使用 @Autowired 注入要测试的资源
- 定义测试方法进行测试

在 test/java 下创建 com.itheima 包，在该包下创建测试类，将 BookService 注入到该测试类中![image-20231104093704871](https://gitee.com/coi4/test/raw/master/img/image-20231104093704871.png)

### 4、SpringBoot整合mybatis

SpringBoot整合Mybatis的开发过程:

- 创建SpringBoot工程![image-20231103091253297](https://gitee.com/coi4/test/raw/master/img/image-20231103091253297.png)
- 勾选配置使用的技术，能够实现自动添加起步依赖包![image-20231103091329693](https://gitee.com/coi4/test/raw/master/img/image-20231103091329693.png)
- 定义实体类
- 定义dao接口
- 定义测试类
- 设置dataSource相关属性(JDBC参数)![image-20231103091351658](https://gitee.com/coi4/test/raw/master/img/image-20231103091351658.png)
- 定义数据层接口映射配置（告诉 Mybatis 哪个是 dao 接口）![image-20231103091411182](https://gitee.com/coi4/test/raw/master/img/image-20231103091411182.png)
- #指定使用Druid数据源：
  - 导入依赖![image-20231104094124826](https://gitee.com/coi4/test/raw/master/img/image-20231104094124826.png)
  - yml中配置文件配置：通过 spring.datasource.type 来配置使用什么数据源![image-20231104094224170](https://gitee.com/coi4/test/raw/master/img/image-20231104094224170.png)

### 5、案例

创建工程：创建 SpringBoot 工程，在创建工程时需要勾选 web 、 mysql 、 mybatis ；工程中使用到了 Druid ，所以需要导入 Druid 的坐标

代码拷贝：![image-20231104094433936](https://gitee.com/coi4/test/raw/master/img/image-20231104094433936.png)

- 修改：
  - Springmvc_11_page 中 config 包下的是配置类，而 SpringBoot 工程不需要这些配置类，所以这些可以直接删除
  - dao 包下的接口上在拷贝到 springboot_09-ssm 工程中需要在接口中添加 @Mapper 注解
  - BookServiceTest 测试需要改成 SpringBoot 整合 junit 的![image-20231104094619261](https://gitee.com/coi4/test/raw/master/img/image-20231104094619261.png)

配置文件：在 application.yml 配置文件中需要配置![image-20231104094654165](https://gitee.com/coi4/test/raw/master/img/image-20231104094654165.png)

静态资源：SpringBoot 程序中是没有 webapp 目录的，静态资源需要放在 resources 下的 static 下

## 五、mybatisplus

### 1、入门案例与简历

MybatisPlus(简称MP)是基于MyBatis框架基础上开发的增强型工具，旨在简化开发、提供效率。https://mp.baomidou.com/

MP的特性:

- 无侵入：只做增强不做改变，不会对现有工程产生影响
- 强大的 CRUD 操作：内置通用 Mapper，少量配置即可实现单表CRUD 操作
- 支持 Lambda：编写查询条件无需担心字段写错
- 支持主键自动生成
- 内置分页插件......

开发方式

- 基于MyBatis使用MyBatisPlus
- 基于Spring使用MyBatisPlus
- **基于SpringBoot使用MyBatisPlus**

springboot整合mybatisplus：

- **创建数据库及表**

  ```
  create database if not exists mybatisplus_db character set utf8;
  use mybatisplus_db;
  CREATE TABLE user (
  id bigint(20) primary key auto_increment,
  name varchar(32) not null,
  password varchar(32) not null,
  age int(3) not null ,
  tel varchar(32) not null
  );
  insert into user values(1,'Tom','tom',3,'18866668888');
  insert into user values(2,'Jerry','jerry',4,'16688886666');
  insert into user values(3,'Jock','123456',41,'18812345678');
  insert into user values(4,'传智播客','itcast',15,'4006184000');
  ```

- **创建****SpringBoot****工程**

- **勾选配置使用技术**![image-20231103091610761](https://gitee.com/coi4/test/raw/master/img/image-20231103091610761.png)

  - 由于MP并未被收录到idea的系统内置配置，无法直接选择加入，需要手动在pom.xml中配置添加

- **pom.xml****补全依赖**

  ```
  <dependency>
  <groupId>com.baomidou</groupId>
  <artifactId>mybatis-plus-boot-starter</artifactId>
  <version>3.4.1</version>
  </dependency>
  <dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>druid</artifactId>
  <version>1.1.16</version>
  </dependency>
  ```

  - druid数据源可以加也可以不加，SpringBoot有内置的数据源，可以配置成使用Druid数据源
  - 从MP的依赖关系可以看出，通过依赖传递已经将MyBatis与MyBatis整合Spring的jar包导入，我们不需要额外在添加MyBatis的相关jar包

- **添加****MP****的相关配置信息**：resources默认生成的是properties配置文件，可以将其替换成yml文件，并在文件中配置数据库

  连接的相关信息: application.yml

  ```
  spring:
  datasource:
  type: com.alibaba.druid.pool.DruidDataSource
  driver-class-name: com.mysql.cj.jdbc.Driver
  url: jdbc:mysql://localhost:3306/mybatisplus_db?serverTimezone=UTC
  username: root
  password: root
  ```

- **根据数据库表创建实体类**

  ```
  public class User {
  private Long id;
  private String name;
  private String password;
  private Integer age;
  private String tel;
  //setter...getter...toString方法略
  }
  ```

- **创建****Dao****接口**

  ```
  @Mapper
  public interface UserDao extends BaseMapper<User>{
  }
  ```

- **编写引导类**

  ```
  @SpringBootApplication
  //@MapperScan("com.itheima.dao")
  public class Mybatisplus01QuickstartApplication {
  public static void main(String[] args) {
  SpringApplication.run(Mybatisplus01QuickstartApplication.class, args);
  }
  }
  ```

  - Dao接口要想被容器扫描到，有两种解决方案:

    - 方案一:在Dao接口上添加@Mapper注解，并且确保Dao处在引导类所在包或其子包中

      该方案的缺点是需要在每一Dao接口中添加注解

    - 方案二:在引导类上添加@MapperScan注解，其属性为所要扫描的Dao所在包

      该方案的好处是只需要写一次，则指定包下的所有Dao接口都能被扫描到，@Mapper就可以不写。

- **编写测试类**

  ```
  @SpringBootTest
  class MpDemoApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  public void testGetAll() {
  List<User> userList = userDao.selectList(null);
  System.out.println(userList);
  }
  }
  ```

  - 有报错（userDao注入的时候下面有红线提示），但不影响正常运行

跟整合MyBatis相比，不需要在DAO接口中编写方法和SQL语句，只需要继承BaseMapper接口即可。

### 2、标准数据层开发

重点学习的是数据层标准的CRUD(增删改查)的实现与分页功能

标准使用：

![image-20231103092627943](https://gitee.com/coi4/test/raw/master/img/image-20231103092627943.png)

- 新增：int insert (T t) （T:泛型，新增用来保存新增数据；int:返回值，新增成功后返回1，没有新增成功返回的是0）

  ```java
  @SpringBootTest
  class Mybatisplus01QuickstartApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  void testSave() {
  User user = new User();
  user.setName("黑马程序员");
  user.setPassword("itheima");
  user.setAge(12);
  user.setTel("4006184000");
  userDao.insert(user);
  }
  }
  ```

- 删除：int deleteById (Serializable id)（Serializable：参数类型；int:返回值类型，数据删除成功返回1，未删除数据返回0。）

  ```
  @SpringBootTest
  class Mybatisplus01QuickstartApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  void testDelete() {
  userDao.deleteById(1401856123725713409L);
  }
  }
  ```

- 修改：int updateById(T t);（传入的对象中需要有ID属性值)

- **根据****ID****查询**：T selectById (Serializable id)（T:根据ID查询只会返回一条数据)

  ```
  @SpringBootTest
  class Mybatisplus01QuickstartApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  void testGetById() {
  User user = userDao.selectById(2L);
  System.out.println(user);
  }
  }
  ```

- **查询所有**：List<T> selectList(Wrapper<T> queryWrapper)（Wrapper：用来构建条件查询的条件，目前我们没有可直接传为Null；List:因为查询的是所有，所以返回的数据是一个集合）

  ```
  @SpringBootTest
  class Mybatisplus01QuickstartApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  void testGetAll() {
  List<User> userList = userDao.selectList(null);
  System.out.println(userList);
  }
  }
  ```

- **Lombok**：对模型类编写的优化方法；一个Java类库，提供了一组注解，简化POJO实体类开发。

  - 模型类的编写都需要哪些内容:
  
    - 私有属性
    - setter...getter...方法
    - toString方法
    - 构造函数
    
  - 步骤：
  
    - **添加****lombok****依赖**（版本不写，springboot已经管理）
  
      ```
      <dependency>
      <groupId>org.projectlombok</groupId>
      <artifactId>lombok</artifactId>
      <!--<version>1.18.12</version>-->
      </dependency>
      ```
  
    - **安装****Lombok****的插件**（**如果删除****setter****和****getter****方法程序有报红，则需要安装插件**）![image-20231103125952166](https://gitee.com/coi4/test/raw/master/img/image-20231103125952166.png)
  
      - 找不到lombok插件：https://plugins.jetbrains.com/plugin/6317-lombok/versions
        - 根据自己IDEA的版本下载对应的lombok插件，下载成功后，在IDEA中采用离线安装的方式进行安装。![image-20231103130122827](https://gitee.com/coi4/test/raw/master/img/image-20231103130122827.png)
  
    - **模型类上添加注解**
  
      - @Setter:为模型类的属性提供setter方法
  
      - @Getter:为模型类的属性提供getter方法
  
      - @ToString:为模型类的属性提供toString方法
  
      - @EqualsAndHashCode:为模型类的属性提供equals和hashcode方法
  
      - *@Data:是个组合注解，包含上面的注解的功能
  
      - *@NoArgsConstructor:提供一个无参构造函数
  
      - *@AllArgsConstructor:提供一个包含所有参数的构造函数
  
      - ```
        @Data
        @AllArgsConstructor
        @NoArgsConstructor
        public class User {
        private Long id;
        private String name;
        private String password;
        private Integer age;
        private String tel;
        }
        ```

- 分页功能： 

  IPage<T> selectPage(IPage<T> page, Wrapper<T> queryWrapper)

  - IPage:用来构建分页查询条件

    Wrapper：用来构建条件查询的条件，目前我们没有可直接传为Null

    IPage:返回值，你会发现构建分页条件和方法的返回值都是IPage

  - 步骤

    - **调用方法传入参数获取返回值**

      ```
      @SpringBootTest
      class Mybatisplus01QuickstartApplicationTests {
      @Autowired
      private UserDao userDao;
      //分页查询
      @Test
      void testSelectPage(){
      //1 创建IPage分页对象,设置分页参数,1为当前页码，3为每页显示的记录数
      IPage<User> page=new Page<>(1,3);
      //2 执行分页查询
      userDao.selectPage(page,null);
      //3 获取分页结果
      System.out.println("当前页码值："+page.getCurrent());
      System.out.println("每页显示数："+page.getSize());
      System.out.println("一共多少页："+page.getPages());
      System.out.println("一共多少条数据："+page.getTotal());
      System.out.println("数据："+page.getRecords());
      }
      }
      ```

    - **设置分页拦截器**（代码可在官网查看）![image-20231103130911303](https://gitee.com/coi4/test/raw/master/img/image-20231103130911303.png)

      ```
      @Configuration
      public class MybatisPlusConfig {
      @Bean
      public MybatisPlusInterceptor mybatisPlusInterceptor(){
      //1 创建MybatisPlusInterceptor拦截器对象
      MybatisPlusInterceptor mpInterceptor=new MybatisPlusInterceptor();
      //2 添加分页拦截器
      mpInterceptor.addInnerInterceptor(new PaginationInnerInterceptor());
      return mpInterceptor;
      }
      }
      ```

    - 运行测试程序（如果想查看MP执行的SQL语句，可以修改application.yml配置文件，打开日志可以在控制台打印出对应的SQL语句，调试完后记得关闭）

      ```
      mybatis-plus:
      configuration:
      log-impl: org.apache.ibatis.logging.stdout.StdOutImpl #打印SQL日志到控制台
      ```

3、DQL编程控制（查）

条件查询方式：

类：MyBatisPlus将书写复杂的SQL查询条件进行了封装，使用编程的形式完成查询条件的组合。（Wrapper类）

环境构建：

- 创建一个SpringBoot项目

- pom.xml中添加对应的依赖

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
  https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.5.0</version>
  </parent>
  <groupId>com.itheima</groupId>
  <artifactId>mybatisplus_02_dql</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  13 <properties>
  14 <java.version>1.8</java.version>
  15 </properties>
  16 <dependencies>
  17
  18 <dependency>
  19 <groupId>com.baomidou</groupId>
  20 <artifactId>mybatis-plus-boot-starter</artifactId>
  21 <version>3.4.1</version>
  22 </dependency>
  23
  24 <dependency>
  25 <groupId>org.springframework.boot</groupId>
  26 <artifactId>spring-boot-starter</artifactId>
  27 </dependency>
  28
  29 <dependency>
  30 <groupId>com.alibaba</groupId>
  31 <artifactId>druid</artifactId>
  32 <version>1.1.16</version>
  33 </dependency>
  34
  35 <dependency>
  36 <groupId>mysql</groupId>
  37 <artifactId>mysql-connector-java</artifactId>
  38 <scope>runtime</scope>
  39 </dependency>
  40
  41 <dependency>
  42 <groupId>org.springframework.boot</groupId>
  43 <artifactId>spring-boot-starter-test</artifactId>
  44 <scope>test</scope>
  45 </dependency>
  46
  47 <dependency>
  48 <groupId>org.projectlombok</groupId>
  49 <artifactId>lombok</artifactId>
  50 </dependency>
  51
  52 </dependencies>
  53
  54 <build>
  55 <plugins>
  56 <plugin>
  57 <groupId>org.springframework.boot</groupId>
  58 <artifactId>spring-boot-maven-plugin</artifactId>
  59 </plugin>
  60 </plugins>
  61 </build>
  62
  63 </project>
  64
  ```

- 编写UserDao接口

  ```
   @Mapper
  2 public interface UserDao extends BaseMapper<User> {
  3 }
  ```

- 编写模型类

  ```
  1 @Data
  2 public class User {
  3 private Long id;
  4 private String name;
  5 private String password;
  6 private Integer age;
  7 private String tel;
  8 }
  ```

- 编写引导类

  ```
  1 @SpringBootApplication
  2 public class Mybatisplus02DqlApplication {
  3
  4 public static void main(String[] args) {
  5 SpringApplication.run(Mybatisplus02DqlApplication.class, args);
  6 }
  7
  8 }
  ```

- 编写配置文件

  ```
  1 # dataSource
  2 spring:
  3 datasource:
  4 type: com.alibaba.druid.pool.DruidDataSource
  5 driver-class-name: com.mysql.cj.jdbc.Driver
  6 url: jdbc:mysql://localhost:3306/mybatisplus_db?serverTimezone=UTC
  7 username: root
  8 password: root
  9 # mp日志
  10 mybatis-plus:
  11 configuration:
  12 log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  ```

- 编写测试类

  ```
  1 @SpringBootTest
  2 class Mybatisplus02DqlApplicationTests {
  3
  4 @Autowired
  5 private UserDao userDao;
  6
  7 @Test
  8 void testGetAll(){
  9 List<User> userList = userDao.selectList(null);
  10 System.out.println(userList);
  11 }
  12 }
  ```

  ![image-20231103132110595](https://gitee.com/coi4/test/raw/master/img/image-20231103132110595.png)

- 测试时日志多，速度慢，不利于查看结果：

  - 取消初始化spring日志打印，resources目录下添加logback.xml，名称固定，内容如下:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
     <configuration>
     </configuration>
    ```

  - 取消MybatisPlus启动banner图标：application.yml添加如下内容:

    ```
    # mybatis-plus日志控制台输出
    mybatis-plus:
    configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
    global-config:
    banner: off # 关闭mybatisplus启动图标
    ```

  - 取消SpringBoot的log打印：application.yml添加如下内容:

    ```
    spring:
    main:
    banner-mode: off # 关闭SpringBoot启动图标(banner)
    ```

构建条件查询：入口在Wrapper这个类上，找它对应的实现类，实现类多（有多种构建查询条件对象的方式）

- 第一种:**QueryWrapper**

  ```java
  1 @SpringBootTest
  2 class Mybatisplus02DqlApplicationTests {
  3
  4 @Autowired
  5 private UserDao userDao;
  6
  7 @Test
  8 void testGetAll(){
  9 QueryWrapper qw = new QueryWrapper();
  10 qw.lt("age",18);//lt: 小于(<)
  11 List<User> userList = userDao.selectList(qw);
  12 System.out.println(userList);
  13 }
  14 }
  ```

- 第二种:**QueryWrapper****的基础上使用****lambda**

  ```java
  1 @SpringBootTest
  2 class Mybatisplus02DqlApplicationTests {
  3
  4 @Autowired
  5 private UserDao userDao;
  6
  7 @Test
  8 void testGetAll(){
  9 QueryWrapper<User> qw = new QueryWrapper<User>();
  10 qw.lambda().lt(User::getAge, 10);//添加条件//User::getAget,为lambda表达式中的，类名::方法名
  11 List<User> userList = userDao.selectList(qw);
  12 System.out.println(userList);
  13 }
  14 }
  ```

- 第三种:**LambdaQueryWrapper**

  ```
  @SpringBootTest
  class Mybatisplus02DqlApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  void testGetAll(){
  LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
  lqw.lt(User::getAge, 10);
  List<User> userList = userDao.selectList(lqw);
  System.out.println(userList);
  }
  }
  ```

多条件构建：以上三种都为一个条件，多条件：

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {
@Autowired
private UserDao userDao;
@Test
void testGetAll(){
LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
lqw.lt(User::getAge, 30);
lqw.gt(User::getAge, 10);//10到30之间
    //gt：大于(>)，构建时支持链式
 //lqw.lt(User::getAge, 30).gt(User::getAge, 10);
    //30或10：lqw.lt(User::getAge, 10).or().gt(User::getAge, 30);
List<User> userList = userDao.selectList(lqw);
System.out.println(userList);
}
}
```

null判定：使用一个age属性，如何去接收页面上的两个值

- 方式一：添加属性age2,这种做法可以但是会影响到原模型类的属性内容

- 方式二：新建一个模型类,让其继承User类，并在其中添加age2属性，UserQuery在拥有User属性后同时添加了age2属性

- ```java
  @SpringBootTest
  class Mybatisplus02DqlApplicationTests {
  
   @Autowired
  private UserDao userDao;
  @Test
  void testGetAll(){
  //模拟页面传递过来的查询数据
  UserQuery uq = new UserQuery();
  uq.setAge(10);
  uq.setAge2(30);
  LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
  lqw.lt(null!=uq.getAge2(),User::getAge, uq.getAge2());//返回true，则添加条件，返回false则不添加条件
  lqw.gt(null!=uq.getAge(),User::getAge, uq.getAge());
  List<User> userList = userDao.selectList(lqw);
  System.out.println(userList);
  }
  }
  ```

查询投影：查询投影即不查询所有字段，只查询出指定内容的数据。

查询指定字段：

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {
@Autowired
private UserDao userDao;
@Test
void testGetAll(){
LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
lqw.select(User::getId,User::getName,User::getAge);//select(...)方法用来设置查询的字段列，可以设置多个
List<User> userList = userDao.selectList(lqw);
System.out.println(userList);
}
}
```

- 如果使用的不是lambda，就需要手动指定字段

  ```java
  @SpringBootTest
  class Mybatisplus02DqlApplicationTests {
  @Autowired
  private UserDao userDao;
  @Test
  void testGetAll(){
  QueryWrapper<User> lqw = new QueryWrapper<User>();
  lqw.select("id","name","age","tel");
  List<User> userList = userDao.selectList(lqw);
  System.out.println(userList);
  }
  }
  ```

聚合查询：

> 聚合函数查询，完成count、max、min、avg、sum的使用
>
> count:总记录数
>
> max:最大值
>
> min:最小值
>
> avg:平均值
>
> sum:求和

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {
@Autowired
private UserDao userDao;
@Test
void testGetAll(){//为了在做结果封装的时候能够更简单，我们将上面的聚合函数都起了个名称，方面后期来获取这些数
据
QueryWrapper<User> lqw = new QueryWrapper<User>();
//lqw.select("count(*) as count");
//SELECT count(*) as count FROM user
//lqw.select("max(age) as maxAge");
//SELECT max(age) as maxAge FROM user
//lqw.select("min(age) as minAge");
//SELECT min(age) as minAge FROM user
//lqw.select("sum(age) as sumAge");
//SELECT sum(age) as sumAge FROM user
lqw.select("avg(age) as avgAge");
//SELECT avg(age) as avgAge FROM user
List<Map<String, Object>> userList = userDao.selectMaps(lqw);
System.out.println(userList);
}
}
```

分组查询：

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {
@Autowired
private UserDao userDao;
@Test
void testGetAll(){
QueryWrapper<User> lqw = new QueryWrapper<User>();
lqw.select("count(*) as count,tel");
lqw.groupBy("tel");//groupBy为分组
List<Map<String, Object>> list = userDao.selectMaps(lqw);
System.out.println(list);
}
}
```

注：

- 聚合与分组查询，无法使用lambda表达式来完成
- MP只是对MyBatis的增强，如果MP实现不了，我们可以直接在DAO接口中使用MyBatis的方式实现

查询条件设定：具体可参考官方文档https://mp.baomidou.com/guide/wrapper.html#abstractwrapper

MP的查询条件有很多:

- 范围匹配（> 、 = 、between）
- 模糊匹配（like）
- 空判定（null）
- 包含性匹配（in）
- 分组（group）
- 排序（order）
- ……

等值查询：

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {
@Autowired
private UserDao userDao;
@Test
void testGetAll(){
LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
lqw.eq(User::getName, "Jerry").eq(User::getPassword, "jerry");//eq()： 相当于 =
User loginUser = userDao.selectOne(lqw);//selectList：查询结果为多个或者单个；selectOne:查询结果为单个
System.out.println(loginUser);
}
}
```

范围查询：

```
lqw.between(User::getAge, 10, 30);
//SELECT id,name,password,age,tel FROM user WHERE (age BETWEEN ? AND
?)
//gt():大于(>)
ge():大于等于(>=)
lt():小于(<)
lte():小于等于(<=)
between():between ? and ?
```

模糊查询：

```
//查询表中name属性的值以J开头的用户信息,使用like进行模糊查询
lqw.likeLeft(User::getName, "J");
//SELECT id,name,password,age,tel FROM user WHERE (name LIKE ?)
//like():前后加百分号,如 %J%
likeLeft():前面加百分号,如 %J
likeRight():后面加百分号,如 J%
```

排序查询：![image-20231103221401948](https://gitee.com/coi4/test/raw/master/img/image-20231103221401948.png)

```java
//查询所有数据，然后按照id降序
/**
* condition ：条件，返回boolean，
当condition为true，进行排序，如果为false，则不排序
* isAsc:是否为升序，true为升序，false为降序
* columns：需要操作的列
*/
lwq.orderBy(true,false, User::getId);
```

- orderBy排序
  - condition:条件，true则添加排序，false则不添加排序
  - isAsc:是否为升序，true升序，false降序
  - columns:排序字段，可以有多个
- orderByAsc/Desc(单个column):按照指定字段进行升序/降序
- orderByAsc/Desc(多个column):按照多个字段进行升序/降序
- orderByAsc/Desc
  - condition:条件，true添加排序，false不添加排序
  - 多个columns：按照多个字段进行排序

**映射匹配兼容性**：

之所以数据能够成功的从表中获取并封装到模型对象中，原因是表的字段列名和模型类的属性名一样。

- **表字段与编码属性设计不同步**（两边都不能修改）：@TableField（模型类属性定义上方） ,使用该注解可以实现模型类属性名和表的列名之间的映射关系![image-20231103221917005](https://gitee.com/coi4/test/raw/master/img/image-20231103221917005.png)
- **编码中添加了数据库中未定义的属性**：的sql语句中在select的时候查询了数据库不存在的字段，程序运行就会报错：@TableField注解的属性exist，设置该字段是否在数据库表中存在，如果设置为false则不存在，生成sql语句查询的时候，就不会再查询该字段了。![image-20231103222122609](https://gitee.com/coi4/test/raw/master/img/image-20231103222122609.png)
- **采用默认查询开放了更多的字段查看权限**：（密码不可看）@TableField属性select，设置默认是否需要查询该字段的值，true(默认值)表示默认查询该字段，false表示默认不查询该字段。![image-20231103222354583](https://gitee.com/coi4/test/raw/master/img/image-20231103222354583.png)
- **表名与编码开发设计不同步**：表的名称和模型类的名称不一致，导致查询失败（**Table 'databaseName.tableNaem' doesn't exist**）；@TableName来设置表与模型类之间的对应关系。![image-20231103222642233](https://gitee.com/coi4/test/raw/master/img/image-20231103222642233.png)

4、DML编程控制（增删改）

新增： id生成策略控制：新增成功后，主键ID是一个很长串的内容，我们更想要的是按照数据库表字段进行自增长；不同的业务采用的ID生成方式应该是不一样的

#分布式ID：多台数据库服务器进行存储

步骤：

- 环境构建：创建springboot项目，添加依赖，编写UserDao接口，编写模型类，编写引导类，编写配置文件，编写测试类，测试

- 代码：

  - AUTO策略：

    - ****设置生成策略为****AUTO：

      ```
      @Data
      @TableName("tbl_user")
      public class User {
      @TableId(type = IdType.AUTO)
      private Long id;
      private String name;
      @TableField(value="pwd",select=false)
      private String password;
      private Integer age;
      private String tel;
      @TableField(exist=false)
      private Integer online;
      }
      ```

    - **删除测试数据并修改自增值**：![image-20231103223441645](https://gitee.com/coi4/test/raw/master/img/image-20231103223441645.png)

    - ![image-20231103223457050](https://gitee.com/coi4/test/raw/master/img/image-20231103223457050.png)

  - NONE: 不设置id生成策略

  - INPUT:用户手工输入id

    - 设置生成策略为INPUT（这种ID生成策略，需要将表的自增策略删除掉）![image-20231103231517453](https://gitee.com/coi4/test/raw/master/img/image-20231103231517453.png)

    - **添加数据手动设置****ID**

      ```
      @SpringBootTest
      class Mybatisplus03DqlApplicationTests {
      @Autowired
      private UserDao userDao;
      @Test
      void testSave(){
      User user = new User();
      //设置主键ID的值
      user.setId(666L);
      user.setName("黑马程序员");
      user.setPassword("itheima");
      user.setAge(12);
      user.setTel("4006184000");
      userDao.insert(user);
      }
      }
      ```

  - ASSIGN_ID:雪花算法生成id(可兼容数值型与字符串型)（不需要手动设置ID，如果手动设置ID，则会使用自己设置的值；生成的ID就是一个Long类型的数据）

    - **设置生成策略为****ASSIGN_ID**
    - 添加数据不设置****ID**

  - ASSIGN_UUID:以UUID生成算法作为id生成策略额（主键的类型不能是Long，而应该改成String类型）

    - **设置生成策略为****ASSIGN_UUID**
    - **修改表的主键类型**![image-20231104004655120](https://gitee.com/coi4/test/raw/master/img/image-20231104004655120.png)
    - ****添加数据不设置****ID

  - 其他的几个策略均已过时，都将被ASSIGN_ID和ASSIGN_UUID代替掉。

- 选择：

  - NONE: 不设置id生成策略，MP不自动生成，约等于INPUT,所以这两种方式都需要用户手动设置，但是手动设置第一个问题是容易出现相同的ID造成主键冲突，为了保证主键不冲突就需要做很多判定，实现起来比较复杂
  - AUTO:数据库ID自增,这种策略适合在数据库服务器只有1台的情况下使用,不可作为分布式ID使用
  - ASSIGN_UUID:可以在分布式的情况下使用，而且能够保证唯一，但是生成的主键是32位的字符串，长度过长占用空间而且还不能排序，查询性能也慢
  - ASSIGN_ID:可以在分布式的情况下使用，生成的是Long类型的数字，可以排序性能也高，但是生成的策略和服务器时间有关，如果修改了系统时间就有可能导致出现重复主键

- 简化配置：

  - **模型类主键策略设置**：在项目中的每一个模型类上都需要使用相同的生成策略；让所有的模型类都可以使用该主键ID策略

    - 在配置文件中添加如下内容

      ```
      mybatis-plus:
       global-config:
         db-config:
            id-type: assign_id
      ```

  - **数据库表与模型类的映射关系**：MP会默认将模型类的类名名首字母小写作为表名使用，假如数据库表的名称都以tbl_开头，那么我们

    就需要将所有的模型类上添加@TableName

    - 简化方式为在配置文件中配置如下内容

      ```
      mybatis-plus:
      global-config:
      db-config:
      table-prefix: tbl_
      ```

**多记录操作**：

多条删除：

```
int deleteBatchIds(@Param(Constants.COLLECTION) Collection<? extends
Serializable> idList);
```

```
@Test
void testDelete(){
//删除指定多条数据
List<Long> list = new ArrayList<>();
list.add(1402551342481838081L);
list.add(1402553134049501186L);
list.add(1402553619611430913L);
userDao.deleteBatchIds(list);
}
}
```

批量查询：

```
List<T> selectBatchIds(@Param(Constants.COLLECTION) Collection<? extends
Serializable> idList);
```

```
void testGetByIds(){
//查询指定多条数据
List<Long> list = new ArrayList<>();
list.add(1L);
list.add(3L);
list.add(4L);
userDao.selectBatchIds(list);
```

逻辑删除：

- 物理删除:业务数据从数据库中丢弃，执行的是delete操作

- 逻辑删除:为数据设置是否可用状态字段，删除时设置状态字段为不可用状态，数据保留在数据库中，执行的是update操作

- 步骤：

  - 修改数据库表添加**deleted**列：字段名可以任意，内容也可以自定义，比如0代表正常，1代表删除，可以在添加列的同时设置其默认值为0正常。![image-20231104014013330](https://gitee.com/coi4/test/raw/master/img/image-20231104014013330.png)

  - 实体类添加属性

    - 添加与数据库表的列对应的一个属性名，名称可以任意，如果和数据表列名对不上，可以使用@TableField进行关系映射，如果一致，则会自动对应。

    - 标识新增的字段为逻辑删除字段，使用@TableLogic

      ```
      @Data
      //@TableName("tbl_user") 可以不写是因为配置了全局配置
      public class User {
      @TableId(type = IdType.ASSIGN_UUID)
      private String id;
      private String name;
      @TableField(value="pwd",select=false)
      private String password;
      private Integer age;
      private String tel;
      @TableField(exist=false)
      private Integer online;
      @TableLogic(value="0",delval="1")
      //value为正常数据的值，delval为删除数据的值
      private Integer deleted;
      }
      ```

    - **运行删除方法**：

      ```
      @SpringBootTest
       class Mybatisplus03DqlApplicationTests {
      
       @Autowired
       private UserDao userDao;
      
       @Test
       void testDelete(){
       userDao.deleteById(1L);
       }
       }
      ```

- MP的逻辑删除会将所有的查询都添加一个未被删除的条件，也就是已经被删除的数据是不应该被查询出来的。

  - 想把已经删除的数据都查询出来：

    ```
    @Mapper
    public interface UserDao extends BaseMapper<User> {
    //查询所有数据包含已经被删除的数据
    @Select("select * from tbl_user")
    public List<User> selectAll();
    }
    ```

- 如果每个表都要有逻辑删除，那么就需要在每个模型类的属性上添加@TableLogic注解

  ```
  mybatis-plus:
  global-config:
  db-config:
  # 逻辑删除字段名
  logic-delete-field: deleted
  # 逻辑删除字面值：未删除为0
  logic-not-delete-value: 0
  # 逻辑删除字面值：删除为1
  logic-delete-value: 1
  ```

乐观锁：乐观锁主要解决的问题是当要更新一条记录的时候，希望这条记录没有被别人更新。https://mp.baomidou.com/guide/interceptor-optimistic-locker.html#optimisticlockerinnerinterceptor

- 实现：

  - **数据库表添加列**,给列设置默认值为1

  - **在模型类中添加对应的属性**

    ```
    @Version
    private Integer version;
    ```

  - **添加乐观锁的拦截器**

    ```
    @Configuration
    public class MpConfig {
    @Bean
    public MybatisPlusInterceptor mpInterceptor() {
    //1.定义Mp拦截器
    MybatisPlusInterceptor mpInterceptor = new MybatisPlusInterceptor();
    //2.添加乐观锁拦截器
    mpInterceptor.addInnerInterceptor(new
    OptimisticLockerInnerInterceptor());
    return mpInterceptor;
    }
    }
    ```

  - 执行更新操作

    ```
    @SpringBootTest
    class Mybatisplus03DqlApplicationTests {
    @Autowired
    private UserDao userDao;
    @Test
    void testUpdate(){
    User user = new User();
    user.setId(3L);
    user.setName("Jock666");
    user.setVersion(1);
    userDao.updateById(user);
    }
    }
    ```

5、快速开发

**代码生成器实现**：https://mp.baomidou.com/guide/generator.html

- **创建一个**Maven项目
- **导入对应的**jar包
- **编写引导类**
- **创建代码生成类**
- 运行程序

**MP**中Service的CRUD：提供Service接口和实现类，分别是: IService和ServiceImpl ,后者是对前者的一个具体实现

Service的修改：

```
 public interface UserService extends IService<User>{

 }

 @Service
 public class UserServiceImpl extends ServiceImpl<UserDao, User> implements
UserService{

 }
```

