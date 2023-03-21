

# 云服务器初始

## Linux初始操作

### 1.安装vmwa Tools

**切换成超级管理员**

```shell
sudo su 
```

```shell
apt-get install open-vm-tools-desktop -y
```

报错 `E：Could not get lock /var/lib/dpkg/lock-frontend - open`

先尝试：

```shell
killall apt apt-get
```

如果还是不行，则：

```shell
rm /var/lib/apt/lists/lock
rm /var/cache/apt/archives/lock
rm /var/lib/dpkg/lock*
```

最后：

```shell
sudo apt update
```

### 2.远程连接ssh与文件传输

**安装SSH**

```shell
sudo apt install -y openssh-server
```

**启动SSH服务**

```shell
sudo service ssh start
```

### 3.安装mysql(注意最好先下载mysql安装包)

**安装MySQL依赖包**

```shell
apt install -y libaio1 libncurses*
sudo apt-get install -y libaio1 libncurses*
#更新包索引：
# sudo apt-get update
#安装 libncurses5-dev deb 包：
# sudo apt-get install libncurses5-dev
```

**下载mysql**

```
wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz
```

你也可以在本地电脑中提前下载好，通过scp等方式，上传到Linux中

**解压到 /usr/local/ 目录中**

```shell
tar -zxvf mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz -C /usr/local/
```

**重命名文件夹**

> 进入 `/usr/local/`目录，将 `mysql-5.7.13-linux-glibc2.5-x86_64` 重命名为 `mysql/`

```shell
cd /usr/local/
mv mysql-5.7.13-linux-glibc2.5-x86_64 mysql/
```

**创建一个叫做`mysql`的系统帐号**

```shell
$ useradd -s /bin/false -M mysql

# 删除系统中默认MySQL配置文件
$ rm -f /etc/my.cnf /etc/mysql/my.cnf /usr/local/mysql/etc/my.cnf ~/.my.cnf

# 初始化数据库目录，执行成功后，在/usr/local/mysql中，将新产生一个data目录
$ /usr/local/mysql/bin/mysqld --initialize-insecure --user=mysql

[Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
[Warning] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
```

**vi /usr/local/mysql/my.cnf**

```shell
[mysqld]
port = 3306

server_id = 1
log_bin = mysql-bin
```

### **[配置全局变量](https://so.csdn.net/so/search?q=vim&spm=1001.2101.3001.7020)**

> 命令进入编辑

```shell
vim /etc/profile
```

> 最后加入内容  :wq 保存退出

```shell
export JAVA_HOME=/usr/local/jdk1.8.0_321
export MYSQL_HOME=/usr/local/mysql
export PATH=$JAVA_HOME/bin:$MYSQL_HOME/bin:$PATH
```

> 重新加载配置文件

```shell
source /etc/profile
```

> 解决配置文件不生效

```shell
#vim ~/.bashrc
if [ -f /etc/profile ]; then
. /etc/profile
fi
source /etc/profile
```



### **启动服务**

```
/usr/local/mysql/bin/mysqld_safe --user=mysql &
```

> 测试成不成功

```shell
/usr/local/mysql/bin/mysql -uroot -p
```



# ubuntu常用指令

### 连接备份数据库

**连接云服务器**

```shell
ssh ubuntu@175.24.118.73
ssh ubuntu@124.221.172.234
ssh demo@192.168.19.129
ssh root@192.168.1.105
```



**交换文件**

```sql
#本机文件放到服务器上
scp ./forum.sql ubuntu@175.24.118.73:/tmp/forum.sql
#把服务器上的备份文件,拷贝到从服务器上
scp ubuntu@192.168.88.88:/tmp/test.sql /tmp/db.test.sql 

#解压
tar -zxvf jdk-8u201-linux-x64.tar.gz -C /usr/local/
#压缩
tar -zvcf forum_v3.tar.gz .\forum_v3_jar
```



**备份主服务器的test 数据库**

```shell
#如果从服务器在使用中,可以锁定数据库禁止写入配好后再解锁
mysql>flush tables with read lock;
mysql>unlock tables;
```

**备份文件**

```shell
#备份数据文件
/usr/local/mysql/bin/mysqldump -uroot -p -lF test >'/tmp/db.test.sql'
#到入数据
mysql -uroot -p forum < /tmp/forum.sql
```

**连接主服务器**

```sql
change master to master_user='jack',master_password='123',master_host='124.221.172.234',master_port=3306;
```

```shell
#开启线程连接主服务器
start slave; 
# stop slave;
#一定要开放端口   
show slave status\G;
show master status;
show processlist;
```

```
 INSERT INTO `forum`.`user`(`username`, `nickname`, `password`, `mobile`, `avatar`, `level`, `email`, `created_at`, `update_at`) VALUES ('marry', 'marry', 'marry', 'marry', 'marry', 0, 'marry', '2022-03-09 16:02:08', '2022-03-09 16:02:08');
```



### 账号相关

**删除用户**

```sql
mysql>delete from mysql.user where user='jack'
```

**新增用户**

```sql
mysql>grant all on *.* to jack@"%" identified by "123";
```

> 查询环境下的用户

```sql
mysql>select user,host from mysql.user;
mysql>select user,host from mysql.user\G;
```

**远程连接**

```shell
mysql -ujack -p123 -h 124.221.172.234
```

### 服务启动与修改

```shell
/usr/local/mysql/support-files/mysql.server start|stop|restart
/usr/local/mysql/bin/mysqld_safe --user=mysql &
```

> 查看mysql进程

```shell
ps -le | grep mysqld  
losf -i 8080
plill mysqld
```

### 日志查看

> /usr/lcoal/mysql/data/

**查看日志内容**

```shell
/usr/local/mysql/bin/mysqlbinlog -v data/mysql-bin.000001
/user/local/mysql/bin/mysqlbinlog -v --base64-output=decode0rows mysql-bin.000001
```

**在binlog常规操作**

```sql
mysql>show master status;	#查看当前binlog日志
mysql>reset master;			#清空所有的binlog文件
mysql>flush logs; 			#启用一个新的binlog日志
```

**清空所有bin-log**

```sql
mysql>reset master;
mysql>show master status;
```



****



# Java项目部署

## 一、准备工作

在服务器端安装并配置好以下工具：Nginx（将`/usr/local/nginx/html `文件夹内的内容清空）、JDK、MySQL、redis



修改 Nginx 配置文件 `nginx.conf` 如下，然后让 Nginx 加载新的配置文件，命令是 `nginx -s reload`，就实现了反向代理和负载均衡

> vi /usr/local/nginx/conf/nginx.conf

```shell
http {
    # 配置两台上游服务器，例如是 Java 启动的 Spring Boot 服务
    upstream backend {
        server 172.19.13.56:8080 weight=1 max_fails=0;
        server 172.19.13.57:8080 weight=1 max_fails=0;
    }

    server {
    
        listen       80;
        server_name  _;

        location / {
            proxy_pass   http://backend;        # 将请求转发到上游服务器
            proxy_set_header    X-Real-IP  $remote_addr;
            proxy_set_header    HTTP_X_FORWARDED_FOR $remote_addr;
            proxy_set_header    X-Forwarded-For  $proxy_add_x_forwarded_for;
            proxy_set_header    X-Forwarded-Proto $scheme;
            proxy_set_header    Host    $host;
        }
    }
}
```

## 二、前端

> 进入前端的项目目录,src同级目录，生成一个build文件夹

```shell
#构建之前注意公网ip
npm run build
#在打包之前,在 package.json 中 private 下(位置任意)添加
"homepage": "./",
```

> 使用scp命令将本机build文件夹内的所有文件上传到服务器端

```shell
#先删除nginx/html/下其他文件
$ rm /usr/local/nginx/html/*

scp -r ./build/* ubuntu@124.221.172.234:./
mv /home/ubuntu/* /usr/local/nginx/html/
#将11.22.33.44替换为你服务器的公⽹IP
```

本机浏览器访问服务器公网IP即可

## 三、后端

进入后端的项目目录，运行下列代码，在target文件夹内生成一个jar包

```shell
$ mvn clean package -Dmaven.test.skip=true
```

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <!--version>2.3.5.RELEASE</version>-->
    <configuration>
        <excludes>
            <exclude>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
            </exclude>
        </excludes>
    </configuration>
</plugin>
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <source>1.8</source>
        <target>1.8</target>
    </configuration>
</plugin>
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-jar-plugin</artifactId>
    <configuration>
        <archive>
            <manifest>
                <addClasspath>true</addClasspath>
                <useUniqueVersions>false</useUniqueVersions>
                <classpathPrefix>lib</classpathPrefix>
                   <!--注意类路径 -->
                <mainClass>com.example.demo.DemoApplication</mainClass>
            </manifest>
            <manifestEntries>
                <version>${project.version}</version>
            </manifestEntries>
        </archive>
    </configuration>
</plugin>
```

将jar包上传到服务器端的/opt文件夹内

```shell
$ scp ./target/forum-1.0-SNAPSHOT.jar(jar包名称) root@11.22.33.44:/opt
```

使用下列代码即可运行

```shell
# netstat -ntulp | grep 8080
$ java -jar jar包名称
# 后台运行任务
# nohup  java -jar包名称 > forum_v3.log 2>&1 &
```

## 四、注意

1、请根据你服务器的公网IP修改前后端文件中相对应的url 如：前端的http请求url和后端的静态资源地址不再是本机localhost，而是服务器url 2、后端配置文件中的指定端口号server.port，需要在阿里云安全组规则中手动添加 ![image-20210406172243651.png](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201961.png)

## Nginx安装

**下载nginx**

```
wget http://nginx.org/download/nginx-1.20.1.tar.gz
```

**解压nginx**

```
tar -zxvf nginx-1.20.1.tar.gz
```

**下载OpenSSL**

```
wget https://www.openssl.org/source/openssl-1.1.1l.tar.gz
```

**解压OpenSSL**

```
tar -zxvf openssl-1.1.1l.tar.gz
```

**编译nginx**

> 进入nginx目录

```
cd ./nginx-1.20.1
```

> 安装编译nginx需要的工具

```
apt install -y gcc make libpcre3-dev zlib1g-dev
apt-get update
```

**设置配置**

```
./configure --with-http_ssl_module --with-openssl=../openssl-1.1.1l
```

![image-20220310092236852](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201962.png)



```
./configure --help	帮助
```



**编译**

```
make
```

```
make install
```

**启动nginx服务**

> 进入编译好的nginx目录

```
cd /usr/local/nginx
```

**启动服务**

```
/usr/local/nginx/sbin/nginx
```

> 查看端口是否启动成功

```
netstat -tnulp | grep 80
```

> 结果如下说明成功

```
tcp  0  0 0.0.0.0:80  0.0.0.0:*   LISTEN  50909/nginx: master 
```





****



## JDK安装



**一、下载**

安装配置

以 8u201版本为例，官网下载  `jdk-8u201-linux-x64.tar.gz`，并上传到 Linux 中，根据操作系统下载对应版本，目前主流的服务器大多数都是 x64 架构，选择 `x64 Compressed Archive` 即可，下载地址：

```shell
https://www.oracle.com/java/technologies/downloads/
```

> 本机路径示例

```shell
#在物理机将数据传输到虚拟机
scp D:\code\linux\jdk-8u321-linux-x64.tar.gz ubuntu@124.221.172.234:./
```

**二、解压**

```shell
$ cd /home/ubuntu
$ tar -zxvf jdk-8u321-linux-x64.tar.gz -C /usr/local/

# 查看解压后的目录名称（版本号不同，目录名称不一样）
$ ls /usr/local/
jdk1.8.0_321
```

 **三、配置环境变量**

```shell
$ vi /etc/profile

# 在最后面新增如下内容：（注意替换为你当前使用版本对应的目录名）
JAVA_HOME=/usr/local/jdk1.8.0_321/
PATH=$JAVA_HOME/bin:$PATH
```

 **四、让配置文件生效**

```shell
$ source /etc/profile

$ java -version
java version "1.8.0_321"

$ javac -version
javac 1.8.0_321
```

****

## redis安装

```shell
$ wget https://download.redis.io/releases/redis-6.2.4.tar.gz
$ tar xzf redis-6.2.4.tar.gz
$ cd redis-6.2.4
$ make
$ ./src/redis-server    # 启动服务
$ cd /home/ubuntu/redis-6.2.4
$ ./src/redis-cli       # 进入控制台
redis> set foo bar
OK
redis> get foo
"bar"

#查看端口
 #lsof -i :6379
```

```
配置文件
安装目录下的redis.conf
bind 0.0.0.0   //允许访问IP 0000为无限制
​
requirepass 123456   //修改密码
​
daemonize yes     //守护进程（开启后台运行）
​
protected mode no   //禁止外网访问  开启很危险
```



****

## [Maven安装与配置(不重要)](https://www.cnblogs.com/eagle6688/p/7838224.html)

一、需要准备的东西

\1. JDK

\2. Eclipse

\3. Maven程序包

二、下载与安装

\1. 前往https://maven.apache.org/download.cgi下载最新版的Maven程序：

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201963.png)

\2. 将文件解压到D:\Program Files\Apache\maven目录下:

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201964.png)

\3. 新建环境变量MAVEN_HOME，赋值D:\Program Files\Apache\maven

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201965.png)

\4. 编辑环境变量Path，追加%MAVEN_HOME%\bin\;

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201966.png)

\5. 至此，maven已经完成了安装，我们可以通过DOS命令检查一下我们是否安装成功：

```
mvn -v
```

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181201967.png)

三、配置Maven本地仓库

\1. 在D:\Program Files\Apache\目录下新建maven-repository文件夹，该目录用作maven的本地库。

\2. 打开D:\Program Files\Apache\maven\conf\settings.xml文件，查找下面这行代码：

```
<localRepository>/path/to/local/repo</localRepository>
```

localRepository节点默认是被注释掉的，需要把它移到注释之外，然后将localRepository节点的值改为我们在3.1中创建的目录D:\Program Files\Apache\maven-repository。

\3. localRepository节点用于配置本地仓库，本地仓库其实起到了一个缓存的作用，它的默认地址是 C:\Users\用户名.m2。

当我们从maven中获取jar包的时候，maven首先会在本地仓库中查找，如果本地仓库有则返回；如果没有则从远程仓库中获取包，并在本地库中保存。

此外，我们在maven项目中运行mvn install，项目将会自动打包并安装到本地仓库中。

\4. 运行一下DOS命令

```
mvn help:system
```

如果前面的配置成功，那么D:\Program Files\Apache\maven-repository会出现一些文件。



# 搭建内网穿透服务器

#### 一、[内网穿透](https://so.csdn.net/so/search?q=内网穿透&spm=1001.2101.3001.7020)简介

1. 官方说法：内网穿透，也即 NAT 穿透，进行 NAT 穿透是为了使具有某一个特定源 IP 地址和源端口号的数据包不被 NAT 设备屏蔽而正确路由到内网主机。
2. 个人理解：浏览器中我们所能访问的网站都是公网ip地址，而我们所用的网络（路由器、光猫等）都是内网，如192.168.0.1、127.0.0.1，而当我们在本地部署项目时，想让别人访问我们的本地地址（内网）来使用我们的项目，这个时候，别人是访问不了的。因为运营商出于安全策略考虑，普通用户只能使用内网。那么，这就用到内网穿透了。
3. 简单来说，内网穿透就是将内网ip转为公网ip

#### 二、内网穿透原理

1. 原理图

   ![image-20210810194934715](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/171-ubuntu%25E5%25AE%2589%25E8%25A3%2585/e0a1294a7623f1a448959e2c2099a151.png)

2. 原理：本地电脑通过连接公网中的电脑FRP来进行数据交互，而其他用户所获取到的数据直接来自公网电脑，而公网电脑只作为一个转接站来传输数据而不去保留数据。公网电脑的带宽直接影响到数据传输的速率。

#### 三、在服务器上搭建FRP

1. 准备工作

   - VPS一台（也可以是具有公网IP的实体机）
   - 访问目标设备（就是你最终要访问的设备）
   - 简单的Linux基础（会用cp等几个简单命令即可）

2. 服务端设置

   - 使用xshell工具连接linux服务器

   - 使用命令查看系统架构：arch

   - 根据显示结果去下载相对应的软件

     ```shell
     下载相对应架构的FRP版本
     wget https://github.com/fatedier/frp/releases/download/v0.22.0/frp_0.22.0_linux_amd64.tar.gz
     
     解压缩
     tar -zxvf frp_0.22.0_linux_amd64.tar.gz
     
     移动到自定义文件夹
     cp -r frp_0.22.0_linux_amd64 frp
     
     进入自定义文件夹
     cd frp
     
     查看文件
     ls -a
     
     frps----------------->服务器端启动器
     frps.ini------------->服务器端配置文件
     frpc----------------->用户端启动器
     frpc.ini------------->用户端配置文件
     12345678910111213141516171819
     ```

   - 修改配置信息：vim frps.ini

     ```shell
     [common]
     bind_port = 7000				#用户端需要连接的端口
     dashboard_port = 8088 			#Web监控端端口
     token = 12345678				#连接秘钥
     dashboard_user = 1993884953@qq.com			#Web端用户名
     dashboard_pwd = cw5233cw			#Web端密码
     vhost_http_port = 10080			
     vhost_https_port = 10443
     
     #“vhost_http_port”和“vhost_https_port”用于反向代理HTTP主机时使用，本文不涉及HTTP协议，因而照抄或者删除这两条均可。
     12345678910
     ```

   - 启动FRP服务：./frps -c frps.ini

   - 此时访问 公网ip:8088并使用自己设置的用户名密码登录，即可看到仪表板界面

   - 将服务在后台运行

     ```shell
     nohup ./frps -c frps.ini &
     #输出如下内容即表示正常运行
     nohup: ignoring input and appending output to 'nohup.out'
     #此时可先使用Ctrl+C关闭nohup，frps依然会在后台运行，使用jobs命令查看后台运行的程序
     jobs
     #使用kill %Id 可以关闭后台运行的程序
     123456
     ```

3. 客户端设置

   - 根据客户端设备的情况选择相应的frp程序进行下载

   - 用文本编辑器打开frpc.ini，与服务端类似

     ```shell
     [common]
     server_addr = 公网IP
     server_port = 7000
     token = won517574356
     [rdp]
     type = tcp
     local_ip = 127.0.0.1           
     local_port = 3389
     remote_port = 7001  
     [smb]
     type = tcp
     local_ip = 127.0.0.1
     local_port = 445
     remote_port = 7002
     
     #“server_addr”为服务端IP地址，填入即可。
     #“server_port”为服务器端口，填入你设置的端口号即可，如果未改变就是7000
     #“token”是你在服务器上设置的连接口令，原样填入即可。
     #上面frpc.ini的rdp、smb字段都是自己定义的规则，自定义端口对应时格式如下。
     #“[xxx]”表示一个规则名称，自己定义，便于查询即可。
     #“type”表示转发的协议类型，有TCP和UDP等选项可以选择，如有需要请自行查询frp手册。
     #“local_port”是本地应用的端口号，按照实际应用工作在本机的端口号填写即可。
     #“remote_port”是该条规则在服务端开放的端口号，自己填写并记录即可。
     1234567891011121314151617181920212223
     ```

     ![frp的原理](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/171-ubuntu%25E5%25AE%2589%25E8%25A3%2585/3f2026fb451d864bb5dd348d22329bff.png)

4. 客户端的frpc程序不能直接双击运行！

   ```shell
   #使用命令提示符或Powershell进入该目录下
   cd C:\frp
   #并执行
   ./frpc -c frpc.ini
   #运行frpc程序，窗口中输出如下内容表示运行正常。
   login to server success, get run id 
   server udp port [0]
   2019/01/12 16:14:56 [I] [proxy_manager.go:136] [2b65b4e58a5917ac] proxy added: [rdp smb]
   2019/01/12 16:14:56 [I] [control.go:143] [smb] start proxy success
   2019/01/12 16:14:56 [I] [control.go:143] [rdp] start proxy success
   12345678910
   ```

5. windows客户端配置后台运行及开机启动

   ```shell
   #frpc运行时始终有一个命令行窗口运行在前台，影响美观，我们可以使用一个批处理文件来将其运行在后台，而且可以双击执行，每次打开frpc不用再自己输命令了。
   #在任何一个目录下新建一个文本文件并将其重命名为“frpc.bat”，编辑，粘贴如下内容并保存。
   @echo off
   if "%1" == "h" goto begin
   mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit
   :begin
   REM
   cd C:\frp
   frpc -c frpc.ini
   exit
   #将cd后的路径更改为你的frpc实际存放的目录。
   #之后直接运行这个 .bat 文件即可启动frpc并隐藏窗口（可在任务管理器中退出）。
   #至于开机启动，把这个 .bat 文件直接扔进Windows的开机启动文件夹就好了 :)
   #至此，客户端配置完成，之后就是你自己根据需要在frpc.ini后追加规则即可。
   #强烈建议你在使用frp直接测试内网穿透前，先在局域网内测试好相关功能的正常使用，并配置好可能会影响的Windows防火墙等内容，在内网调试通过后再使用frp进行内网穿透测试。
   123456789101112131415
   ```

文章知识点与官方知识档案匹配，可进一步学习相关知识

![image-20220326112635213](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/171-ubuntu%25E5%25AE%2589%25E8%25A3%2585/image-20220326112635213.png)

# frp搭建与使用详细教程

## 前置准备

- 外网服务器一台（或者有公网ip的机器如阿里服务器）；
- 内网服务器一台（win10电脑）；

## 下载脚本部署文件

下载地址：[GitHub地址](https://links.jianshu.com/go?to=http%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttps%3A%2F%2Fgithub.com%2Ffatedier%2Ffrp%2Freleases)

![img](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/171-ubuntu%25E5%25AE%2589%25E8%25A3%2585/webp-16482659409701.webp)

image.png


或者百度云盘下载：[https://pan.baidu.com/s/1yLXRrIE6Zlxebx8Ym22v2Q](https://links.jianshu.com/go?to=https%3A%2F%2Fpan.baidu.com%2Fs%2F1yLXRrIE6Zlxebx8Ym22v2Q)
提取码：q5dp



注意事项：
1）服务器端和内网机器端下载的版本要相同，否则可能会影响内网穿透
2）根据服务器系统选择合适的脚本

脚本主要分为服务端与客户端文件
1.外网服务器端用到的是Frps和Frps.ini
2.win10电脑用到的是Frpc和Frpc.ini

注：
服务端部署，可以只保留服务端文件 frps**
​客户端部署，可以只保留客户端文件 frpc**

### 外网服务器

#### 1、解压压缩包并命重命名文件夹：



```css
mkdir frp
tar  xzvf  frp_0.33.0_linux_386.tar.gz
mv  frp_0.33.0_linux_386  frp

创建frp文件夹，然后上传linux压缩包至文件夹并解压
```

#### 2、外网服务端配置

**2.1配置Frps.ini文件**
1.进入frp文件夹下：cd frp，修改frps.ini文件 （vim frps.ini）
2.修改完成，:wq 退出



```csharp
[common]
#内网穿透服务器端监听的IP地址，可以省略，默认为127.0.0.1
bind_addr = 0.0.0.0
#服务器端监听的端口，默认是7000，可自定义
bind_port = 7001
```

**2.2启动命令**
注：需要切换到文件目录



```swift
./frps -c frps.ini

Ctrl+C停止服务
```

**3.3启动日志**



```go
2019/03/23 17:27:41 [I] [service.go:136] frps tcp listen on 0.0.0.0:7001
2019/03/23 17:27:41 [I] [service.go:178] http service listen on 0.0.0.0:8006
2019/03/23 17:27:41 [I] [root.go:204] Start frps success
```

则说明服务器端已经启动Frp服务，监听的端口是7001。

### win10客户端配置

#### 1、解压压缩包并命重命名文件夹：

创建frp文件夹，然后下载的windows压缩包至文件夹并解压

#### 2、内网服务配置

**2.1内网机器配置Frpc.ini**
 1.进入frp文件夹下找到frpc.ini右击Notepade++打开
 2.修改完成，保存退出



```bash
[common]
#外网-服务器端ip
server_addr = xx.xx.xx.xx
#外网-服务器端监听的端口(必须与Frps.ini中的配置一致)
server_port = 7001

[ssh]
#配置类型为http协议
type = tcp
#内网机器的IP
local_ip = 127.0.0.1
#内网需要监听的端口（win10所启服务端口）
local_port = 9999
remote_port = 9999
use_encryption = true
# if true, message will be compressed
use_compression = true
```

启动命令

注：Ctrl+R 执行cmd  需要再frp文件路径下执行



```swift
./frpc -c frpc.ini

Ctrl+C停止服务
```

启动日志



```go
2019/03/23 17:28:21 **[I] [service.go:221] login to server success, get run id [3435ffb8820dbcf1], server udp port [0]**

2019/03/23 17:28:21 **[I] [proxy_manager.go:137] [3435ffb8820dbcf1] proxy added: [web]**

2019/03/23 17:28:21 **[I] [control.go:144] [web] start proxy success**
```

#### 访问内网http服务

1、启动服务端frps服务成功
 2、启动win10客户frpc服务成功
 3、启动需要映射本机服务成功
 server_addr:local_port

示例：http://148.70.12.345:9999
 访问成功，至此搭建成功！



作者：Nikon937
链接：https://www.jianshu.com/p/6be158cc3685
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## 设置frp开机自启

创建服务文件

```bash
sudo vim /etc/systemd/system/frpc.service
```

填入如下信息，`ExecStart`请自行替换

```ini
[Unit]
Description=Frp Client
After=network.target
Wants=network.target

[Service]
Restart=on-failure
RestartSec=5
ExecStart=/usr/local/frp/frpc_linux_arm

[Install]
WantedBy=multi-user.target
#刷新服务列表：
systemctl daemon-reload

#设置开机自启
systemctl enable frpc
#关闭开机自启
systemctl disable frpc

#启动服务
systemctl start frpc
#停止服务
systemctl stop frpc
#服务状态
systemctl status frpc
```

## 自测笔记

自启动

```
[Unit]
Description=Frp Client
After=network.target
Wants=network.target

[Service]
Restart=on-failure
RestartSec=5
ExecStart=/root/frp/frps -c /root/frp/frps.ini

[Install]
WantedBy=multi-user.target
```

# rabbitmq

常见的消息队列有：

- ActiveMQ
- RabbitMQ
- Kafka
- RocketMQ

接下来，我们主要掌握 RabbitMQ，官方文档 https://www.rabbitmq.com/

Ubuntu下安装步骤如下：

```javascript
# 更新源
$ sudo apt-get update

#卸载
$ apt remove rabbitmq-server

# 安装 RabbitMQ
$ sudo apt-get install rabbitmq-server

# 添加 admin 用户， 密码设置为 admin123
$ sudo rabbitmqctl add_user admin admin123

# 将 admin 用户设置为管理员角色
$ sudo rabbitmqctl set_user_tags admin administrator

# 设置 admin 赋权
$ sudo rabbitmqctl set_permissions -p / admin '.*' '.*' '.*'

# 启用图形管理界面
$ sudo rabbitmq-plugins enable rabbitmq_management
```

安装完成后，管理界面在15672端口，浏览器访问

[http://your-rabbitmq-server-ip:15672](http://your-rabbitmq-server-ip:15672/)

服务管理命令

```
sudo service rabbitmq-server stop
sudo service rabbitmq-server start
sudo service rabbitmq-server restart
```

Java中调用，添加pom依赖

```javascript
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.10.0</version>
</dependency>
```

Java代码如下

```javascript
import com.rabbitmq.client.*;

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.util.concurrent.TimeoutException;

public class Demo {
    public static void main(String[] args) throws IOException, TimeoutException {

        publish1();
        publish2();

        //consume();
    }


    private static void publish1() throws IOException, TimeoutException {
        //创建连接工厂
        ConnectionFactory factory = new ConnectionFactory();

        factory.setUsername("admin");
        factory.setPassword("admin123");

        //设置 RabbitMQ 地址
        factory.setHost("localhost");
        factory.setPort(5672);

        //建立到代理服务器到连接
        Connection conn = factory.newConnection();

        //获得信道
        Channel channel = conn.createChannel();

        //声明队列。
        //参数1：队列名
        //参数2：持久化 （true表示是，队列将在服务器重启时依旧存在）
        //参数3：独占队列（创建者可以使用的私有队列，断开后自动删除）
        //参数4：当所有消费者客户端连接断开时是否自动删除队列
        //参数5：队列的其他参数
        channel.queueDeclare("msg", true, false, false, null);

        //发布消息
        String message = "hello";

        // 基本发布消息
        // 第一个参数为交换机名称(空)
        // 第二个参数为队列映射的路由key(直接使用队列名)
        // 第三个参数为消息的其他属性、
        // 第四个参数为发送信息的主体
        channel.basicPublish("", "msg", MessageProperties.MINIMAL_PERSISTENT_BASIC, message.getBytes(StandardCharsets.UTF_8));

        channel.close();
        conn.close();
    }

    private static void publish2() throws IOException, TimeoutException {
        //创建连接工厂
        ConnectionFactory factory = new ConnectionFactory();

        factory.setUsername("admin");
        factory.setPassword("admin123");

        //设置 RabbitMQ 地址
        factory.setHost("localhost");
        factory.setPort(5672);

        //建立到代理服务器到连接
        Connection conn = factory.newConnection();

        //获得信道
        Channel channel = conn.createChannel();

        //声明交换器
        String exchangeName = "/chat";
        channel.exchangeDeclare(exchangeName, "direct", true);


        //声明队列。
        //参数1：队列名
        //参数2：持久化 （true表示是，队列将在服务器重启时依旧存在）
        //参数3：独占队列（创建者可以使用的私有队列，断开后自动删除）
        //参数4：当所有消费者客户端连接断开时是否自动删除队列
        //参数5：队列的其他参数
        channel.queueDeclare("msg", true, false, false, null);

        //队列绑定到交换机
        String routingKey = "tag1";
        channel.queueBind("msg", "/chat", routingKey);


        //发布消息
        String message = "hello";


        // 基本发布消息
        // 第一个参数为交换机名称、
        // 第二个参数为队列映射的路由key、
        // 第三个参数为消息的其他属性 指定持久化 (创建队列也需要配置持久化)
        // 第四个参数为发送信息的主体
        channel.basicPublish("/chat", "tag1", MessageProperties.MINIMAL_PERSISTENT_BASIC, message.getBytes(StandardCharsets.UTF_8));


        channel.close();
        conn.close();
    }

    private static void consume() throws IOException, TimeoutException {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setUsername("admin");
        factory.setPassword("admin123");

        //设置 RabbitMQ 地址
        factory.setHost("localhost");
        factory.setPort(5672);

        //建立到代理服务器到连接
        Connection conn = factory.newConnection();

        //获得信道
        Channel channel = conn.createChannel();

        //声明队列
        channel.queueDeclare("msg", true, false, false, null);

        while (true) {
            //消费消息
            boolean autoAck = false;
            String consumerTag = "";
            channel.basicConsume("msg", autoAck, consumerTag, new DefaultConsumer(channel) {
                @Override
                public void handleDelivery(String consumerTag,
                                           Envelope envelope,
                                           AMQP.BasicProperties properties,
                                           byte[] body) throws IOException {

                    String routingKey = envelope.getRoutingKey();
                    String contentType = properties.getContentType();

                    System.out.println("消费的路由键：" + routingKey);
                    System.out.println("消费的内容类型：" + contentType);

                    System.out.println("消费的消息体内容：");
                    String bodyStr = new String(body, "UTF-8");
                    System.out.println(bodyStr);

                    sleep(1000);

                    //确认消息
                    long deliveryTag = envelope.getDeliveryTag();
                    channel.basicAck(deliveryTag, false);

                }
            });
        }
    }

    private static void sleep(long t) {
        try {
            Thread.sleep(t);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

为`社区(论坛)`项目中添加邮件功能，在用户的每次登录时，发邮件，使用MQ完成。

```
张三 你好：
    你的帐号 jack 于yyy-mm-dd hh:ii:ss 登录xxx，IP地址为：xxx.xxx.xxx.xxx，如果非本人操作，请及时修改密码
```

