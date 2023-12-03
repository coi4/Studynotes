# Nginx



## 一、安装部署

[【初探篇】Nginx的安装部署_潮浪之巅的博客-CSDN博客](https://hashnode.blog.csdn.net/article/details/124502959)

## 二、基本使用

### 1、Nginx目录结构

```
[root@localhost ~]# tree /usr/local/nginx
/usr/local/nginx
├── client_body_temp                 # POST 大文件暂存目录
├── conf                             # Nginx所有配置文件的目录
│   ├── fastcgi.conf                 # fastcgi相关参数的配置文件
│   ├── fastcgi.conf.default         # fastcgi.conf的原始备份文件
│   ├── fastcgi_params               # fastcgi的参数文件
│   ├── fastcgi_params.default       
│   ├── koi-utf
│   ├── koi-win
│   ├── mime.types                   # 媒体类型
│   ├── mime.types.default
│   ├── nginx.conf                   #这是Nginx默认的主配置文件，日常使用和修改的文件
│   ├── nginx.conf.default
│   ├── scgi_params                  # scgi相关参数文件
│   ├── scgi_params.default  
│   ├── uwsgi_params                 # uwsgi相关参数文件
│   ├── uwsgi_params.default
│   └── win-utf
├── fastcgi_temp                     # fastcgi临时数据目录
├── html                             # Nginx默认站点目录
│   ├── 50x.html                     # 错误页面优雅替代显示文件，例如出现502错误时会调用此页面
│   └── index.html                   # 默认的首页文件
├── logs                             # Nginx日志目录
│   ├── access.log                   # 访问日志文件
│   ├── error.log                    # 错误日志文件
│   └── nginx.pid                    # pid文件，Nginx进程启动后，会把所有进程的ID号写到此文件
├── proxy_temp                       # 临时目录
├── sbin                             # Nginx 可执行文件目录
│   └── nginx                        # Nginx 二进制可执行程序
├── scgi_temp                        # 临时目录
└── uwsgi_temp                       # 临时目录

```

主要目录是conf，html，sbin

- conf放的是核心配置文件
- html放的是静态页面
  - 50x.html是发生错误展示的页面
  - index.html是默认的访问页面
  - 可以在该目录下新建html，然后在浏览器中访问
- logs文件夹用于存放日志信息
  - error.log存放出错的信息，nginx.pid存放的是当前nginx的pid
- sbin存放的是可执行文件,可以用./nginx启动nginx：

### 2、基本运行原理

Nginx的进程是使用经典的master-worker模型，启动后，会有一个master进程和多个worker进程；

master进程主要用来管理worker进程，包含：接受来自外界的信号，向各worker进程发送信号，监控worker进程的运行状态，当worker进程退出后（异常情况况下），会重新启动新的worker进程；

worker进程主要处理基本的网络事件，多个worker进程之间是对等的他们同等竞争来自客户端的请求，各进程之间相互独立；

一个请求，只可能是一个worker进程处理，一个worker进程，不可能处理其他进程的请求；

进程的个数是可以设置的，一般设置与cpu核数相同

### 3、Nginx基本配置文件

默认配置文件是Nginx.conf

```
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}


http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;

    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;
    
     #长连接超时时间，单位是秒
    keepalive_timeout  65;

 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  localhost;

	#配置根目录以及默认页面
        location / {
            root   html;
            index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }

}

```

### 4、虚拟主机与域名解析

虚拟主机使用特殊的软硬件技术，把一台运行在因特网上的服务器主机分成一台台虚拟的主机，每一台主机都具有独立的域名，具有完整的Internet服务器功能（WWW、FTP、Email等）虚拟主机之间完全独立，并可由用户自行管理

域名解析就是域名到IP地址的转换过程，IP地址是网路上表示站点的数字地址，为了更好记，用域名代替IP地址标识站点地址。域名解析工作由DNS服务器完成

IP地址：Internet　Protocol；一种通信协议，因特网基本是IP网组成；IP地址就是因特网上某个设备的一个编号；一般由网络号，主机号，掩码组成（发件人地址是网络号，姓名是主机号，收件人地址为要访问的IP的网络号，收件人姓名为访问IP的主机号）

ｄｎｓ：访问因特网必须知道对端的IP地址，访问网络一般只知道域名，转换

域名、dns、IP地址的关系

- 域名是相对于网站来说的，IP地址相对网络来说（输入域名——>域名解析服务器(dns)解析成IP地址-->访问IP地址-->完成访问的内容-->返回信息)
- Internet上的计算机IP地址是唯一的,一个IP地址对应一个计算机
- 一台计算机上可以有很多服务,即一个ip地址对应很多域名(一个计算机上有很多网站)

IP地址和DNS地址的区别

- DNS服务器地址是用于域名解析的地址；IP地址是单个主机唯一的IP地址
- 一个是私网地址；一个是公网地址
- 一个作为主机的逻辑标志，一个作为域名解析服务器的访问地址

http协议：应用层协议,由请求和响应构成,是一个标准的客户端服务器模型，一个无状态的协议；通常承载于TCP（传输层协议，IP为网络层）协议之上，有时也承载于TLS或SSL协议层之上，构成https

客户端与服务器的数据交互流程：

- 客户机与服务器需建立TCP连接，只要单击某个超级链接，HTTP工作开始（TCP工作流程如图）![image-20220430195747864](https://gitee.com/coi4/test/raw/master/img/19c3020d653f5c14f1504af78a801f87.png)
- 建立连接后，客户机发送一个请求给服务器，请求方式的格式为：统一资源标识符（URL）、协议版本号，后边是MIME信息包括请求修饰符、客户机信息和可能的内容
- 服务器接收到请求后，给予相应响应信息，其格式为一个状态行，包括信息的协议版本号、一个成功或错误的代码，后边是MIME信息包括服务器信息、实体信息和可能的内容，例如返回一个HTML的文本。
- 客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户机与服务器断开连接。如果在以上过程中的某一步出现错误，那么产生错误的信息将返回到客户端，有显示屏输出。对于用户来说，这些过程是由HTTP自己完成的，用户只要用鼠标点击，等待信息显示就可以了。

虚拟主机原理：虚拟主机是为了在同一台物理机器上运行多个不同的网站，提高资源利用率引入的技术；

- 一般web服务器一个ip地址的80端口号只对应一个网站，web服务器在不使用多个ip地址和端口的情况下，如果需要支持多个相对独立的网站就需要一种机制来分辨同一个ip地址上的不同网站的请求，这就出现了主机头绑定的方法
  - 将给不同网站空间对应不同域名，已连接请求中的域名字段来分发和应答正确的对应空间的文件执行结果
  - 使用主机头绑定域名A和B到他们对应的空间文件夹C和D。当含有域名A的web请求信息到达192.168.8.101时，web服务器将执行它对应的空间C中的首页文件，并返回给客户端，含有域名B的web请求信息同理，web服务器将执行它对应的空间D中的首页文件，并返回给客户端，所以在使用主机头绑定功能后就不能使用ip地址访问其上的任何网站了，因为请求信息中不存在域名信息，所以会出错。

**监听不同域名**：配置nginx.cfg

```
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}


http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;

    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;
    
     #长连接超时时间，单位是秒
    keepalive_timeout  65;

 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  test80.xzj520520.cn;

	#配置根目录以及默认页面
        location / {
            root   /www/test80;
            index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }
    
    
    #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  test81.xzj520520.cn;

	#配置根目录以及默认页面
        location / {
            root   /www/test81;
            index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }

```

配置单机域名:![image-20220430124859557](https://gitee.com/coi4/test/raw/master/img/ba83f6445941356fb0ca5aa8780a0412.png)

使用systemctl reload nginx重新加载配置

测试，访问http://test80.xzj520520.cn/（如果匹配不到会访问到第一个站点

**监听多个端口**：修改nginx.conf

```
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}


http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;

    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;
    
     #长连接超时时间，单位是秒
    keepalive_timeout  65;

 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  localhost;

	#配置根目录以及默认页面
        location / {
            root   /www/test80;
            index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }
    
    
    #虚拟主机的配置
    server {
    #监听端口
        listen       81;
        #域名，可以有多个，用空格隔开
        server_name  localhost;

	#配置根目录以及默认页面
        location / {
            root   /www/test81;
            index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }

}

```

使用systemctl reload nginx重新加载配置(需要关闭防火墙,否则81端口不能访问)

在如下位置新建test80,test81![image-20220430123543100](https://gitee.com/coi4/test/raw/master/img/5a29e5e8f40fcef889b4c4d9da622d89.png)

test80,test81新建index.html![image-20220430123616583](https://gitee.com/coi4/test/raw/master/img/9ae7147a5175203bf50f49d5801cac3a.png)

访问：http://192.168.8.101/

**泛域名**:利用通配符* （星号）来做次级域名以实现所有的次级域名均指向同一IP地址

- 可以让域名支持无限的子域名(这也是泛域名解析最大的用途)。
- 防止用户错误输入导致的网站不能访问的问题
- 可以让直接输入网址登陆网站的用户输入简洁的网址即可访问网站
- 可以实现无限二级域名功能，提供免费的url转发，在IDC部门实现自动分配免费网址，在大型企业中实现网址分类管理等等

### 5、servername多种匹配方式

可以在同一个servername中配置多个域名

完整匹配：

- server中可以配置多个域名

```
server_name  test81.xzj520520.cn  test82.xzj520520.cn;
```

通配符匹配：精确匹配的优先级大于通配符匹配和正则匹配

- ```
  server_name  *.xzj520520.cn;
  ```

通配符结束匹配：

- ```
  server_name  www.xzj520520.*;
  ```

正则匹配：

- ![image-20220430170058418](https://gitee.com/coi4/test/raw/master/img/41d0a93f50338db6ed3b62480fc92319.png)
- 正则匹配格式，必须以~开头，比如：server_name ~^www\d+\.example\.net$;。如果开头没有~，则nginx认为是精确匹配。在逻辑上，需要添加^和$锚定符号。注意，正则匹配格式中.为正则元字符，如果需要匹配.，则需要反斜线转义。如果正则匹配中含有{和}则需要双引号引用起来，避免nginx报错，如果没有加双引号，则nginx会报如下错误：directive "server_name" is not terminated by ";" in ...。

特殊匹配格式：

```
server_name ""; 匹配Host请求头不存在的情况。
```

匹配顺序：

- 1.精确的名字 2. 以*号开头的最长通配符名称，例如 `*.example.org` 3. 以`*`号结尾的最长通配符名称，例如 `mail.* `4. 第一个匹配的正则表达式（在配置文件中出现的顺序）

优化:

- 尽量使用精确匹配;
2. 当定义大量server_name时或特别长的server_name时，需要在http级别调整server_names_hash_max_size和server_names_hash_bucket_size，否则nginx将无法启动。

### 6、反向代理

![image-20220430170948611](https://gitee.com/coi4/test/raw/master/img/2c4bf89af40ccce29bec18a69d9c3e11.png)

反向代理指以代理服务器来接受Internet上的连接请求，然后将请求转发给内部网络上的器；并将从服务器上得到的结果返回给Internet上请求连接的客户端

两种模型：

- 作为内容服务器的替身（具有必须保持安全的敏感信息，可在防火墙外设置一个代理服务器作为内容服务器的替身，如果内容服务器返回错误消息，代理服务器会先行截取该消息并更改标头中列出的任何URL，然后再将消息发送给客户机，如此可以防止外部客户机获取内容服务器的重定向URL）
- 作为内容服务器的负载均衡器（可以在一个组织内使用多个代理服务器来平衡各web服务期间的网络负载，可以利用代理服务器的高速缓存特性，创建一个用于负载平衡的服务器池）（可以位于防火墙的任意一侧，如果web服务器每天接收大量的请求，则可以使用代理服务器分担web服务器的负载并提高网络访问效率

#### 6.1、反向代理配置![image-20220430182343864](https://gitee.com/coi4/test/raw/master/img/5f7011630051c26dceabac426398d8da.png)

#### 6.2、基于反向代理的负载均衡器

克隆两个centos，ip分别设为192.168.8.102，192.168.8.103（网段要用自己的电脑对应）

![image-20220430184102076](https://gitee.com/coi4/test/raw/master/img/ee071c0b85cc9e477fda83cd1b8816c5.png)

修改静态ip

![image-20220430184135760](https://gitee.com/coi4/test/raw/master/img/5a6583de9e03b8b09e25c986ef014fc2.png)

![image-20220430184225267](https://gitee.com/coi4/test/raw/master/img/ea3bdc4d593bb79f5f5b5ae2cc1d8e6a.png)

重启网络服务：

![image-20220430184320760](https://gitee.com/coi4/test/raw/master/img/45e242f2f8e53f37e9e44b3604fb1bb2.png)

配置好虚拟机之后,配置nginx.cfg

102的nginx.cfg

```
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

102的nginx在html目录下的index.html文件

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>I am from 192.168.8.102</h1>
</body>
</html>
```

访问http://192.168.8.102/

将101代理到102：101的nginx.conf

```
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}


http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;

    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;
    
     #长连接超时时间，单位是秒
    keepalive_timeout  65;

 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  test80.xzj520520.cn;

	#配置根目录以及默认页面
        location / {
            proxy_pass http://192.168.8.102;
            # root   /www/test80;
            # index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }
    

}

```

**配置101的负载均衡（轮询模式）**

![image-20220430190409638](https://gitee.com/coi4/test/raw/master/img/666d5e0ed07a7351ace225743985ce38.png)

```
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}


http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;

    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;
    
     #长连接超时时间，单位是秒
    keepalive_timeout  65;

#定义一组服务器
upstream httpds{
    server 192.168.8.102:80;
    server 192.168.8.103:80;
}

 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  test80.xzj520520.cn;

	#配置根目录以及默认页面
        location / {
            proxy_pass http://httpds;
            # root   /www/test80;
            # index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }
    

}

```

多次访问http://192.168.8.101/发现102和103被交替访问

**配置101的负载均衡（权重模式）**

```
worker_processes  1; #允许进程数量，建议设置为cpu核心数或者auto自动检测，注意Windows服务器上虽然可以启动多个processes，但是实际只会用其中一个

events {
    #单个进程最大连接数（最大连接数=连接数*进程数）
    #根据硬件调整，和前面工作进程配合起来用，尽量大，但是别把cpu跑到100%就行。
    worker_connections  1024;
}


http {
    #文件扩展名与文件类型映射表(是conf目录下的一个文件)
    include       mime.types;
    #默认文件类型，如果mime.types预先定义的类型没匹配上，默认使用二进制流的方式传输
    default_type  application/octet-stream;

    #sendfile指令指定nginx是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度。
    sendfile        on;
    
     #长连接超时时间，单位是秒
    keepalive_timeout  65;

#定义一组服务器
upstream httpds{
    server 192.168.8.102 weight=10;
    server 192.168.8.103 weight=1;
    # server 192.168.8.102 weight=10 down; #down表示不参与负载均衡
    # server 192.168.8.102 weight=10 backup; #backup表示是备用服务器，没有服务器可用的时候使用
}

 #虚拟主机的配置
    server {
    #监听端口
        listen       80;
        #域名，可以有多个，用空格隔开
        server_name  test80.xzj520520.cn;

	#配置根目录以及默认页面
        location / {
            proxy_pass http://httpds;
            # root   /www/test80;
            # index  index.html index.htm;
        }

	#出错页面配置
        error_page   500 502 503 504  /50x.html;
        #/50x.html文件所在位置
        location = /50x.html {
            root   html;
        }
        
    }
    

}

```

多次访问http://192.168.8.101/发现102访问的次数多余103访问的次数。

