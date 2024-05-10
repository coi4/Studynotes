# Linux

## 一、初识

### 1、操作系统概述

计算机=硬件+软件

> 硬件：计算机系统中由电子、机械和光电元件等组成的各种物理装置的总称
>
> 软件：用户和计算机硬件之间的接口和桥梁，用户通过软件与计算机进行交流

操作系统是软件的一类

![image-20231123093911920](https://gitee.com/coi4/test/raw/master/img/image-20231123093911920.png)

主要负责：作为用户和计算机硬件之间的桥梁，**调度和管理**计算机硬件进行工作

- 用户使用操作系统，操作系统安排硬件干活
- 没有操作系统，计算机就是一堆无法使用的塑料

常见操作系统：

- PC端：windows 、Linux、macOS
- 移动端：Android、ios、HarmonyOS

### 2、初识Linux

林纳斯 托瓦兹大学期间觉得Linux不好用，自己写！！！

Linux系统组成部分：Linux系统内核+系统级应用程序

> 内核提供系统最核心的功能：调度CPU、调度内存、调度文件系统、调度网络通讯、调度IO...
>
> 系统应用程序：出厂自带程序（文件管理器、任务管理器、图片查看、音乐播放等）

内核与系统级应用程序关系示例：

- 无论是自带音乐播放器还是自行安装的第三方播放器，均是由播放器程序，调用内核提供的相关功能，由内核调度CPU解码、音响发声等


http://www.kernek.org上下载内核，

免费开源，有很多发行版

> 发行版：内核上，封装系统级应用程序，组合在一起就是发行版
>
> - 基础命令100%相同，部分操作不同（如软件安装）

### 3、虚拟机介绍

![image-20231123165144210](https://gitee.com/coi4/test/raw/master/img/image-20231123165144210.png)

借助虚拟化技术，可以在系统中，**通过软件，模拟计算机硬件**，并**给虚拟硬件安装真实的操作系统**，这样就可以在电脑中，虚拟出一个完整的电脑，以供我们学习Linux系统

### 4、VMware WorkStation安装

通过虚拟化的软件来获得虚拟机

下载地址：http://www.vmware.com/cn/products/woekstation-pro.html(下载试用版)

安装：![image-20231123170341212](https://gitee.com/coi4/test/raw/master/img/image-20231123170341212.png)

![image-20231123170404995](https://gitee.com/coi4/test/raw/master/img/image-20231123170404995.png)

网络和internet高级网络设置中或通过快捷键：win+r输入ncpa.cpl回车即可打开

### 5、VMware上安装Linux

下载CentOS操作系统（Linux发行版）：

- 下载操作系统的安装文件，CentOS7.6版本![image-20231123170713959](https://gitee.com/coi4/test/raw/master/img/image-20231123170713959.png)
  - 下载链接http://vault.centos.org/7.6.1810/isos/x86_64/CentOS-7-x86_64-DVD-1810.iso
  - 课程资料中
- 安装：
  - 打开VMware![image-20231123171057307](https://gitee.com/coi4/test/raw/master/img/image-20231123171057307.png)
  - 按照步骤创建虚拟机，等待(完成后及开启了CentOS系统的安装）![image-20231123171219703](https://gitee.com/coi4/test/raw/master/img/image-20231123171219703.png)
  - 点击用户名，输入密码![image-20231123171340218](https://gitee.com/coi4/test/raw/master/img/image-20231123171340218.png)

### 6、远程连接Linux系统

对于操作系统的使用：

- 图形化页面使用操作系统：以图形化反馈的形式去使用操作系统
- 以命令形式使用：以获得字符反馈的形式去使用

Linux一般使用命令行（都可以）！

VMware可以得到Linux虚拟机，但是在**VMware上操作Linux命令行不太方便**（复制粘贴，上传下载等跨越VMware不方便（和Linux系统的各类交互，跨越VMware不方便），所以选择使用——FinalShell——远程连接到Linux上

下载地址：http://www.hostbuf.com/downloads/finalshell_install.exe（下载后双击打开）

安装：按照提示一直下一步![image-20231123172729049](https://gitee.com/coi4/test/raw/master/img/image-20231123172729049.png)

连接到Linux系统：

- 查询Linux的ip地址：在Linux操作系统中，桌面空白右键点击：open in terminal，输入ifconfig![image-20231123172848441](https://gitee.com/coi4/test/raw/master/img/image-20231123172848441.png)

- 打开Finshell，配置到Linux的连接：![image-20231123173231465](https://gitee.com/coi4/test/raw/master/img/image-20231123173231465.png)

  ![image-20231123173252333](https://gitee.com/coi4/test/raw/master/img/image-20231123173252333.png)

- 打开连接管理器

  ![image-20231123173416111](https://gitee.com/coi4/test/raw/master/img/image-20231123173416111.png)

- 点击接受并保存：![image-20231123173532744](https://gitee.com/coi4/test/raw/master/img/image-20231123173532744.png)

- 连接成功：

  ![image-20240402095815190](https://gitee.com/coi4/test/raw/master/img/image-20240402095815190.png)

Linux虚拟机如果重启，有可能，发生ip改变，如果改变，需要在FinalShell中修改连接的IP地址

### #WSL

功能：可获得Ubuntu系统（Linux发行版）环境

WSL作为Windows10系统带来的全新特点，正在逐步颠覆开发人员既有的选择——使用WSL可以以非常轻量化的方式，得到Linux系统环境

WSL：Windows Subsystem for Linux，是**用于Windows系统之上的Linux子系统**，**可以在Windows系统中获得Linux系统环境**，并完全直连计算机硬件，**无需通过虚拟机虚拟硬件**

![image-20231123175352527](https://gitee.com/coi4/test/raw/master/img/image-20231123175352527.png)

WSL是**Windows10自带**功能，**需要开启，无需下载**

- ![屏幕截图 2023-11-27 094127](https://gitee.com/coi4/test/raw/master/img/202311270944370.png)![屏幕截图 2023-11-27 094146](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-27%20094146.png)



- 点击确定后会进行部署，最后重启即可


- 打开Windows应用商店，搜索Ubuntu![image-20231127094647423](https://gitee.com/coi4/test/raw/master/img/image-20231127094647423.png)


- 点击获取并安装，点击启动


- 输入用户名创建用户，输入两次密码确认![image-20231127094818266](https://gitee.com/coi4/test/raw/master/img/image-20231127094818266.png)![image-20231127094834409](https://gitee.com/coi4/test/raw/master/img/image-20231127094834409.png)


Ubuntu自带终端窗口软件不太好用，使用terminal（应用商店搜）![image-20231127095034755](https://gitee.com/coi4/test/raw/master/img/image-20231127095034755.png)

- 安装![image-20231127095118426](https://gitee.com/coi4/test/raw/master/img/image-20231127095118426.png)![image-20231127095132166](https://gitee.com/coi4/test/raw/master/img/image-20231127095132166.png)


- 再次打开terminal，即默认使用Ubuntu系统（WSL）


WSL虽然好用，但是是直连我们自己的电脑的，**如果误操作可能带来重要文件的丢失甚至损坏系统！！！**

### #虚拟机快照

学习时无法避免**损坏Linux操作系统**，重新安装很麻烦，VMware（Workstation（Windows版）和Funsion（Mac版）支持为虚拟机制作快照，通过快照将当前虚拟机的状态保存下来，以后可以通过快照恢复虚拟机到保存的状态

在VMware worktation中制作并还原快照

![image-20231127095737865](https://gitee.com/coi4/test/raw/master/img/image-20231127095737865.png)

快照**制作**需要虚拟机**关机状态下**（不关机比较慢）

## 二、基础命令

### 1、目录结构

树型结构，没有盘符，只有一个**根目录/**，所有文件都在它下面

路径之间的层级关系，使用：/来表示（Windows使用‘\’)![屏幕截图 2023-11-27 181344](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-27%20181344.png)

![屏幕截图 2023-11-27 181352](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-27%20181352.png)

### 2、命令入门

命令通用格式：![image-20231127182046499](https://gitee.com/coi4/test/raw/master/img/image-20231127182046499.png)

command：命令本身

> ls命令：**列出目录下的内容**
>
> ![image-20231127182229358](https://gitee.com/coi4/test/raw/master/img/image-20231127182229358.png)
>
> - -a：all，**列全部（包括隐藏**（以.开头的文件\文件夹会自动隐藏））
>
> - -l：**以列表（竖向排列）形式展示**内容，并展示更多信息（与图形化类似）
>
> - 组合：ls -l -a或ls -la或ls -al
>
> - -h：以易于阅读的形式**列出文件大小**，K、M、G（必须搭配-l使用）
>
> - 可-alh
>
> - Linux路径是此命令可选的参数，当**不使用选项和参数**，直接使用ls命令本体，表示以**平埔**形式列出当前工作目录下的内容（**HOME目录**）；
>
>   > HOME目录：个人账户目录；/home/用户名
>
>   VMware中图形化界面查看
>
>   ![屏幕截图 2023-11-30 163926](https://gitee.com/coi4/test/raw/master/img/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-30%20163926.png)
>
> cd/pwd：**目录切换**相关命令
>
> - cd（change directory）后面不跟参数，则默认切回HOME目录![image-20231130165000126](https://gitee.com/coi4/test/raw/master/img/image-20231130165000126.png)
>   - 相对路径：以当前目录为起点（无需以/开头）
>   - 特殊路径字符：
>     - . ：表示当前目录，cd ./Desktop与cd Desktop效果一样
>     - .. ：表示上一级目录，cd ..切换到上一级目录，cd ../.. 切换到上二级目录
>     - ~ :表示HOME目录,cd ~ /Desktop即可切换到HOME内的Desktop
> - pwd（print work directory）**查看当前工作目录**；直接输入无参数
>
> mkdir：make directory**创建目录（文件夹）**
>
> - mkdir [-p] Linux路径
> - 参数必填，-p可选（表示**自动创建**不存在的父目录，适用于创建连续多层级的目录）
> - 创建文件夹需要修改权限，确保**操作均在**HOME目录内（外需要获取权限）

文件操作命令：

> touch：**创建文件**； touch Linux路径
>
> cat：**查看文件内容**；cat Linux路径![image-20231130170226436](https://gitee.com/coi4/test/raw/master/img/image-20231130170226436.png)
>
> more：**查看文件内容**；cat直接将内容全部显示出来，**more支持翻页**（空格翻页，通过q退出查看）
>
> cp：**复制文件、文件夹**；cp [-r] 参数1 参数2
>
> - -r ：递归（**复制文件夹必须使用**）
> - 参数1：被复制的文件或文件夹路径
> - 参数2：要复制去的地方的路径
>
> mv：**移动**文件或文件夹；mv 参数1 参数2
>
> - 参数2：如果目标不存在，则进行改名，确保目标存在（对要移动的文件改名）![image-20231130171614812](https://gitee.com/coi4/test/raw/master/img/image-20231130171614812.png)
>
> rm：**删除文件、文件夹**（谨慎使用）；rm [-r -f] 参数1 参数2 ...参数N
>
> - ![image-20231201104913550](https://gitee.com/coi4/test/raw/master/img/image-20231201104913550.png)
>
> - -r用于删除文件夹
> - -f强制删除(普通用户删除内容不会弹出提示,只有root管理员用户删除内容会有提示;一般用户用不到-f)
> - 参数N表示要删除的文件或文件夹路径,按照空格隔开
> - 可以通过su - root,并输入密码123456临时切换到root用户体验
> - 通过exit,退回普通用户(临时用root,用完要退出,不要一直用)
> - 支持*：模糊匹配![image-20231201104807000](https://gitee.com/coi4/test/raw/master/img/image-20231201104807000.png)
>
> which：**查找一系列命令的程序文件放在哪里**（每一个命令的本体都是二进制可执行程序.exe）；which cd（查询cd命令二进制文件存放地址）
>
> find：**按文件名查找文件**；find / -name "test"![image-20231201105411284](https://gitee.com/coi4/test/raw/master/img/image-20231201105411284.png)
>
> - 可切换到root用户获得最大权限
> - 支持*
> - ![image-20231201105725230](https://gitee.com/coi4/test/raw/master/img/image-20231201105725230.png)
>   - find / -size -10k
>   - +、-表示大于和小于
>   - n表示大小数字
>   - kMG表示大小单位（kb、MB、GB）
>
> grep：**过滤文件内容(**从文件中通过关键字过滤文件行)；grep "itheima" iheima.txt![image-20231201110039862](https://gitee.com/coi4/test/raw/master/img/image-20231201110039862.png)
>
> - -n表示在结果中显示匹配的行的行号
> - 关键字：带有空格或其它特殊符号，建议用“”将关键字包围
> - 文件路径可作为内容输入端口
> - ![image-20231201110547564](https://gitee.com/coi4/test/raw/master/img/image-20231201110547564.png)
>
> wc：**统计内容数量**(统计文件的行数、单词数量等)![image-20231201110628459](https://gitee.com/coi4/test/raw/master/img/image-20231201110628459.png)
>
> - -c：统计bytes数量
> - -m：统计字符数量
> - -l：统计行数
> - -w：统计单词数量
> - ![image-20231201110811296](https://gitee.com/coi4/test/raw/master/img/image-20231201110811296.png)

管道符：特殊符号 | ；将管道符左边命令的结果，作为右边命令的输入![image-20231201110959474](https://gitee.com/coi4/test/raw/master/img/image-20231201110959474.png)

![image-20231201111046823](https://gitee.com/coi4/test/raw/master/img/image-20231201111046823.png)

![image-20231201111432328](https://gitee.com/coi4/test/raw/master/img/image-20231201111432328.png)

> echo：在命令行内**输出指定内容**；复杂内容用“”![image-20231201111605073](https://gitee.com/coi4/test/raw/master/img/image-20231201111605073.png)
>
> ![  ](https://gitee.com/coi4/test/raw/master/img/image-20231201111653977.png)
>
> - 反引号（飘号）`：echo pwd只能输出内容pwd，反引号将其包围，会被作为命令执行
> - 重定向符：>和>>；`echo "Hello Linux" > itheima.txt`（文件中的内容变为“Hello，，”）
>   - ">"：将左侧命令的结果,**覆盖**到符号右侧指定文件中
>   - ">>"：将左侧命令结果，追加**写入**到符号右侧指定文件中
>
> tail：**查看文件尾部内容**，跟踪文件的最新更改![image-20231201112703724](https://gitee.com/coi4/test/raw/master/img/image-20231201112703724.png)
>
> - -f：表示持续跟踪
> - -num：表示查看尾部多少行，不填默认10行；`tail -3 /var/log/vm ware-network.log`![image-20231201113002539](https://gitee.com/coi4/test/raw/master/img/image-20231201113002539.png)

![image-20231201115157836](https://gitee.com/coi4/test/raw/master/img/image-20231201115157836.png)

### 3、vi编辑器

visual interface简称,Linux中最经典的文本编辑器

> vim编辑器：vim是vi的加强版本,兼容vi的所有指令,还有shell程序编辑的功能,可以不同颜色的字体辨别语法的正确性
>

三种工作模式:

- 命令模式：所敲的按键编辑器都理解为命令，以命令驱动执行不同的功能，此模式下，**不能自由进行文本编辑**
- 输入模式：可以对文件内容进行自由编辑
- 底线命令模式：以：开始，通常用于**文件的保存、退出**

![image-20231201122743296](https://gitee.com/coi4/test/raw/master/img/image-20231201122743296.png)

进入vi编辑器会进入命令模式。通过命令模式输入键盘指令，可以进入输入模式。输入模式需要退回到命令模式，然后通过命令可以进入底线命令模式![image-20231201140959772](https://gitee.com/coi4/test/raw/master/img/image-20231201140959772.png)

![image-20231201141021688](https://gitee.com/coi4/test/raw/master/img/image-20231201141021688.png)

![image-20231201141110307](https://gitee.com/coi4/test/raw/master/img/image-20231201141110307.png)

![image-20231201141120500](https://gitee.com/coi4/test/raw/master/img/image-20231201141120500.png)

![image-20231201141158958](https://gitee.com/coi4/test/raw/master/img/image-20231201141158958.png)

如果需要通过vi/vim编辑器编辑文件，通过如下命令：![image-20231201140713762](https://gitee.com/coi4/test/raw/master/img/image-20231201140713762.png)

如果文件路径表示文件不存在，此命令会用于编辑新文件，存在则编辑已有文件

查看命令帮助和手册：

- --help，查看命令的帮助；`ls --help`(列出ls命令的帮助文档)

- man ，如果想要查看命令的详细手册,可以通过man命令查看；`man ls`（查看ls命令的详细手册）

全英文，阅读吃力，通过重定向符`man ls > ls-man.txt`，输出手册到文件，通过翻译软件翻译内容查看

## 三、用户和权限

### 1、认识root用户

root用户：超级管理员；拥有最大权限的账户名

每一个操作系统，均采用多用户的管理模式进行权限管理

一旦出了HOME目录，大多数地方，普通用户仅有只读和执行权限，无修改权限

> su：switch user用于账户切换的系统命令![image-20231203143159860](https://gitee.com/coi4/test/raw/master/img/image-20231203143159860.png)
>
> - "-"表示是否在切换用户后加载环境变量，建议带上
> - 用户名，表示要切换的用户，省略表示切换到root
> - 切换后可通过exit命令退回上一个用户，也可以ctrl+d
> - 使用普通用户，切换到其他用户需要输入密码，如切换到root用户
> - 使用root用户切换到其他用户，无需密码，直接切换
>
> sudo：普通的命令授权，**临时**以root身份执行；可为这一条命令临时赋予root授权![image-20231203143655078](https://gitee.com/coi4/test/raw/master/img/image-20231203143655078.png)
>
> - 不是所有的用户，都有权利使用sudo，需要为普通用户**配置sudo认证**
>   - 切换到root用户，执行`visudo`命令，会自动通过vi编辑器打开：/etc/sudoers
>   - 在文件的最后添加![image-20231203144013780](https://gitee.com/coi4/test/raw/master/img/image-20231203144013780.png)
>     - NOPASSWD:ALL表示使用sudo命令，无需输入密码
>   - 最后通过wq保存
>   - 切换回普通用户![image-20231203144205863](https://gitee.com/coi4/test/raw/master/img/image-20231203144205863.png)
>   - 执行的命令，均以root运行

### 2、用户、用户组管理

用户可以加入多个用户组

Linux中关于权限的管控级别有2个级别（针对某文件，可以控制用户的权限，也可以控制用户组的权限）

- 针对用户的权限控制
- 针对用户组的权限控制

用户组管理：

以下命令需**root用户执行**

> groupadd 用户组名：创建用户组
>
> groupdel 用户组名：删除用户组
>
> useradd [-g -d] 用户名：创建用户
>
> - -g指定用户组，不指定-g，会**创建同名组**并自动加入，指定-g需要组已经存在，如**已存在同名组，必须使用-g**
> - -d：指定用户HOME路径，不指定，HOME目录默认在：/home/用户名
>
> userdel [-r] 用户名：删除用户
>
> - -r删除用户的HOME目录，不使用-r，删除用户时，HOME目录保留
>
> id[用户名]：**查看**用户所属组，如果不提供用户名则查看自身
>
> usermod -aG 用户组 用户名：将指定用户**加入**指定用户组
>
> getent：**查看**当前系统中有哪些用户/组![image-20231203145641200](https://gitee.com/coi4/test/raw/master/img/image-20231203145641200.png)
>
> ![image-20231203145759881](https://gitee.com/coi4/test/raw/master/img/image-20231203145759881.png)
>
> ![image-20240402143045526](https://gitee.com/coi4/test/raw/master/img/image-20240402143045526.png)
>
> ![image-20231203145732662](https://gitee.com/coi4/test/raw/master/img/image-20231203145732662.png)
>
> ![image-20240402143139028](https://gitee.com/coi4/test/raw/master/img/image-20240402143139028.png)
>
> ![image-20231203145813966](https://gitee.com/coi4/test/raw/master/img/image-20231203145813966.png)

### 3、查看权限控制

认知权限信息

通过ls -l 可以以列表形式查看内容，并显示权限细节

![image-20231203145953445](https://gitee.com/coi4/test/raw/master/img/image-20231203145953445.png)

序列1![image-20231203150318198](https://gitee.com/coi4/test/raw/master/img/image-20231203150318198.png)

![image-20231203150357030](https://gitee.com/coi4/test/raw/master/img/image-20231203150357030.png)

![image-20231203150441875](https://gitee.com/coi4/test/raw/master/img/image-20231203150441875.png)

![image-20240402143640743](https://gitee.com/coi4/test/raw/master/img/image-20240402143640743.png)

### 4、修改权限控制

> chmod：**修改**文件、文件夹的**权限**信息（只有文件、文件夹的所属用户或root用户可以修改）![image-20231203150915958](https://gitee.com/coi4/test/raw/master/img/image-20231203150915958.png)
>
> - -R对文件夹内全部内容应用同样的操作
> - ![image-20231203151232189](https://gitee.com/coi4/test/raw/master/img/image-20231203151232189.png)
> - ![image-20231203151246884](https://gitee.com/coi4/test/raw/master/img/image-20231203151246884.png)
> - ![image-20231203151308110](https://gitee.com/coi4/test/raw/master/img/image-20231203151308110.png)
> - ![image-20231203151356087](https://gitee.com/coi4/test/raw/master/img/image-20231203151356087.png)
>
> chown：**修改**文件、文件夹的**所属**用户和用户组（普通用户无法修改所属为其他用户或组，此命令只适用于root用户执行）![image-20231203151550913](https://gitee.com/coi4/test/raw/master/img/image-20231203151550913.png)
>
> - -R：同chmod，对文件内全部内容应用相同规则
> - 用户：修改所属用户
> - 用户组：修改所属用户组
> - ：：用于分隔
>
> ![image-20231203151635392](https://gitee.com/coi4/test/raw/master/img/image-20231203151635392.png)

## #总结

可选择下载VMware Workstation虚拟机下载CentOS操作系统（下载虚拟机、CentOS和FinalShell，查看网络适配器是否正常，VMware连接，查询Linux的IP地址，FinalShell连接）；或选择WSL中配置Ubuntu系统

基础指令（ls，cd，pwd，mkdir，/touch，cat，more，cp，mv，rm，which，find，/grep，wc，echo，tail）

权限命令（su，sudo，/groupadd，groupdel，useradd，userdel，id，usermod -aG，getent passwd，getent group，/chmod，chown）

Vi编辑器使用vi 文件名，i，esc，：，wq；



## 四、实用操作

### 1、快捷键

> ctrl+c：强制停止
>
> - 终止程序的运行
> - 命令输入错误，退出，重新输入
>
> ctrl+d：退出或登出
>
> - 退出帐户
> - 退出某些特定程序的专属页面（不能退出vi/vim
>
> history：查看历史输入命令
>
> ！命令前缀：自动执行上一次匹配前缀的命令（自动匹配上一个命令）（如！py 匹配python）
>
> ctrl+r：输入内容去匹配历史命令
>
> - 如果搜索的内容是需要的，回车直接执行；键盘左右键可以得到但不执行
>
> ctrl+a：跳到命令开头
>
> ctrl+e：跳到结尾
>
> +键盘左键：向左跳一个单词
>
> +右键。。。
>
> +l：清空终端内容（等同于clear命令）

### 2、软件安装

安装包：

- win系统：exe文件、msi文件
- mac系统：dmg文件、pkg文件

应用商店：

- win：Microsoft store
- mac：Appstore
- Linux：yum命令（Linux命令行内的应用商店）

> yum：RPM包软件管理器，用于自动化安装配置Linux软甲，并自动解决依赖问题
>
> - `yum [-y] [install | remove | search] 软件名称`
>   - -y ：自动确认，无需确认安装或卸载过程
>   - remove：卸载
>   - search：搜索；是否有
>   - yum命令需要root权限，需要联网
>
> apt：Ubuntu的包管理器
>
> - `apt [-y] ,,,,`

### 3、systemctl

控制软件的启动和关闭

能够被sytemctl管理的软件，一般称之为服务

> `systemctl start |stop | status |enable |disable 服务名`
>
> - status：查看状态
> - enable：开启开机自启
> - disable：关闭开机自启
>

系统内置的服务：

- NetworkManager：主网络服务
- network：副网络服务
- firewalld：防火墙服务
- sshd：ssh服务

除了内置的服务，部分第三方软件安装后也可以以systemctl进行控制（自动注册）

- > yum install -y ntp：可以通过ntpd 服务名，配合systemctl进行控制

### 4、软连接

创建软连接，可以将文件、文件夹链接到其他位置（快捷方式）

> ` ln -s 参数1 参数2`
>
> - -s：创建软连接
> - 参数1：被链接的文件或文件夹
> - 参数2：要链接去的目的地
>

### 5、日期、时区

查看系统时间

`date [-d] [+ 格式化字符串]`

- -d：按照给定的字符串显示日期，一般用于日期计算

  ![image-20240403172859598](https://gitee.com/coi4/test/raw/master/img/image-20240403172859598.png)

- 格式化字符串：通过特定的字符串标记，来控制显示的日期格式（如果中间有空格，要使用双引号）

  ![image-20240403172707968](https://gitee.com/coi4/test/raw/master/img/image-20240403172707968.png)

修改Linux时区(使用root权限，执行如下命令)

`rm -f /etc/localtime`

`sudo ln -s /user/share/zoneinfo/Asia/Shanghai  /etc/localtime`

ntp程序：自动校准系统时间

`yum -y install ntp`

`systemctl start ntpd`

`systemctl enable ntpd`

手动校准（需root权限）：`ntpdate -u ntp.aliyun.com`

- 通过阿里云提供的服务网址配合ntpdate命令自动校准

6、IP地址、主机名

IP地址（对外联络地址）主要有2个版本：V4，V6（V6少用）

IPv4版本的地址格式：a.b.c.d（表示0~255的数字）

可以通过ifcofig查看本机的IP地址，如果无法使用该命令，可以安装：yum -y install net-tools

> 127.0.0.1：指代本机
>
> 0.0.0.0：可以用于指代本机；可以在端口绑定中用来确定绑定关系；在一些ip地址限制中，表示所有ip的意思（放行规则设置为，表示允许任意ip访问）

主机名：主机的名称，用于标识一个计算机

hostname查看

hostnamectl set-hostname 主机名，修改（需root）

重新登陆FinalShell即可看到已修改（@后面即为）

域名（网址）解析：通过ip地址访问服务器，麻烦，用域名（主机名或替代的字符地址）代替（通过主机名找到对应计算机的ip地址）

- 解析过程：先查看本机的记录（私人地址本），在联网去DNS服务器询问![image-20240406163038061](https://gitee.com/coi4/test/raw/master/img/image-20240406163038061.png)

配置主机名映射：FinalShell通过ip地址连接到Linux服务器，如何通过域名连接

- 在Windows的host文件中配置记录![image-20240406163229459](https://gitee.com/coi4/test/raw/master/img/image-20240406163229459.png)

  ![image-20240406163247861](https://gitee.com/coi4/test/raw/master/img/image-20240406163247861.png)

虚拟机配置固定IP：

当前虚拟机的Linux，其ip地址是通过DHCP服务获取的

> DHCP：动态获取IP地址，每次重启设备后都会获取一次，可能导致ip地址频繁变更（映射也要）

- 在VMware中配置ip地址网关和网段（ip地址的范围）![image-20240406170447210](https://gitee.com/coi4/test/raw/master/img/image-20240406170447210.png)
- 在Linux系统中手动修改配置文件，固定ip地址![image-20240406170122700](https://gitee.com/coi4/test/raw/master/img/image-20240406170122700.png)

7、网络传输

通过

8、进程管理

9、主机状态

10、环境变量

11、上传下载

12、压缩解压