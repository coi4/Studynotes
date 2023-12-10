# Docker

## 1、初识

软件环境迁移问题（开发环境，测试环境，生产环境）

Dockers是一个开源的应用容器引擎，基于go实现；可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的Linux机器上；17.03版本之后分为CE版本（社区版）和EE版本（企业版）

容器是完全使用沙箱机制，相互隔离；容器性能开销极低；

安装：基于CentOS7安装https://www.docker.com

架构：

-  镜像（image）：相当于是一个root文件系统。比如官方镜像ubuntu：16.04就包含了完整的一套Ubuntu16.04最小系统的root文件系统
- 容器（Container）：镜像和容器的关系就像是面对对象程序设计中的类和对象一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等等
- 仓库（Repository）：仓库可看成一个代码控制中心用来保存镜像

配置Dockers镜像加速器：默认情况下，将来从docker hub（https://hub.docker.com/）上下载docker的镜像，太慢，一般都会配置镜像加速器

- USTC：中科大镜像加速器（https://docker.mirrors.ustc.edu.cn）
- 阿里云
- 网易云
- 腾讯云

## 2、命令

进程相关命令：

- 启动docker服务：

  ```
  systemctl start docker
  ```

- 停止

  ```
  systemctl stop docker
  ```

- 重启

  ```
  systemctl restart docker
  ```

- 查看状态

  ```
  systemctl status docker
  ```

- 开机启动

  ```
  systemctl enable docker
  ```

镜像相关命令

- 查看镜像

  ```
  docker images
  docker images –q # 查看所用镜像的id
  ```

- 搜索镜像

  ```
  docker search 镜像名称
  ```

- 拉取镜像：从Docker仓库下载镜像到本地，镜像名称格式为 名称:版本号，如果版本号不指定则是最新的版本。如果不知道镜像版本，可以去docker hub 搜索对应镜像查看。

  ```
  docker pull 镜像名称
  ```

- 删除镜像

  ```
  docker rmi 镜像id # 删除指定本地镜像
  docker rmi `docker images -q` # 删除所有本地镜像
  ```

容器相关命令

- 查看容器

  ```
  docker ps # 查看正在运行的容器
  docker ps –a # 查看所有容器
  ```

- 创建并启动容器

  ```
  docker run 参数
  ```

  - 参数说明
    -  -i：保持容器运行。通常与 -t 同时使用。加入it这两个参数后，容器创建后自动进入容器中，退出容器后，容器自动关闭。
    -  -t：为容器重新分配一个伪输入终端，通常与 -i 同时使用。
    -  -d：以守护（后台）模式运行容器。创建一个容器在后台运行，需要使用docker exec 进入容器。退出后，容器不会关闭。
    -  -it 创建的容器一般称为交互式容器，-id 创建的容器一般称为守护式容
    -  --name：为创建的容器命名。

- 进入容器

  ```
  docker exec 参数 # 退出容器，容器不会关闭
  ```

- 停止容器

  ```
  docker stop 容器名称
  ```

- 启动

  ```
  docker start 容器名称
  ```

- 删除：如果容器是运行状态则删除失败，需要停止容器才能删除

  ```
  docker rm 容器名称
  ```

- 查看信息

  ```
  docker inspect 容器名称
  ```

## 3、容器数据卷

数据卷是宿主机中的一个目录或文件；当容器目录和数据卷目录绑定后，对方的修改会立即同步；一个数据卷可以被多个容器同时挂载；一个容器也可以被挂载多个数据卷![image-20231204172141012](https://gitee.com/coi4/test/raw/master/img/image-20231204172141012.png)

数据卷作用：

- 容器数据持久化
- 外部机器和容器间接通信
- 容器之间数据交换

配置

- 创建启动容器时，使用 –v 参数 设置数据卷

  ```
  docker run ... –v 宿主机目录(文件):容器内目录(文件) ...
  ```

- 目录必须是绝对路径

- 如果目录不在，会自动创建

- 可以挂载多个数据卷

配置数据卷容器：多容器进行数据交换（多个容器挂载一个数据卷）

- 创建一个容器，挂载一个目录，让其他容器继承自该容器

- 创建启动c3数据卷容器，使用 –v 参数 设置数据卷

  ```
  docker run –it --name=c3 –v /volume centos:7 /bin/bash
  ```

- 创建启动 c1 c2 容器，使用 –-volumes-from 参数 设置数据卷

  ```
  docker run –it --name=c1 --volumes-from c3 centos:7 /bin/bash
  docker run –it --name=c2 --volumes-from c3 centos:7 /bin/bash
  ```

## 4、应用部署

MySQL部署：在Docker容器中部署MySQL，并通过外部mysql客户端操作MySQL Server。

- 步骤
  - 搜索mysql镜像
  -  拉取mysql镜像
  -  创建容器
  -  操作容器中的mysql
- 端口映射：容器内的网络服务和外部机器不能直接通信；外部机器和宿主机可以直接通信；宿主机和容器可以直接通信；当容器中的网络服务需要被外部机器访问时，可以将容器中提供服务的端口映射到宿主机的端口上。外部机器访问宿主机的该端口，从而间接访问容器的服务。

Tomcat部署：在Docker容器中部署Tomcat，并通过外部机器访问Tomcat部署的项目。

- 步骤
  -  搜索tomcat镜像
  -  拉取tomcat镜像
  -  创建容器
  -  部署项目
  -  测试访问

Nginx部署：在Docker容器中部署Nginx，并通过外部机器访问Nginx。

- 步骤
  - 搜索Nginx镜像
  -  拉取Nginx镜像
  -  创建容器
  -  测试访问

Redis部署：在Docker容器中部署Redis，并通过外部机器访问Redis。

- 步骤
  -  搜索Redis镜像
  -  拉取Redis镜像
  -  创建容器
  -  测试访问

## 5、Dockerfile

操作系统组成部分：

- 进程调度子系统
- 进程通信子系统
- 内存管理子系统
- 设备管理子系统
- 文件管理子系统
- 网络通信子系统
- 作业控制子系统

Linux文件系统由bootfs和rootfs两部分组成

- bootfs：包含bootloader（引导加载程序）和kernel（内核）
- rootfs：root文件系统，包含的就是典型Linux系统中的/dev，/proc，/bin，/etc等标准目录文件
- 不同的Linux发行版，bootfs基本一样，而rootfs不同，如ubuntu，centos等

Docker镜像是由特殊的文件系统叠加而成，最低端是bootfs，并使用宿主机的bootfs，第二层是root文件系统rootfs，称为base image，再往上可以叠加其他的镜像文件；同一文件系统技术能够将不同层整合成一个文件系统，为这些层提供了一个统一的视角，这样就隐藏了多层的存在，在用户看来，只存在一个文件系统；

一个人镜像可以放在另一个镜像的上面，位于下面的镜像。称为父镜像，最底部的镜像成为基础镜像；当从一个镜像启动容器时，docker会在最顶层加载一个读写文件系统成为容器（复用）![image-20231204174618561](https://gitee.com/coi4/test/raw/master/img/image-20231204174618561.png)

镜像本质是一个分层文件系统

Docker 中一个centos镜像为什么只有200MB，而一个centos操作系统的iso文件要几个个G：Centos的Iiso镜像文件包含bootfs和rootfs，centos镜像复用bootfs，只有rootfs和其他镜像层

Docker 中一个tomcat镜像为什么有500MB，而一个tomcat安装包只有70多MB：由于docker中镜像是分层的，tomcat虽然只有70多MB，但他需要依赖于父镜像和基础镜像，所有整个对外暴露的tomcat镜像大小500多MB

镜像制作

- 容器转为镜像

  ```
  docker commit 容器id 镜像名称:版本号
  docker save -o 压缩文件名称 镜像名称:版本号
  docker load –i 压缩文件名称
  ```

- dockerfile：一个文本文件；包含一条条的指令，每一条指令构建一层，基于基础镜像，最终构建出一个新的镜像

  - 对于开发人员：可以为开发团队提供一个完全一致的开发环境
  - 测试人员：可以直接拿开发时所构建的镜像或通过Dockerfile文件构建一个新的镜像开始工作
  - 运维人员：部署时，可以实现应用的无缝移植

关键字：查看 文档目录中的《dockerfile.md》

案例：

需求：自定义centos7镜像。要求： 默认登录路径为 /usr； 可以使用vim

步骤：

- 定义父镜像：FROM centos:7
- 定义作者信息：MAINTAINER itheima <itheima@itcast.cn>
-  执行安装vim命令： RUN yum install -y vim
-  定义默认的工作目录：WORKDIR /usr
-  定义容器启动执行的命令：CMD /bin/bash
-  通过dockerfile构建镜像：docker bulid –f dockerfile文件路径 –t 镜像名称:版本

需求：定义dockerfile，发布springboot项目

步骤：

-  定义父镜像：FROM java:8
-  定义作者信息：MAINTAINER itheima <itheima@itcast.cn>
-  将jar包添加到容器： ADD springboot.jar app.jar
-  定义容器启动执行的命令：CMD java–jar app.jar
-  通过dockerfile构建镜像：docker bulid –f dockerfile文件路径 –t 镜像名称:版本

## 6、服务编排

服务编排：按照一定业务规则批量管理容器

微服务架构的应用系统中一般包含若干个微服务，每一个微服务一般都会部署多个实例，如果每一个微服务都需要手动启停，维护工作量大

- 从Dockerfile build image或者去dockerhub拉取image
- 创建多个container
- 管理这些container（启动停止删除）

Docker Compose：编排多容器分布式部署的工具，提供命令集管理容器化应用的完整开发周期

- 利用dockerfile定义运行环境镜像
- 使用docker-compose.yml定义组成应用的各服务
- 运行docker-composo up 启动应用

docker-compose安装使用：《docker-compose.md》

案例

## 7、私有仓库

Docker hub（https://hub.docker.com）：公共镜像仓库

无法访问互联网，不希望将自己的镜像放到公网当中——搭建自己的私有仓库来存储和管理自己的镜像

## 8、相关概念

docker容器虚拟化与传统虚拟机比较

- 相同：
  - 具有相似的资源隔离和分配优势
- 不同：
  - 容器虚拟化的是操作系统，虚拟机虚拟化的是硬件
  - 传统虚拟机可以运行不同的操作系统，容器只能运行同一类型操作系统

![image-20231204181315453](https://gitee.com/coi4/test/raw/master/img/image-20231204181315453.png)

![image-20231204181327216](https://gitee.com/coi4/test/raw/master/img/image-20231204181327216.png)

容器就是将软件打包成标准化单元，以用于开发、交付和部署

- 容器镜像是轻量的、可执行的独立软件包
- 容器化软件在任何环境中都能始终如一的运行
- 容器赋予了软件独立性（免受外在环境差异的影响

![image-20231204181108958](https://gitee.com/coi4/test/raw/master/img/image-20231204181108958.png)

