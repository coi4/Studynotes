---
cotypora-copy-images-to: upload
---

# git教程

#### 1、版本控制器

能记录我们对文档的所有修改,所有版本的一个软件，一般特性如下：

> 1. 能够记录历史版本，回退历史版本
> 2. 团队开发，方便代码合并

##### 1.1、版本控制器的方式

> * 集中式版本控制工具
>   * 版本库集中存放在中央服务器的；team里每个人work时从中央服务器下载代码；必须联网才能工作；个人修改后提交到中央版本库
>   * 服务器一旦宕机无法提交代码；离线无法提交代码，无法及时记录
>   * e.g. ，SVN和CVS（微软）
> * 分布式版本控制工具
>   * 没有中央服务器，每个人电脑上都是一个完整的版本库；无需联网；多人协作只需要各自的修改推送给对方，就能互相看到对方的修改
>   * e.g. ，Git

##### 1.2、SVN

被淘汰，用不上，了解即可。

![image-20231009134201640](https://gitee.com/coi4/test/raw/master/img/image-20231009134201640.png)

##### 1.3、Git

常用！

> Git是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。是Linus Torvalds为了帮助管理Linux内核开发而开发的一个开放源码的版本控制软件。

![image-20231009134926596](https://gitee.com/coi4/test/raw/master/img/image-20231009134926596.png)

##### 1.4、Git工作流程图

![image-20231009161020517](https://gitee.com/coi4/test/raw/master/img/image-20231009161020517.png)

> * 本地仓库：是在开发人员**自己电脑上**的Git仓库,存放我们的代码(.git 隐藏文件夹就是我们的本地仓库)  
> * 远程仓库：是在**远程服务器上**的Git仓库,存放代码(可以是github.com或者gitee.com 上的仓库,或者自己该公司的服务器)
> * 工作区: 我们自己写代码(文档)的地方
> * 暂存区: 在 本地仓库中的一个特殊的文件(index) 叫做暂存区,临时存储我们即将要提交的文件
> * Clone：克隆，就是将远程仓库复制到本地仓库
> * checkout：检出，就是从本地仓库中检出一个仓库分支然后进行修订
> * add：添加，就是在提交前先将代码提交到暂存区
> * commit：提交，就是提交到本地仓库的当前分支。本地仓库中保存修改的各个历史版本
> * fetch：抓取，就是从远程库抓取到本地仓库，不进行任何的合并动作，一般操作比较少
> * Push：推送，就是将本地仓库代码上传到远程仓库
> * Pull：拉取，就是将远程仓库代码下载到本地仓库,并将代码 克隆到本地工作区

#### 2、Git安装与常用命令

> 导读：会用到一些基本的Linux命令：
>
> * ls/ll     查看当前目录（ll可查看隐藏文件，常用0
> * cat      查看文件内容
> * touch  创建文件
> * vi         vi编辑器（方便不同操作系统展示）
> * clear： 清除窗口
> * rm -rf xx文件：删除xx文件
> * mv 原文件名  改的文件名：修改文件名

##### 2.1 Git环境配置

###### 2.1.1 下载与安装

下载地址：<u>https://git-scm.com/download</u>

![image-20231009163327782](https://gitee.com/coi4/test/raw/master/img/image-20231009163327782.png)

下载完成后可以得到如下安装文件：

![image-20231009163843595](https://gitee.com/coi4/test/raw/master/img/image-20231009163843595.png)

双击安装。安装完成后在桌面（或其他目录）点击右键，如果能够看到如下两个菜单说明安装成功。

![image-20231009164148144](https://gitee.com/coi4/test/raw/master/img/image-20231009164148144.png)

> * Git Gui：Git提供的图形界面工具
> * Git Bash：Git提供的命令行工具

###### 2.1.2 基本配置

安装完成后**首先要做的事**是设置用户名称和Email地址。**这是非常重要的！！！**每次Git提交都会使用该用户信息。

1. 打开Gitbash

2. 设置用户信息

   ```git
   git config --global user.name"你的用户名“
   git config --global user.email"你的邮箱（可随意设置）”
   ```

   查看配置信息

   ```git
   git config --global user.name
   git config --global user.email
   ```

###### 2.1.3 为常用指令配置别名（选读）

将常用的繁杂的指令参数设置别名，以简单化，方便，效率高

1. 打开用户目录（C盘user目录），创建.bashrc文件

   （若不允许创建点号开头文件，可打开gitBash，执行touch ~/.bashrc）

2. 在.bashrc文件中输入如下内容：

   ```python
   #用于输出git提交日志
   alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
   #用于输出当前目录所有文件及基本信息
   alias ll='ls -al'
   ```

3. 打开gitbash，执行source ~/.bashrc

###### 2.1.4 解决Git Bash乱码问题（选读）

1. 打开gitbash执行下面命令

   ```python
   git config --global core.quotepath false
   ```

   

2. 在 ${git_home}/etc/bash.bashrc 文件最后加入下面两行

   ```python
   export LANG="zh_CN.UTF-8"
   export LC_ALL="zh_CN.UTF-8"
   ```

##### *2.2 获取本地仓库

要对代码进行版本控制，首先需要获得本地仓库

1. 电脑任意位置**创建一空目录**作为本地Git仓库
2. 进入空目录，右键**打开gitbash**
3. **执行git init命令**
4. 创建成功后，执行**ll**命令可查看到.git目录

##### 2.3 基础操作指令

 ![image-20231009173651168](https://gitee.com/coi4/test/raw/master/img/image-20231009173651168.png)

> * git add .：1.4中有备注（工作区--> 暂存区）
>
> * git commit -m""： 1.4中有备注（暂存区 --> 本地仓库）
>
> * git status：查看修改的状态（暂存区、工作区）
>
> * git log：查看提交日志（log）（2.1.3中有提到如何简化）
>
> * git reset --hard commitID（ID可用git-log或git log查看）：版本切换
>
>   * 查看已删除记录
>     * git reflog
>   * git选中即复制，粘贴有鼠标滑动滚轮没有右键选paste
>
> * 忽略提交（该文件无需纳入Git管理，也不希望总出现在未跟踪文件列表，一般为自动生成的文件，如日志文件）
>
>   * 在工作目录中创建.gitignore文件，列出要忽略的文件格式
>
>     * ```python
>       # 所有以.a 结尾的文件讲被忽略(递归)
>       *.a
>       # 不管其他规则怎样,强制不忽略  lib.a
>       !lib.a
>       # 只忽略 文件 TODO (注意这里是文件)
>       /TODO
>       # 忽略 build文件夹下所有内容(递归) 这里是文件夹
>       build/
>       # 忽略 doc 目录下以 *.txt 结尾的文件 (不递归)
>       doc/*.txt
>       # 忽略 doc 目录下以 *.pdf 结尾的文件 (递归)
>       doc/**/*.pdf
>       ```

#### 3、分支

使用分支意味可以把工作从开发主线上分离来进行重大bug修改、开发新的功能，以免影响开发主线

*工作区只能有一个分支

##### 3.1 基础操作

> * git branch：查看本地分支
> * git branch 分支名：创建本地分支
> * *git checkout 分支名：切换分支
> * *git checkout -b  分支名：**创建并切换**
> * *git merge：**合并**分支
> * git branch -d 分支名：删除分支
> * git branch -D 分支名：强制删除

##### 3.2 解决冲突

两个分支上对文件修改可能会产生冲突，例如同时修改了同一个文件的同一行，需要手动解决

1. 根据提示找到冲突文件，处理文件中冲突的地方![image-20231010132305150](https://gitee.com/coi4/test/raw/master/img/image-20231010132305150.png)
2. add
3. commit

##### 3.3 使用原则与流程

> * master（生产）分支
> * release（tag）/xxx1：用来标记每次上线的提交结点
> * develop（开发）：会不断有新feature分支合并进来；线上部署时，再由develop合并到master
> * feature/xxx1：业务开发并测试完成后合并到develop，合并后可删除；为了完成不同开发需求
> * hotfix/bug_xxx：作为线上bug修复使用，修复完成后合并到master、test、develop；合并后可删除
> * test：代码测试
> * pre：预上线分支

#### 4 、远程仓库

常用托管服务器（远程仓库）：GitHub、gitee（码云）、GitLab

##### 4.1、 准备工作

###### 4.1.1 、注册码云

###### 4.1.2 、创建远程仓库

![image-20231010140728535](https://gitee.com/coi4/test/raw/master/img/image-20231010140728535.png)

![image-20231010140841745](https://gitee.com/coi4/test/raw/master/img/image-20231010140841745.png)

###### 4.1.3 、配置SSH公钥

1. git生成SSH公钥

   - ssh-keygen -t rsa
   - 不断回车
     - 若公钥已存在，自动覆盖

2. gitee设置账户公钥

   - 获取公钥
     - cat -/.ssh/id_rsa.pub
     - 复制内容
   - ![image-20231010135934649](https://gitee.com/coi4/test/raw/master/img/image-20231010135934649.png)

   - 验证是否配置成功
     - ssh -T git@gitee.com

##### *4.2 、操作远程仓库

> * git remote add origin 仓库路径：**添加**远程仓库，先初始化本地库，然后与已创建的远程库进行对接
>
> * git remote：**查看**远程仓库
>
> * git push [-f] [--set-upstream] origin 本地分支名：远端分支名 ：**推送**到远程仓库
>
>   * 远分支名与本分支名相同，可只写本分支名
>     * git push origin master
>   * --set-upstream **推送同时关联**
>   * 当前分支与远端分支已关联，可省略成git push
>
> * git branch -vv：**查看关联**关系
>
>   ------
>
>   
>
> * git clone 仓库路径 [本地目录]:若已有远端仓库，可直接**克隆**到本地
>
>   `git remote add`只是在你的git配置中创建了一个条目，指定了一个特定网址的名称。您必须有一个现有的git存储库才能使用它。
>
>   `git clone`通过复制位于指定URI的现有git存储库来创建一个新的git存储库。
>
>   `clone`命令创建您指定的存储库的本地副本。`remote add`添加了一个远程存储库，您可以将其推送到或从中拉出。
>
>   相当于`clone`的svn是`checkout`
>
> * git fetch [remote name] [branch name]:抓取，将仓库里的**更新**都**抓取到本地**，不会进行合并；若不指定远端名称和分支名，则抓取所有分支
>
> * git pull [remote name] [branch name]：拉取，将远端仓库的**修改拉到本地并自动合并**，等同于fetch+merge；若不指定远端名称和分支名，则抓取并更新当前分支
>
> * 解决合并冲突：A用户修改后优先推送到远程仓库，B用户修订提交到本地仓库后，推送时晚于A，故**需先拉取远程仓库的提交，经过合并后才能推送到远端分支**，与解决本地分支冲突相同

#### 5、在idea中使用Git

##### 5.1、配置Git

如果Git安装在默认路径下，idea会自动找到git的位置，若修改了安装路径，则需要手动配置下Git的路径。选择File-->Settings打开设置窗口，找到Version Control下的git选项

##### 5.2、操作Git

1. 创建远程仓库

   ![image-20231010232837070](https://gitee.com/coi4/test/raw/master/img/image-20231010232837070.png)

2. 初始化本地仓库（获取）

   File-->open

   ![image-20231010232710852](https://gitee.com/coi4/test/raw/master/img/image-20231010232710852.png)

3. 设置远程仓库（remote add

   ![image-20231010234742774](https://gitee.com/coi4/test/raw/master/img/image-20231010234742774.png)

4. 提交到本地仓库

   ![image-20231010232943237](https://gitee.com/coi4/test/raw/master/img/image-20231010232943237.png)

5. 推送

   ![image-20231010235531598](https://gitee.com/coi4/test/raw/master/img/image-20231010235531598.png)

6. 克隆

   ![image-20231010235555247](https://gitee.com/coi4/test/raw/master/img/image-20231010235555247.png)

7. 创建分支

   - ![image-20231010235808494](https://gitee.com/coi4/test/raw/master/img/image-20231010235808494.png)

8. 切换分支及其他相关操作

   ![image-20231010235844803](https://gitee.com/coi4/test/raw/master/img/image-20231010235844803.png)

9. 解决冲突

   ![image-20231010235906509](https://gitee.com/coi4/test/raw/master/img/image-20231010235906509.png)

![image-20231011000922850](https://gitee.com/coi4/test/raw/master/img/image-20231011000922850.png)

#### 6、注意事项

* 切换分支前先提交本地的修改
* 代码及时提交
* 遇到问题不要删除文件目录

#### 7、总结

git配置ssh公钥

建立远程仓库

获取本地仓库

本地仓库remote add远程仓库

克隆远程仓库

本地push远程pull

















