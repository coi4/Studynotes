# maven

## 一、基础

### 1、简介

![image-20231024181136419](https://gitee.com/coi4/test/raw/master/img/image-20231024181136419.png)

![image-20231025103342679](https://gitee.com/coi4/test/raw/master/img/image-20231025103342679.png)

> **项目构建**：提供标准的、跨平台的自动化项目构建方式
>
> **依赖管理**：方便快捷的管理项目依赖的资源，避免资源间版本冲突问题
>
> **统一开发结构**：提供标准的、统一的项目结构

### 2、下载与安装

解压安装、环境变量的配置

下载地址：https://maven.apache.org/download.cgi

**解压：**

​    Maven属于绿色版软件，解压即安装

**环境变量配置：**

1. 依赖Java,需要配置JAVA_HOME
2. 设置MAVEN自身的运行环境，需要配置MAVEN_HOME

**测试环境配置结果：**

​    MVN命令

### 3、基础概念（重）

#### 3.1、仓库

存储资源，包含各种jar包

![image-20231025104700374](https://gitee.com/coi4/test/raw/master/img/image-20231025104700374.png)

- 本地仓库：自己电脑上的，连接远程仓库获取资源
- 远程仓库：非本机电脑上的，为本地仓库提供资源
  - 中央仓库：存储所有资源，Maven维护
    - 都是开源的，不能存储具有版权的资源
  - 私服：部门/公司范围内存储的资源仓库，从中央获取（获一次永久保存，下载快）
    - 保存具有版权的资源
    - 一定范围内共享资源，仅对内部开放，不对外开放

#### 3.2、坐标

描述仓库中资源的位置https://repo1.maven.org/maven2/*？

- groupld：定义当前项目隶属**组织名（**通常为域名反写（org.mybatis)（com.itheima））
- artifactld：定义当前**项目名**称（通常为模块名，例如CRM、SMS）
- version:定义当前项目**版本号**
- packaging：定义当前项目的**打包方式**

#### 3.3、仓库配置

本地仓库配置（资源下载到的地方）：

- Maven启动后会自动保存下载的资源到本地仓库
  - 默认位置：当前目录位置为登录用户名所在目录下的.m2文件夹中。conf文件夹下settings.xml文件，通过替换`<localRepository>`标签中的地址，重新自定义本地仓库位置。
  
    ```
    <localRepository>$(user.home)/.m2/repository</localRepository>
    ```
  
  - 自定义：当前目录位置为 D:\maven\repository文件夹中。
  
    ```
    <localRepository>D:\maven\repository</localRepository>
    ```

远程仓库配置（资源来源）： Maven默认连接的是位于国外的服务器，下载速度比较慢，可用国内的[阿里云镜像](https://so.csdn.net/so/search?q=阿里云镜像&spm=1001.2101.3001.7020)仓库进行替换。

- Maven默认连接的仓库位置

  ```
  <repositories>
     <repository>
        <id>central</id>
        <name>Central Repository</name>
        <url>https://repo.maven.apache.org/maven2 </url>
        <layout>default</layout>
        <snapshots>
            <enabled>false</enabled>
       </snapshots>
     </repository>
  </repositories>
  ```

镜像仓库配置：

-  在settting文件中配置阿里云镜像仓库。

  ```
  <mirrors>
  <!--配置具体的仓库的下载镜像-->
      <mirror>
          <!--此镜像的唯一标识符,用来区分不同的mirror元素-->
          <id>nexus-aliyun</id>
          <!--对哪种仓库进行镜像，简单说就是替代哪个仓库-->
          <mirrorOf>central</mirrorOf>
          <!--镜像名称-->
          <name>Nexus aliyun</name> 
          <!--镜像URL -->
          <url>http://maven.aliyun.com/nexus/content/groups/public</url>
      </mirror>
  </mirrors>
  ```

setting文件的区别：

- 全局setting：定义了当前计算器中maven的公共配置
- 用户setting：定义了当前用户的配置

### 4、项目（重）

#### 4.1、手工

##### 4.1.1、布置maven目录结构

![image-20231025113104447](https://gitee.com/coi4/test/raw/master/img/image-20231025113104447.png)

- src同层下创建pom.xml文件

  ```
  <?xml version="1.0" encoding=UTF-8"?>
  <project
       xmlns="http://maven.apache.org/POM/4.0.0"
       xmlns:xsi="http:〃www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://maven.apache.org/POM/4.0.0http://maven.apache.org/maven-v4_0_0.xsd"> 
       <modelVersion>4.0.0</modelVersion>
       <groupId>com.itheima</groupId>
       <artifactId>project-java</artifactId>
       <version>1.0</version>
       <packaging>jar</packaging> 
       <dependencies> 
       	 <dependency>
  			<groupId>junit</groupId> 
  			<artifactId>junit</artifactId> 
  			<version>4.12</version> 
  		 </dependency> 
  	 </dependencies>
  </project>
  ```

##### 4.1.2、常用项目构建命令

- mvn开头，后面添加功能参数，可以一次执行多个命令，使用空格分隔；在pom文件所在目录下执行以下命令
- ![image-20231025113744781](https://gitee.com/coi4/test/raw/master/img/image-20231025113744781.png)
  - mvn compile：编译项目；此时会进行两个操作：
    - 下载插件。在本地仓库中下载执行compile功能所需的插件。
    - 编译项目。target目录下就是编译完成的内容。
  - mvn clean：清除编译完成的目录target
  - mvn test：测试，生成的测试报告位于target/surefire-reports目录下。
  - mvn package：打包源程序。过程中包含compile和test操作。
  - mvn install：将打包好的jar包安装到本地仓库。注意jar包的存放位置：groupId+artifactId+version

##### 4.1.3、插件创建工程

- 创建工程

  - ```mvn
    mvn archetype:generate
    -DgroupId={project-packaging} 
    -DartifactId={project-name} 
    -DarchetypeArtifactId=maven-archetype-quickstart
    -DinteractiveMode=false
    ```

- 创建java工程

  - ```
    mvn archetype:generate -DgroupId=com.itheima -DartifactId=java-project -
    DarchetypeArtifactId=maven-archetype-quickstart -Dversion=0.0.1-snapshot -
    DinteractiveMode=false
    ```

- 创建Web工程

  - ```
    mvn archetype:generate -DgroupId=com.itheima -DartifactId=web-project -
    DarchetypeArtifactId=maven-archetype-webapp -Dversion=0.0.1-snapshot -
    DinteractiveMode=false
    ```

  - ![image-20231025114410653](https://gitee.com/coi4/test/raw/master/img/image-20231025114410653.png)

#### 4.2、idea

##### 4.2.1、配置maven

- 存在兼容性问题，避免冲突，使用3.6.1版本
- all settings![image-20231121223548099](https://gitee.com/coi4/test/raw/master/img/image-20231121223548099.png)
- ![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/20210225171423540.jpg)

##### 4.2.2、手工创建Java项目

- ![image-20231025115430380](https://gitee.com/coi4/test/raw/master/img/image-20231025115430380.png)

  ![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/20210225172400702.jpg)

  ![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/20210225172512703.jpg)

  > src/main/java  —— 存放项目的.java 文件 
  > src/main/resources —— 存放项目资源文件，如数据库的配置文件 
  > src/test/java —— 存放所有单元测试.java 文件，如 JUnit 测试类 
  > target —— 项目输出位置，编译后的class 文件会输出到此目录 
  > pom.xml ——maven 项目核心配置文件 

- 只是普通Java项目，不是web项目

  - 在main目录下创建一个webapp文件夹
- 选择当前工程（项目名，如hello_maven）![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/20210225172724469.jpg)
  
- 修改路径信息(Structrue——Modules——Web）（arctifacts不为空）![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/20210225172912100.jpg)
  
- idea中的构建命令执行，作用同mvn

  ![img](https://gitee.com/coi4/test/raw/master/img/a11560dc5fdc43ee8341e2b380541bec.png)

  可通过添加Maven运行环境，达到相同的命令效果：![img](https://gitee.com/coi4/test/raw/master/img/b4a4a6590a1e4a33aa8f94138d4f8944.png)

  添加之后，点击运行按钮即可执行相应的命令。

  ![img](https://gitee.com/coi4/test/raw/master/img/66933f7f6a7141cca1af0b67c7c9218e.png)

##### 4.2.3、原型创建Java项目

- ![image-20231025115534060](https://gitee.com/coi4/test/raw/master/img/image-20231025115534060.png)

##### 4.2.4、原型创建web项目

- ![img](https://gitee.com/coi4/test/raw/master/img/20180513231612737)

##### 4.2.5、插件

启动Web工程需要用到Tomcat插件，在pom文件中添加以下[Tomcat7](https://so.csdn.net/so/search?q=Tomcat7&spm=1001.2101.3001.7020)插件。

- Tomcat7安装与运行
  
  - ![img](https://gitee.com/coi4/test/raw/master/img/20180514000006947)
  
    ![img](https://gitee.com/coi4/test/raw/master/img/20180514000438394)
  
    ![img](https://gitee.com/coi4/test/raw/master/img/20180514000754548)
  
    ![img](https://gitee.com/coi4/test/raw/master/img/201805141059394)
  
    ![img](https://gitee.com/coi4/test/raw/master/img/20180514110444440)
  
  - ![image-20231025115725677](https://gitee.com/coi4/test/raw/master/img/image-20231025115725677.png)
  
  - 添加之后可以看到，web项目中已经有了tomcat插件；双击可启动服务器![img](https://gitee.com/coi4/test/raw/master/img/5ed1f217f0844bdaa0249b451d87d220.png)
  
  - 端口被占用：
  
    - 调出系统cmd窗口
    - 通过netstat -ano|findstr 1099查询是哪个pid占用了端口
    - 通过taskkill /f /t /im 13120直接结束掉占用端口的进程
    - ![img](https://gitee.com/coi4/test/raw/master/img/20180514002611624)

### 5、依赖管理（重）

依赖指当前项目运行所需的jar，一个项目可设置多个依赖

依赖配置

- ![image-20231025120139397](https://gitee.com/coi4/test/raw/master/img/image-20231025120139397.png)

依赖传递

- 直接传递：当前项目中通过依赖配置建立的依赖关系
- 间接传递：被资源的资源如果依赖其他资源，当前项目间接依赖其他资源

**依赖传递冲突问题**：

- 路径优先：当依赖中出现相同的资源时，层级越深，优先级越低，层级越浅，优先级越高。
- 声明优先：当资源在相同层级被依赖时，配置顺序靠前的覆盖配置顺序靠后的。
- 特殊优先：当同级配置了相同资源的不同版本，后配置的覆盖先配置的。

可选依赖（不透明）

- 可选依赖指对外隐藏当前所依赖的资源一一不透明：将某依赖的`<optional>`标签指定为true时，间接引用该依赖的项目将无法看到该依赖资源。![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/5222dc63d16e4cbea6010c92a1b95ff6.png)

排除依赖（不需要）

- 排除依赖指主动断开间接依赖的资源，被排除的资源无需指定版本一一不需要。![img](https://gitee.com/coi4/test/raw/master/img/221f4986064f4bfc9bc11ea249649cbb.png)

依赖范围

-  依赖的jar默认情况可以在任何地方使用，可以通过scope标签设定其作用范围。 如下，表示junit依赖仅在测试代码中生效。

  ```
  <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
  </dependency>
  ```

 scope的可选值有4种，分别为compile(默认值)、test、provided、runtime.它们在项目中的作用范围各不相同。

**scope作用范围**

- 主程序范围有效（main文件夹范围内）
- 测试程序范围有效（test文件夹范围内）
- 是否参与打包（package指令范围内）

![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/e2a4e43f56744af6a97504622df12a95.png)

### 6、生命周期与插件

#### 6.1、构建生命周期

Maven对项目构建的生命周期划分为3个阶段。

- clean生命周期：清理工作。
  - ![img](https://gitee.com/coi4/test/raw/master/img/4358329a67c24c43b72f37c583a5eefc.png)
- default生命周期：核心工作，例如编译，测试，打包，部署等。
  - ![img](https://gitee.com/coi4/test/raw/master/img/d69792dcfbcb427285555c492542ddcc.png)
- site生命周期：产生报告，发布站点等。
  - ![img](https://gitee.com/coi4/test/raw/master/img/f49e151e59724ec3afab38aa50545878.png)

#### 6.2、插件

- 清理clean：将以前编译得到的旧文件class字节码文件删除
- 编译compile：将java源程序编译成class字节码文件
- 测试test：自动测试，自动调用junit程序
- 报告report：**测试**程序执行的**结果**
- 打包package：动态Web工程打War包，java工程打jar包
- 安装install：Maven特定的概念-----将打包得到的文件**复制到“仓库”**中的指定位置
- 部署deploy：将动态Web工程生成的war包**复制到Servlet容器**下，使其可以运行

插件与生命周期内的阶段绑定，在执行到对应生命周期时执行对应的插件功能。

通过插件可以自定义其他功能。

![image-20231106103319501](https://gitee.com/coi4/test/raw/master/img/image-20231106103319501.png)

运行到default生命周期的generate-test-resources阶段时就要执行这个插件。

## 二、高级

### 1、分模块开发与设计（重）

将一个工程的各个模块拆分成独立的项目，把工程进行模块划分，一个模块只负责一块内容，模块之间通过接口进行通信；主模块ssm中无任何内容

**ssm_pojo拆分**：

- 新建模块
- 拷贝原始项目中对应的相关内容到ssm_pojo模块中

**ssm_dao拆分**：

- 新建模块
- 拷贝原始项目中对应的相关内容到ssm_dao模块中
- pom.xml：引入数据层相关坐标即可。直接依赖ssm_pojo（对ssm_pojo模块执行install命令，将其安装到本地仓库）

**ssm_service拆分**：

- 新建模块
- 拷贝原始项目中对应的相关内容到ssm_service模块中
- pom.xml：引入数据层相关坐标即可。直接依赖ssm_dao（对ssm_dao模块执行install命令，将其安装到本地仓库），间接依赖ssm_pojo（有ssm_dao模块负责依赖关系的建立）

**ssm_controller拆分**：

- 新建模块
- 拷贝原始项目中对应的相关内容到ssm_service模块中
- pom.xml：引入数据层相关坐标即可。直接依赖ssm_dao（对ssm_dao模块执行install命令，将其安装到本地仓库），间接依赖ssm_pojo（有ssm_dao模块负责依赖关系的建立）

注：

- 模块中仅包含当前模块对应的功能类与配置文件。
- spring核心配置根据模块功能不同进行独立制作。
- 当前模块所依赖的模块通过导入坐标的形式加入当前模块后才可以使用。
- web.xml需要加载所有的spring核心配置文件。

### 2、聚合（重）

多模块构建维护：

一个模块 如ssm_dao模块做了更新，重新进行了install操作，可能会由于这个模块的调整而致使其他模块无法使用。

聚合的工作机制：增加一个新的模块，通过新模块来管理其他4个**模块**，当compile或install这个新模块时，其管理的4个模块会同时进行compile或install。

 聚合用于快速构建maven工程，一次性构建多个项目/模块。

步骤：

- 创建一个空模块，打包类型定义为pom

  ```
  <packaging>pom</packaging>
  ```

- 定义当前模块进行构建操作时关联的其他模块名称。

  ```
  <modules>
  	<module>../ssm_controller</module>
  	<module>../ssm_service</module>
  	<module>../ssm_dao</module>
  	<module>../ssm_pojo</module>
  </modules>
  ```

  执行顺序与配置顺序无关

### 3、继承（重）

模块依赖关系维护：

原始的各个模块可能会依赖一些相同的资源，比如ssm_service和ssm_dao都会用到spring-context，但它们可能因所使用的版本不一致而产生兼容问题。

继承的工作机制：增加一个新的模块，管理下面4个模块的**资源依赖**。新的模块称为父模块，被管理资源依赖的模块称为子模块。在父模块指定所有子模块用到的依赖的资源和对应版本，子模块使用资源时指定依赖资源即可，无需再声明版本，解决资源版本一致性问题。

#### 3.1、继承

 通过继承可以实现在子工程中沿用父工程中的配置。maven中的继承与java中的继承相似，在子工程中配置继承关系。

- 定义在父工程中
- 使用在子工程中（无需配置version）

步骤：

- 在子工程中声明其父工程坐标与对应的位置。

  ```
  <!-- 定义该工程的父工程-->
  <parent>
  	<groupId>com.itheima</groupId>
  	<artifactId>ssm</artifactId>
  	<version>1.0-SNAPSHOT</version>
  	<!-- 填写父工程的pom文件 -->
  	<relativePath>../ssm/pom.xml</relativePath>
  </parent>
  ```

#### 3.2、继承依赖定义

在父工程中定义依赖管理：

```
<!--声明此处进行依赖管理 -->
<dependencyManagement>
	<!--具体的依赖 -->
	<dependencies>
		<!--spring环境 -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>5.1.9.RELEASE</version>
		</dependency>
	<dependencies>
<dependencyManagement>
```

#### 3.3、继承依赖使用

 在子工程中定义依赖关系，无需声明依赖版本，版本参照父工程中依赖的版本。

```
<dependencies>
	<!--spring环境 -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-context</artifactId>
	</dependency>
</dependencies>
```

#### 3.4、继承的资源

![img](https://gitee.com/coi4/test/raw/master/img/2baa7fba651142b59dc7db27ce333426.png)

#### 3.5、继承与聚合

聚合用于快速构建项目。

继承用于快速配置。

相同点：

聚合与继承的pom.xml文件打包方式均为pom，**可以将两种关系制作到同一个pom文件中**。
聚合与继承均属于设计型模块，并无实际的模块内容。
不同点：

聚合是在当前模块中配置关系，聚合可以感知到参与聚合的模块有哪些。
继承是在子模块中配置关系，父模块无法感知哪些子模块继承了自己。

### 4、属性（重）

通过定义依赖的属性保证版本统一。

类别：

- 自定义属性：等同于定义变量，方便统一维护。

  - **定义格式：**

    ```
    <!--定义自定义属性 -->
    <properties>
    	<spring.version>5.1.9.RELEASE</spring.version>
    	<junit.version>4.12</junit.version>
    </properties>
    ```

  - **调用格式：**

    ```
    <dependency>
    	<groupId>org.springframework</groupId>
    	<artifactId>spring-context</artifactId>
    	<version>${spring.version}</version>
    </dependency>
    ```

- 内置属性：使用maven内置属性，快速配置。

  - **调用格式：**

    ```
    ${basedir}//maven项目的根目录（pom.xml文件的父目录）
    ${version}//与${project.version}等价
    ```

- Setting属性：使用maven配置文件setting.xml中的标签属性，用于动态配置

  ```
  ${settings.localRepository}
  ```

- Java系统属性：读取Java系统属性。

  - **调用格式：**

    ```
    ${user.home}
    ```

  - **系统属性查询方式：**mvn help:system

- 环境变量属性：使用maven配置文件setting.xml中的标签属性，用于动态配置。

  - **调用格式：**

    ```
    ${env.JAVA_HOME}
    ```

  - **系统属性查询方式：**mvn help:system

![img](https://gitee.com/coi4/test/raw/master/img/f3cb5a1a8a794fa3a1fa2d47f7f69549.png)

[10. maven属性_pom.xml没有properties-CSDN博客](https://blog.csdn.net/u014454538/article/details/115360004)

### 5、版本管理

#### 5.1、工程版本

- SNAPSHOT（快照版本）
          项目开发过程中，为方便团队成员合作，解决模块间相互依赖和时时更新的问题，开发者对每个模块进行构建的时候，输出的**临时性版本**叫做快照版本（测试阶段版本）。快照版本会随着开发的进展不断更新。

- RELEASE（发布版本）
          项目开发到进入阶段里程碑后，向团队外部发布较为稳定的版本，这种版本所对应的构件文件是稳定的，即便进行功能的后续开发，也**不会改变当前发布版本内容**，这种版本称为发布版本。

5.3、工程版本号约定

约定规范：

- <主版本>.<次版本>.<增量版本>.<里程碑版本>
- 主版本：表示项目重大**架构**的变更，如：spring5相较于spring4的迭代。
- 次版本：表示有较大的**功能**增加和变化，或者全面系统的修复漏洞。
- 增量版本：表示有重大**漏洞**的修复。
- 里程碑版本：表明一个版本的里程碑（版本内部）。

### 6、资源配置

#### 6.1、资源配置多文件维护

工程中还有jdbc([什么是JDBC？这篇文章告诉你 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/140885502#:~:text=这篇文章告诉你 1 (1)JDBC驱动管理器：负责注册特定的JDBC驱动器，主要通过java.sql. Driver Manager类实现。,2 (2)JDBC驱动器API：由Sun公司负责制定，其中最主要的接口是java.sql. Driver接口。 3 (3)JDBC驱动器：它是一种数据库驱动，由数据库厂商创建，也称为JDBC驱动程序JDBC驱动器实现了JDBC驱动器API，负责与特定的数据库连接，以及处理通信细节。))的用户等一些自定义的属性，可以在pom文件中一起进行管理。

![img](https://gitee.com/coi4/test/raw/master/img/27e0d794794446e7a77b329bc4ce8685.png)

#### 6.2、配置文件引用pom属性

作用： 在任意配置文件中加载pom文件中定义的属性。

**调用格式：**

```
${jdbc.url}
```

**开启配置文件加载pom属性：**

```
<!--配置资源文件对应的信息 -->
<resources>
	<resource>
		<!--设定配置文件对应的位置目录，支持使用属性动态设定路径-->
		<directory>${project.basedir}/src/main/resources</directory>
		<!--开启对配置文件的资源加载过滤-->
		<filtering>true</filtering>
	</resource>
</resources>
```

### 7、多环境开发配置

#### 7.1、多环境兼容

很多情况下，生产环境、开发环境、测试环境的属性值配置各不同。因此需要在不同的环境上加载其对应的属性配置。达到多环境兼容的目的。

#### 7.2、多环境配置

dev/test/pro 对应 开发/测试/生产

`activeByDefault` 将开发环境设置为默认环境

```
<!--创建多环境 -->
<profiles>
	<!--定义具体的环境：生成环境 -->
	<profile>
		<!--定义环境对应的唯一名称 -->
		<id>pro_env</id>
		<!--定义环境中专用的属性值 -->
		<properties>
			<jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
		</properties>
		<!--设置默认启动 -->
		<activation>
			<activeByDefault>true</activeByDefault>
		</activation>
	</profile>
	<!--定义具体的环境：开发环境 -->
	<profile>
		<id>dev_env</id>
		……
	</profile>
</profiles>
```

右侧 maven projects > Profiles 可以勾选对应的环境。

#### 7.3、加载指定环境

**作用：**
    加载指定环境。

**调用格式：**
mvn 指令 –P 环境定义id

![img](https://gitee.com/coi4/test/raw/master/img/f0a8dc1c300c4d9ca80ff07d95ca6f8d.png)

### 8、跳过测试

场景

- 整体模块功能未开发
- 模块中某个功能未开发完毕
- 单个功能更新调试导致其他功能失败
- 快速打包

方式

- **使用命令跳过测试**：mvn 指令 –D skipTests

  - 执行的指令生命周期必须包含测试环节。

    ![img](https://gitee.com/coi4/test/raw/master/img/283edf2710af43948b41a9423dd86934.png)

    ![img](https://gitee.com/coi4/test/raw/master/img/67eea87f5a6240538c6d39a03995d20b.png)

- **使用界面操作跳过测试**![img](https://gitee.com/coi4/test/raw/master/img/0940cc2c26c94ffd81733e9e34345df0.png)

- **使用配置跳过测试**

  ```
  <plugin>
  	<artifactId>maven-surefire-plugin</artifactId>
  	<version>2.22.1</version>
  	<configuration>
  		<skipTests>true</skipTests><!--设置跳过测试 -->
  		<includes> <!--包含指定的测试用例 -->
  			<include>**/User*Test.java</include>
  		</includes>
  		<excludes><!--排除指定的测试用例 -->
  			<exclude>**/User*TestCase.java</exclude>
  		</excludes>
  	</configuration>
  </plugin>
  ```

### 9、私服（重）

#### 9.1、分模块合作开发

不同的开发者开发不同的内容，如果需要用到公共资源可以直接从中央仓库下载。如果开发者之间需要用到对方开发的资源。则可以建立一台公共的计算机（私服），开发者将资源上传到该计算机，即可实现小范围内的资源共享；私服必须与中央服务器分离开

![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/30feea613e914c6795cda119bced1bed.png)

#### 9.2、私服搭建

**Nexus**：Sonatype公司的一款maven私服产品。

下载：https://help.sonatype.com/repomanager3/download

**安装、启动与配置**：

- 启动服务器（命令行启动）
  nexus.exe /run nexus
- 访问服务器（默认端口：8081）http://localhost:8081
- 修改基础配置信息
           安装路径下etc目录中nexus-default.properties文件保存有nexus基础配置信息，例如默认访问端口。

- 修改服务器运行配置信息
          安装路径下bin目录中nexus.vmoptions文件保存有nexus服务器启动对应的配置信息，例如默认占用内存空间。

#### 9.3、私服资源获取

![img](https://gitee.com/coi4/test/raw/master/img/1e27cfdee07c46459fc6be0b1f120451.png)

#### 9.4、仓库分类

**宿主仓库hosted**：保存无法从中央仓库获取的资源（自主研发/第三方非开源项目）![img](https://gitee.com/coi4/test/raw/master/img/320cd7574f9f4845a206f7e112e49428.png)

**代理仓库proxy**：代理远程仓库，通过nexus访问其他公共仓库，例如中央仓库。![img](https://gitee.com/coi4/test/raw/master/img/ecd44f7b8c6d4e90b97726bcf1397e37.png)

**仓库组group**：将若干个仓库组成一个群组，简化配置；仓库组不能保存资源，属于设计型仓库。![img](https://gitee.com/coi4/test/raw/master/img/0ab2a951f1924b5381132fa51e735811.png)

#### 9.5、手动资源上传

上传资源时应提供对应的信息：

- 保存的位置（宿主仓库）
- 资源文件
- 对应坐标

![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/be09d4b9a080405988fa1879d37331a5.png)

#### 9.6、idea环境中资源上传与下载

![在这里插入图片描述](https://gitee.com/coi4/test/raw/master/img/abd9f2c06cd34492915d49638dd47ef9.png)

#### 9.7、访问私服配置

**本地仓库访问私服**

- 配置本地仓库访问私服的权限（setting.xml）

  ```
  <servers>
  	<server>
  		<id>heima-release</id>
  		<username>admin</username>
  		<password>admin</password>
  	</server>
  	<server>
  		<id>heima-snapshots</id>
  		<username>admin</username>
  		<password>admin</password>
  	</server>
  </servers>
  ```

- 配置本地仓库资源来源（setting.xml）

  ```
  <mirrors>
  	<mirror>
  		<id>nexus-heima</id>
  		<mirrorOf>*</mirrorOf>
  		<url>http://localhost:8081/repository/maven-public/</url>
  	</mirror>
  </mirrors>
  ```

**项目工程访问私服**

- 配置当前项目访问私服上传资源的保存位置（pom.xml）

  ```
  <distributionManagement>
  	<repository>
  		<id>heima-release</id>
  		<url>http://localhost:8081/repository/heima-release/</url>
  	</repository>
  	<snapshotRepository>
  		<id>heima-snapshots</id>
  		<url>http://localhost:8081/repository/heima-snapshots/</url>
  	</snapshotRepository>
  </distributionManagement>
  ```

- 发布资源到私服命令
  mvn deploy

## 三、总结

1. 下载——仓库配置，idea创建项目（配置maven，Java工程，web工程，插件设置），配置依赖
2. 分模块操作(聚合，继承)
3. 多环境设置，跳过测试
4. 私服（下载，安装，搭建，私服获取资源，上传到私服，idea上/下，访问权限）

repositories：仓库

dependencies：依赖

build——plugins：插件

plugin：跳过测试

frofiles：环境

properties：自定义属性

