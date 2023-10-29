# maven

## 一、基础

### 1、简介

![image-20231024181136419](https://gitee.com/coi4/test/raw/master/img/image-20231024181136419.png)

![image-20231025103342679](https://gitee.com/coi4/test/raw/master/img/image-20231025103342679.png)

> 项目构建：提供标准的、跨平台的自动化项目构建方式
>
> 依赖管理：方便快捷的管理项目依赖的资源，避免资源间版本冲突问题
>
> 统一开发结构：提供标准的、统一的项目结构

### 2、下载与安装？

解压安装、环境变量的配置

### 3、基础概念（重）？

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
  - 默认位置：？
  - 自定义：

远程仓库配置（资源来源）：

镜像仓库配置：

setting文件的区别：

- 全局setting：定义了当前计算器中maven的公共配置
- 用户setting：定义了当前用户的配置

### 4、项目（重）

#### 4.1、手工？

##### 4.1.1、布置maven目录结构

![image-20231025113104447](https://gitee.com/coi4/test/raw/master/img/image-20231025113104447.png)

- src同层下创建pom.xml文件？

##### 4.1.2、常用项目构建命令？

- mvn开头，后面添加功能参数，可以一次执行多个命令，使用空格分隔
- ![image-20231025113744781](https://gitee.com/coi4/test/raw/master/img/image-20231025113744781.png)

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

- 存在兼容性问题，避免冲突，使用3.6.1版本？
- ![image-20231025115324785](https://gitee.com/coi4/test/raw/master/img/image-20231025115324785.png)
- ？

##### 4.2.2、手工创建Java项目？

- ![image-20231025115430380](https://gitee.com/coi4/test/raw/master/img/image-20231025115430380.png)
- 命令执行？

##### 4.2.3、原型创建Java项目

- ![image-20231025115534060](https://gitee.com/coi4/test/raw/master/img/image-20231025115534060.png)

##### 4.2.4、原型创建web项目

- ![image-20231025115548890](https://gitee.com/coi4/test/raw/master/img/image-20231025115548890.png)

##### 4.2.5、插件？

- Tomcat7安装与运行？
  - ![image-20231025115725677](https://gitee.com/coi4/test/raw/master/img/image-20231025115725677.png)
- 运行web项目

### 5、依赖管理（重）

依赖指当前项目运行所需的jar，一个项目可设置多个依赖

依赖配置

- ![image-20231025120139397](https://gitee.com/coi4/test/raw/master/img/image-20231025120139397.png)

依赖传递

- 直接传递：当前项目中通过依赖配置建立的依赖关系
- 间接传递：被资源的资源如果依赖其他资源，当前项目间接依赖其他资源

可选依赖

排除依赖

依赖范围

### 6、生命周期与插件

## 二、高级

