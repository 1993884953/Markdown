# Docker环境配置

### Docker-redis搭建

```shell
$ docker pull redis:latest
```

```shell
$ docker images
```

```shell
$ docker run -itd --name redis-test -p 6379:6379  redis
```

```shell
$ docker exec -it redis-test /bin/bash
```

```shell
配置文件
安装目录下的redis.conf
bind 0.0.0.0   //允许访问IP 0000为无限制
requirepass 123456   //修改密码
daemonize yes     	//守护进程（开启后台运行）
appendonly yes 		//持久化
protected mode no   //禁止外网访问  开启很危险
```

```
bind 0.0.0.0 
protected-mode no
appendonly yes
daemonize no
requirepass 123456
```

```shell
docker run -p 6379:6379 --name redis -v /root/redis_data/data:/data -v /root/redis_data/conf/redis.conf:/etc/redis/redis.conf -d redis redis-server /etc/redis/redis.conf --appendonly yes 
```

> mkdir -p /root/redis_data/conf/
>
> vi /root/redis_data/conf/redis.conf
>
> 加入以下内容
> bind 192.168.1.100 10.0.0.1
> bind 127.0.0.1 ::1
> bind 127.0.0.1

```shell
bind 0.0.0.0 

protected-mode no

port 6379

tcp-backlog 511

requirepass 123456

timeout 0

tcp-keepalive 300

daemonize no

supervised no

pidfile /var/run/redis_6379.pid

loglevel notice

logfile ""

databases 30

always-show-logo yes

save 900 1
save 300 10
save 60 10000

stop-writes-on-bgsave-error yes

rdbcompression yes

rdbchecksum yes

dbfilename dump.rdb

dir ./

replica-serve-stale-data yes

replica-read-only yes

repl-diskless-sync no

repl-disable-tcp-nodelay no

replica-priority 100

lazyfree-lazy-eviction no
lazyfree-lazy-expire no
lazyfree-lazy-server-del no
replica-lazy-flush no

appendonly yes

appendfilename "appendonly.aof"

no-appendfsync-on-rewrite no

auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb

aof-load-truncated yes

aof-use-rdb-preamble yes

lua-time-limit 5000

slowlog-max-len 128

notify-keyspace-events ""

hash-max-ziplist-entries 512
hash-max-ziplist-value 64

list-max-ziplist-size -2

list-compress-depth 0

set-max-intset-entries 512

zset-max-ziplist-entries 128
zset-max-ziplist-value 64

hll-sparse-max-bytes 3000

stream-node-max-bytes 4096
stream-node-max-entries 100

activerehashing yes

hz 10

dynamic-hz yes

aof-rewrite-incremental-fsync yes

rdb-save-incremental-fsync yes
```

### Docker-nacos 集群部署

#### 1.下载nacos镜像

```docker
docker search nacos-server  // 搜索nacos镜像 jerry6290/nacos-server
docker pull nacos-server    // 下载nacos镜像,特殊版本可以带版本号
docker pull jerry6290/nacos-server
```



#### 2.准备mysql

[https://github.com/alibaba/nacos/blob/develop/distribution/conf/nacos-mysql.sql](https://link.zhihu.com/?target=https%3A//github.com/alibaba/nacos/blob/develop/distribution/conf/nacos-mysql.sql)

```sql
/*
 * Copyright 1999-2018 Alibaba Group Holding Ltd.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info   */
/******************************************/
CREATE TABLE `config_info` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(255) DEFAULT NULL,
  `content` longtext NOT NULL COMMENT 'content',
  `md5` varchar(32) DEFAULT NULL COMMENT 'md5',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `src_user` text COMMENT 'source user',
  `src_ip` varchar(50) DEFAULT NULL COMMENT 'source ip',
  `app_name` varchar(128) DEFAULT NULL,
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  `c_desc` varchar(256) DEFAULT NULL,
  `c_use` varchar(64) DEFAULT NULL,
  `effect` varchar(64) DEFAULT NULL,
  `type` varchar(64) DEFAULT NULL,
  `c_schema` text,
  `encrypted_data_key` text NOT NULL COMMENT '秘钥',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfo_datagrouptenant` (`data_id`,`group_id`,`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_info';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info_aggr   */
/******************************************/
CREATE TABLE `config_info_aggr` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(255) NOT NULL COMMENT 'group_id',
  `datum_id` varchar(255) NOT NULL COMMENT 'datum_id',
  `content` longtext NOT NULL COMMENT '内容',
  `gmt_modified` datetime NOT NULL COMMENT '修改时间',
  `app_name` varchar(128) DEFAULT NULL,
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfoaggr_datagrouptenantdatum` (`data_id`,`group_id`,`tenant_id`,`datum_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='增加租户字段';


/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info_beta   */
/******************************************/
CREATE TABLE `config_info_beta` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(128) NOT NULL COMMENT 'group_id',
  `app_name` varchar(128) DEFAULT NULL COMMENT 'app_name',
  `content` longtext NOT NULL COMMENT 'content',
  `beta_ips` varchar(1024) DEFAULT NULL COMMENT 'betaIps',
  `md5` varchar(32) DEFAULT NULL COMMENT 'md5',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `src_user` text COMMENT 'source user',
  `src_ip` varchar(50) DEFAULT NULL COMMENT 'source ip',
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  `encrypted_data_key` text NOT NULL COMMENT '秘钥',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfobeta_datagrouptenant` (`data_id`,`group_id`,`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_info_beta';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info_tag   */
/******************************************/
CREATE TABLE `config_info_tag` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(128) NOT NULL COMMENT 'group_id',
  `tenant_id` varchar(128) DEFAULT '' COMMENT 'tenant_id',
  `tag_id` varchar(128) NOT NULL COMMENT 'tag_id',
  `app_name` varchar(128) DEFAULT NULL COMMENT 'app_name',
  `content` longtext NOT NULL COMMENT 'content',
  `md5` varchar(32) DEFAULT NULL COMMENT 'md5',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `src_user` text COMMENT 'source user',
  `src_ip` varchar(50) DEFAULT NULL COMMENT 'source ip',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfotag_datagrouptenanttag` (`data_id`,`group_id`,`tenant_id`,`tag_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_info_tag';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_tags_relation   */
/******************************************/
CREATE TABLE `config_tags_relation` (
  `id` bigint(20) NOT NULL COMMENT 'id',
  `tag_name` varchar(128) NOT NULL COMMENT 'tag_name',
  `tag_type` varchar(64) DEFAULT NULL COMMENT 'tag_type',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(128) NOT NULL COMMENT 'group_id',
  `tenant_id` varchar(128) DEFAULT '' COMMENT 'tenant_id',
  `nid` bigint(20) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`nid`),
  UNIQUE KEY `uk_configtagrelation_configidtag` (`id`,`tag_name`,`tag_type`),
  KEY `idx_tenant_id` (`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_tag_relation';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = group_capacity   */
/******************************************/
CREATE TABLE `group_capacity` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键ID',
  `group_id` varchar(128) NOT NULL DEFAULT '' COMMENT 'Group ID，空字符表示整个集群',
  `quota` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '配额，0表示使用默认值',
  `usage` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '使用量',
  `max_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个配置大小上限，单位为字节，0表示使用默认值',
  `max_aggr_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '聚合子配置最大个数，，0表示使用默认值',
  `max_aggr_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个聚合数据的子配置大小上限，单位为字节，0表示使用默认值',
  `max_history_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '最大变更历史数量',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_group_id` (`group_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='集群、各Group容量信息表';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = his_config_info   */
/******************************************/
CREATE TABLE `his_config_info` (
  `id` bigint(20) unsigned NOT NULL,
  `nid` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `data_id` varchar(255) NOT NULL,
  `group_id` varchar(128) NOT NULL,
  `app_name` varchar(128) DEFAULT NULL COMMENT 'app_name',
  `content` longtext NOT NULL,
  `md5` varchar(32) DEFAULT NULL,
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `src_user` text,
  `src_ip` varchar(50) DEFAULT NULL,
  `op_type` char(10) DEFAULT NULL,
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  `encrypted_data_key` text NOT NULL COMMENT '秘钥',
  PRIMARY KEY (`nid`),
  KEY `idx_gmt_create` (`gmt_create`),
  KEY `idx_gmt_modified` (`gmt_modified`),
  KEY `idx_did` (`data_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='多租户改造';


/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = tenant_capacity   */
/******************************************/
CREATE TABLE `tenant_capacity` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键ID',
  `tenant_id` varchar(128) NOT NULL DEFAULT '' COMMENT 'Tenant ID',
  `quota` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '配额，0表示使用默认值',
  `usage` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '使用量',
  `max_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个配置大小上限，单位为字节，0表示使用默认值',
  `max_aggr_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '聚合子配置最大个数',
  `max_aggr_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个聚合数据的子配置大小上限，单位为字节，0表示使用默认值',
  `max_history_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '最大变更历史数量',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_tenant_id` (`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='租户容量信息表';


CREATE TABLE `tenant_info` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `kp` varchar(128) NOT NULL COMMENT 'kp',
  `tenant_id` varchar(128) default '' COMMENT 'tenant_id',
  `tenant_name` varchar(128) default '' COMMENT 'tenant_name',
  `tenant_desc` varchar(256) DEFAULT NULL COMMENT 'tenant_desc',
  `create_source` varchar(32) DEFAULT NULL COMMENT 'create_source',
  `gmt_create` bigint(20) NOT NULL COMMENT '创建时间',
  `gmt_modified` bigint(20) NOT NULL COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_tenant_info_kptenantid` (`kp`,`tenant_id`),
  KEY `idx_tenant_id` (`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='tenant_info';

CREATE TABLE `users` (
	`username` varchar(50) NOT NULL PRIMARY KEY,
	`password` varchar(500) NOT NULL,
	`enabled` boolean NOT NULL
);

CREATE TABLE `roles` (
	`username` varchar(50) NOT NULL,
	`role` varchar(50) NOT NULL,
	UNIQUE INDEX `idx_user_role` (`username` ASC, `role` ASC) USING BTREE
);

CREATE TABLE `permissions` (
    `role` varchar(50) NOT NULL,
    `resource` varchar(255) NOT NULL,
    `action` varchar(8) NOT NULL,
    UNIQUE INDEX `uk_role_permission` (`role`,`resource`,`action`) USING BTREE
);

INSERT INTO users (username, password, enabled) VALUES ('nacos', '$2a$10$EuWPZHzz32dJN7jexM34MOeYirDdFAZm2kuWj7VEOJhhZkDrxfvUu', TRUE);

INSERT INTO roles (username, role) VALUES ('nacos', 'ROLE_ADMIN');
```



#### 3.容器运行

**3.1 nacos1**

```docker
docker run -d \
-e PREFER_HOST_MODE=hostname \
-e MODE=cluster \
-e NACOS_SERVERS="106.15.65.54:8845 106.15.65.54:8846 106.15.65.54:8847" \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=123456 \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e NACOS_SERVER_IP=106.15.65.54 \
-p 8845:8848 \
--name nacos1 \
nacos/nacos-server:latest
```

**3.2 nacos2**

```docker
docker run -d \
-e PREFER_HOST_MODE=hostname \
-e MODE=cluster \
-e NACOS_SERVERS="106.15.65.54:8845 106.15.65.54:8846 106.15.65.54:8847" \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=jack \
-e MYSQL_SERVICE_PASSWORD=123 \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e NACOS_SERVER_IP=106.15.65.54 \
-p 8846:8848 \
--name nacos2 \
nacos/nacos-server:latest
```

**3.3 nacos3**

```docker
docker run -d \
-e PREFER_HOST_MODE=hostname \
-e MODE=cluster \
-e NACOS_SERVERS="106.15.65.54:8845 106.15.65.54:8846 106.15.65.54:8847" \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=jack \
-e MYSQL_SERVICE_PASSWORD=123 \
-e MYSQL_SERVICE_DB_NAME=nacos \
-e NACOS_SERVER_IP=106.15.65.54 \
-p 8847:8848 \
--name nacos3 \
nacos/nacos-server:latest
```

##### 3.4 测试容器是否启动成功

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153438.jpg)

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153440.jpg)

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153441.jpg)



#### 4.使用Nginx反向代理Nacos集群

```yml
spring:
application:
name: order-service
cloud:
nacos:
discovery:
server-addr: ip:80 # nginx负责反向代理 负载均衡
```



使用`docker pull nginx`拉取nginx的最新版本,使用如下指令创建一个nginx容器:

```css
docker run --name my-nginx -p 8848:8080 -d nginx
```

获得了一个nginx容器后使用指令:

```bash
docker cp 你的容器id:/etc/nginx/nginx.conf /usr/local/nginx/conf/nginx.conf
```

这一步可以将容器中的nginx配置文件拷贝到宿主机中的/usr/local/nginx/conf目录下。 使用`docker stop 容器id`和`docker rm 容器id`停止并删除之前创建的nginx容器。

```perl
docker run --restart=always --name my-nginx -v /usr/local/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -p 8848:80 -d nginx
```

```
docker run --restart=always --name my-nginx 
-v /usr/local/nginx/conf/nginx.conf:/etc/nginx/nginx.conf 
-v /home/nginx/dist:/usr/share/nginx/html
-p 8080:80 -d nginx
```

使用该指令得到一个全新的nginx容器,并且我们通过修改宿主机中的`/usr/local/nginx/conf/nginx.conf` 文件即可修改nginx容器中的配置文件,我们使用命令`vi /usr/local/nginx/conf/nginx.conf`使用i键进入修改模式,在文件的末尾添加下面的内容

```ini
http {
    
    # 配置两台上游服务器，例如是 Java 启动的 Spring Boot 服务
    upstream backend {
        server 106.15.65.54:8845 weight=1 max_fails=0;
        server 106.15.65.54:8846 weight=1 max_fails=0;
        server 106.15.65.54:8847 weight=1 max_fails=0;
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

完成修改后esc退出修改模式,shift+zz完成修改并退出。 使用`docker restart my-nginx`重启nginx容器后访问`http://192.168.248.129:8080/nacos`发现进入到nacos的管理后台,于是乎使用Nginx反向代理Nacos集群也已经完成了。 ![反向代理完成](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153442.png)

**本次博客的内容也到此为止了,如果对博客内容有疑问可以私信联系笔者，如果这篇文章对你有用希望你能点一个赞，谢谢~**

BDawn: [使用docker部署nacos集群](https://link.juejin.cn/?target=https%3A%2F%2Fblog.csdn.net%2FBDawn%2Farticle%2Fdetails%2F106234675).

```
docker run  -p 8181:8181 xggz/mqr:latest 
```



### 集群部署2

```shell
docker run -d   \
--restart=always \
 -e PREFER_HOST_MODE=hostname \
-e MODE=standalone \
 -e NACOS_SERVER_PORT=8848 \
 -e NACOS_SERVER_IP=124.221.172.234 \
 -e NACOS_SERVERS="124.221.172.234:8848" \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=jack123 \
-e MYSQL_SERVICE_DB_NAME=nacos \
 -p 8848:8848  \
 --name nacos-server8848 \
 --ip 124.221.172.234 \
 nacos/nacos-server:1.4.2
```

```
docker run -d \
-e MODE=standalone \
-e PREFER_HOST_MODE=hostname \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=jack \
-e MYSQL_SERVICE_DB_NAME=nacos \
-p 8848:8848 \
--name nacos-server \
--restart=always \
nacos/nacos-server:1.4.2
```



```shell
# 创建一个自定义网络
docker network ls
docker network create --driver bridge --subnet=172.20.0.0/16 --gateway=172.20.0.1 mynetwork
docker network inspect mynetwork

#创建Nacos容器
docker run -d --restart=always  \
 -e PREFER_HOST_MODE=hostname \
 -e MODE=cluster \
 -e NACOS_SERVER_PORT=8848 \
 -e NACOS_SERVER_IP=172.20.0.2 \
 -e NACOS_SERVERS="172.20.0.2:8848 172.20.0.3:8848 172.20.0.4:8848" \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=123456 \
-e MYSQL_SERVICE_DB_NAME=nacos \
 -p 8845:8848 --net=mynetwork \
 --name nacos-server8845 \
 --ip 172.20.0.2 \
 nacos/nacos-server:latest
 
 
docker run -d --restart=always \
 -e PREFER_HOST_MODE=hostname \
 -e MODE=cluster \
 -e NACOS_SERVER_PORT=8848 \
 -e NACOS_SERVER_IP=172.20.0.3 \
 -e NACOS_SERVERS="172.20.0.2:8848 172.20.0.3:8848 172.20.0.4:8848" \
 -e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=123456 \
-e MYSQL_SERVICE_DB_NAME=nacos \
 -p 8846:8848 --net=mynetwork \
 --name nacos-server8846 \
 --ip 172.20.0.3 \
 nacos/nacos-server:latest
 
docker run -d --restart=always \
 -e PREFER_HOST_MODE=hostname \
 -e MODE=cluster \
 -e NACOS_SERVER_PORT=8848 \
 -e NACOS_SERVER_IP=172.20.0.4 \
 -e NACOS_SERVERS="172.20.0.2:8848 172.20.0.3:8848 172.20.0.4:8848" \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=124.221.172.234 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=123456 \
-e MYSQL_SERVICE_DB_NAME=nacos \
 -p 8847:8848 --net=mynetwork \
 --name nacos-server8847 \
 --ip 172.20.0.4 \
 nacos/nacos-server:latest
```



### Docker-mysql一主双从

https://blog.csdn.net/u014592931/article/details/124725951

版权

1、主从数据库原理

```
读写分离，基本的原理是让主数据库处理事务性增、改、删操作（INSERT、UPDATE、DELETE），
而从数据库处理SELECT查询操作。数据库复制被用来把事务性操作导致的变更同步到集群中的从
数据库(此处依赖组从复制).
```

2、读写分离的原因

```
数据库写入效率要低于读取效率，一般系统中数据读取频率高于写入频率，单个数据库实例在写入的时候会影响读取性能，
这是做读写分离的原因.
什么时候用读写分离
数据库不一定要读写分离，如果程序使用数据库，更新多，而查询少的情况下不会考虑使用。利用数据库主从同步，再
通过读写分离可以分担数据库压力，提高查询及写入性能。
```

3、实现机制

```
MySQL服务器之间的主从同步是基于`二进制日志机制`，主服务器使用二进制日志来记录数据库的变动情况
从服务器通过读取和执行该日志文件来保持和主服务器的数据一致
```

![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153443.png)

4、实现主从数据的搭建（基于[docker](https://so.csdn.net/so/search?q=docker&spm=1001.2101.3001.7020)）

5、拉取最新的mysql镜像

```
docker pull mysql:5.7.13
```

![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153444.png)

6、配置主数据库

```shell
# a、文件夹用于存放配置文件以及数据库数据
mkdir -p /root/mysql_data/mysql_master/mysql.conf.d
touch /root/mysql_data/mysql_master/mysql.conf.d/mysqld.cnf
vi 	/root/mysql_data/mysql_master/mysql.conf.d/mysqld.cnf
	
#a、主机配置  
[mysqld]
## 同一局域网内注意要唯一
server-id=100
## 开启二进制日志功能，可以随便取（关键）
log-bin=mysql-bin

#二级制日志格式，有三种 row，statement，mixed
#binlog-format=ROW
#同步的数据库，不配的话就是同步所有库
#binlog-do-db=test
#不同步的数据库
#binlog-ignore-db=mysql
#binlog-ignore-db=information_schema
#binlog-ignore-db=performation_schema
#binlog-ignore-db=sys
```

7、配置从数据库

```shell
mkdir -p /root/mysql_data/mysql_slave/mysql_master/data
mkdir -p /root/mysql_data/mysql_slave/mysql_master/mysql.conf.d
vi /root/mysql_data/mysql_slave/mysql.conf.d/mysqld.cnf
#b、从机配置 
[mysqld]
## 设置server_id,注意要唯一
server-id=101  
## 开启二进制日志功能，以备Slave作为其它Slave的Master时使用
log-bin=mysql-slave-bin   
## relay_log配置中继日志
relay_log=edu-mysql-relay-bin  

#设置为只读
read_only=1
```

8、创建对应的docker

```shell
#2.启动master
sudo docker run  -d --name mysql-master -p 3306:3306 -e MYSQL_ROOT_PASSWORD=jack123 \
--restart=always \
-v /etc/localtime:/etc/localtime \
-v /root/mysql_data/mysql_master/data:/var/lib/mysql \
-v /root/mysql_data/mysql_master/mysql.conf.d:/etc/mysql/conf.d mysql:5.7.13
        
#3.启动slave         
sudo docker run  -d --name mysql-slave -p 3307:3306 -e MYSQL_ROOT_PASSWORD=123456 \
--restart=always \
-v /root/mysql_data/mysql_slave/data:/var/lib/mysql \
-v /root/mysql_data/mysql_slave/mysql.conf.d:/etc/mysql/conf.d mysql:5.7.13

注意点：映射文件夹路径必须写绝对路径 映射端口不要出现冲突

#3.启动slave1     
sudo docker run  -d --name mysql-slave2 -p 3308:3306 -e MYSQL_ROOT_PASSWORD=123456 \
-v /root/mysql_data/mysql_slave2/data:/var/lib/mysql \
-v /root/mysql_data/mysql_slave2/mysql.conf.d:/etc/mysql/conf.d mysql:5.7.13
```

![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153445.png)

9、验证数据是否启动正常

```shell
是否能够正常链接
mysql -uroot -p123456 -h 124.221.172.234 --port=3306
mysql -uroot -p123456 -h 124.221.172.234 --port=3307
mysql -uroot -p123456 -h 124.221.172.234 --port=3308
```

10、配置master



```shell
# 登录到主机
mysql -uroot -p123456 -h 124.221.172.234 --port=3306

# 创建从机账号
CREATE USER slave IDENTIFIED BY 'slave';
#mysql> drop user 'slave'@'%';
#mysql> flush privileges; 
GRANT SELECT, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'slave'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'slave'@'%';
# 刷新权限
FLUSH PRIVILEGES;
# 查看二进制日志信息, 记录 文件名 和 偏移量, 后面会用到
mysql> SHOW MASTER STATUS;
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000003 |     955  |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------+
```

11、配置slave

```shell
# 登录到从机
$ mysql -uroot -p123456 -h 124.221.172.234 -P3307
# 从机连接到主机
$ change master to master_host='124.221.172.234', master_port=3306, master_user='slave', master_password='slave', master_log_file='mysql-bin.000003', master_log_pos=955;
# 停止从机服务
$ STOP SLAVE;
# 开启从机服务
$ start slave;
$ show slave status\G;
```

12、注意点

```shell
a、master_log_file、以及master_log_pos一定要对应上，否则无法链接
b、如出现Authentication plugin 'caching_sha2_password' reported error: Authentication requires secure connection. 
Error_code: MY-002061问题，是密码插件问题，如下修改即可
ALTER USER 'slave'@'%' IDENTIFIED WITH mysql_native_password BY 'slave';
FLUSH PRIVILEGES;
```

![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153446.png)



###  Docker-sentinel dockerfile

#### **Dockerfile文件**

```
java -Dserver.port=10011 -Dcsp.sentinel.dashboard.server=localhost:10011 -Dproject.name=sentinel-dashboard -jar ./sentinel-dashboard-1.8.1.jar
```





```dockerfile
#这是基础镜像
#FROM openjdk
#目前我找到最小的jdk包
FROM dquintela/openjdk-8-jdk-alpine
#镜像的制作人
MAINTAINER 1993884953@qq.com


#工作目录
#WORKDIR /game/server/wry-user-server

#复制jar包到镜像中，并且将名字改成 app.jar
#COPY target/*.jar app.jar
COPY ./*.jar app.jar
WORKDIR /tmp

# 在容器启动的时候运行命里，来启动我们的项目 （这其实就是一段Linux命令）

# 这个启动命里根据你的实际情况更改

ENTRYPOINT ["java","-jar","/app.jar"]
ENTRYPOINT ["java","-jar","/sentinel-dashboard.jar"]
```

### Docker-rabbit

```
docker run \
 -e RABBITMQ_DEFAULT_USER=admin \
 -e RABBITMQ_DEFAULT_PASS=admin \
 --name rabbitmq \
 --hostname rabbitmq \
 -p 15672:15672 \
 -p 5672:5672 \
 -d \
 -v /root/rabbit_data/rabbitmq:/var/lib/rabbitmq \
rabbitmq:management
```



```shell
docker run \
 -e RABBITMQ_DEFAULT_USER=admin \
 -e RABBITMQ_DEFAULT_PASS=admin \
 --name rabbitmq \
 --hostname rabbitmq \
 -p 15672:15672 \
 -p 5672:5672 \
 -d \
 -v /root/rabbit_data/rabbitmq:/var/lib/rabbitmq \
rabbitmq:3.9.9-management
```

### [远程CA证书](https://zhuanlan.zhihu.com/p/361907950)

**1.创建Docker CA文件夹，存放CA私钥和公钥**

> mkdir -p /usr/local/docker-ca
> cd /usr/local/docker-ca

**2.【**创建证书**】利用openssl生成私钥。**执行：

> openssl genrsa -aes256 -out ca-key.pem 4096

**接下来需要连续输入两次私钥密码：**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153447.jpg)

**3.【**创建证书**】利用openssl生成自签证书。**执行：

> openssl req -new -x509 -days 365 -key ca-key.pem -sha256 -out ca.pem

其中指令含义为：

*-x509：专用于CA生成自签证书，如果不是自签证书则不需要此项*

-days：证书的有效期限，单位是day（天），默认是365天

**接下来需要连续输入刚刚的私钥密码、国家、省、市、组织名称等：**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153448.jpg)

**4.【**颁发服务端证书**】利用openssl在需要使用证书的主机上生成服务端私钥。**执行：

> openssl genrsa -out server-key.pem 4096

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153449.jpg)

**5.【**颁发服务端证书**】利用openssl生成服务端证书签名请求文件。**执行：

> openssl req -subj "/CN=$HOST" -sha256 -new -key server-key.pem -out server.csr

**其中$Host换成你自己服务器外网的IP（或者换成域名，都可）**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153450.jpg)

**6.【**颁发服务端证书**】创建服务端证书扩展配置文件，配置白名单。**因为如此配置后已经是SSL连接，所以笔者这里推荐配置0.0.0.0，即所有IP均可以连接，但只有拥有证书的才可以连接成功。

**若第五步$HOST填写的是ip地址的话，$Host换成你自己服务器外网的IP，执行下面命令：**

> echo subjectAltName = IP:$HOST,IP:0.0.0.0 >> extfile.cnf

**若第五步$HOST填写的是域名的话，$Host换成你自己的域名，执行下面命令：**

> **echo subjectAltName = DNS:$HOST,IP:0.0.0.0 >> extfile.cnf**

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153451.jpg)

执行命令，将扩展使用属性设置为仅用于服务器身份验证：

> echo extendedKeyUsage = serverAuth >> extfile.cnf

**7.【**颁发服务端证书**】根据证书签署请求文件颁发服务端证书。**执行：

> openssl x509 -req -days 365 -sha256 -in server.csr -CA ca.pem -CAkey ca-key.pem \-CAcreateserial -out server-cert.pem -extfile extfile.cnf

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153452.jpg)

**8.【**颁发客户端证书**】利用openssl生成客户端私钥。**执行：

> openssl genrsa -out key.pem 4096

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153453.jpg)

**9.【**颁发客户端证书**】利用openssl生成客户端证书签名请求文件。**执行：

> openssl req -subj '/CN=client' -new -key key.pem -out client.csr

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153454.jpg)

**10.【**颁发客户端证书**】创建服务端证书扩展配置文件。**执行：

> echo extendedKeyUsage = clientAuth >> extfile.cnf

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153455.jpg)

**11.【**颁发客户端证书**】根据证书签署请求文件颁发客户端证书。**执行：

> openssl x509 -req -days 365 -sha256 -in client.csr -CA ca.pem -CAkey ca-key.pem \-CAcreateserial -out cert.pem -extfile extfile.cnf

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153456.jpg)

**12.【归集文件】删除无必要的证书签名请求文件。**执行：

> rm -v client.csr server.csr

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153457.jpg)

**13.【归集文件】归集服务器证书。**执行：

```
cp server-*.pem /etc/docker/
cp ca.pem /etc/docker/
```

**14.修改Docker配置。修改Docker守护程序仅接受来自提供CA信任的证书的客户端的连接：**

> vim /lib/systemd/system/docker.service

**修改ExecStart，为其添加四个指令：**

> ExecStart=/usr/bin/dockerd --tlsverify --tlscacert=/etc/docker/ca.pem --tlscert=/etc/docker/server-cert.pem --tlskey=/etc/docker/server-key.pem -H tcp://0.0.0.0:2376 -H unix:///var/run/docker.sock

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153458.jpg)

**15.重启Docker：**

> systemctl daemon-reload
> systemctl restart docker

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153459.jpg)

#### idea配

```shell
# 下载证书
scp root@124.221.172.234:/usr/local/docker-ca/* ./
```



![image-20220814201914211](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153460.png)

![image-20220811183349255](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153461.png)



#  SpringCloud01





## 1.认识微服务

随着互联网行业的发展，对服务的要求也越来越高，服务架构也从单体架构逐渐演变为现在流行的微服务架构。这些架构之间有怎样的差别呢？

### 1.0.学习目标

了解微服务架构的优缺点





### 1.1.单体架构

**单体架构**：将业务的所有功能集中在一个项目中开发，打成一个包部署。

![image-20210713202807818](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153462.png)

单体架构的优缺点如下：

**优点：**

- 架构简单
- 部署成本低

**缺点：**

- 耦合度高（维护困难、升级困难）



### 1.2.分布式架构

**分布式架构**：根据业务功能对系统做拆分，每个业务功能模块作为独立项目开发，称为一个服务。

![image-20210713203124797](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153463.png)



分布式架构的优缺点：

**优点：**

- 降低服务耦合
- 有利于服务升级和拓展

**缺点：**

- 服务调用关系错综复杂



分布式架构虽然降低了服务耦合，但是服务拆分时也有很多问题需要思考：

- 服务拆分的粒度如何界定？
- 服务之间如何调用？
- 服务的调用关系如何管理？

人们需要制定一套行之有效的标准来约束分布式架构。



### 1.3.微服务

微服务的架构特征：

- 单一职责：微服务拆分粒度更小，每一个服务都对应唯一的业务能力，做到单一职责
- 自治：团队独立、技术独立、数据独立，独立部署和交付
- 面向服务：服务提供统一标准的接口，与语言和技术无关
- 隔离性强：服务调用做好隔离、容错、降级，避免出现级联问题

![image-20210713203753373](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153464.png)

微服务的上述特性其实是在给分布式架构制定一个标准，进一步降低服务之间的耦合度，提供服务的独立性和灵活性。做到高内聚，低耦合。

因此，可以认为**微服务**是一种经过良好架构设计的**分布式架构方案** 。

但方案该怎么落地？选用什么样的技术栈？全球的互联网公司都在积极尝试自己的微服务落地方案。

其中在Java领域最引人注目的就是SpringCloud提供的方案了。

### 1.4.SpringCloud

SpringCloud是目前国内使用最广泛的微服务框架。官网地址：https://spring.io/projects/spring-cloud。

SpringCloud集成了各种微服务功能组件，并基于SpringBoot实现了这些组件的自动装配，从而提供了良好的开箱即用体验。

其中常见的组件包括：

![image-20210713204155887](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153465.png)



另外，SpringCloud底层是依赖于SpringBoot的，并且有版本的兼容关系，如下：

![image-20210713205003790](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153466.png)

我们课堂学习的版本是 Hoxton.SR10，因此对应的SpringBoot版本是2.3.x版本。



### 1.5.总结

- 单体架构：简单方便，高度耦合，扩展性差，适合小型项目。例如：学生管理系统

- 分布式架构：松耦合，扩展性好，但架构复杂，难度大。适合大型互联网项目，例如：京东、淘宝

- 微服务：一种良好的分布式架构方案

  ①优点：拆分粒度更小、服务更独立、耦合度更低

  ②缺点：架构非常复杂，运维、监控、部署难度提高

- SpringCloud是微服务架构的一站式解决方案，集成了各种优秀微服务功能组件





## 2.服务拆分和远程调用

任何分布式架构都离不开服务的拆分，微服务也是一样。

### 2.1.服务拆分原则

这里我总结了微服务拆分时的几个原则：

- 不同微服务，不要重复开发相同业务
- 微服务数据独立，不要访问其它微服务的数据库
- 微服务可以将自己的业务暴露为接口，供其它微服务调用

![image-20210713210800950](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153467.png)



### 2.2.服务拆分示例

以课前资料中的微服务cloud-demo为例，其结构如下：

![image-20210713211009593](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153468.png)

cloud-demo：父工程，管理依赖

- order-service：订单微服务，负责订单相关业务
- user-service：用户微服务，负责用户相关业务

要求：

- 订单微服务和用户微服务都必须有各自的数据库，相互独立
- 订单服务和用户服务都对外暴露Restful的接口
- 订单服务如果需要查询用户信息，只能调用用户服务的Restful接口，不能查询用户数据库



#### 2.2.1.导入Sql语句

首先，将课前资料提供的`cloud-order.sql`和`cloud-user.sql`导入到mysql中：

![image-20210713211417049](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153469.png)



cloud-user表中初始数据如下：

![image-20210713211550169](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153470.png)

cloud-order表中初始数据如下：

![image-20210713211657319](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153471.png)



cloud-order表中持有cloud-user表中的id字段。



#### 2.2.2.导入demo工程

用IDEA导入课前资料提供的Demo：

![image-20210713211814094](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153472.png)



项目结构如下：

![image-20210713212656887](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153473.png)





导入后，会在IDEA右下角出现弹窗：

![image-20210713212349272](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153474.png)

点击弹窗，然后按下图选择：

![image-20210713212336185](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153475.png)

会出现这样的菜单：

![image-20210713212513324](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153476.png)



配置下项目使用的JDK：

![image-20210713220736408](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153477.png)



### 2.3.实现远程调用案例



在order-service服务中，有一个根据id查询订单的接口：

![image-20210713212749575](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153478.png)

根据id查询订单，返回值是Order对象，如图：

![image-20210713212901725](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153479.png)

其中的user为null





在user-service中有一个根据id查询用户的接口：

![image-20210713213146089](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153480.png)

查询的结果如图：

![image-20210713213213075](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153481.png)





#### 2.3.1.案例需求：

修改order-service中的根据id查询订单业务，要求在查询订单的同时，根据订单中包含的userId查询出用户信息，一起返回。

![image-20210713213312278](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153482.png)



因此，我们需要在order-service中 向user-service发起一个http的请求，调用http://localhost:8081/user/{userId}这个接口。

大概的步骤是这样的：

- 注册一个RestTemplate的实例到Spring容器
- 修改order-service服务中的OrderService类中的queryOrderById方法，根据Order对象中的userId查询User
- 将查询的User填充到Order对象，一起返回



#### 2.3.2.注册RestTemplate

首先，我们在order-service服务中的OrderApplication启动类中，注册RestTemplate实例：

```java
package cn.itcast.order;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.web.client.RestTemplate;

@MapperScan("cn.itcast.order.mapper")
@SpringBootApplication
public class OrderApplication {

    public static void main(String[] args) {
        SpringApplication.run(OrderApplication.class, args);
    }

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```



#### 2.3.3.实现远程调用

修改order-service服务中的cn.itcast.order.service包下的OrderService类中的queryOrderById方法：

![image-20210713213959569](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153483.png)







### 2.4.提供者与消费者

在服务调用关系中，会有两个不同的角色：

**服务提供者**：一次业务中，被其它微服务调用的服务。（提供接口给其它微服务）

**服务消费者**：一次业务中，调用其它微服务的服务。（调用其它微服务提供的接口）

![image-20210713214404481](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153484.png)



但是，服务提供者与服务消费者的角色并不是绝对的，而是相对于业务而言。

如果服务A调用了服务B，而服务B又调用了服务C，服务B的角色是什么？

- 对于A调用B的业务而言：A是服务消费者，B是服务提供者
- 对于B调用C的业务而言：B是服务消费者，C是服务提供者



因此，服务B既可以是服务提供者，也可以是服务消费者。





## 3.Eureka注册中心



假如我们的服务提供者user-service部署了多个实例，如图：

![image-20210713214925388](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153485.png)



大家思考几个问题：

- order-service在发起远程调用的时候，该如何得知user-service实例的ip地址和端口？
- 有多个user-service实例地址，order-service调用时该如何选择？
- order-service如何得知某个user-service实例是否依然健康，是不是已经宕机？



### 3.1.Eureka的结构和作用

这些问题都需要利用SpringCloud中的注册中心来解决，其中最广为人知的注册中心就是Eureka，其结构如下：

![image-20210713220104956](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153486.png)



回答之前的各个问题。

问题1：order-service如何得知user-service实例地址？

获取地址信息的流程如下：

- user-service服务实例启动后，将自己的信息注册到eureka-server（Eureka服务端）。这个叫服务注册
- eureka-server保存服务名称到服务实例地址列表的映射关系
- order-service根据服务名称，拉取实例地址列表。这个叫服务发现或服务拉取



问题2：order-service如何从多个user-service实例中选择具体的实例？

- order-service从实例列表中利用负载均衡算法选中一个实例地址
- 向该实例地址发起远程调用



问题3：order-service如何得知某个user-service实例是否依然健康，是不是已经宕机？

- user-service会每隔一段时间（默认30秒）向eureka-server发起请求，报告自己状态，称为心跳
- 当超过一定时间没有发送心跳时，eureka-server会认为微服务实例故障，将该实例从服务列表中剔除
- order-service拉取服务时，就能将故障实例排除了



> 注意：一个微服务，既可以是服务提供者，又可以是服务消费者，因此eureka将服务注册、服务发现等功能统一封装到了eureka-client端



因此，接下来我们动手实践的步骤包括：

![image-20210713220509769](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153487.png)



### 3.2.搭建eureka-server

首先大家注册中心服务端：eureka-server，这必须是一个独立的微服务

#### 3.2.1.创建eureka-server服务

在cloud-demo父工程下，创建一个子模块：

![image-20210713220605881](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153488.png)

填写模块信息：

![image-20210713220857396](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153489.png)



然后填写服务信息：

![image-20210713221339022](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153490.png)



#### 3.2.2.引入eureka依赖

引入SpringCloud为eureka提供的starter依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```



#### 3.2.3.编写启动类

给eureka-server服务编写一个启动类，一定要添加一个@EnableEurekaServer注解，开启eureka的注册中心功能：

```java
package cn.itcast.eureka;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }
}
```



#### 3.2.4.编写配置文件

编写一个application.yml文件，内容如下：

```yaml
server:
  port: 10086
spring:
  application:
    name: eureka-server
eureka:
  client:
    service-url: 
      defaultZone: http://127.0.0.1:10086/eureka
```



#### 3.2.5.启动服务

启动微服务，然后在浏览器访问：http://127.0.0.1:10086

看到下面结果应该是成功了：

![image-20210713222157190](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153491.png)







### 3.3.服务注册

下面，我们将user-service注册到eureka-server中去。

#### 1）引入依赖

在user-service的pom文件中，引入下面的eureka-client依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```



#### 2）配置文件

在user-service中，修改application.yml文件，添加服务名称、eureka地址：

```yaml
spring:
  application:
    name: userservice
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10086/eureka
```



#### 3）启动多个user-service实例

为了演示一个服务有多个实例的场景，我们添加一个SpringBoot的启动配置，再启动一个user-service。



首先，复制原来的user-service启动配置：

![image-20210713222656562](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153492.png)

然后，在弹出的窗口中，填写信息：**-Dserver.port-8082**

![image-20210713222757702](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153493.png)



现在，SpringBoot窗口会出现两个user-service启动配置：

![image-20210713222841951](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153494.png)

不过，第一个是8081端口，第二个是8082端口。

启动两个user-service实例：

![image-20210713223041491](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153495.png)

查看eureka-server管理页面：

![image-20210713223150650](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153496.png)





### 3.4.服务发现

下面，我们将order-service的逻辑修改：向eureka-server拉取user-service的信息，实现服务发现。

#### 1）引入依赖

之前说过，服务发现、服务注册统一都封装在eureka-client依赖，因此这一步与服务注册时一致。

在order-service的pom文件中，引入下面的eureka-client依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```



#### 2）配置文件

服务发现也需要知道eureka地址，因此第二步与服务注册一致，都是配置eureka信息：

在order-service中，修改application.yml文件，添加服务名称、eureka地址：

```yaml
spring:
  application:
    name: orderservice
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:10086/eureka
```



#### 3）服务拉取和负载均衡

最后，我们要去eureka-server中拉取user-service服务的实例列表，并且实现负载均衡。

不过这些动作不用我们去做，只需要添加一些注解即可。



在order-service的OrderApplication中，给RestTemplate这个Bean添加一个@LoadBalanced注解：

![image-20210713224049419](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153497.png)



修改order-service服务中的cn.itcast.order.service包下的OrderService类中的queryOrderById方法。修改访问的url路径，用服务名代替ip、端口：

![image-20210713224245731](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153498.png)



spring会自动帮助我们从eureka-server端，根据userservice这个服务名称，获取实例列表，而后完成负载均衡。



## 4.Ribbon负载均衡

上一节中，我们添加了@LoadBalanced注解，即可实现负载均衡功能，这是什么原理呢？



### 4.1.负载均衡原理

SpringCloud底层其实是利用了一个名为Ribbon的组件，来实现负载均衡功能的。

![image-20210713224517686](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153499.png)

那么我们发出的请求明明是http://userservice/user/1，怎么变成了http://localhost:8081的呢？



### 4.2.源码跟踪

为什么我们只输入了service名称就可以访问了呢？之前还要获取ip和端口。

显然有人帮我们根据service名称，获取到了服务实例的ip和端口。它就是`LoadBalancerInterceptor`，这个类会在对RestTemplate的请求进行拦截，然后从Eureka根据服务id获取服务列表，随后利用负载均衡算法得到真实的服务地址信息，替换服务id。

我们进行源码跟踪：

#### 1）LoadBalancerIntercepor

![1525620483637](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153500.png)

可以看到这里的intercept方法，拦截了用户的HttpRequest请求，然后做了几件事：

- `request.getURI()`：获取请求uri，本例中就是 http://user-service/user/8
- `originalUri.getHost()`：获取uri路径的主机名，其实就是服务id，`user-service`
- `this.loadBalancer.execute()`：处理服务id，和用户请求。

这里的`this.loadBalancer`是`LoadBalancerClient`类型，我们继续跟入。



#### 2）LoadBalancerClient

继续跟入execute方法：

![1525620787090](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153501.png)

代码是这样的：

- getLoadBalancer(serviceId)：根据服务id获取ILoadBalancer，而ILoadBalancer会拿着服务id去eureka中获取服务列表并保存起来。
- getServer(loadBalancer)：利用内置的负载均衡算法，从服务列表中选择一个。本例中，可以看到获取了8082端口的服务



放行后，再次访问并跟踪，发现获取的是8081：

 ![1525620835911](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153502.png)

果然实现了负载均衡。



#### 3）负载均衡策略IRule

在刚才的代码中，可以看到获取服务使通过一个`getServer`方法来做负载均衡:

 ![1525620835911](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153502.png)

我们继续跟入：

![1544361421671](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153503.png)

继续跟踪源码chooseServer方法，发现这么一段代码：

 ![1525622652849](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153504.png)

我们看看这个rule是谁：

 ![1525622699666](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153505.png)

这里的rule默认值是一个`RoundRobinRule`，看类的介绍：

 ![1525622754316](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153506.png)

这不就是轮询的意思嘛。

到这里，整个负载均衡的流程我们就清楚了。



#### 4）总结

SpringCloudRibbon的底层采用了一个拦截器，拦截了RestTemplate发出的请求，对地址做了修改。用一幅图来总结一下：

![image-20210713224724673](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153507.png)



基本流程如下：

- 拦截我们的RestTemplate请求http://userservice/user/1
- RibbonLoadBalancerClient会从请求url中获取服务名称，也就是user-service
- DynamicServerListLoadBalancer根据user-service到eureka拉取服务列表
- eureka返回列表，localhost:8081、localhost:8082
- IRule利用内置负载均衡规则，从列表中选择一个，例如localhost:8081
- RibbonLoadBalancerClient修改请求地址，用localhost:8081替代userservice，得到http://localhost:8081/user/1，发起真实请求



### 4.3.负载均衡策略



#### 4.3.1.负载均衡策略

负载均衡的规则都定义在IRule接口中，而IRule有很多不同的实现类：

![image-20210713225653000](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153508.png)

不同规则的含义如下：

| **内置负载均衡规则类**    | **规则描述**                                                 |
| ------------------------- | ------------------------------------------------------------ |
| RoundRobinRule            | 简单轮询服务列表来选择服务器。它是Ribbon默认的负载均衡规则。 |
| AvailabilityFilteringRule | 对以下两种服务器进行忽略：   （1）在默认情况下，这台服务器如果3次连接失败，这台服务器就会被设置为“短路”状态。短路状态将持续30秒，如果再次连接失败，短路的持续时间就会几何级地增加。  （2）并发数过高的服务器。如果一个服务器的并发连接数过高，配置了AvailabilityFilteringRule规则的客户端也会将其忽略。并发连接数的上限，可以由客户端的<clientName>.<clientConfigNameSpace>.ActiveConnectionsLimit属性进行配置。 |
| WeightedResponseTimeRule  | 为每一个服务器赋予一个权重值。服务器响应时间越长，这个服务器的权重就越小。这个规则会随机选择服务器，这个权重值会影响服务器的选择。 |
| **ZoneAvoidanceRule**     | 以区域可用的服务器为基础进行服务器的选择。使用Zone对服务器进行分类，这个Zone可以理解为一个机房、一个机架等。而后再对Zone内的多个服务做轮询。 |
| BestAvailableRule         | 忽略那些短路的服务器，并选择并发数较低的服务器。             |
| RandomRule                | 随机选择一个可用的服务器。                                   |
| RetryRule                 | 重试机制的选择逻辑                                           |



默认的实现就是ZoneAvoidanceRule，是一种轮询方案



#### 4.3.2.自定义负载均衡策略

通过定义IRule实现可以修改负载均衡规则，有两种方式：

1. 代码方式：在order-service中的OrderApplication类中，定义一个新的IRule：

```java
@Bean
public IRule randomRule(){
    return new RandomRule();
}
```



2. 配置文件方式：在order-service的application.yml文件中，添加新的配置也可以修改规则：

```yaml
userservice: ## 给某个微服务配置负载均衡规则，这里是userservice服务
  ribbon:
    NFLoadBalancerRuleClassName: com.netflix.loadbalancer.RandomRule ## 负载均衡规则 
```



> **注意**，一般用默认的负载均衡规则，不做修改。



### 4.4.饥饿加载

Ribbon默认是采用懒加载，即第一次访问时才会去创建LoadBalanceClient，请求时间会很长。

而饥饿加载则会在项目启动时创建，降低第一次访问的耗时，通过下面配置开启饥饿加载：

```yaml
ribbon:
  eager-load:
    enabled: true
    clients: userservice
```



## 5.Nacos注册中心

国内公司一般都推崇阿里巴巴的技术，比如注册中心，SpringCloudAlibaba也推出了一个名为Nacos的注册中心。

### 5.1.认识和安装Nacos

[Nacos](https://nacos.io/)是阿里巴巴的产品，现在是[SpringCloud](https://spring.io/projects/spring-cloud)中的一个组件。相比[Eureka](https://github.com/Netflix/eureka)功能更加丰富，在国内受欢迎程度较高。

![image-20210713230444308](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153509.png)



安装方式可以参考课前资料《Nacos安装指南.md》





### 5.2.服务注册到nacos

Nacos是SpringCloudAlibaba的组件，而SpringCloudAlibaba也遵循SpringCloud中定义的服务注册、服务发现规范。因此使用Nacos和使用Eureka对于微服务来说，并没有太大区别。

主要差异在于：

- 依赖不同
- 服务地址不同



#### 1）引入依赖

在cloud-demo父工程的pom文件中的`<dependencyManagement>`中引入SpringCloudAlibaba的依赖：

```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.2.6.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```

然后在user-service和order-service中的pom文件中引入nacos-discovery依赖：

```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```



> **注意**：不要忘了注释掉eureka的依赖。



#### 2）配置nacos地址

在user-service和order-service的application.yml中添加nacos地址：

```yaml
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
```



> **注意**：不要忘了注释掉eureka的地址



#### 3）重启

重启微服务后，登录nacos管理页面，可以看到微服务信息：

![image-20210713231439607](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153510.png)



### 5.3.服务分级存储模型

一个**服务**可以有多个**实例**，例如我们的user-service，可以有:

- 127.0.0.1:8081
- 127.0.0.1:8082
- 127.0.0.1:8083

假如这些实例分布于全国各地的不同机房，例如：

- 127.0.0.1:8081，在上海机房
- 127.0.0.1:8082，在上海机房
- 127.0.0.1:8083，在杭州机房

Nacos就将同一机房内的实例 划分为一个**集群**。

也就是说，user-service是服务，一个服务可以包含多个集群，如杭州、上海，每个集群下可以有多个实例，形成分级模型，如图：

![image-20210713232522531](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153512.png)



微服务互相访问时，应该尽可能访问同集群实例，因为本地访问速度更快。当本集群内不可用时，才访问其它集群。例如：

![image-20210713232658928](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153513.png)

杭州机房内的order-service应该优先访问同机房的user-service。





#### 5.3.1.给user-service配置集群



修改user-service的application.yml文件，添加集群配置：

```yaml
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ ## 集群名称
```

重启两个user-service实例后，我们可以在nacos控制台看到下面结果：

![image-20210713232916215](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153514.png)



我们再次复制一个user-service启动配置，添加属性：

```sh
-Dserver.port=8083 -Dspring.cloud.nacos.discovery.cluster-name=SH
```

配置如图所示：

![image-20210713233528982](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153515.png)



启动UserApplication3后再次查看nacos控制台：

![image-20210713233727923](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153516.png)



#### 5.3.2.同集群优先的负载均衡

默认的`ZoneAvoidanceRule`并不能实现根据同集群优先来实现负载均衡。

因此Nacos中提供了一个`NacosRule`的实现，可以优先从同集群中挑选实例。

1）给order-service配置集群信息

修改order-service的application.yml文件，添加集群配置：

```sh
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ ## 集群名称
```



2）修改负载均衡规则

修改order-service的application.yml文件，修改负载均衡规则：

```yaml
userservice:
  ribbon:
    NFLoadBalancerRuleClassName: com.alibaba.cloud.nacos.ribbon.NacosRule ## 负载均衡规则 
```



### 5.4.权重配置

实际部署中会出现这样的场景：

服务器设备性能有差异，部分实例所在机器性能较好，另一些较差，我们希望性能好的机器承担更多的用户请求。

但默认情况下NacosRule是同集群内随机挑选，不会考虑机器的性能问题。



因此，Nacos提供了权重配置来控制访问频率，权重越大则访问频率越高。



在nacos控制台，找到user-service的实例列表，点击编辑，即可修改权重：

![image-20210713235133225](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153517.png)

在弹出的编辑窗口，修改权重：

![image-20210713235235219](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153518.png)





> **注意**：如果权重修改为0，则该实例永远不会被访问



### 5.5.环境隔离

Nacos提供了namespace来实现环境隔离功能。

- nacos中可以有多个namespace
- namespace下可以有group、service等
- 不同namespace之间相互隔离，例如不同namespace的服务互相不可见



![image-20210714000101516](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153519.png)



#### 5.5.1.创建namespace

默认情况下，所有service、data、group都在同一个namespace，名为public：

![image-20210714000414781](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153520.png)



我们可以点击页面新增按钮，添加一个namespace：

![image-20210714000440143](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153521.png)



然后，填写表单：

![image-20210714000505928](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153522.png)

就能在页面看到一个新的namespace：

![image-20210714000522913](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153523.png)



#### 5.5.2.给微服务配置namespace

给微服务配置namespace只能通过修改配置来实现。

例如，修改order-service的application.yml文件：

```yaml
spring:
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        cluster-name: HZ
        namespace: 492a7d5d-237b-46a1-a99a-fa8e98e4b0f9 ## 命名空间，填ID
```



重启order-service后，访问控制台，可以看到下面的结果：

![image-20210714000830703](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153524.png)



![image-20210714000837140](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153525.png)

此时访问order-service，因为namespace不同，会导致找不到userservice，控制台会报错：

![image-20210714000941256](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153526.png)



### 5.6.Nacos与Eureka的区别

Nacos的服务实例分为两种l类型：

- 临时实例：如果实例宕机超过一定时间，会从服务列表剔除，默认的类型。

- 非临时实例：如果实例宕机，不会从服务列表剔除，也可以叫永久实例。



配置一个服务实例为永久实例：

```yaml
spring:
  cloud:
    nacos:
      discovery:
        ephemeral: false ## 设置为非临时实例
```





Nacos和Eureka整体结构类似，服务注册、服务拉取、心跳等待，但是也存在一些差异：

![image-20210714001728017](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153527.png)



- Nacos与eureka的共同点
  - 都支持服务注册和服务拉取
  - 都支持服务提供者心跳方式做健康检测

- Nacos与Eureka的区别
  - Nacos支持服务端主动检测提供者状态：临时实例采用心跳模式，非临时实例采用主动检测模式
  - 临时实例心跳不正常会被剔除，非临时实例则不会被剔除
  - Nacos支持服务列表变更的消息推送模式，服务列表更新更及时
  - Nacos集群默认采用AP方式，当集群中存在非临时实例时，采用CP模式；Eureka采用AP方式

# Nacos安装指南



## 1.Windows安装

开发阶段采用单机安装即可。

### 1.1.下载安装包

在Nacos的GitHub页面，提供有下载链接，可以下载编译好的Nacos服务端或者源代码：

GitHub主页：https://github.com/alibaba/nacos

GitHub的Release下载页：https://github.com/alibaba/nacos/releases

如图：

![image-20210402161102887](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153528.png)



本课程采用1.4.1.版本的Nacos，课前资料已经准备了安装包：

![image-20210402161130261](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153529.png)

windows版本使用`nacos-server-1.4.1.zip`包即可。



### 1.2.解压

将这个包解压到任意非中文目录下，如图：

![image-20210402161843337](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153530.png)

目录说明：

- bin：启动脚本
- conf：配置文件



### 1.3.端口配置

Nacos的默认端口是8848，如果你电脑上的其它进程占用了8848端口，请先尝试关闭该进程。

**如果无法关闭占用8848端口的进程**，也可以进入nacos的conf目录，修改配置文件中的端口：

![image-20210402162008280](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153531.png)

修改其中的内容：

![image-20210402162251093](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153532.png)



### 1.4.启动

启动非常简单，进入bin目录，结构如下：

![image-20210402162350977](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153533.png)

然后执行命令即可：

- windows命令：

  ```
  startup.cmd -m standalone
  ```


执行后的效果如图：

![image-20210402162526774](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153534.png)



### 1.5.访问

在浏览器输入地址：http://127.0.0.1:8848/nacos即可：

![image-20210402162630427](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153535.png)

默认的账号和密码都是nacos，进入后：

![image-20210402162709515](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153536.png)





## 2.Linux安装

Linux或者Mac安装方式与Windows类似。

### 2.1.安装JDK

Nacos依赖于JDK运行，索引Linux上也需要安装JDK才行。

上传jdk安装包：

![image-20210402172334810](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153537.png)

上传到某个目录，例如：`/usr/local/`



然后解压缩：                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     

```sh
tar -xvf jdk-8u144-linux-x64.tar.gz
```

然后重命名为java



配置环境变量：

```sh
export JAVA_HOME=/usr/local/java
export PATH=$PATH:$JAVA_HOME/bin
```

设置环境变量：

```sh
source /etc/profile
```





### 2.2.上传安装包

如图：

![image-20210402161102887](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153528.png)

也可以直接使用课前资料中的tar.gz：

![image-20210402161130261](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153529.png)

上传到Linux服务器的某个目录，例如`/usr/local/src`目录下：

![image-20210402163715580](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153538.png)



### 2.3.解压

命令解压缩安装包：

```sh
tar -xvf nacos-server-1.4.1.tar.gz
```

然后删除安装包：

```sh
rm -rf nacos-server-1.4.1.tar.gz
```

目录中最终样式：

![image-20210402163858429](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153539.png)

目录内部：

![image-20210402164414827](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153540.png)



### 2.4.端口配置

与windows中类似



### 2.5.启动

在nacos/bin目录中，输入命令启动Nacos：

```sh
sh startup.sh -m standalone
```







## 3.Nacos的依赖

父工程：

```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.2.5.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```



客户端：

```xml
<!-- nacos客户端依赖包 -->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>

```



# Nacos集群搭建



## 1.集群结构图

官方给出的Nacos集群图：



![image-20210409210621117](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153541.png)

其中包含3个nacos节点，然后一个负载均衡器代理3个Nacos。这里负载均衡器可以使用nginx。

我们计划的集群结构：

![image-20210409211355037](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153542.png)



三个nacos节点的地址：

| 节点   | ip            | port |
| ------ | ------------- | ---- |
| nacos1 | 192.168.150.1 | 8845 |
| nacos2 | 192.168.150.1 | 8846 |
| nacos3 | 192.168.150.1 | 8847 |



## 2.搭建集群

搭建集群的基本步骤：

- 搭建数据库，初始化数据库表结构
- 下载nacos安装包
- 配置nacos
- 启动nacos集群
- nginx反向代理



### 2.1.初始化数据库

Nacos默认数据存储在内嵌数据库Derby中，不属于生产可用的数据库。

官方推荐的最佳实践是使用带有主从的高可用数据库集群，主从模式的高可用数据库可以参考**传智教育**的后续高手课程。

这里我们以单点的数据库为例来讲解。

首先新建一个数据库，命名为nacos，而后导入下面的SQL：

```sql
CREATE TABLE `config_info` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(255) DEFAULT NULL,
  `content` longtext NOT NULL COMMENT 'content',
  `md5` varchar(32) DEFAULT NULL COMMENT 'md5',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `src_user` text COMMENT 'source user',
  `src_ip` varchar(50) DEFAULT NULL COMMENT 'source ip',
  `app_name` varchar(128) DEFAULT NULL,
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  `c_desc` varchar(256) DEFAULT NULL,
  `c_use` varchar(64) DEFAULT NULL,
  `effect` varchar(64) DEFAULT NULL,
  `type` varchar(64) DEFAULT NULL,
  `c_schema` text,
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfo_datagrouptenant` (`data_id`,`group_id`,`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_info';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info_aggr   */
/******************************************/
CREATE TABLE `config_info_aggr` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(255) NOT NULL COMMENT 'group_id',
  `datum_id` varchar(255) NOT NULL COMMENT 'datum_id',
  `content` longtext NOT NULL COMMENT '内容',
  `gmt_modified` datetime NOT NULL COMMENT '修改时间',
  `app_name` varchar(128) DEFAULT NULL,
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfoaggr_datagrouptenantdatum` (`data_id`,`group_id`,`tenant_id`,`datum_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='增加租户字段';


/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info_beta   */
/******************************************/
CREATE TABLE `config_info_beta` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(128) NOT NULL COMMENT 'group_id',
  `app_name` varchar(128) DEFAULT NULL COMMENT 'app_name',
  `content` longtext NOT NULL COMMENT 'content',
  `beta_ips` varchar(1024) DEFAULT NULL COMMENT 'betaIps',
  `md5` varchar(32) DEFAULT NULL COMMENT 'md5',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `src_user` text COMMENT 'source user',
  `src_ip` varchar(50) DEFAULT NULL COMMENT 'source ip',
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfobeta_datagrouptenant` (`data_id`,`group_id`,`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_info_beta';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_info_tag   */
/******************************************/
CREATE TABLE `config_info_tag` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(128) NOT NULL COMMENT 'group_id',
  `tenant_id` varchar(128) DEFAULT '' COMMENT 'tenant_id',
  `tag_id` varchar(128) NOT NULL COMMENT 'tag_id',
  `app_name` varchar(128) DEFAULT NULL COMMENT 'app_name',
  `content` longtext NOT NULL COMMENT 'content',
  `md5` varchar(32) DEFAULT NULL COMMENT 'md5',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  `src_user` text COMMENT 'source user',
  `src_ip` varchar(50) DEFAULT NULL COMMENT 'source ip',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_configinfotag_datagrouptenanttag` (`data_id`,`group_id`,`tenant_id`,`tag_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_info_tag';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = config_tags_relation   */
/******************************************/
CREATE TABLE `config_tags_relation` (
  `id` bigint(20) NOT NULL COMMENT 'id',
  `tag_name` varchar(128) NOT NULL COMMENT 'tag_name',
  `tag_type` varchar(64) DEFAULT NULL COMMENT 'tag_type',
  `data_id` varchar(255) NOT NULL COMMENT 'data_id',
  `group_id` varchar(128) NOT NULL COMMENT 'group_id',
  `tenant_id` varchar(128) DEFAULT '' COMMENT 'tenant_id',
  `nid` bigint(20) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`nid`),
  UNIQUE KEY `uk_configtagrelation_configidtag` (`id`,`tag_name`,`tag_type`),
  KEY `idx_tenant_id` (`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='config_tag_relation';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = group_capacity   */
/******************************************/
CREATE TABLE `group_capacity` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键ID',
  `group_id` varchar(128) NOT NULL DEFAULT '' COMMENT 'Group ID，空字符表示整个集群',
  `quota` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '配额，0表示使用默认值',
  `usage` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '使用量',
  `max_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个配置大小上限，单位为字节，0表示使用默认值',
  `max_aggr_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '聚合子配置最大个数，，0表示使用默认值',
  `max_aggr_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个聚合数据的子配置大小上限，单位为字节，0表示使用默认值',
  `max_history_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '最大变更历史数量',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_group_id` (`group_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='集群、各Group容量信息表';

/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = his_config_info   */
/******************************************/
CREATE TABLE `his_config_info` (
  `id` bigint(64) unsigned NOT NULL,
  `nid` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
  `data_id` varchar(255) NOT NULL,
  `group_id` varchar(128) NOT NULL,
  `app_name` varchar(128) DEFAULT NULL COMMENT 'app_name',
  `content` longtext NOT NULL,
  `md5` varchar(32) DEFAULT NULL,
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `src_user` text,
  `src_ip` varchar(50) DEFAULT NULL,
  `op_type` char(10) DEFAULT NULL,
  `tenant_id` varchar(128) DEFAULT '' COMMENT '租户字段',
  PRIMARY KEY (`nid`),
  KEY `idx_gmt_create` (`gmt_create`),
  KEY `idx_gmt_modified` (`gmt_modified`),
  KEY `idx_did` (`data_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='多租户改造';


/******************************************/
/*   数据库全名 = nacos_config   */
/*   表名称 = tenant_capacity   */
/******************************************/
CREATE TABLE `tenant_capacity` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键ID',
  `tenant_id` varchar(128) NOT NULL DEFAULT '' COMMENT 'Tenant ID',
  `quota` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '配额，0表示使用默认值',
  `usage` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '使用量',
  `max_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个配置大小上限，单位为字节，0表示使用默认值',
  `max_aggr_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '聚合子配置最大个数',
  `max_aggr_size` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '单个聚合数据的子配置大小上限，单位为字节，0表示使用默认值',
  `max_history_count` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '最大变更历史数量',
  `gmt_create` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `gmt_modified` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_tenant_id` (`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='租户容量信息表';


CREATE TABLE `tenant_info` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'id',
  `kp` varchar(128) NOT NULL COMMENT 'kp',
  `tenant_id` varchar(128) default '' COMMENT 'tenant_id',
  `tenant_name` varchar(128) default '' COMMENT 'tenant_name',
  `tenant_desc` varchar(256) DEFAULT NULL COMMENT 'tenant_desc',
  `create_source` varchar(32) DEFAULT NULL COMMENT 'create_source',
  `gmt_create` bigint(20) NOT NULL COMMENT '创建时间',
  `gmt_modified` bigint(20) NOT NULL COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `uk_tenant_info_kptenantid` (`kp`,`tenant_id`),
  KEY `idx_tenant_id` (`tenant_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='tenant_info';

CREATE TABLE `users` (
	`username` varchar(50) NOT NULL PRIMARY KEY,
	`password` varchar(500) NOT NULL,
	`enabled` boolean NOT NULL
);

CREATE TABLE `roles` (
	`username` varchar(50) NOT NULL,
	`role` varchar(50) NOT NULL,
	UNIQUE INDEX `idx_user_role` (`username` ASC, `role` ASC) USING BTREE
);

CREATE TABLE `permissions` (
    `role` varchar(50) NOT NULL,
    `resource` varchar(255) NOT NULL,
    `action` varchar(8) NOT NULL,
    UNIQUE INDEX `uk_role_permission` (`role`,`resource`,`action`) USING BTREE
);

INSERT INTO users (username, password, enabled) VALUES ('nacos', '$2a$10$EuWPZHzz32dJN7jexM34MOeYirDdFAZm2kuWj7VEOJhhZkDrxfvUu', TRUE);

INSERT INTO roles (username, role) VALUES ('nacos', 'ROLE_ADMIN');
```



### 2.2.下载nacos

nacos在GitHub上有下载地址：https://github.com/alibaba/nacos/tags，可以选择任意版本下载。

本例中才用1.4.1版本：

![image-20210409212119411](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153543.png)









### 2.3.配置Nacos

将这个包解压到任意非中文目录下，如图：

![image-20210402161843337](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153544.png)

目录说明：

- bin：启动脚本
- conf：配置文件



进入nacos的conf目录，修改配置文件cluster.conf.example，重命名为cluster.conf：

![image-20210409212459292](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153545.png)

然后添加内容：

```
127.0.0.1:8845
127.0.0.1.8846
127.0.0.1.8847
```



然后修改application.properties文件，添加数据库配置

```properties
spring.datasource.platform=mysql

db.num=1

db.url.0=jdbc:mysql://127.0.0.1:3306/nacos?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useUnicode=true&useSSL=false&serverTimezone=UTC
db.user.0=root
db.password.0=123
```



### 2.4.启动

将nacos文件夹复制三份，分别命名为：nacos1、nacos2、nacos3

![image-20210409213335538](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153546.png) 

然后分别修改三个文件夹中的application.properties，

nacos1:

```properties
server.port=8845
```

nacos2:

```properties
server.port=8846
```

nacos3:

```properties
server.port=8847
```



然后分别启动三个nacos节点：

```
startup.cmd
```



### 2.5.nginx反向代理

找到课前资料提供的nginx安装包： 

![image-20210410103253355](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153547.png) 

解压到任意非中文目录下：

![image-20210410103322874](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153548.png) 

修改conf/nginx.conf文件，配置如下：

```nginx
upstream nacos-cluster {
    server 127.0.0.1:8845;
	server 127.0.0.1:8846;
	server 127.0.0.1:8847;
}

server {
    listen       80;
    server_name  localhost;

    location /nacos {
        proxy_pass http://nacos-cluster;
    }
}
```

./nginx.e

而后在浏览器访问：http://localhost/nacos即可。



代码中application.yml文件配置如下：

```yaml
spring:
  cloud:
    nacos:
      server-addr: localhost:80 ## Nacos地址
```

![image-20220717235606250](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153549.png)

### 2.6.优化



- 实际部署时，需要给做反向代理的nginx服务器设置一个域名，这样后续如果有服务器迁移nacos的客户端也无需更改配置.

- Nacos的各个节点应该部署到多个不同服务器，做好容灾和隔离





# SpringCloud02



## 0.学习目标







## 1.Nacos配置管理

Nacos除了可以做注册中心，同样可以做配置管理来使用。



### 1.1.统一配置管理

当微服务部署的实例越来越多，达到数十、数百时，逐个修改微服务配置就会让人抓狂，而且很容易出错。我们需要一种统一配置管理方案，可以集中管理所有实例的配置。

![image-20210714164426792](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153550.png)



Nacos一方面可以将配置集中管理，另一方可以在配置变更时，及时通知微服务，实现配置的热更新。



#### 1.1.1.在nacos中添加配置文件

如何在nacos中管理配置呢？

![image-20210714164742924](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153551.png)

然后在弹出的表单中，填写配置信息：

![image-20210714164856664](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153552.png)



> 注意：项目的核心配置，需要热更新的配置才有放到nacos管理的必要。基本不会变更的一些配置还是保存在微服务本地比较好。



#### 1.1.2.从微服务拉取配置

微服务要拉取nacos中管理的配置，并且与本地的application.yml配置合并，才能完成项目启动。

但如果尚未读取application.yml，又如何得知nacos地址呢？

因此spring引入了一种新的配置文件：bootstrap.yaml文件，会在application.yml之前被读取，流程如下：

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153553.png)



1）引入nacos-config依赖

首先，在user-service服务中，引入nacos-config的客户端依赖：

```xml
<!--nacos配置管理依赖-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
</dependency>
```

2）添加bootstrap.yaml

然后，在user-service中添加一个bootstrap.yaml文件，内容如下：

```yaml
spring:
  application:
    name: userservice ## 服务名称
  profiles:
    active: dev #开发环境，这里是dev 
  cloud:
    nacos:
      server-addr: localhost:8848 ## Nacos地址
      config:
        file-extension: yaml ## 文件后缀名
```

这里会根据spring.cloud.nacos.server-addr获取nacos地址，再根据

`${spring.application.name}-${spring.profiles.active}.${spring.cloud.nacos.config.file-extension}`作为文件id，来读取配置。

本例中，就是去读取`userservice-dev.yaml`：

![image-20210714170845901](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153554.png)

![image-20220717235731516](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153555.png)

3）读取nacos配置

在user-service中的UserController中添加业务逻辑，读取pattern.dateformat配置：

![image-20210714170337448](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153556.png)



完整代码：

```java
package cn.itcast.user.web;

import cn.itcast.user.pojo.User;
import cn.itcast.user.service.UserService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

@Slf4j
@RestController
@RequestMapping("/user")
public class UserController {

    @Autowired
    private UserService userService;

    @Value("${pattern.dateformat}")
    private String dateformat;
    
    @GetMapping("now")
    public String now(){
        return LocalDateTime.now().format(DateTimeFormatter.ofPattern(dateformat));
    }
    // ...略
}
```



在页面访问，可以看到效果：

![image-20210714170449612](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153557.png)





### 1.2.配置热更新

我们最终的目的，是修改nacos中的配置后，微服务中无需重启即可让配置生效，也就是**配置热更新**。



要实现配置热更新，可以使用两种方式：

#### 1.2.1.方式一

在@Value注入的变量所在类上添加注解@RefreshScope：

![image-20210714171036335](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153558.png)



#### 1.2.2.方式二

使用@ConfigurationProperties注解代替@Value注解。

在user-service服务中，添加一个类，读取patterrn.dateformat属性：

```java
package cn.itcast.user.config;

import lombok.Data;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@Data
@ConfigurationProperties(prefix = "pattern")
public class PatternProperties {
    private String dateformat;
}
```



在UserController中使用这个类代替@Value：

![image-20210714171316124](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153559.png)



完整代码：

```java
package cn.itcast.user.web;

import cn.itcast.user.config.PatternProperties;
import cn.itcast.user.pojo.User;
import cn.itcast.user.service.UserService;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

@Slf4j
@RestController
@RequestMapping("/user")
public class UserController {

    @Autowired
    private UserService userService;

    @Autowired
    private PatternProperties patternProperties;

    @GetMapping("now")
    public String now(){
        return LocalDateTime.now().format(DateTimeFormatter.ofPattern(patternProperties.getDateformat()));
    }

    // 略
}
```





### 1.3.配置共享

其实微服务启动时，会去nacos读取多个配置文件，例如：

- `[spring.application.name]-[spring.profiles.active].yaml`，例如：userservice-dev.yaml

- `[spring.application.name].yaml`，例如：userservice.yaml

而`[spring.application.name].yaml`不包含环境，因此可以被多个环境共享。



下面我们通过案例来测试配置共享



#### 1）添加一个环境共享配置

我们在nacos中添加一个userservice.yaml文件：

![image-20210714173233650](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153560.png)



#### 2）在user-service中读取共享配置

在user-service服务中，修改PatternProperties类，读取新添加的属性：

![image-20210714173324231](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153561.png)

在user-service服务中，修改UserController，添加一个方法：

![image-20210714173721309](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153562.png)



#### 3）运行两个UserApplication，使用不同的profile

修改UserApplication2这个启动项，改变其profile值：

![image-20210714173538538](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153563.png)



![image-20210714173519963](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153564.png)



这样，UserApplication(8081)使用的profile是dev，UserApplication2(8082)使用的profile是test。

启动UserApplication和UserApplication2

访问http://localhost:8081/user/prop，结果：

![image-20210714174313344](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153565.png)

访问http://localhost:8082/user/prop，结果：

![image-20210714174424818](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153566.png)

可以看出来，不管是dev，还是test环境，都读取到了envSharedValue这个属性的值。





#### 4）配置共享的优先级

当nacos、服务本地同时出现相同属性时，优先级有高低之分：

![image-20210714174623557](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153567.png)





### 1.4.搭建Nacos集群

Nacos生产环境下一定要部署为集群状态，部署方式参考课前资料中的文档：

![image-20210714174728042](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153568.png)



## 2.Feign远程调用



先来看我们以前利用RestTemplate发起远程调用的代码：

![image-20210714174814204](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153570.png)

存在下面的问题：

•代码可读性差，编程体验不统一

•参数复杂URL难以维护



Feign是一个声明式的http客户端，官方地址：https://github.com/OpenFeign/feign

其作用就是帮助我们优雅的实现http请求的发送，解决上面提到的问题。

![image-20210714174918088](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153571.png)





### 2.1.Feign替代RestTemplate

Fegin的使用步骤如下：

#### 1）引入依赖

我们在order-service服务的pom文件中引入feign的依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```



#### 2）添加注解

在order-service的启动类添加注解开启Feign的功能：

![image-20210714175102524](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153572.png)



#### 3）编写Feign的客户端

在order-service中新建一个接口，内容如下：

```java
package cn.itcast.order.client;

import cn.itcast.order.pojo.User;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

@FeignClient("userservice")
public interface UserClient {
    @GetMapping("/user/{id}")
    User findById(@PathVariable("id") Long id);
}
```



这个客户端主要是基于SpringMVC的注解来声明远程调用的信息，比如：

- 服务名称：userservice
- 请求方式：GET
- 请求路径：/user/{id}
- 请求参数：Long id
- 返回值类型：User

这样，Feign就可以帮助我们发送http请求，无需自己使用RestTemplate来发送了。





#### 4）测试

修改order-service中的OrderService类中的queryOrderById方法，使用Feign客户端代替RestTemplate：

![image-20210714175415087](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153573.png)

是不是看起来优雅多了。





#### 5）总结

使用Feign的步骤：

① 引入依赖

② 添加@EnableFeignClients注解

③ 编写FeignClient接口

④ 使用FeignClient中定义的方法代替RestTemplate



### 2.2.自定义配置

Feign可以支持很多的自定义配置，如下表所示：

| 类型                   | 作用             | 说明                                                   |
| ---------------------- | ---------------- | ------------------------------------------------------ |
| **feign.Logger.Level** | 修改日志级别     | 包含四种不同的级别：NONE、BASIC、HEADERS、FULL         |
| feign.codec.Decoder    | 响应结果的解析器 | http远程调用的结果做解析，例如解析json字符串为java对象 |
| feign.codec.Encoder    | 请求参数编码     | 将请求参数编码，便于通过http请求发送                   |
| feign. Contract        | 支持的注解格式   | 默认是SpringMVC的注解                                  |
| feign. Retryer         | 失败重试机制     | 请求失败的重试机制，默认是没有，不过会使用Ribbon的重试 |

一般情况下，默认值就能满足我们使用，如果要自定义时，只需要创建自定义的@Bean覆盖默认Bean即可。



下面以日志为例来演示如何自定义配置。

#### 2.2.1.配置文件方式

基于配置文件修改feign的日志级别可以针对单个服务：

```yaml
feign:  
  client:
    config: 
      userservice: ## 针对某个微服务的配置
        loggerLevel: FULL ##  日志级别 
```

也可以针对所有服务：

```yaml
feign:  
  client:
    config: 
      default: ## 这里用default就是全局配置，如果是写服务名称，则是针对某个微服务的配置
        loggerLevel: FULL ##  日志级别 
```



而日志的级别分为四种：

- NONE：不记录任何日志信息，这是默认值。
- BASIC：仅记录请求的方法，URL以及响应状态码和执行时间
- HEADERS：在BASIC的基础上，额外记录了请求和响应的头信息
- FULL：记录所有请求和响应的明细，包括头信息、请求体、元数据。



#### 2.2.2.Java代码方式

也可以基于Java代码来修改日志级别，先声明一个类，然后声明一个Logger.Level的对象：

```java
public class DefaultFeignConfiguration  {
    @Bean
    public Logger.Level feignLogLevel(){
        return Logger.Level.BASIC; // 日志级别为BASIC
    }
}
```



如果要**全局生效**，将其放到启动类的@EnableFeignClients这个注解中：

```java
@EnableFeignClients(defaultConfiguration = DefaultFeignConfiguration .class) 
```



如果是**局部生效**，则把它放到对应的@FeignClient这个注解中：

```java
@FeignClient(value = "userservice", configuration = DefaultFeignConfiguration .class) 
```







### 2.3.Feign使用优化

Feign底层发起http请求，依赖于其它的框架。其底层客户端实现包括：

•URLConnection：默认实现，不支持连接池

•Apache HttpClient ：支持连接池

•OKHttp：支持连接池



因此提高Feign的性能主要手段就是使用**连接池**代替默认的URLConnection。



这里我们用Apache的HttpClient来演示。

1）引入依赖

在order-service的pom文件中引入Apache的HttpClient依赖：

```xml
<!--httpClient的依赖 -->
<dependency>
    <groupId>io.github.openfeign</groupId>
    <artifactId>feign-httpclient</artifactId>
</dependency>
```



2）配置连接池

在order-service的application.yml中添加配置：

```yaml
feign:
  client:
    config:
      default: ## default全局的配置
        loggerLevel: BASIC ## 日志级别，BASIC就是基本的请求和响应信息
  httpclient:
    enabled: true ## 开启feign对HttpClient的支持
    max-connections: 200 ## 最大的连接数
    max-connections-per-route: 50 ## 每个路径的最大连接数
```



接下来，在FeignClientFactoryBean中的loadBalance方法中打断点：

![image-20210714185925910](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153574.png)

Debug方式启动order-service服务，可以看到这里的client，底层就是Apache HttpClient：

![image-20210714190041542](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153575.png)







总结，Feign的优化：

1.日志级别 尽量用basic

2.使用HttpClient或OKHttp代替URLConnection

①  引入feign-httpClient依赖

②  配置文件开启httpClient功能，设置连接池参数



### 2.4.最佳实践

所谓最近实践，就是使用过程中总结的经验，最好的一种使用方式。

自习观察可以发现，Feign的客户端与服务提供者的controller代码非常相似：

feign客户端：

![image-20210714190542730](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153576.png)

UserController：

![image-20210714190528450](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153577.png)



有没有一种办法简化这种重复的代码编写呢？





#### 2.4.1.继承方式

一样的代码可以通过继承来共享：

1）定义一个API接口，利用定义方法，并基于SpringMVC注解做声明。

2）Feign客户端和Controller都集成改接口



![image-20210714190640857](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153578.png)



优点：

- 简单
- 实现了代码共享

缺点：

- 服务提供方、服务消费方紧耦合

- 参数列表中的注解映射并不会继承，因此Controller中必须再次声明方法、参数列表、注解





#### 2.4.2.抽取方式

将Feign的Client抽取为独立模块，并且把接口有关的POJO、默认的Feign配置都放到这个模块中，提供给所有消费者使用。

例如，将UserClient、User、Feign的默认配置都抽取到一个feign-api包中，所有微服务引用该依赖包，即可直接使用。

![image-20210714214041796](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153579.png)





#### 2.4.3.实现基于抽取的最佳实践

##### 1）抽取

首先创建一个module，命名为feign-api：

![image-20210714204557771](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153580.png)

项目结构：

![image-20210714204656214](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153581.png)

在feign-api中然后引入feign的starter依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```



然后，order-service中编写的UserClient、User、DefaultFeignConfiguration都复制到feign-api项目中

![image-20210714205221970](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153582.png)



##### 2）在order-service中使用feign-api

首先，删除order-service中的UserClient、User、DefaultFeignConfiguration等类或接口。



在order-service的pom文件中中引入feign-api的依赖：

```xml
<dependency>
    <groupId>cn.itcast.demo</groupId>
    <artifactId>feign-api</artifactId>
    <version>1.0</version>
</dependency>
```



修改order-service中的所有与上述三个组件有关的导包部分，改成导入feign-api中的包



##### 3）重启测试

重启后，发现服务报错了：

![image-20210714205623048](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153583.png)



这是因为UserClient现在在cn.itcast.feign.clients包下，

而order-service的@EnableFeignClients注解是在cn.itcast.order包下，不在同一个包，无法扫描到UserClient。



##### 4）解决扫描包问题

方式一：

指定Feign应该扫描的包：

```java
@EnableFeignClients(basePackages = "cn.itcast.feign.clients")
```



方式二：

指定需要加载的Client接口：

```java
@EnableFeignClients(clients = {UserClient.class})
```









## 3.Gateway服务网关

Spring Cloud Gateway 是 Spring Cloud 的一个全新项目，该项目是基于 Spring 5.0，Spring Boot 2.0 和 Project Reactor 等响应式编程和事件流技术开发的网关，它旨在为微服务架构提供一种简单有效的统一的 API 路由管理方式。



### 3.1.为什么需要网关

Gateway网关是我们服务的守门神，所有微服务的统一入口。

网关的**核心功能特性**：

- 请求路由
- 权限控制
- 限流

架构图：

![image-20210714210131152](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153584.png)



**权限控制**：网关作为微服务入口，需要校验用户是是否有请求资格，如果没有则进行拦截。

**路由和负载均衡**：一切请求都必须先经过gateway，但网关不处理业务，而是根据某种规则，把请求转发到某个微服务，这个过程叫做路由。当然路由的目标服务有多个时，还需要做负载均衡。

**限流**：当请求流量过高时，在网关中按照下流的微服务能够接受的速度来放行请求，避免服务压力过大。



在SpringCloud中网关的实现包括两种：

- gateway
- zuul

Zuul是基于Servlet的实现，属于阻塞式编程。而SpringCloudGateway则是基于Spring5中提供的WebFlux，属于响应式编程的实现，具备更好的性能。





### 3.2.gateway快速入门

下面，我们就演示下网关的基本路由功能。基本步骤如下：

1. 创建SpringBoot工程gateway，引入网关依赖
2. 编写启动类
3. 编写基础配置和路由规则
4. 启动网关服务进行测试



#### 1）创建gateway服务，引入依赖

创建服务：

![image-20210714210919458](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153585.png)

引入依赖：

```xml
<!--网关-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
<!--nacos服务发现依赖-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```



#### 2）编写启动类

```java
package cn.itcast.gateway;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class GatewayApplication {

	public static void main(String[] args) {
		SpringApplication.run(GatewayApplication.class, args);
	}
}
```



#### 3）编写基础配置和路由规则

创建application.yml文件，内容如下：

```yaml
server:
  port: 10010 ## 网关端口
spring:
  application:
    name: gateway ## 服务名称
  cloud:
    nacos:
      server-addr: localhost:8848 ## nacos地址
    gateway:
      routes: ## 网关路由配置
        - id: user-service ## 路由id，自定义，只要唯一即可
          ## uri: http://127.0.0.1:8081 ## 路由的目标地址 http就是固定地址
          uri: lb://userservice ## 路由的目标地址 lb就是负载均衡，后面跟服务名称
          predicates: ## 路由断言，也就是判断请求是否符合路由规则的条件
            - Path=/user/** ## 这个是按照路径匹配，只要以/user/开头就符合要求
```



我们将符合`Path` 规则的一切请求，都代理到 `uri`参数指定的地址。

本例中，我们将 `/user/**`开头的请求，代理到`lb://userservice`，lb是负载均衡，根据服务名拉取服务列表，实现负载均衡。



#### 4）重启测试

重启网关，访问http://localhost:10010/user/1时，符合`/user/**`规则，请求转发到uri：http://userservice/user/1，得到了结果：

![image-20210714211908341](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153586.png)





#### 5）网关路由的流程图

整个访问的流程如下：

![image-20210714211742956](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153587.png)







总结：

网关搭建步骤：

1. 创建项目，引入nacos服务发现和gateway依赖

2. 配置application.yml，包括服务基本信息、nacos地址、路由

路由配置包括：

1. 路由id：路由的唯一标示

2. 路由目标（uri）：路由的目标地址，http代表固定地址，lb代表根据服务名负载均衡

3. 路由断言（predicates）：判断路由的规则，

4. 路由过滤器（filters）：对请求或响应做处理



接下来，就重点来学习路由断言和路由过滤器的详细知识





### 3.3.断言工厂

我们在配置文件中写的断言规则只是字符串，这些字符串会被Predicate Factory读取并处理，转变为路由判断的条件

例如Path=/user/**是按照路径匹配，这个规则是由

`org.springframework.cloud.gateway.handler.predicate.PathRoutePredicateFactory`类来

处理的，像这样的断言工厂在SpringCloudGateway还有十几个:

| **名称**   | **说明**                       | **示例**                                                     |
| ---------- | ------------------------------ | ------------------------------------------------------------ |
| After      | 是某个时间点后的请求           | -  After=2037-01-20T17:42:47.789-07:00[America/Denver]       |
| Before     | 是某个时间点之前的请求         | -  Before=2031-04-13T15:14:47.433+08:00[Asia/Shanghai]       |
| Between    | 是某两个时间点之前的请求       | -  Between=2037-01-20T17:42:47.789-07:00[America/Denver],  2037-01-21T17:42:47.789-07:00[America/Denver] |
| Cookie     | 请求必须包含某些cookie         | - Cookie=chocolate, ch.p                                     |
| Header     | 请求必须包含某些header         | - Header=X-Request-Id, \d+                                   |
| Host       | 请求必须是访问某个host（域名） | -  Host=**.somehost.org,**.anotherhost.org                   |
| Method     | 请求方式必须是指定方式         | - Method=GET,POST                                            |
| Path       | 请求路径必须符合指定规则       | - Path=/red/{segment},/blue/**                               |
| Query      | 请求参数必须包含指定参数       | - Query=name, Jack或者-  Query=name                          |
| RemoteAddr | 请求者的ip必须是指定范围       | - RemoteAddr=192.168.1.1/24                                  |
| Weight     | 权重处理                       |                                                              |



我们只需要掌握Path这种路由工程就可以了。



### 3.4.过滤器工厂

GatewayFilter是网关中提供的一种过滤器，可以对进入网关的请求和微服务返回的响应做处理：

![image-20210714212312871](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153588.png)



#### 3.4.1.路由过滤器的种类

Spring提供了31种不同的路由过滤器工厂。例如：

| **名称**             | **说明**                     |
| -------------------- | ---------------------------- |
| AddRequestHeader     | 给当前请求添加一个请求头     |
| RemoveRequestHeader  | 移除请求中的一个请求头       |
| AddResponseHeader    | 给响应结果中添加一个响应头   |
| RemoveResponseHeader | 从响应结果中移除有一个响应头 |
| RequestRateLimiter   | 限制请求的流量               |



#### 3.4.2.请求头过滤器

下面我们以AddRequestHeader 为例来讲解。

> **需求**：给所有进入userservice的请求添加一个请求头：Truth=itcast is freaking awesome!



只需要修改gateway服务的application.yml文件，添加路由过滤即可：

```yaml
spring:
  cloud:
    gateway:
      routes:
      - id: user-service 
        uri: lb://userservice 
        predicates: 
        - Path=/user/** 
        filters: ## 过滤器
        - AddRequestHeader=Truth, Itcast is freaking awesome! ## 添加请求头
```

当前过滤器写在userservice路由下，因此仅仅对访问userservice的请求有效。





#### 3.4.3.默认过滤器

如果要对所有的路由都生效，则可以将过滤器工厂写到default下。格式如下：

```yaml
spring:
  cloud:
    gateway:
      routes:
      - id: user-service 
        uri: lb://userservice 
        predicates: 
        - Path=/user/**
      default-filters: ## 默认过滤项
      - AddRequestHeader=Truth, Itcast is freaking awesome! 
```



#### 3.4.4.总结

过滤器的作用是什么？

① 对路由的请求或响应做加工处理，比如添加请求头

② 配置在路由下的过滤器只对当前路由的请求生效

defaultFilters的作用是什么？

① 对所有路由都生效的过滤器



### 3.5.全局过滤器

上一节学习的过滤器，网关提供了31种，但每一种过滤器的作用都是固定的。如果我们希望拦截请求，做自己的业务逻辑则没办法实现。

#### 3.5.1.全局过滤器作用

全局过滤器的作用也是处理一切进入网关的请求和微服务响应，与GatewayFilter的作用一样。区别在于GatewayFilter通过配置定义，处理逻辑是固定的；而GlobalFilter的逻辑需要自己写代码实现。

定义方式是实现GlobalFilter接口。

```java
public interface GlobalFilter {
    /**
     *  处理当前请求，有必要的话通过{@link GatewayFilterChain}将请求交给下一个过滤器处理
     *
     * @param exchange 请求上下文，里面可以获取Request、Response等信息
     * @param chain 用来把请求委托给下一个过滤器 
     * @return {@code Mono<Void>} 返回标示当前过滤器业务结束
     */
    Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain);
}
```



在filter中编写自定义逻辑，可以实现下列功能：

- 登录状态判断
- 权限校验
- 请求限流等





#### 3.5.2.自定义全局过滤器

需求：定义全局过滤器，拦截请求，判断请求的参数是否满足下面条件：

- 参数中是否有authorization，

- authorization参数值是否为admin

如果同时满足则放行，否则拦截



实现：

在gateway中定义一个过滤器：

```java
package cn.itcast.gateway.filters;

import org.springframework.cloud.gateway.filter.GatewayFilterChain;
import org.springframework.cloud.gateway.filter.GlobalFilter;
import org.springframework.core.annotation.Order;
import org.springframework.http.HttpStatus;
import org.springframework.stereotype.Component;
import org.springframework.web.server.ServerWebExchange;
import reactor.core.publisher.Mono;

@Order(-1)
@Component
public class AuthorizeFilter implements GlobalFilter {
    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        // 1.获取请求参数
        MultiValueMap<String, String> params = exchange.getRequest().getQueryParams();
        // 2.获取authorization参数
        String auth = params.getFirst("authorization");
        // 3.校验
        if ("admin".equals(auth)) {
            // 放行
            return chain.filter(exchange);
        }
        // 4.拦截
        // 4.1.禁止访问，设置状态码
        exchange.getResponse().setStatusCode(HttpStatus.FORBIDDEN);
        // 4.2.结束处理
        return exchange.getResponse().setComplete();
    }
}
```





#### 3.5.3.过滤器执行顺序

请求进入网关会碰到三类过滤器：当前路由的过滤器、DefaultFilter、GlobalFilter

请求路由后，会将当前路由过滤器和DefaultFilter、GlobalFilter，合并到一个过滤器链（集合）中，排序后依次执行每个过滤器：

![image-20210714214228409](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153589.png)



排序的规则是什么呢？

- 每一个过滤器都必须指定一个int类型的order值，**order值越小，优先级越高，执行顺序越靠前**。
- GlobalFilter通过实现Ordered接口，或者添加@Order注解来指定order值，由我们自己指定
- 路由过滤器和defaultFilter的order由Spring指定，默认是按照声明顺序从1递增。
- 当过滤器的order值一样时，会按照 defaultFilter > 路由过滤器 > GlobalFilter的顺序执行。



详细内容，可以查看源码：

`org.springframework.cloud.gateway.route.RouteDefinitionRouteLocator#getFilters()`方法是先加载defaultFilters，然后再加载某个route的filters，然后合并。



`org.springframework.cloud.gateway.handler.FilteringWebHandler#handle()`方法会加载全局过滤器，与前面的过滤器合并后根据order排序，组织过滤器链



### 3.6.跨域问题



#### 3.6.1.什么是跨域问题

跨域：域名不一致就是跨域，主要包括：

- 域名不同： www.taobao.com 和 www.taobao.org 和 www.jd.com 和 miaosha.jd.com

- 域名相同，端口不同：localhost:8080和localhost8081

跨域问题：浏览器禁止请求的发起者与服务端发生跨域ajax请求，请求被浏览器拦截的问题



解决方案：CORS，这个以前应该学习过，这里不再赘述了。不知道的小伙伴可以查看https://www.ruanyifeng.com/blog/2016/04/cors.html



#### 3.6.2.模拟跨域问题

找到课前资料的页面文件：

![image-20210714215713563](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153590.png)

放入tomcat或者nginx这样的web服务器中，启动并访问。

可以在浏览器控制台看到下面的错误：

![image-20210714215832675](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153591.png)



从localhost:8090访问localhost:10010，端口不同，显然是跨域的请求。



#### 3.6.3.解决跨域问题

在gateway服务的application.yml文件中，添加下面的配置：

```yaml
spring:
  cloud:
    gateway:
      ## 。。。
      globalcors: ## 全局的跨域处理
        add-to-simple-url-handler-mapping: true ## 解决options请求被拦截问题
        corsConfigurations:
          '[/**]':
            allowedOrigins: ## 允许哪些网站的跨域请求 
              - "http://localhost:8090"
            allowedMethods: ## 允许的跨域ajax的请求方式
              - "GET"
              - "POST"
              - "DELETE"
              - "PUT"
              - "OPTIONS"
            allowedHeaders: "*" ## 允许在请求中携带的头信息
            allowCredentials: true ## 是否允许携带cookie
            maxAge: 360000 ## 这次跨域检测的有效期
```







# Docker实用篇

## 0.学习目标

## 1.初识Docker

### 1.1.什么是Docker

微服务虽然具备各种各样的优势，但服务的拆分通用给部署带来了很大的麻烦。

- 分布式系统中，依赖的组件非常多，不同组件之间部署时往往会产生一些冲突。
- 在数百上千台服务中重复部署，环境不一定一致，会遇到各种问题



#### 1.1.1.应用部署的环境问题

大型项目组件较多，运行环境也较为复杂，部署时会碰到一些问题：

- 依赖关系复杂，容易出现兼容性问题

- 开发、测试、生产环境有差异



![image-20210731141907366](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153592.png)



例如一个项目中，部署时需要依赖于node.js、Redis、RabbitMQ、MySQL等，这些服务部署时所需要的函数库、依赖项各不相同，甚至会有冲突。给部署带来了极大的困难。



#### 1.1.2.Docker解决依赖兼容问题

而Docker确巧妙的解决了这些问题，Docker是如何实现的呢？

Docker为了解决依赖的兼容问题的，采用了两个手段：

- 将应用的Libs（函数库）、Deps（依赖）、配置与应用一起打包

- 将每个应用放到一个隔离**容器**去运行，避免互相干扰

![image-20210731142219735](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153593.png)



这样打包好的应用包中，既包含应用本身，也保护应用所需要的Libs、Deps，无需再操作系统上安装这些，自然就不存在不同应用之间的兼容问题了。



虽然解决了不同应用的兼容问题，但是开发、测试等环境会存在差异，操作系统版本也会有差异，怎么解决这些问题呢？



#### 1.1.3.Docker解决操作系统环境差异

要解决不同操作系统环境差异问题，必须先了解操作系统结构。以一个Ubuntu操作系统为例，结构如下：

![image-20210731143401460](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153594.png)



结构包括：

- 计算机硬件：例如CPU、内存、磁盘等
- 系统内核：所有Linux发行版的内核都是Linux，例如CentOS、Ubuntu、Fedora等。内核可以与计算机硬件交互，对外提供**内核指令**，用于操作计算机硬件。
- 系统应用：操作系统本身提供的应用、函数库。这些函数库是对内核指令的封装，使用更加方便。



应用于计算机交互的流程如下：

1）应用调用操作系统应用（函数库），实现各种功能

2）系统函数库是对内核指令集的封装，会调用内核指令

3）内核指令操作计算机硬件



Ubuntu和CentOSpringBoot都是基于Linux内核，无非是系统应用不同，提供的函数库有差异：

![image-20210731144304990](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153595.png)



此时，如果将一个Ubuntu版本的MySQL应用安装到CentOS系统，MySQL在调用Ubuntu函数库时，会发现找不到或者不匹配，就会报错了：

![image-20210731144458680](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153596.png)



Docker如何解决不同系统环境的问题？

- Docker将用户程序与所需要调用的系统(比如Ubuntu)函数库一起打包
- Docker运行到不同操作系统时，直接基于打包的函数库，借助于操作系统的Linux内核来运行

如图：

![image-20210731144820638](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153597.png)



#### 1.1.4.小结

Docker如何解决大型项目依赖关系复杂，不同组件依赖的兼容性问题？

- Docker允许开发中将应用、依赖、函数库、配置一起**打包**，形成可移植镜像
- Docker应用运行在容器中，使用沙箱机制，相互**隔离**



Docker如何解决开发、测试、生产环境有差异的问题？

- Docker镜像中包含完整运行环境，包括系统函数库，仅依赖系统的Linux内核，因此可以在任意Linux操作系统上运行



Docker是一个快速交付应用、运行应用的技术，具备下列优势：

- 可以将程序及其依赖、运行环境一起打包为一个镜像，可以迁移到任意Linux操作系统
- 运行时利用沙箱机制形成隔离容器，各个应用互不干扰
- 启动、移除都可以通过一行命令完成，方便快捷



### 1.2.Docker和虚拟机的区别

Docker可以让一个应用在任何操作系统中非常方便的运行。而以前我们接触的虚拟机，也能在一个操作系统中，运行另外一个操作系统，保护系统中的任何应用。



两者有什么差异呢？



**虚拟机**（virtual machine）是在操作系统中**模拟**硬件设备，然后运行另一个操作系统，比如在 Windows 系统里面运行 Ubuntu 系统，这样就可以运行任意的Ubuntu应用了。

**Docker**仅仅是封装函数库，并没有模拟完整的操作系统，如图：

![image-20210731145914960](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153598.png)

对比来看：

![image-20210731152243765](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153599.png)



小结：

Docker和虚拟机的差异：

- docker是一个系统进程；虚拟机是在操作系统中的操作系统

- docker体积小、启动速度快、性能好；虚拟机体积大、启动速度慢、性能一般







### 1.3.Docker架构



#### 1.3.1.镜像和容器

Docker中有几个重要的概念：

**镜像（Image）**：Docker将应用程序及其所需的依赖、函数库、环境、配置等文件打包在一起，称为镜像。

**容器（Container）**：镜像中的应用程序运行后形成的进程就是**容器**，只是Docker会给容器进程做隔离，对外不可见。



一切应用最终都是代码组成，都是硬盘中的一个个的字节形成的**文件**。只有运行时，才会加载到内存，形成进程。



而**镜像**，就是把一个应用在硬盘上的文件、及其运行环境、部分系统函数库文件一起打包形成的文件包。这个文件包是只读的。

**容器**呢，就是将这些文件中编写的程序、函数加载到内存中允许，形成进程，只不过要隔离起来。因此一个镜像可以启动多次，形成多个容器进程。



![image-20210731153059464](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153600.png)



例如你下载了一个QQ，如果我们将QQ在磁盘上的运行**文件**及其运行的操作系统依赖打包，形成QQ镜像。然后你可以启动多次，双开、甚至三开QQ，跟多个妹子聊天。



#### 1.3.2.DockerHub

开源应用程序非常多，打包这些应用往往是重复的劳动。为了避免这些重复劳动，人们就会将自己打包的应用镜像，例如Redis、MySQL镜像放到网络上，共享使用，就像GitHub的代码共享一样。

- DockerHub：DockerHub是一个官方的Docker镜像的托管平台。这样的平台称为Docker Registry。

- 国内也有类似于DockerHub 的公开服务，比如 [网易云镜像服务](https://c.163yun.com/hub)、[阿里云镜像库](https://cr.console.aliyun.com/)等。



我们一方面可以将自己的镜像共享到DockerHub，另一方面也可以从DockerHub拉取镜像：

![image-20210731153743354](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153601.png)



#### 1.3.3.Docker架构

我们要使用Docker来操作镜像、容器，就必须要安装Docker。

Docker是一个CS架构的程序，由两部分组成：

- 服务端(server)：Docker守护进程，负责处理Docker指令，管理镜像、容器等

- 客户端(client)：通过命令或RestAPI向Docker服务端发送指令。可以在本地或远程向服务端发送指令。



如图：

![image-20210731154257653](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153602.png)



#### 1.3.4.小结



镜像：

- 将应用程序及其依赖、环境、配置打包在一起

容器：

- 镜像运行起来就是容器，一个镜像可以运行多个容器

Docker结构：

- 服务端：接收命令或远程请求，操作镜像或容器

- 客户端：发送命令或者请求到Docker服务端

DockerHub：

- 一个镜像托管的服务器，类似的还有阿里云镜像服务，统称为DockerRegistry



### 1.4.安装Docker

企业部署一般都是采用Linux操作系统，而其中又数CentOS发行版占比最多，因此我们在CentOS下安装Docker。参考课前资料中的文档：

![image-20210731155002425](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153603.png)





## 2.Docker的基本操作

### 2.1.镜像操作



#### 2.1.1.镜像名称

首先来看下镜像的名称组成：

- 镜名称一般分两部分组成：[repository]:[tag]。
- 在没有指定tag时，默认是latest，代表最新版本的镜像

如图：

![image-20210731155141362](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153604.png)

这里的mysql就是repository，5.7就是tag，合一起就是镜像名称，代表5.7版本的MySQL镜像。



#### 2.1.2.镜像命令

常见的镜像操作命令如图：

![image-20210731155649535](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153605.png)



#### 2.1.3.案例1-拉取、查看镜像

需求：从DockerHub中拉取一个nginx镜像并查看

1）首先去镜像仓库搜索nginx镜像，比如[DockerHub](https://hub.docker.com/):

![image-20210731155844368](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153606.png)

2）根据查看到的镜像名称，拉取自己需要的镜像，通过命令：docker pull nginx

![image-20210731155856199](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153607.png)

3）通过命令：docker images 查看拉取到的镜像

![image-20210731155903037](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153608.png)



#### 2.1.4.案例2-保存、导入镜像

需求：利用docker save将nginx镜像导出磁盘，然后再通过load加载回来

1）利用docker xx --help命令查看docker save和docker load的语法

例如，查看save命令用法，可以输入命令：

```sh
docker save --help
```

结果：

![image-20210731161104732](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153609.png)



命令格式：

```shell
docker save -o [保存的目标文件名称] [镜像名称]
```



2）使用docker save导出镜像到磁盘 

运行命令：

```sh
docker save -o nginx.tar nginx:latest
```

结果如图：

![image-20210731161354344](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153610.png)



3）使用docker load加载镜像

先删除本地的nginx镜像：

```sh
docker rmi nginx:latest
```



然后运行命令，加载本地文件：

```sh
docker load -i nginx.tar
```

结果：

![image-20210731161746245](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153611.png)





#### 2.1.5.练习

需求：去DockerHub搜索并拉取一个Redis镜像

目标：

1）去DockerHub搜索Redis镜像

2）查看Redis镜像的名称和版本

3）利用docker pull命令拉取镜像

4）利用docker save命令将 redis:latest打包为一个redis.tar包

5）利用docker rmi 删除本地的redis:latest

6）利用docker load 重新加载 redis.tar文件



### 2.2.容器操作

#### 2.2.1.容器相关命令

容器操作的命令如图：

![image-20210731161950495](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153612.png)

容器保护三个状态：

- 运行：进程正常运行
- 暂停：进程暂停，CPU不再运行，并不释放内存
- 停止：进程终止，回收进程占用的内存、CPU等资源



其中：

- docker run：创建并运行一个容器，处于运行状态
- docker pause：让一个运行的容器暂停
- docker unpause：让一个容器从暂停状态恢复运行
- docker stop：停止一个运行的容器
- docker start：让一个停止的容器再次运行

- docker rm：删除一个容器



#### 2.2.2.案例-创建并运行一个容器

创建并运行nginx容器的命令：

```sh
docker run --name containerName -p 80:80 -d nginx
```

命令解读：

- docker run ：创建并运行一个容器
- --name : 给容器起一个名字，比如叫做mn
- -p ：将宿主机端口与容器端口映射，冒号左侧是宿主机端口，右侧是容器端口
- -d：后台运行容器
- nginx：镜像名称，例如nginx



这里的`-p`参数，是将容器端口映射到宿主机端口。

默认情况下，容器是隔离环境，我们直接访问宿主机的80端口，肯定访问不到容器中的nginx。

现在，将容器的80与宿主机的80关联起来，当我们访问宿主机的80端口时，就会被映射到容器的80，这样就能访问到nginx了：

![image-20210731163255863](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153613.png)



#### 2.2.3.案例-进入容器，修改文件

**需求**：进入Nginx容器，修改HTML文件内容，添加“传智教育欢迎您”

**提示**：进入容器要用到docker exec命令。



**步骤**：

1）进入容器。进入我们刚刚创建的nginx容器的命令为：

```sh
docker exec -it mn bash
```

命令解读：

- docker exec ：进入容器内部，执行一个命令

- -it : 给当前进入的容器创建一个标准输入、输出终端，允许我们与容器交互

- mn ：要进入的容器的名称

- bash：进入容器后执行的命令，bash是一个linux终端交互命令



2）进入nginx的HTML所在目录 /usr/share/nginx/html

容器内部会模拟一个独立的Linux文件系统，看起来如同一个linux服务器一样：

![image-20210731164159811](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153614.png)

nginx的环境、配置、运行文件全部都在这个文件系统中，包括我们要修改的html文件。

查看DockerHub网站中的nginx页面，可以知道nginx的html目录位置在`/usr/share/nginx/html`

我们执行命令，进入该目录：

```sh
cd /usr/share/nginx/html
```

 查看目录下文件：

![image-20210731164455818](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153615.png)





3）修改index.html的内容

容器内没有vi命令，无法直接修改，我们用下面的命令来修改：

```sh
sed -i -e 's#Welcome to nginx#传智教育欢迎您#g' -e 's#<head>#<head><meta charset="utf-8">#g' index.html
```



在浏览器访问自己的虚拟机地址，例如我的是：http://192.168.150.101，即可看到结果：

![image-20210731164717604](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153616.png)



#### 2.2.4.小结



docker run命令的常见参数有哪些？

- --name：指定容器名称
- -p：指定端口映射
- -d：让容器后台运行

查看容器日志的命令：

- docker logs
- 添加 -f 参数可以持续查看日志

查看容器状态：

- docker ps
- docker ps -a 查看所有容器，包括已经停止的









### 2.3.数据卷（容器数据管理）

在之前的nginx案例中，修改nginx的html页面时，需要进入nginx内部。并且因为没有编辑器，修改文件也很麻烦。

这就是因为容器与数据（容器内文件）耦合带来的后果。

![image-20210731172440275](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153617.png)

要解决这个问题，必须将数据与容器解耦，这就要用到数据卷了。



#### 2.3.1.什么是数据卷

**数据卷（volume）**是一个虚拟目录，指向宿主机文件系统中的某个目录。

![image-20210731173541846](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153618.png)

一旦完成数据卷挂载，对容器的一切操作都会作用在数据卷对应的宿主机目录了。

这样，我们操作宿主机的/var/lib/docker/volumes/html目录，就等于操作容器内的/usr/share/nginx/html目录了





#### 2.3.2.数据集操作命令



数据卷操作的基本语法如下：

```sh
docker volume [COMMAND]
```

docker volume命令是数据卷操作，根据命令后跟随的command来确定下一步的操作：

- create 创建一个volume
- inspect 显示一个或多个volume的信息
- ls 列出所有的volume
- prune 删除未使用的volume
- rm 删除一个或多个指定的volume



#### 2.3.3.创建和查看数据卷

**需求**：创建一个数据卷，并查看数据卷在宿主机的目录位置

① 创建数据卷

```sh
docker volume create html
```



② 查看所有数据

```sh
docker volume ls
```

结果：

![image-20210731173746910](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153619.png)





③ 查看数据卷详细信息卷

```sh
docker volume inspect html
```

结果：

![image-20210731173809877](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153620.png)

可以看到，我们创建的html这个数据卷关联的宿主机目录为`/var/lib/docker/volumes/html/_data`目录。







**小结**：

数据卷的作用：

- 将容器与数据分离，解耦合，方便操作容器内数据，保证数据安全

数据卷操作：

- docker volume create：创建数据卷
- docker volume ls：查看所有数据卷
- docker volume inspect：查看数据卷详细信息，包括关联的宿主机目录位置
- docker volume rm：删除指定数据卷
- docker volume prune：删除所有未使用的数据卷



#### 2.3.4.挂载数据卷

我们在创建容器时，可以通过 -v 参数来挂载一个数据卷到某个容器内目录，命令格式如下：

```sh
docker run \
  --name mn \
  -v html:/root/html \
  -p 8080:80
  nginx \
```

这里的-v就是挂载数据卷的命令：

- `-v html:/root/htm` ：把html数据卷挂载到容器内的/root/html这个目录中



#### 2.3.5.案例-给nginx挂载数据卷

**需求**：创建一个nginx容器，修改容器内的html目录内的index.html内容



**分析**：上个案例中，我们进入nginx容器内部，已经知道nginx的html目录所在位置/usr/share/nginx/html ，我们需要把这个目录挂载到html这个数据卷上，方便操作其中的内容。

**提示**：运行容器时使用 -v 参数挂载数据卷

步骤：

① 创建容器并挂载数据卷到容器内的HTML目录

```sh
docker run --name mn -v html:/usr/share/nginx/html -p 80:80 -d nginx
```



② 进入html数据卷所在位置，并修改HTML内容

```sh
## 查看html数据卷的位置
docker volume inspect html
## 进入该目录
cd /var/lib/docker/volumes/html/_data
## 修改文件
vi index.html
```



#### 2.3.6.案例-给MySQL挂载本地目录

容器不仅仅可以挂载数据卷，也可以直接挂载到宿主机目录上。关联关系如下：

- 带数据卷模式：宿主机目录 --> 数据卷 ---> 容器内目录
- 直接挂载模式：宿主机目录 ---> 容器内目录

如图：

![image-20210731175155453](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153621.png)

**语法**：

目录挂载与数据卷挂载的语法是类似的：

- -v [宿主机目录]:[容器内目录]
- -v [宿主机文件]:[容器内文件]





**需求**：创建并运行一个MySQL容器，将宿主机目录直接挂载到容器



实现思路如下：

1）在将课前资料中的mysql.tar文件上传到虚拟机，通过load命令加载为镜像

2）创建目录/tmp/mysql/data

3）创建目录/tmp/mysql/conf，将课前资料提供的hmy.cnf文件上传到/tmp/mysql/conf

4）去DockerHub查阅资料，创建并运行MySQL容器，要求：

① 挂载/tmp/mysql/data到mysql容器内数据存储目录

② 挂载/tmp/mysql/conf/hmy.cnf到mysql容器的配置文件

③ 设置MySQL密码



#### 2.3.7.小结

docker run的命令中通过 -v 参数挂载文件或目录到容器中：

- -v volume名称:容器内目录
- -v 宿主机文件:容器内文
- -v 宿主机目录:容器内目录

数据卷挂载与目录直接挂载的

- 数据卷挂载耦合度低，由docker来管理目录，但是目录较深，不好找
- 目录挂载耦合度高，需要我们自己管理目录，不过目录容易寻找查看







## 3.Dockerfile自定义镜像

常见的镜像在DockerHub就能找到，但是我们自己写的项目就必须自己构建镜像了。

而要自定义镜像，就必须先了解镜像的结构才行。

### 3.1.镜像结构

镜像是将应用程序及其需要的系统函数库、环境、配置、依赖打包而成。

我们以MySQL为例，来看看镜像的组成结构：

![image-20210731175806273](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153622.png)



简单来说，镜像就是在系统函数库、运行环境基础上，添加应用程序文件、配置文件、依赖文件等组合，然后编写好启动脚本打包在一起形成的文件。



我们要构建镜像，其实就是实现上述打包的过程。



### 3.2.Dockerfile语法

构建自定义的镜像时，并不需要一个个文件去拷贝，打包。

我们只需要告诉Docker，我们的镜像的组成，需要哪些BaseImage、需要拷贝什么文件、需要安装什么依赖、启动脚本是什么，将来Docker会帮助我们构建镜像。



而描述上述信息的文件就是Dockerfile文件。



**Dockerfile**就是一个文本文件，其中包含一个个的**指令(Instruction)**，用指令来说明要执行什么操作来构建镜像。每一个指令都会形成一层Layer。

![image-20210731180321133](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153623.png)



更新详细语法说明，请参考官网文档： https://docs.docker.com/engine/reference/builder







### 3.3.构建Java项目



#### 3.3.1.基于Ubuntu构建Java项目

需求：基于Ubuntu镜像构建一个新镜像，运行一个java项目

- 步骤1：新建一个空文件夹docker-demo

  ![image-20210801101207444](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153624.png)

- 步骤2：拷贝课前资料中的docker-demo.jar文件到docker-demo这个目录

  ![image-20210801101314816](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153625.png)

- 步骤3：拷贝课前资料中的jdk8.tar.gz文件到docker-demo这个目录

  ![image-20210801101410200](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153626.png)

- 步骤4：拷贝课前资料提供的Dockerfile到docker-demo这个目录

  ![image-20210801101455590](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153627.png)

  其中的内容如下：

  ```dockerfile
  ## 指定基础镜像
  FROM ubuntu:16.04
  ## 配置环境变量，JDK的安装目录
  ENV JAVA_DIR=/usr/local
  
  ## 拷贝jdk和java项目的包
  COPY ./jdk8.tar.gz $JAVA_DIR/
  COPY ./docker-demo.jar /tmp/app.jar
  
  ## 安装JDK
  RUN cd $JAVA_DIR \
   && tar -xf ./jdk8.tar.gz \
   && mv ./jdk1.8.0_144 ./java8
  
  ## 配置环境变量
  ENV JAVA_HOME=$JAVA_DIR/java8
  ENV PATH=$PATH:$JAVA_HOME/bin
  
  ## 暴露端口
  EXPOSE 8090
  ## 入口，java项目的启动命令
  ENTRYPOINT java -jar /tmp/app.jar
  ```

  

- 步骤5：进入docker-demo

  将准备好的docker-demo上传到虚拟机任意目录，然后进入docker-demo目录下

- 步骤6：运行命令：

  ```sh
  docker build -t javaweb:1.0 .
  ```

  

最后访问 http://192.168.150.101:8090/hello/count，其中的ip改成你的虚拟机ip



#### 3.3.2.基于java8构建Java项目

虽然我们可以基于Ubuntu基础镜像，添加任意自己需要的安装包，构建镜像，但是却比较麻烦。所以大多数情况下，我们都可以在一些安装了部分软件的基础镜像上做改造。

例如，构建java项目的镜像，可以在已经准备了JDK的基础镜像基础上构建。



需求：基于java:8-alpine镜像，将一个Java项目构建为镜像

实现思路如下：

- ① 新建一个空的目录，然后在目录中新建一个文件，命名为Dockerfile

- ② 拷贝课前资料提供的docker-demo.jar到这个目录中

- ③ 编写Dockerfile文件：

  - a ）基于java:8-alpine作为基础镜像

  - b ）将app.jar拷贝到镜像中

  - c ）暴露端口

  - d ）编写入口ENTRYPOINT

    内容如下：

    ```dockerfile
    FROM java:8-alpine
    COPY ./app.jar /tmp/app.jar
    EXPOSE 8090
    ENTRYPOINT java -jar /tmp/app.jar
    ```

    

- ④ 使用docker build命令构建镜像

- ⑤ 使用docker run创建容器并运行



### 3.4.小结

小结：

1. Dockerfile的本质是一个文件，通过指令描述镜像的构建过程

2. Dockerfile的第一行必须是FROM，从一个基础镜像来构建

3. 基础镜像可以是基本操作系统，如Ubuntu。也可以是其他人制作好的镜像，例如：java:8-alpine



## 4.Docker-Compose

Docker Compose可以基于Compose文件帮我们快速的部署分布式应用，而无需手动一个个创建和运行容器！

![image-20210731180921742](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153628.png)

### 4.1.初识DockerCompose

Compose文件是一个文本文件，通过指令定义集群中的每个容器如何运行。格式如下：

```json
version: "3.8"
 services:
  mysql:
    image: mysql:5.7.25
    environment:
     MYSQL_ROOT_PASSWORD: 123 
    volumes:
     - "/tmp/mysql/data:/var/lib/mysql"
     - "/tmp/mysql/conf/hmy.cnf:/etc/mysql/conf.d/hmy.cnf"
  web:
    build: .
    ports:
     - "8090:8090"

```

上面的Compose文件就描述一个项目，其中包含两个容器：

- mysql：一个基于`mysql:5.7.25`镜像构建的容器，并且挂载了两个目录
- web：一个基于`docker build`临时构建的镜像容器，映射端口时8090



DockerCompose的详细语法参考官网：https://docs.docker.com/compose/compose-file/



其实DockerCompose文件可以看做是将多个docker run命令写到一个文件，只是语法稍有差异。



### 4.2.安装DockerCompose

参考课前资料



### 4.3.部署微服务集群

**需求**：将之前学习的cloud-demo微服务集群利用DockerCompose部署



**实现思路**：

① 查看课前资料提供的cloud-demo文件夹，里面已经编写好了docker-compose文件

② 修改自己的cloud-demo项目，将数据库、nacos地址都命名为docker-compose中的服务名

③ 使用maven打包工具，将项目中的每个微服务都打包为app.jar

④ 将打包好的app.jar拷贝到cloud-demo中的每一个对应的子目录中

⑤ 将cloud-demo上传至虚拟机，利用 docker-compose up -d 来部署



#### 4.3.1.compose文件

查看课前资料提供的cloud-demo文件夹，里面已经编写好了docker-compose文件，而且每个微服务都准备了一个独立的目录：

![image-20210731181341330](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153629.png)

内容如下：

```yaml
version: "3.2"

services:
  nacos:
    image: nacos/nacos-server
    environment:
      MODE: standalone
    ports:
      - "8848:8848"
  mysql:
    image: mysql:5.7.25
    environment:
      MYSQL_ROOT_PASSWORD: 123
    volumes:
      - "$PWD/mysql/data:/var/lib/mysql"
      - "$PWD/mysql/conf:/etc/mysql/conf.d/"
  userservice:
    build: ./user-service
  orderservice:
    build: ./order-service
  gateway:
    build: ./gateway
    ports:
      - "10010:10010"
```

可以看到，其中包含5个service服务：

- `nacos`：作为注册中心和配置中心
  - `image: nacos/nacos-server`： 基于nacos/nacos-server镜像构建
  - `environment`：环境变量
    - `MODE: standalone`：单点模式启动
  - `ports`：端口映射，这里暴露了8848端口
- `mysql`：数据库
  - `image: mysql:5.7.25`：镜像版本是mysql:5.7.25
  - `environment`：环境变量
    - `MYSQL_ROOT_PASSWORD: 123`：设置数据库root账户的密码为123
  - `volumes`：数据卷挂载，这里挂载了mysql的data、conf目录，其中有我提前准备好的数据
- `userservice`、`orderservice`、`gateway`：都是基于Dockerfile临时构建的



查看mysql目录，可以看到其中已经准备好了cloud_order、cloud_user表：

![image-20210801095205034](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153630.png)

查看微服务目录，可以看到都包含Dockerfile文件：

![image-20210801095320586](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153631.png)

内容如下：

```dockerfile
FROM java:8-alpine
COPY ./app.jar /tmp/app.jar
ENTRYPOINT java -jar /tmp/app.jar
```





#### 4.3.2.修改微服务配置

因为微服务将来要部署为docker容器，而容器之间互联不是通过IP地址，而是通过容器名。这里我们将order-service、user-service、gateway服务的mysql、nacos地址都修改为基于容器名的访问。

如下所示：

```yaml
spring:
  datasource:
    url: jdbc:mysql://mysql:3306/cloud_order?useSSL=false
    username: root
    password: 123
    driver-class-name: com.mysql.jdbc.Driver
  application:
    name: orderservice
  cloud:
    nacos:
      server-addr: nacos:8848 ## nacos服务地址
```



#### 4.3.3.打包

接下来需要将我们的每个微服务都打包。因为之前查看到Dockerfile中的jar包名称都是app.jar，因此我们的每个微服务都需要用这个名称。

可以通过修改pom.xml中的打包名称来实现，每个微服务都需要修改：

```xml
<build>
  <!-- 服务打包的最终名称 -->
  <finalName>app</finalName>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
  </plugins>
</build>
```

打包后：

![image-20210801095951030](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153632.png)

#### 4.3.4.拷贝jar包到部署目录

编译打包好的app.jar文件，需要放到Dockerfile的同级目录中。注意：每个微服务的app.jar放到与服务名称对应的目录，别搞错了。

user-service：

![image-20210801100201253](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153633.png)

order-service：

![image-20210801100231495](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153634.png)

gateway：

![image-20210801100308102](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153635.png)

#### 4.3.5.部署

最后，我们需要将文件整个cloud-demo文件夹上传到虚拟机中，理由DockerCompose部署。

上传到任意目录：

![image-20210801100955653](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153636.png)

部署：

进入cloud-demo目录，然后运行下面的命令：

```sh
docker-compose up -d
```







## 5.Docker镜像仓库 



### 5.1.搭建私有镜像仓库

参考课前资料《CentOS7安装Docker.md》



### 5.2.推送、拉取镜像

推送镜像到私有镜像服务必须先tag，步骤如下：

① 重新tag本地镜像，名称前缀为私有仓库的地址：192.168.150.101:8080/

 ```sh
docker tag nginx:latest 192.168.150.101:8080/nginx:1.0 
 ```



② 推送镜像

```sh
docker push 192.168.150.101:8080/nginx:1.0 
```



③ 拉取镜像

```sh
docker pull 192.168.150.101:8080/nginx:1.0 
```

# Centos 7 安装Docker

```shell
$ mkdir /opt; cd /opt
$ wget https://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/Packages/docker-ce-19.03.9-3.el7.x86_64.rpm
$ wget https://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/Packages/docker-ce-cli-19.03.9-3.el7.x86_64.rpm
$ wget https://mirrors.aliyun.com/docker-ce/linux/centos/7/x86_64/stable/Packages/containerd.io-1.3.9-3.1.el7.x86_64.rpm

# 清理原有版本
$ yum remove -y docker* container-selinux

$ yum localinstall -y *.rpm

$ mkdir /etc/docker/
$ vi /etc/docker/daemon.json
{
    "graph": "/var/lib/docker",
    "insecure-registries":["hub:5000"]
}

$ systemctl daemon-reload
$ systemctl enable docker
$ service docker start
```



## 0.安装Docker

Docker 分为 CE 和 EE 两大版本。CE 即社区版（免费，支持周期 7 个月），EE 即企业版，强调安全，付费使用，支持周期 24 个月。

Docker CE 分为 `stable` `test` 和 `nightly` 三个更新频道。

官方网站上有各种环境下的 [安装指南](https://docs.docker.com/install/)，这里主要介绍 Docker CE 在 CentOS上的安装。

## 1.CentOS安装Docker

Docker CE 支持 64 位版本 CentOS 7，并且要求内核版本不低于 3.10， CentOS 7 满足最低内核的要求，所以我们在CentOS 7安装Docker。



### 1.1.卸载（可选）

如果之前安装过旧版本的Docker，可以使用下面命令卸载：

```
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine \
                  docker-ce
```



### 1.2.安装docker

首先需要大家虚拟机联网，安装yum工具

```sh
yum install -y yum-utils \
           device-mapper-persistent-data \
           lvm2 --skip-broken
```



然后更新本地镜像源：

```shell
## 设置docker镜像源
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    
sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

yum makecache fast
```





然后输入命令：

```shell
yum install -y docker-ce
```

docker-ce为社区免费版本。稍等片刻，docker即可安装成功。



### 1.3.启动docker

Docker应用需要用到各种端口，逐一去修改防火墙设置。非常麻烦，因此建议大家直接关闭防火墙！

启动docker前，一定要关闭防火墙后！！

启动docker前，一定要关闭防火墙后！！

启动docker前，一定要关闭防火墙后！！



```sh
## 关闭
systemctl stop firewalld
## 禁止开机启动防火墙
systemctl disable firewalld
```



通过命令启动docker：

```sh
systemctl start docker  ## 启动docker服务

systemctl stop docker  ## 停止docker服务

systemctl restart docker  ## 重启docker服务
```



然后输入命令，可以查看docker版本：

```
docker -v
```

如图：

![image-20210418154704436](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153637.png) 



### 1.4.配置镜像加速

docker官方镜像仓库网速较差，我们需要设置国内镜像服务：

参考阿里云的镜像加速文档：https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors





## 2.CentOS7安装DockerCompose



### 2.1.下载

Linux下需要通过命令下载：

```sh
## 安装
curl -L https://github.com/docker/compose/releases/download/1.23.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```

如果下载速度较慢，或者下载失败，可以使用课前资料提供的docker-compose文件：

![image-20210417133020614](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153638.png)

上传到`/usr/local/bin/`目录也可以。



### 2.2.修改文件权限

修改文件权限：

```sh
## 修改权限
chmod +x /usr/local/bin/docker-compose
```





### 2.3.Base自动补全命令：

```sh
## 补全命令
curl -L https://raw.githubusercontent.com/docker/compose/1.29.1/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose
```

如果这里出现错误，需要修改自己的hosts文件：

```sh
echo "199.232.68.133 raw.githubusercontent.com" >> /etc/hosts
```





## 3.Docker镜像仓库

搭建镜像仓库可以基于Docker官方提供的DockerRegistry来实现。

官网地址：https://hub.docker.com/_/registry



### 3.1.简化版镜像仓库

Docker官方的Docker Registry是一个基础版本的Docker镜像仓库，具备仓库管理的完整功能，但是没有图形化界面。

搭建方式比较简单，命令如下：

```sh
docker run -d \
    --restart=always \
    --name registry	\
    -p 5000:5000 \
    -v registry-data:/var/lib/registry \
    registry
```



命令中挂载了一个数据卷registry-data到容器内的/var/lib/registry 目录，这是私有镜像库存放数据的目录。

访问http://YourIp:5000/v2/_catalog 可以查看当前私有镜像服务中包含的镜像



### 3.2.带有图形化界面版本

使用DockerCompose部署带有图象界面的DockerRegistry，命令如下：

```yaml
version: '3.0'
services:
  registry:
    image: registry
    volumes:
      - ./registry-data:/var/lib/registry
  ui:
    image: joxit/docker-registry-ui:static
    ports:
      - 8080:80
    environment:
      - REGISTRY_TITLE=传智教育私有仓库
      - REGISTRY_URL=http://registry:5000
    depends_on:
      - registry
```



### 3.3.配置Docker信任地址

我们的私服采用的是http协议，默认不被Docker信任，所以需要做一个配置：

```sh
## 打开要修改的文件
vi /etc/docker/daemon.json
## 添加内容：
"insecure-registries":["http://192.168.150.101:8080"]
## 重加载
systemctl daemon-reload
## 重启docker
systemctl restart docker
```

# 微服务保护





## 1.初识Sentinel



### 1.1.雪崩问题及解决方案



#### 1.1.1.雪崩问题



微服务中，服务间调用关系错综复杂，一个微服务往往依赖于多个其它微服务。

 ![1533829099748](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153639.png)



如图，如果服务提供者I发生了故障，当前的应用的部分业务因为依赖于服务I，因此也会被阻塞。此时，其它不依赖于服务I的业务似乎不受影响。

 ![1533829198240](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153640.png)

但是，依赖服务I的业务请求被阻塞，用户不会得到响应，则tomcat的这个线程不会释放，于是越来越多的用户请求到来，越来越多的线程会阻塞：

 ![1533829307389](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153642.png)

服务器支持的线程和并发数有限，请求一直阻塞，会导致服务器资源耗尽，从而导致所有其它服务都不可用，那么当前服务也就不可用了。

那么，依赖于当前服务的其它服务随着时间的推移，最终也都会变的不可用，形成级联失败，雪崩就发生了：

![image-20210715172710340](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153643.png)



#### 1.1.2.超时处理

解决雪崩问题的常见方式有四种：

•超时处理：设定超时时间，请求超过一定时间没有响应就返回错误信息，不会无休止等待

![image-20210715172820438](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153644.png)



#### 1.1.3.仓壁模式

方案2：仓壁模式

仓壁模式来源于船舱的设计：

![image-20210715172946352](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153645.png)

船舱都会被隔板分离为多个独立空间，当船体破损时，只会导致部分空间进入，将故障控制在一定范围内，避免整个船体都被淹没。



于此类似，我们可以限定每个业务能使用的线程数，避免耗尽整个tomcat的资源，因此也叫线程隔离。

![image-20210715173215243](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153646.png)



#### 1.1.4.断路器

断路器模式：由**断路器**统计业务执行的异常比例，如果超出阈值则会**熔断**该业务，拦截访问该业务的一切请求。

断路器会统计访问某个服务的请求数量，异常比例：

![image-20210715173327075](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153647.png)

当发现访问服务D的请求异常比例过高时，认为服务D有导致雪崩的风险，会拦截访问服务D的一切请求，形成熔断：

![image-20210715173428073](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153648.png)



#### 1.1.5.限流

**流量控制**：限制业务访问的QPS，避免服务因流量的突增而故障。

![image-20210715173555158](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153649.png)







#### 1.1.6.总结

什么是雪崩问题？

- 微服务之间相互调用，因为调用链中的一个服务故障，引起整个链路都无法访问的情况。



可以认为：

**限流**是对服务的保护，避免因瞬间高并发流量而导致服务故障，进而避免雪崩。是一种**预防**措施。

**超时处理、线程隔离、降级熔断**是在部分服务故障时，将故障控制在一定范围，避免雪崩。是一种**补救**措施。





### 1.2.服务保护技术对比

在SpringCloud当中支持多种服务保护技术：

- [Netfix Hystrix](https://github.com/Netflix/Hystrix)
- [Sentinel](https://github.com/alibaba/Sentinel)
- [Resilience4J](https://github.com/resilience4j/resilience4j)

早期比较流行的是Hystrix框架，但目前国内实用最广泛的还是阿里巴巴的Sentinel框架，这里我们做下对比：

|                | **Sentinel**                                   | **Hystrix**                   |
| -------------- | ---------------------------------------------- | ----------------------------- |
| 隔离策略       | 信号量隔离                                     | 线程池隔离/信号量隔离         |
| 熔断降级策略   | 基于慢调用比例或异常比例                       | 基于失败比率                  |
| 实时指标实现   | 滑动窗口                                       | 滑动窗口（基于 RxJava）       |
| 规则配置       | 支持多种数据源                                 | 支持多种数据源                |
| 扩展性         | 多个扩展点                                     | 插件的形式                    |
| 基于注解的支持 | 支持                                           | 支持                          |
| 限流           | 基于 QPS，支持基于调用关系的限流               | 有限的支持                    |
| 流量整形       | 支持慢启动、匀速排队模式                       | 不支持                        |
| 系统自适应保护 | 支持                                           | 不支持                        |
| 控制台         | 开箱即用，可配置规则、查看秒级监控、机器发现等 | 不完善                        |
| 常见框架的适配 | Servlet、Spring Cloud、Dubbo、gRPC  等         | Servlet、Spring Cloud Netflix |







### 1.3.Sentinel介绍和安装



#### 1.3.1.初识Sentinel

Sentinel是阿里巴巴开源的一款微服务流量控制组件。官网地址：https://sentinelguard.io/zh-cn/index.html

Sentinel 具有以下特征:

•**丰富的应用场景**：Sentinel 承接了阿里巴巴近 10 年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。

•**完备的实时监控**：Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。

•**广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与 Spring Cloud、Dubbo、gRPC 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。

•**完善的** **SPI** **扩展点**：Sentinel 提供简单易用、完善的 SPI 扩展接口。您可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。



#### 1.3.2.安装Sentinel

1）下载

sentinel官方提供了UI控制台，方便我们对系统做限流设置。大家可以在[GitHub](https://github.com/alibaba/Sentinel/releases)下载。

课前资料也提供了下载好的jar包：

![image-20210715174252531](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153650.png)



2）运行

将jar包放到任意非中文目录，执行命令：

```sh
java -jar sentinel-dashboard-1.8.1.jar
```

如果要修改Sentinel的默认端口、账户、密码，可以通过下列配置：

| **配置项**                       | **默认值** | **说明**   |
| -------------------------------- | ---------- | ---------- |
| server.port                      | 8080       | 服务端口   |
| sentinel.dashboard.auth.username | sentinel   | 默认用户名 |
| sentinel.dashboard.auth.password | sentinel   | 默认密码   |

例如，修改端口：

```sh
java -Dserver.port=10011 -jar sentinel-dashboard-1.8.1.jar
```

```shell
nohup java -Dserver.port=10011 -Dcsp.sentinel.dashboard.server=localhost:10011 -Dproject.name=sentinel-dashboard -jar ./sentinel-dashboard-1.8.1.jar
```





3）访问

访问http://localhost:8080页面，就可以看到sentinel的控制台了：

![image-20210715190827846](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153651.png)

需要输入账号和密码，默认都是：sentinel



登录后，发现一片空白，什么都没有：

![image-20210715191134448](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153652.png)

这是因为我们还没有与微服务整合。





### 1.4.微服务整合Sentinel

我们在order-service中整合sentinel，并连接sentinel的控制台，步骤如下：

1）引入sentinel依赖

```xml
<!--sentinel-->
<dependency>
    <groupId>com.alibaba.cloud</groupId> 
    <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
</dependency>
```



2）配置控制台

修改application.yaml文件，添加下面内容：

```yaml
server:
  port: 8088
spring:
  cloud: 
    sentinel:
      transport:
        dashboard: localhost:8080
```



3）访问order-service的任意端点

打开浏览器，访问http://localhost:8088/order/101，这样才能触发sentinel的监控。

然后再访问sentinel的控制台，查看效果：

![image-20210715191241799](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153653.png)





## 2.流量控制

雪崩问题虽然有四种方案，但是限流是避免服务因突发的流量而发生故障，是对微服务雪崩问题的预防。我们先学习这种模式。

### 2.1.簇点链路

当请求进入微服务时，首先会访问DispatcherServlet，然后进入Controller、Service、Mapper，这样的一个调用链就叫做**簇点链路**。簇点链路中被监控的每一个接口就是一个**资源**。

默认情况下sentinel会监控SpringMVC的每一个端点（Endpoint，也就是controller中的方法），因此SpringMVC的每一个端点（Endpoint）就是调用链路中的一个资源。



例如，我们刚才访问的order-service中的OrderController中的端点：/order/{orderId}

![image-20210715191757319](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153654.png)



流控、熔断等都是针对簇点链路中的资源来设置的，因此我们可以点击对应资源后面的按钮来设置规则：

- 流控：流量控制
- 降级：降级熔断
- 热点：热点参数限流，是限流的一种
- 授权：请求的权限控制





### 2.1.快速入门



#### 2.1.1.示例

点击资源/order/{orderId}后面的流控按钮，就可以弹出表单。

![image-20210715191757319](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153654.png)

表单中可以填写限流规则，如下：

![image-20210715192010657](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153655.png)

其含义是限制 /order/{orderId}这个资源的单机QPS为1，即每秒只允许1次请求，超出的请求会被拦截并报错。



#### 2.1.2.练习：

需求：给 /order/{orderId}这个资源设置流控规则，QPS不能超过 5，然后测试。







1）首先在sentinel控制台添加限流规则

![image-20210715192455429](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153656.png)

2）利用jmeter测试

如果没有用过jmeter，可以参考课前资料提供的文档《Jmeter快速入门.md》

课前资料提供了编写好的Jmeter测试样例：

![image-20210715200431615](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153657.png)

打开jmeter，导入课前资料提供的测试样例：

![image-20210715200537171](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153658.png)

选择：

![image-20210715200635414](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153659.png)

20个用户，2秒内运行完，QPS是10，超过了5.

选中`流控入门，QPS<5`右键运行：

![image-20210715200804594](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153660.png)



> 注意，不要点击菜单中的执行按钮来运行。



结果：

![image-20210715200853671](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153661.png)

可以看到，成功的请求每次只有5个





### 2.2.流控模式

在添加限流规则时，点击高级选项，可以选择三种**流控模式**：

- 直接：统计当前资源的请求，触发阈值时对当前资源直接限流，也是默认的模式
- 关联：统计与当前资源相关的另一个资源，触发阈值时，对当前资源限流
- 链路：统计从指定链路访问到本资源的请求，触发阈值时，对指定链路限流

![image-20210715201827886](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153662.png)



快速入门测试的就是直接模式。



#### 2.2.1.关联模式

**关联模式**：统计与当前资源相关的另一个资源，触发阈值时，对当前资源限流

**配置规则**：

![image-20210715202540786](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153663.png)

**语法说明**：当/write资源访问量触发阈值时，就会对/read资源限流，避免影响/write资源。



**使用场景**：比如用户支付时需要修改订单状态，同时用户要查询订单。查询和修改操作会争抢数据库锁，产生竞争。业务需求是优先支付和更新订单的业务，因此当修改订单业务触发阈值时，需要对查询订单业务限流。



**需求说明**：

- 在OrderController新建两个端点：/order/query和/order/update，无需实现业务

- 配置流控规则，当/order/ update资源被访问的QPS超过5时，对/order/query请求限流



1）定义/order/query端点，模拟订单查询

```java
@GetMapping("/query")
public String queryOrder() {
    return "查询订单成功";
}
```

2）定义/order/update端点，模拟订单更新

```java
@GetMapping("/update")
public String updateOrder() {
    return "更新订单成功";
}
```

重启服务，查看sentinel控制台的簇点链路：

![image-20210716101805951](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153664.png)



3）配置流控规则

对哪个端点限流，就点击哪个端点后面的按钮。我们是对订单查询/order/query限流，因此点击它后面的按钮：

![image-20210716101934499](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153665.png)

在表单中填写流控规则：

![image-20210716102103814](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153666.png)



4）在Jmeter测试

选择《流控模式-关联》：

![image-20210716102416266](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153667.png)

可以看到1000个用户，100秒，因此QPS为10，超过了我们设定的阈值：5

查看http请求：

![image-20210716102532554](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153668.png)

请求的目标是/order/update，这样这个断点就会触发阈值。

但限流的目标是/order/query，我们在浏览器访问，可以发现：

![image-20210716102636030](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153669.png)

确实被限流了。



5）总结

![image-20210716103143002](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153670.png)





#### 2.2.2.链路模式

**链路模式**：只针对从指定链路访问到本资源的请求做统计，判断是否超过阈值。

**配置示例**：

例如有两条请求链路：

- /test1 --> /common

- /test2 --> /common

如果只希望统计从/test2进入到/common的请求，则可以这样配置：

![image-20210716103536346](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153671.png)

**实战案例**

需求：有查询订单和创建订单业务，两者都需要查询商品。针对从查询订单进入到查询商品的请求统计，并设置限流。

步骤：

1. 在OrderService中添加一个queryGoods方法，不用实现业务

2. 在OrderController中，改造/order/query端点，调用OrderService中的queryGoods方法

3. 在OrderController中添加一个/order/save的端点，调用OrderService的queryGoods方法

4. 给queryGoods设置限流规则，从/order/query进入queryGoods的方法限制QPS必须小于2



实现：

##### 1）添加查询商品方法

在order-service服务中，给OrderService类添加一个queryGoods方法：

```java
public void queryGoods(){
    System.err.println("查询商品");
}
```



##### 2）查询订单时，查询商品

在order-service的OrderController中，修改/order/query端点的业务逻辑：

```java
@GetMapping("/query")
public String queryOrder() {
    // 查询商品
    orderService.queryGoods();
    // 查询订单
    System.out.println("查询订单");
    return "查询订单成功";
}
```



##### 3）新增订单，查询商品

在order-service的OrderController中，修改/order/save端点，模拟新增订单：

```java
@GetMapping("/save")
public String saveOrder() {
    // 查询商品
    orderService.queryGoods();
    // 查询订单
    System.err.println("新增订单");
    return "新增订单成功";
}
```



##### 4）给查询商品添加资源标记

默认情况下，OrderService中的方法是不被Sentinel监控的，需要我们自己通过注解来标记要监控的方法。

给OrderService的queryGoods方法添加@SentinelResource注解：

```java
@SentinelResource("goods")
public void queryGoods(){
    System.err.println("查询商品");
}
```



链路模式中，是对不同来源的两个链路做监控。但是sentinel默认会给进入SpringMVC的所有请求设置同一个root资源，会导致链路模式失效。

我们需要关闭这种对SpringMVC的资源聚合，修改order-service服务的application.yml文件：

```yaml
spring:
  cloud:
    sentinel:
      web-context-unify: false ## 关闭context整合
```

重启服务，访问/order/query和/order/save，可以查看到sentinel的簇点链路规则中，出现了新的资源：

![image-20210716105227163](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153672.png)



##### 5）添加流控规则

点击goods资源后面的流控按钮，在弹出的表单中填写下面信息：

![image-20210716105408723](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153673.png)



只统计从/order/query进入/goods的资源，QPS阈值为2，超出则被限流。



##### 6）Jmeter测试

选择《流控模式-链路》：

![image-20210716105612312](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153674.png)

可以看到这里200个用户，50秒内发完，QPS为4，超过了我们设定的阈值2

一个http请求是访问/order/save：

![image-20210716105812789](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153675.png)

运行的结果：

![image-20210716110027064](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153676.png)

完全不受影响。



另一个是访问/order/query：

![image-20210716105855951](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153677.png)

运行结果：

![image-20210716105956401](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153678.png)

每次只有2个通过。



#### 2.2.3.总结

流控模式有哪些？

•直接：对当前资源限流

•关联：高优先级资源触发阈值，对低优先级资源限流。

•链路：阈值统计时，只统计从指定资源进入当前资源的请求，是对请求来源的限流



### 2.3.流控效果

在流控的高级选项中，还有一个流控效果选项：

![image-20210716110225104](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153679.png)

流控效果是指请求达到流控阈值时应该采取的措施，包括三种：

- 快速失败：达到阈值后，新的请求会被立即拒绝并抛出FlowException异常。是默认的处理方式。

- warm up：预热模式，对超出阈值的请求同样是拒绝并抛出异常。但这种模式阈值会动态变化，从一个较小值逐渐增加到最大阈值。

- 排队等待：让所有的请求按照先后次序排队执行，两个请求的间隔不能小于指定时长



#### 2.3.1.warm up

阈值一般是一个微服务能承担的最大QPS，但是一个服务刚刚启动时，一切资源尚未初始化（**冷启动**），如果直接将QPS跑到最大值，可能导致服务瞬间宕机。



warm up也叫**预热模式**，是应对服务冷启动的一种方案。请求阈值初始值是 maxThreshold / coldFactor，持续指定时长后，逐渐提高到maxThreshold值。而coldFactor的默认值是3.

例如，我设置QPS的maxThreshold为10，预热时间为5秒，那么初始阈值就是 10 / 3 ，也就是3，然后在5秒后逐渐增长到10.

![image-20210716110629796](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153680.png)



**案例**

需求：给/order/{orderId}这个资源设置限流，最大QPS为10，利用warm up效果，预热时长为5秒



##### 1）配置流控规则：

![image-20210716111012387](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153681.png)



##### 2）Jmeter测试

选择《流控效果，warm up》：

![image-20210716111136699](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153682.png)

QPS为10.

刚刚启动时，大部分请求失败，成功的只有3个，说明QPS被限定在3：

![image-20210716111303701](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153683.png)

随着时间推移，成功比例越来越高：

![image-20210716111404717](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153684.png)



到Sentinel控制台查看实时监控：

![image-20210716111526480](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153685.png)

一段时间后：

![image-20210716111658541](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153686.png)





#### 2.3.2.排队等待

当请求超过QPS阈值时，快速失败和warm up 会拒绝新的请求并抛出异常。

而排队等待则是让所有请求进入一个队列中，然后按照阈值允许的时间间隔依次执行。后来的请求必须等待前面执行完成，如果请求预期的等待时间超出最大时长，则会被拒绝。

工作原理

例如：QPS = 5，意味着每200ms处理一个队列中的请求；timeout = 2000，意味着**预期等待时长**超过2000ms的请求会被拒绝并抛出异常。

那什么叫做预期等待时长呢？

比如现在一下子来了12 个请求，因为每200ms执行一个请求，那么：

- 第6个请求的**预期等待时长** =  200 * （6 - 1） = 1000ms
- 第12个请求的预期等待时长 = 200 * （12-1） = 2200ms



现在，第1秒同时接收到10个请求，但第2秒只有1个请求，此时QPS的曲线这样的：

![image-20210716113147176](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153687.png)

如果使用队列模式做流控，所有进入的请求都要排队，以固定的200ms的间隔执行，QPS会变的很平滑：

![image-20210716113426524](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153688.png)



平滑的QPS曲线，对于服务器来说是更友好的。



**案例**

需求：给/order/{orderId}这个资源设置限流，最大QPS为10，利用排队的流控效果，超时时长设置为5s



##### 1）添加流控规则

![image-20210716114048918](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153689.png)



##### 2）Jmeter测试

选择《流控效果，队列》：

![image-20210716114243558](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153690.png)

QPS为15，已经超过了我们设定的10。

如果是之前的 快速失败、warmup模式，超出的请求应该会直接报错。

但是我们看看队列模式的运行结果：

![image-20210716114429361](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153691.png)

全部都通过了。

再去sentinel查看实时监控的QPS曲线：

![image-20210716114522935](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153692.png)

QPS非常平滑，一致保持在10，但是超出的请求没有被拒绝，而是放入队列。因此**响应时间**（等待时间）会越来越长。

当队列满了以后，才会有部分请求失败：

![image-20210716114651137](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153693.png)





#### 2.3.3.总结

流控效果有哪些？

- 快速失败：QPS超过阈值时，拒绝新的请求

- warm up： QPS超过阈值时，拒绝新的请求；QPS阈值是逐渐提升的，可以避免冷启动时高并发导致服务宕机。

- 排队等待：请求会进入队列，按照阈值允许的时间间隔依次执行请求；如果请求预期等待时长大于超时时间，直接拒绝





### 2.4.热点参数限流

之前的限流是统计访问某个资源的所有请求，判断是否超过QPS阈值。而热点参数限流是**分别统计参数值相同的请求**，判断是否超过QPS阈值。

#### 2.4.1.全局参数限流

例如，一个根据id查询商品的接口：

![image-20210716115014663](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153694.png)

访问/goods/{id}的请求中，id参数值会有变化，热点参数限流会根据参数值分别统计QPS，统计结果：

![image-20210716115131463](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153695.png)

当id=1的请求触发阈值被限流时，id值不为1的请求不受影响。



配置示例：

![image-20210716115232426](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153696.png)

代表的含义是：对hot这个资源的0号参数（第一个参数）做统计，每1秒**相同参数值**的请求数不能超过5



#### 2.4.2.热点参数限流

刚才的配置中，对查询商品这个接口的所有商品一视同仁，QPS都限定为5.

而在实际开发中，可能部分商品是热点商品，例如秒杀商品，我们希望这部分商品的QPS限制与其它商品不一样，高一些。那就需要配置热点参数限流的高级选项了：

![image-20210716115717523](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153697.png)

结合上一个配置，这里的含义是对0号的long类型参数限流，每1秒相同参数的QPS不能超过5，有两个例外：

•如果参数值是100，则每1秒允许的QPS为10

•如果参数值是101，则每1秒允许的QPS为15



#### 2.4.4.案例

**案例需求**：给/order/{orderId}这个资源添加热点参数限流，规则如下：

•默认的热点参数规则是每1秒请求量不超过2

•给102这个参数设置例外：每1秒请求量不超过4

•给103这个参数设置例外：每1秒请求量不超过10



**注意事项**：热点参数限流对默认的SpringMVC资源无效，需要利用@SentinelResource注解标记资源



##### 1）标记资源

给order-service中的OrderController中的/order/{orderId}资源添加注解：

![image-20210716120033572](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153699.png)



##### 2）热点参数限流规则

访问该接口，可以看到我们标记的hot资源出现了：

![image-20210716120208509](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153700.png)

这里不要点击hot后面的按钮，页面有BUG



点击左侧菜单中**热点规则**菜单：

![image-20210716120319009](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153701.png)

点击新增，填写表单：

![image-20210716120536714](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153702.png)



##### 3）Jmeter测试

选择《热点参数限流 QPS1》：

![image-20210716120754527](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153703.png)

这里发起请求的QPS为5.

包含3个http请求：

普通参数，QPS阈值为2

![image-20210716120840501](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153704.png)

运行结果：

![image-20210716121105567](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153705.png)



例外项，QPS阈值为4

![image-20210716120900365](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153706.png)

运行结果：

![image-20210716121201630](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153707.png)



例外项，QPS阈值为10

![image-20210716120919131](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153708.png)

运行结果：

![image-20210716121220305](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153709.png)



## 3.隔离和降级

限流是一种预防措施，虽然限流可以尽量避免因高并发而引起的服务故障，但服务还会因为其它原因而故障。

而要将这些故障控制在一定范围，避免雪崩，就要靠**线程隔离**（舱壁模式）和**熔断降级**手段了。



**线程隔离**之前讲到过：调用者在调用服务提供者时，给每个调用的请求分配独立线程池，出现故障时，最多消耗这个线程池内资源，避免把调用者的所有资源耗尽。

![image-20210715173215243](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153646.png)



**熔断降级**：是在调用方这边加入断路器，统计对服务提供者的调用，如果调用的失败比例过高，则熔断该业务，不允许访问该服务的提供者了。

![image-20210715173428073](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153648.png)





可以看到，不管是线程隔离还是熔断降级，都是对**客户端**（调用方）的保护。需要在**调用方** 发起远程调用时做线程隔离、或者服务熔断。

而我们的微服务远程调用都是基于Feign来完成的，因此我们需要将Feign与Sentinel整合，在Feign里面实现线程隔离和服务熔断。



### 3.1.FeignClient整合Sentinel

SpringCloud中，微服务调用都是通过Feign来实现的，因此做客户端保护必须整合Feign和Sentinel。



#### 3.1.1.修改配置，开启sentinel功能

修改OrderService的application.yml文件，开启Feign的Sentinel功能：

```yaml
feign:
  sentinel:
    enabled: true ## 开启feign对sentinel的支持
```



#### 3.1.2.编写失败降级逻辑

业务失败后，不能直接报错，而应该返回用户一个友好提示或者默认结果，这个就是失败降级逻辑。

给FeignClient编写失败后的降级逻辑

①方式一：FallbackClass，无法对远程调用的异常做处理

②方式二：FallbackFactory，可以对远程调用的异常做处理，我们选择这种



这里我们演示方式二的失败降级处理。

**步骤一**：在feing-api项目中定义类，实现FallbackFactory：

![image-20210716122403502](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153710.png)

代码：

```java
package cn.itcast.feign.clients.fallback;

import cn.itcast.feign.clients.UserClient;
import cn.itcast.feign.pojo.User;
import feign.hystrix.FallbackFactory;
import lombok.extern.slf4j.Slf4j;

@Slf4j
public class UserClientFallbackFactory implements FallbackFactory<UserClient> {
    @Override
    public UserClient create(Throwable throwable) {
        return new UserClient() {
            @Override
            public User findById(Long id) {
                log.error("查询用户异常", throwable);
                return new User();
            }
        };
    }
}

```



**步骤二**：在feing-api项目中的DefaultFeignConfiguration类中将UserClientFallbackFactory注册为一个Bean：

```java
@Bean
public UserClientFallbackFactory userClientFallbackFactory(){
    return new UserClientFallbackFactory();
}
```

**步骤三**：在feing-api项目中的UserClient接口中使用UserClientFallbackFactory：

```java
import cn.itcast.feign.clients.fallback.UserClientFallbackFactory;
import cn.itcast.feign.pojo.User;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

@FeignClient(value = "userservice", fallbackFactory = UserClientFallbackFactory.class)
public interface UserClient {

    @GetMapping("/user/{id}")
    User findById(@PathVariable("id") Long id);
}
```



重启后，访问一次订单查询业务，然后查看sentinel控制台，可以看到新的簇点链路：

![image-20210716123705780](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153711.png)





#### 3.1.3.总结

Sentinel支持的雪崩解决方案：

- 线程隔离（仓壁模式）
- 降级熔断

Feign整合Sentinel的步骤：

- 在application.yml中配置：feign.sentienl.enable=true
- 给FeignClient编写FallbackFactory并注册为Bean
- 将FallbackFactory配置到FeignClient







### 3.2.线程隔离（舱壁模式）



#### 3.2.1.线程隔离的实现方式

线程隔离有两种方式实现：

- 线程池隔离

- 信号量隔离（Sentinel默认采用）

如图：

![image-20210716123036937](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153712.png)



**线程池隔离**：给每个服务调用业务分配一个线程池，利用线程池本身实现隔离效果

**信号量隔离**：不创建线程池，而是计数器模式，记录业务使用的线程数量，达到信号量上限时，禁止新的请求。



两者的优缺点：

![image-20210716123240518](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153713.png)





#### 3.2.2.sentinel的线程隔离

**用法说明**：

在添加限流规则时，可以选择两种阈值类型：

![image-20210716123411217](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153714.png)

- QPS：就是每秒的请求数，在快速入门中已经演示过

- 线程数：是该资源能使用用的tomcat线程数的最大值。也就是通过限制线程数量，实现**线程隔离**（舱壁模式）。



**案例需求**：给 order-service服务中的UserClient的查询用户接口设置流控规则，线程数不能超过 2。然后利用jemeter测试。



##### 1）配置隔离规则

选择feign接口后面的流控按钮：

![image-20210716123831992](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153715.png)

填写表单：

![image-20210716123936844](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153716.png)



##### 2）Jmeter测试

选择《阈值类型-线程数<2》：

![image-20210716124229894](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153717.png)

一次发生10个请求，有较大概率并发线程数超过2，而超出的请求会走之前定义的失败降级逻辑。



查看运行结果：

![image-20210716124147820](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153718.png)

发现虽然结果都是通过了，不过部分请求得到的响应是降级返回的null信息。





#### 3.2.3.总结

线程隔离的两种手段是？

- 信号量隔离

- 线程池隔离

信号量隔离的特点是？

- 基于计数器模式，简单，开销小

线程池隔离的特点是？

- 基于线程池模式，有额外开销，但隔离控制更强





### 3.3.熔断降级

熔断降级是解决雪崩问题的重要手段。其思路是由**断路器**统计服务调用的异常比例、慢请求比例，如果超出阈值则会**熔断**该服务。即拦截访问该服务的一切请求；而当服务恢复时，断路器会放行访问该服务的请求。

断路器控制熔断和放行是通过状态机来完成的：

![image-20210716130958518](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153719.png)

状态机包括三个状态：

- closed：关闭状态，断路器放行所有请求，并开始统计异常比例、慢请求比例。超过阈值则切换到open状态
- open：打开状态，服务调用被**熔断**，访问被熔断服务的请求会被拒绝，快速失败，直接走降级逻辑。Open状态5秒后会进入half-open状态
- half-open：半开状态，放行一次请求，根据执行结果来判断接下来的操作。
  - 请求成功：则切换到closed状态
  - 请求失败：则切换到open状态



断路器熔断策略有三种：慢调用、异常比例、异常数



#### 3.3.1.慢调用

**慢调用**：业务的响应时长（RT）大于指定时长的请求认定为慢调用请求。在指定时间内，如果请求数量超过设定的最小数量，慢调用比例大于设定的阈值，则触发熔断。

例如：

![image-20210716145934347](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153720.png)

解读：RT超过500ms的调用是慢调用，统计最近10000ms内的请求，如果请求量超过10次，并且慢调用比例不低于0.5，则触发熔断，熔断时长为5秒。然后进入half-open状态，放行一次请求做测试。



**案例**

需求：给 UserClient的查询用户接口设置降级规则，慢调用的RT阈值为50ms，统计时间为1秒，最小请求数量为5，失败阈值比例为0.4，熔断时长为5



##### 1）设置慢调用

修改user-service中的/user/{id}这个接口的业务。通过休眠模拟一个延迟时间：

![image-20210716150234787](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153721.png)



此时，orderId=101的订单，关联的是id为1的用户，调用时长为60ms：

![image-20210716150510956](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153722.png)

orderId=102的订单，关联的是id为2的用户，调用时长为非常短；

![image-20210716150605208](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153723.png)



##### 2）设置熔断规则

下面，给feign接口设置降级规则：

![image-20210716150654094](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153724.png)

规则：

![image-20210716150740434](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153725.png)

超过50ms的请求都会被认为是慢请求



##### 3）测试

在浏览器访问：http://localhost:8088/order/101，快速刷新5次，可以发现：

![image-20210716150911004](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153726.png)

触发了熔断，请求时长缩短至5ms，快速失败了，并且走降级逻辑，返回的null



在浏览器访问：http://localhost:8088/order/102，竟然也被熔断了：

![image-20210716151107785](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153727.png)





#### 3.3.2.异常比例、异常数

**异常比例或异常数**：统计指定时间内的调用，如果调用次数超过指定请求数，并且出现异常的比例达到设定的比例阈值（或超过指定异常数），则触发熔断。

例如，一个异常比例设置：

![image-20210716131430682](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153728.png)

解读：统计最近1000ms内的请求，如果请求量超过10次，并且异常比例不低于0.4，则触发熔断。

一个异常数设置：

![image-20210716131522912](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153729.png)

解读：统计最近1000ms内的请求，如果请求量超过10次，并且异常比例不低于2次，则触发熔断。



**案例**

需求：给 UserClient的查询用户接口设置降级规则，统计时间为1秒，最小请求数量为5，失败阈值比例为0.4，熔断时长为5s



##### 1）设置异常请求

首先，修改user-service中的/user/{id}这个接口的业务。手动抛出异常，以触发异常比例的熔断：

![image-20210716151348183](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153730.png)

也就是说，id 为 2时，就会触发异常



##### 2）设置熔断规则

下面，给feign接口设置降级规则：

![image-20210716150654094](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153724.png)

规则：

![image-20210716151538785](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153731.png)

在5次请求中，只要异常比例超过0.4，也就是有2次以上的异常，就会触发熔断。



#####  3）测试

在浏览器快速访问：http://localhost:8088/order/102，快速刷新5次，触发熔断：

![image-20210716151722916](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153732.png)



此时，我们去访问本来应该正常的103：

![image-20210716151844817](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153733.png)





## 4.授权规则

授权规则可以对请求方来源做判断和控制。

### 4.1.授权规则

#### 4.1.1.基本规则

授权规则可以对调用方的来源做控制，有白名单和黑名单两种方式。

- 白名单：来源（origin）在白名单内的调用者允许访问

- 黑名单：来源（origin）在黑名单内的调用者不允许访问

点击左侧菜单的授权，可以看到授权规则：

![image-20210716152010750](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153734.png)

- 资源名：就是受保护的资源，例如/order/{orderId}

- 流控应用：是来源者的名单，                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
  - 如果是勾选白名单，则名单中的来源被许可访问。
  - 如果是勾选黑名单，则名单中的来源被禁止访问。

比如：

![image-20210716152349191](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153735.png)

我们允许请求从gateway到order-service，不允许浏览器访问order-service，那么白名单中就要填写**网关的来源名称（origin）**。

#### 4.1.2.如何获取origin

Sentinel是通过RequestOriginParser这个接口的parseOrigin来获取请求的来源的。

```java
public interface RequestOriginParser {
    /**
     * 从请求request对象中获取origin，获取方式自定义
     */
    String parseOrigin(HttpServletRequest request);
}
```

这个方法的作用就是从request对象中，获取请求者的origin值并返回。

默认情况下，sentinel不管请求者从哪里来，返回值永远是default，也就是说一切请求的来源都被认为是一样的值default。



因此，我们需要自定义这个接口的实现，让**不同的请求，返回不同的origin**。



例如order-service服务中，我们定义一个RequestOriginParser的实现类：

```java
package cn.itcast.order.sentinel;

import com.alibaba.csp.sentinel.adapter.spring.webmvc.callback.RequestOriginParser;
import org.springframework.stereotype.Component;
import org.springframework.util.StringUtils;

import javax.servlet.http.HttpServletRequest;

@Component
public class HeaderOriginParser implements RequestOriginParser {
    @Override
    public String parseOrigin(HttpServletRequest request) {
        // 1.获取请求头
        String origin = request.getHeader("origin");
        // 2.非空判断
        if (StringUtils.isEmpty(origin)) {
            origin = "blank";
        }
        return origin;
    }
}
```

我们会尝试从request-header中获取origin值。



#### 4.1.3.给网关添加请求头

既然获取请求origin的方式是从reques-header中获取origin值，我们必须让**所有从gateway路由到微服务的请求都带上origin头**。

这个需要利用之前学习的一个GatewayFilter来实现，AddRequestHeaderGatewayFilter。

修改gateway服务中的application.yml，添加一个defaultFilter：

```yaml
spring:
  cloud:
    gateway:
      default-filters:
        - AddRequestHeader=origin,gateway
      routes:
       ## ...略
```

这样，从gateway路由的所有请求都会带上origin头，值为gateway。而从其它地方到达微服务的请求则没有这个头。



#### 4.1.4.配置授权规则

接下来，我们添加一个授权规则，放行origin值为gateway的请求。

![image-20210716153250134](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153736.png)

配置如下：

![image-20210716153301069](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153737.png)

现在，我们直接跳过网关，访问order-service服务：

![image-20210716153348396](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153738.png)

通过网关访问：

![image-20210716153434095](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153739.png)







### 4.2.自定义异常结果

默认情况下，发生限流、降级、授权拦截时，都会抛出异常到调用方。异常结果都是flow limmiting（限流）。这样不够友好，无法得知是限流还是降级还是授权拦截。



#### 4.2.1.异常类型



而如果要自定义异常时的返回结果，需要实现BlockExceptionHandler接口：

```java
public interface BlockExceptionHandler {
    /**
     * 处理请求被限流、降级、授权拦截时抛出的异常：BlockException
     */
    void handle(HttpServletRequest request, HttpServletResponse response, BlockException e) throws Exception;
}
```

这个方法有三个参数：

- HttpServletRequest request：request对象
- HttpServletResponse response：response对象
- BlockException e：被sentinel拦截时抛出的异常

这里的BlockException包含多个不同的子类：

| **异常**             | **说明**           |
| -------------------- | ------------------ |
| FlowException        | 限流异常           |
| ParamFlowException   | 热点参数限流的异常 |
| DegradeException     | 降级异常           |
| AuthorityException   | 授权规则异常       |
| SystemBlockException | 系统规则异常       |



#### 4.2.2.自定义异常处理

下面，我们就在order-service定义一个自定义异常处理类：

```java
package cn.itcast.order.sentinel;

import com.alibaba.csp.sentinel.adapter.spring.webmvc.callback.BlockExceptionHandler;
import com.alibaba.csp.sentinel.slots.block.BlockException;
import com.alibaba.csp.sentinel.slots.block.authority.AuthorityException;
import com.alibaba.csp.sentinel.slots.block.degrade.DegradeException;
import com.alibaba.csp.sentinel.slots.block.flow.FlowException;
import com.alibaba.csp.sentinel.slots.block.flow.param.ParamFlowException;
import org.springframework.stereotype.Component;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@Component
    public class SentinelExceptionHandler implements BlockExceptionHandler {
    @Override
    public void handle(HttpServletRequest request, HttpServletResponse response, BlockException e) throws Exception {
        String msg = "未知异常";
        int status = 429;

        if (e instanceof FlowException) {
            msg = "请求被限流了";
        } else if (e instanceof ParamFlowException) {
            msg = "请求被热点参数限流";
        } else if (e instanceof DegradeException) {
            msg = "请求被降级了";
        } else if (e instanceof AuthorityException) {
            msg = "没有权限访问";
            status = 401;
        }

        response.setContentType("application/json;charset=utf-8");
        response.setStatus(status);
        response.getWriter().println("{\"msg\": " + msg + ", \"status\": " + status + "}");
    }
}
```



重启测试，在不同场景下，会返回不同的异常消息.

限流：

![image-20210716153938887](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153740.png)

授权拦截时：

![image-20210716154012736](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153741.png)





## 5.规则持久化

现在，sentinel的所有规则都是内存存储，重启后所有规则都会丢失。在生产环境下，我们必须确保这些规则的持久化，避免丢失。

### 5.1.规则管理模式

规则是否能持久化，取决于规则管理模式，sentinel支持三种规则管理模式：

- 原始模式：Sentinel的默认模式，将规则保存在内存，重启服务会丢失。
- pull模式
- push模式



#### 5.1.1.pull模式

pull模式：控制台将配置的规则推送到Sentinel客户端，而客户端会将配置规则保存在本地文件或数据库中。以后会定时去本地文件或数据库中查询，更新本地规则。

![image-20210716154155238](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153742.png)



#### 5.1.2.push模式

push模式：控制台将配置规则推送到远程配置中心，例如Nacos。Sentinel客户端监听Nacos，获取配置变更的推送消息，完成本地配置更新。

![image-20210716154215456](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153743.png)







### 5.2.实现push模式

详细步骤可以参考课前资料的《sentinel规则持久化》：

![image-20220811181137241](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153744.png)











# Sentinel 规则持久化







### 一、修改order-service服务



修改OrderService，让其监听Nacos中的sentinel规则配置。

具体步骤如下：

#### 1.引入依赖

在order-service中引入sentinel监听nacos的依赖：

```xml
<!--sentinel监听nacos-->
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>
```



#### 2.配置nacos地址

在order-service中的application.yml文件配置nacos地址及监听的配置信息：

```yaml
spring:
  cloud:
    sentinel:
      datasource:
        flow:
          nacos:
            server-addr: localhost:8848 ## nacos地址
            dataId: orderservice-flow-rules
            groupId: SENTINEL_GROUP
            rule-type: flow ## 还可以是：degrade、authority、param-flow
```





### 二、修改sentinel-dashboard源码

SentinelDashboard默认不支持nacos的持久化，需要修改源码。



#### 1. 解压

解压课前资料中的sentinel源码包：

![image-20210618201340086](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153745.png)

然后并用IDEA打开这个项目，结构如下：

![image-20210618201412878](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153746.png)

#### 2. 修改nacos依赖

在sentinel-dashboard源码的pom文件中，nacos的依赖默认的scope是test，只能在测试时使用，这里要去除：

![image-20210618201607831](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153747.png)

将sentinel-datasource-nacos依赖的scope去掉：

```xml
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>
```



#### 3. 添加nacos支持

在sentinel-dashboard的test包下，已经编写了对nacos的支持，我们需要将其拷贝到main下。

![image-20210618201726280](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153748.png)



#### 4. 修改nacos地址

然后，还需要修改测试代码中的NacosConfig类：

![image-20210618201912078](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153749.png)

修改其中的nacos地址，让其读取application.properties中的配置：

![image-20210618202047575](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153750.png)

在sentinel-dashboard的application.properties中添加nacos地址配置：

```properties
nacos.addr=localhost:8848
```



#### 5. 配置nacos数据源

另外，还需要修改com.alibaba.csp.sentinel.dashboard.controller.v2包下的FlowControllerV2类：

![image-20210618202322301](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153751.png)

让我们添加的Nacos数据源生效：

![image-20210618202334536](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153752.png)



#### 6. 修改前端页面

接下来，还要修改前端页面，添加一个支持nacos的菜单。

修改src/main/webapp/resources/app/scripts/directives/sidebar/目录下的sidebar.html文件：

![image-20210618202433356](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153753.png)



将其中的这部分注释打开：

![image-20210618202449881](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153754.png)



修改其中的文本：

![image-20210618202501928](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153755.png)



#### 7. 重新编译、打包项目

运行IDEA中的maven插件，编译和打包修改好的Sentinel-Dashboard：

![image-20210618202701492](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153756.png)



#### 8.启动

启动方式跟官方一样：

```sh
java -jar sentinel-dashboard.jar
```

如果要修改nacos地址，需要添加参数：

```sh
java -jar -Dnacos.addr=localhost:8848 sentinel-dashboard.jar
```





# 分布式事务





## 0.学习目标





## 1.分布式事务问题



### 1.1.本地事务

本地事务，也就是传统的**单机事务**。在传统数据库事务中，必须要满足四个原则：

![image-20210724165045186](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153757.png)



### 1.2.分布式事务

**分布式事务**，就是指不是在单个服务或单个数据库架构下，产生的事务，例如：

- 跨数据源的分布式事务
- 跨服务的分布式事务
- 综合情况



在数据库水平拆分、服务垂直拆分之后，一个业务操作通常要跨多个数据库、服务才能完成。例如电商行业中比较常见的下单付款案例，包括下面几个行为：

- 创建新订单
- 扣减商品库存
- 从用户账户余额扣除金额



完成上面的操作需要访问三个不同的微服务和三个不同的数据库。

![image-20210724165338958](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153758.png)



订单的创建、库存的扣减、账户扣款在每一个服务和数据库内是一个本地事务，可以保证ACID原则。

但是当我们把三件事情看做一个"业务"，要满足保证“业务”的原子性，要么所有操作全部成功，要么全部失败，不允许出现部分成功部分失败的现象，这就是**分布式系统下的事务**了。

此时ACID难以满足，这是分布式事务要解决的问题



### 1.3.演示分布式事务问题

我们通过一个案例来演示分布式事务的问题：

1）**创建数据库，名为seata_demo，然后导入课前资料提供的SQL文件：**

![image-20210724165634571](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153759.png) 

2）**导入课前资料提供的微服务：**

![image-20210724165709994](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153760.png) 

微服务结构如下：

![image-20210724165729273](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153762.png) 

其中：

seata-demo：父工程，负责管理项目依赖

- account-service：账户服务，负责管理用户的资金账户。提供扣减余额的接口
- storage-service：库存服务，负责管理商品库存。提供扣减库存的接口
- order-service：订单服务，负责管理订单。创建订单时，需要调用account-service和storage-service



**3）启动nacos、所有微服务**

**4）测试下单功能，发出Post请求：**

请求如下：

```sh
curl --location --request POST 'http://localhost:8082/order?userId=user202103032042012&commodityCode=100202003032041&count=20&money=200'
```

如图：

![image-20210724170113404](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153763.png)



测试发现，当库存不足时，如果余额已经扣减，并不会回滚，出现了分布式事务问题。



## 2.理论基础

解决分布式事务问题，需要一些分布式系统的基础知识作为理论指导。

### 2.1.CAP定理

1998年，加州大学的计算机科学家 Eric Brewer 提出，分布式系统有三个指标。

> - Consistency（一致性）
> - Availability（可用性）
> - Partition tolerance （分区容错性）

![image-20210724170517944](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153764.png)



它们的第一个字母分别是 C、A、P。

Eric Brewer 说，这三个指标不可能同时做到。这个结论就叫做 CAP 定理。



#### 2.1.1.一致性

Consistency（一致性）：用户访问分布式系统中的任意节点，得到的数据必须一致。

比如现在包含两个节点，其中的初始数据是一致的：

![image-20210724170704694](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153765.png)

当我们修改其中一个节点的数据时，两者的数据产生了差异：

![image-20210724170735847](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153766.png)

要想保住一致性，就必须实现node01 到 node02的数据 同步：

![image-20210724170834855](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153767.png)



#### 2.1.2.可用性

Availability （可用性）：用户访问集群中的任意健康节点，必须能得到响应，而不是超时或拒绝。

如图，有三个节点的集群，访问任何一个都可以及时得到响应：

![image-20210724170932072](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153768.png)

当有部分节点因为网络故障或其它原因无法访问时，代表节点不可用：

![image-20210724171007516](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153769.png)



#### 2.1.3.分区容错

**Partition（分区）**：因为网络故障或其它原因导致分布式系统中的部分节点与其它节点失去连接，形成独立分区。

![image-20210724171041210](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153770.png)



**Tolerance（容错）**：在集群出现分区时，整个系统也要持续对外提供服务



#### 2.1.4.矛盾

在分布式系统中，系统间的网络不能100%保证健康，一定会有故障的时候，而服务有必须对外保证服务。因此Partition Tolerance不可避免。

当节点接收到新的数据变更时，就会出现问题了：

![image-20210724171546472](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153771.png)

如果此时要保证**一致性**，就必须等待网络恢复，完成数据同步后，整个集群才对外提供服务，服务处于阻塞状态，不可用。

如果此时要保证**可用性**，就不能等待网络恢复，那node01、node02与node03之间就会出现数据不一致。



也就是说，在P一定会出现的情况下，A和C之间只能实现一个。



### 2.2.BASE理论

BASE理论是对CAP的一种解决思路，包含三个思想：

- **Basically Available** **（基本可用）**：分布式系统在出现故障时，允许损失部分可用性，即保证核心可用。
- **Soft State（软状态）：**在一定时间内，允许出现中间状态，比如临时的不一致状态。
- **Eventually Consistent（最终一致性）**：虽然无法保证强一致性，但是在软状态结束后，最终达到数据一致。



### 2.3.解决分布式事务的思路

分布式事务最大的问题是各个子事务的一致性问题，因此可以借鉴CAP定理和BASE理论，有两种解决思路：

- AP模式：各子事务分别执行和提交，允许出现结果不一致，然后采用弥补措施恢复数据即可，实现最终一致。

- CP模式：各个子事务执行后互相等待，同时提交，同时回滚，达成强一致。但事务等待过程中，处于弱可用状态。



但不管是哪一种模式，都需要在子系统事务之间互相通讯，协调事务状态，也就是需要一个**事务协调者(TC)**：

![image-20210724172123567](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153772.png)



这里的子系统事务，称为**分支事务**；有关联的各个分支事务在一起称为**全局事务**。



## 3.初识Seata

Seata是 2019 年 1 月份蚂蚁金服和阿里巴巴共同开源的分布式事务解决方案。致力于提供高性能和简单易用的分布式事务服务，为用户打造一站式的分布式解决方案。

官网地址：http://seata.io/，其中的文档、播客中提供了大量的使用说明、源码分析。

![image-20210724172225817](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153773.png)



### 3.1.Seata的架构

Seata事务管理中有三个重要的角色：

- **TC (Transaction Coordinator) -** **事务协调者：**维护全局和分支事务的状态，协调全局事务提交或回滚。

- **TM (Transaction Manager) -** **事务管理器：**定义全局事务的范围、开始全局事务、提交或回滚全局事务。

- **RM (Resource Manager) -** **资源管理器：**管理分支事务处理的资源，与TC交谈以注册分支事务和报告分支事务的状态，并驱动分支事务提交或回滚。



整体的架构如图：

![image-20210724172326452](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153774.png)



Seata基于上述架构提供了四种不同的分布式事务解决方案：

- XA模式：强一致性分阶段事务模式，牺牲了一定的可用性，无业务侵入
- TCC模式：最终一致的分阶段事务模式，有业务侵入
- AT模式：最终一致的分阶段事务模式，无业务侵入，也是Seata的默认模式
- SAGA模式：长事务模式，有业务侵入

无论哪种方案，都离不开TC，也就是事务的协调者。



### 3.2.部署TC服务

参考课前资料提供的文档《 seata的部署和集成.md 》：

![image-20210724172549013](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153775.png)



### 3.3.微服务集成Seata

我们以order-service为例来演示。

#### 3.3.1.引入依赖

首先，在order-service中引入依赖：

```xml
<!--seata-->
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
    <exclusions>
        <!--版本较低，1.3.0，因此排除--> 
        <exclusion>
            <artifactId>seata-spring-boot-starter</artifactId>
            <groupId>io.seata</groupId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>io.seata</groupId>
    <artifactId>seata-spring-boot-starter</artifactId>
    <!--seata starter 采用1.4.2版本-->
    <version>${seata.version}</version>
</dependency>
```



#### 3.3.2.配置TC地址

在order-service中的application.yml中，配置TC服务信息，通过注册中心nacos，结合服务名称获取TC地址：

```yaml
seata:
  registry: ## TC服务注册中心的配置，微服务根据这些信息去注册中心获取tc服务地址
    type: nacos ## 注册中心类型 nacos
    nacos:
      server-addr: 127.0.0.1:8848 ## nacos地址
      namespace: "" ## namespace，默认为空
      group: DEFAULT_GROUP ## 分组，默认是DEFAULT_GROUP
      application: seata-tc-server ## seata服务名称
      username: nacos
      password: nacos
  tx-service-group: seata-demo ## 事务组名称
  service:
    vgroup-mapping: ## 事务组与cluster的映射关系
      seata-demo: SH
```



微服务如何根据这些配置寻找TC的地址呢？

我们知道注册到Nacos中的微服务，确定一个具体实例需要四个信息：

- namespace：命名空间
- group：分组
- application：服务名
- cluster：集群名



以上四个信息，在刚才的yaml文件中都能找到：

![image-20210724173654258](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153776.png)

namespace为空，就是默认的public

结合起来，TC服务的信息就是：public@DEFAULT_GROUP@seata-tc-server@SH，这样就能确定TC服务集群了。然后就可以去Nacos拉取对应的实例信息了。





#### 3.3.3.其它服务

其它两个微服务也都参考order-service的步骤来做，完全一样。



## 4.动手实践

下面我们就一起学习下Seata中的四种不同的事务模式。



### 4.1.XA模式

XA 规范 是 X/Open 组织定义的分布式事务处理（DTP，Distributed Transaction Processing）标准，XA 规范 描述了全局的TM与局部的RM之间的接口，几乎所有主流的数据库都对 XA 规范 提供了支持。



#### 4.1.1.两阶段提交

XA是规范，目前主流数据库都实现了这种规范，实现的原理都是基于两阶段提交。

正常情况：

![image-20210724174102768](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153777.png)

异常情况：

![image-20210724174234987](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153778.png)



一阶段：

- 事务协调者通知每个事物参与者执行本地事务
- 本地事务执行完成后报告事务执行状态给事务协调者，此时事务不提交，继续持有数据库锁

二阶段：

- 事务协调者基于一阶段的报告来判断下一步操作
  - 如果一阶段都成功，则通知所有事务参与者，提交事务
  - 如果一阶段任意一个参与者失败，则通知所有事务参与者回滚事务



#### 4.1.2.Seata的XA模型

Seata对原始的XA模式做了简单的封装和改造，以适应自己的事务模型，基本架构如图：

![image-20210724174424070](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153779.png)



RM一阶段的工作：

​	① 注册分支事务到TC

​	② 执行分支业务sql但不提交

​	③ 报告执行状态到TC

TC二阶段的工作：

- TC检测各分支事务执行状态

  a.如果都成功，通知所有RM提交事务

  b.如果有失败，通知所有RM回滚事务

RM二阶段的工作：

- 接收TC指令，提交或回滚事务





#### 4.1.3.优缺点

XA模式的优点是什么？

- 事务的强一致性，满足ACID原则。
- 常用数据库都支持，实现简单，并且没有代码侵入

XA模式的缺点是什么？

- 因为一阶段需要锁定数据库资源，等待二阶段结束才释放，性能较差
- 依赖关系型数据库实现事务



#### 4.1.4.实现XA模式

Seata的starter已经完成了XA模式的自动装配，实现非常简单，步骤如下：

1）修改application.yml文件（每个参与事务的微服务），开启XA模式：

```yaml
seata:
  data-source-proxy-mode: XA
```



2）给发起全局事务的入口方法添加@GlobalTransactional注解:

本例中是OrderServiceImpl中的create方法.

![image-20210724174859556](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153780.png)



3）重启服务并测试

重启order-service，再次测试，发现无论怎样，三个微服务都能成功回滚。







### 4.2.AT模式

AT模式同样是分阶段提交的事务模型，不过缺弥补了XA模型中资源锁定周期过长的缺陷。

#### 4.2.1.Seata的AT模型

基本流程图：

![image-20210724175327511](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153781.png)



阶段一RM的工作：

- 注册分支事务
- 记录undo-log（数据快照）
- 执行业务sql并提交
- 报告事务状态

阶段二提交时RM的工作：

- 删除undo-log即可

阶段二回滚时RM的工作：

- 根据undo-log恢复数据到更新前



#### 4.2.2.流程梳理

我们用一个真实的业务来梳理下AT模式的原理。

比如，现在又一个数据库表，记录用户余额：

| **id** | **money** |
| ------ | --------- |
| 1      | 100       |

其中一个分支业务要执行的SQL为：

```sql
update tb_account set money = money - 10 where id = 1
```



AT模式下，当前分支事务执行流程如下：

一阶段：

1）TM发起并注册全局事务到TC

2）TM调用分支事务

3）分支事务准备执行业务SQL

4）RM拦截业务SQL，根据where条件查询原始数据，形成快照。

```json
{
    "id": 1, "money": 100
}
```

5）RM执行业务SQL，提交本地事务，释放数据库锁。此时 `money = 90`

6）RM报告本地事务状态给TC



二阶段：

1）TM通知TC事务结束

2）TC检查分支事务状态

​	 a）如果都成功，则立即删除快照

​	 b）如果有分支事务失败，需要回滚。读取快照数据（`{"id": 1, "money": 100}`），将快照恢复到数据库。此时数据库再次恢复为100





流程图：

![image-20210724180722921](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153782.png)



#### 4.2.3.AT与XA的区别

简述AT模式与XA模式最大的区别是什么？

- XA模式一阶段不提交事务，锁定资源；AT模式一阶段直接提交，不锁定资源。
- XA模式依赖数据库机制实现回滚；AT模式利用数据快照实现数据回滚。
- XA模式强一致；AT模式最终一致



#### 4.2.4.脏写问题

在多线程并发访问AT模式的分布式事务时，有可能出现脏写问题，如图：

![image-20210724181541234](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153783.png)



解决思路就是引入了全局锁的概念。在释放DB锁之前，先拿到全局锁。避免同一时刻有另外一个事务来操作当前数据。

![image-20210724181843029](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153784.png)



#### 4.2.5.优缺点

AT模式的优点：

- 一阶段完成直接提交事务，释放数据库资源，性能比较好
- 利用全局锁实现读写隔离
- 没有代码侵入，框架自动完成回滚和提交

AT模式的缺点：

- 两阶段之间属于软状态，属于最终一致
- 框架的快照功能会影响性能，但比XA模式要好很多



#### 4.2.6.实现AT模式

AT模式中的快照生成、回滚等动作都是由框架自动完成，没有任何代码侵入，因此实现非常简单。

只不过，AT模式需要一个表来记录全局锁、另一张表来记录数据快照undo_log。



1）导入数据库表，记录全局锁

导入课前资料提供的Sql文件：seata-at.sql，其中lock_table导入到TC服务关联的数据库，undo_log表导入到微服务关联的数据库：

![image-20210724182217272](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153785.png)

2）修改application.yml文件，将事务模式修改为AT模式即可：

```yaml
seata:
  data-source-proxy-mode: AT ## 默认就是AT
```



3）重启服务并测试







### 4.3.TCC模式

TCC模式与AT模式非常相似，每阶段都是独立事务，不同的是TCC通过人工编码来实现数据恢复。需要实现三个方法：

- Try：资源的检测和预留； 

- Confirm：完成资源操作业务；要求 Try 成功 Confirm 一定要能成功。

- Cancel：预留资源释放，可以理解为try的反向操作。



#### 4.3.1.流程分析

举例，一个扣减用户余额的业务。假设账户A原来余额是100，需要余额扣减30元。

- **阶段一（ Try ）**：检查余额是否充足，如果充足则冻结金额增加30元，可用余额扣除30

初识余额：

![image-20210724182424907](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153786.png)

余额充足，可以冻结：

![image-20210724182457951](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153787.png)



此时，总金额 = 冻结金额 + 可用金额，数量依然是100不变。事务直接提交无需等待其它事务。



- **阶段二（Confirm)**：假如要提交（Confirm），则冻结金额扣减30

确认可以提交，不过之前可用金额已经扣减过了，这里只要清除冻结金额就好了：

![image-20210724182706011](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153788.png)



此时，总金额 = 冻结金额 + 可用金额 = 0 + 70  = 70元





- **阶段二(Canncel)**：如果要回滚（Cancel），则冻结金额扣减30，可用余额增加30

需要回滚，那么就要释放冻结金额，恢复可用金额：

![image-20210724182810734](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153789.png)





#### 4.3.2.Seata的TCC模型

Seata中的TCC模型依然延续之前的事务架构，如图：

![image-20210724182937713](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153790.png)



#### 4.3.3.优缺点

TCC模式的每个阶段是做什么的？

- Try：资源检查和预留
- Confirm：业务执行和提交
- Cancel：预留资源的释放

TCC的优点是什么？

- 一阶段完成直接提交事务，释放数据库资源，性能好
- 相比AT模型，无需生成快照，无需使用全局锁，性能最强
- 不依赖数据库事务，而是依赖补偿操作，可以用于非事务型数据库

TCC的缺点是什么？

- 有代码侵入，需要人为编写try、Confirm和Cancel接口，太麻烦
- 软状态，事务是最终一致
- 需要考虑Confirm和Cancel的失败情况，做好幂等处理



#### 4.3.4.事务悬挂和空回滚

##### 1）空回滚

当某分支事务的try阶段**阻塞**时，可能导致全局事务超时而触发二阶段的cancel操作。在未执行try操作时先执行了cancel操作，这时cancel不能做回滚，就是**空回滚**。

如图：

![image-20210724183426891](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153791.png)

执行cancel操作时，应当判断try是否已经执行，如果尚未执行，则应该空回滚。



##### 2）业务悬挂

对于已经空回滚的业务，之前被阻塞的try操作恢复，继续执行try，就永远不可能confirm或cancel ，事务一直处于中间状态，这就是**业务悬挂**。

执行try操作时，应当判断cancel是否已经执行过了，如果已经执行，应当阻止空回滚后的try操作，避免悬挂





#### 4.3.5.实现TCC模式

解决空回滚和业务悬挂问题，必须要记录当前事务状态，是在try、还是cancel？



##### 1）思路分析

这里我们定义一张表：

```sql
CREATE TABLE `account_freeze_tbl` (
  `xid` varchar(128) NOT NULL,
  `user_id` varchar(255) DEFAULT NULL COMMENT '用户id',
  `freeze_money` int(11) unsigned DEFAULT '0' COMMENT '冻结金额',
  `state` int(1) DEFAULT NULL COMMENT '事务状态，0:try，1:confirm，2:cancel',
  PRIMARY KEY (`xid`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 ROW_FORMAT=COMPACT;

```

其中：

- xid：是全局事务id
- freeze_money：用来记录用户冻结金额
- state：用来记录事务状态



那此时，我们的业务开怎么做呢？

- Try业务：
  - 记录冻结金额和事务状态到account_freeze表
  - 扣减account表可用金额
- Confirm业务
  - 根据xid删除account_freeze表的冻结记录
- Cancel业务
  - 修改account_freeze表，冻结金额为0，state为2
  - 修改account表，恢复可用金额
- 如何判断是否空回滚？
  - cancel业务中，根据xid查询account_freeze，如果为null则说明try还没做，需要空回滚
- 如何避免业务悬挂？
  - try业务中，根据xid查询account_freeze ，如果已经存在则证明Cancel已经执行，拒绝执行try业务



接下来，我们改造account-service，利用TCC实现余额扣减功能。



##### 2）声明TCC接口

TCC的Try、Confirm、Cancel方法都需要在接口中基于注解来声明，

我们在account-service项目中的`cn.itcast.account.service`包中新建一个接口，声明TCC三个接口：

```java
package cn.itcast.account.service;

import io.seata.rm.tcc.api.BusinessActionContext;
import io.seata.rm.tcc.api.BusinessActionContextParameter;
import io.seata.rm.tcc.api.LocalTCC;
import io.seata.rm.tcc.api.TwoPhaseBusinessAction;

@LocalTCC
public interface AccountTCCService {

    @TwoPhaseBusinessAction(name = "deduct", commitMethod = "confirm", rollbackMethod = "cancel")
    void deduct(@BusinessActionContextParameter(paramName = "userId") String userId,
                @BusinessActionContextParameter(paramName = "money")int money);

    boolean confirm(BusinessActionContext ctx);

    boolean cancel(BusinessActionContext ctx);
}
```



##### 3）编写实现类

在account-service服务中的`cn.itcast.account.service.impl`包下新建一个类，实现TCC业务：

```java
package cn.itcast.account.service.impl;

import cn.itcast.account.entity.AccountFreeze;
import cn.itcast.account.mapper.AccountFreezeMapper;
import cn.itcast.account.mapper.AccountMapper;
import cn.itcast.account.service.AccountTCCService;
import io.seata.core.context.RootContext;
import io.seata.rm.tcc.api.BusinessActionContext;
import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
@Slf4j
public class AccountTCCServiceImpl implements AccountTCCService {

    @Autowired
    private AccountMapper accountMapper;
    @Autowired
    private AccountFreezeMapper freezeMapper;

    @Override
    @Transactional
    public void deduct(String userId, int money) {
        // 0.获取事务id
        String xid = RootContext.getXID();
        // 1.扣减可用余额
        accountMapper.deduct(userId, money);
        // 2.记录冻结金额，事务状态
        AccountFreeze freeze = new AccountFreeze();
        freeze.setUserId(userId);
        freeze.setFreezeMoney(money);
        freeze.setState(AccountFreeze.State.TRY);
        freeze.setXid(xid);
        freezeMapper.insert(freeze);
    }

    @Override
    public boolean confirm(BusinessActionContext ctx) {
        // 1.获取事务id
        String xid = ctx.getXid();
        // 2.根据id删除冻结记录
        int count = freezeMapper.deleteById(xid);
        return count == 1;
    }

    @Override
    public boolean cancel(BusinessActionContext ctx) {
        // 0.查询冻结记录
        String xid = ctx.getXid();
        AccountFreeze freeze = freezeMapper.selectById(xid);

        // 1.恢复可用余额
        accountMapper.refund(freeze.getUserId(), freeze.getFreezeMoney());
        // 2.将冻结金额清零，状态改为CANCEL
        freeze.setFreezeMoney(0);
        freeze.setState(AccountFreeze.State.CANCEL);
        int count = freezeMapper.updateById(freeze);
        return count == 1;
    }
}
```







### 4.4.SAGA模式

Saga 模式是 Seata 即将开源的长事务解决方案，将由蚂蚁金服主要贡献。

其理论基础是Hector & Kenneth  在1987年发表的论文[Sagas](https://microservices.io/patterns/data/saga.html)。

Seata官网对于Saga的指南：https://seata.io/zh-cn/docs/user/saga.html

#### 4.4.1.原理

在 Saga 模式下，分布式事务内有多个参与者，每一个参与者都是一个冲正补偿服务，需要用户根据业务场景实现其正向操作和逆向回滚操作。

分布式事务执行过程中，依次执行各参与者的正向操作，如果所有正向操作均执行成功，那么分布式事务提交。如果任何一个正向操作执行失败，那么分布式事务会去退回去执行前面各参与者的逆向回滚操作，回滚已提交的参与者，使分布式事务回到初始状态。

![image-20210724184846396](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153792.png)

Saga也分为两个阶段：

- 一阶段：直接提交本地事务
- 二阶段：成功则什么都不做；失败则通过编写补偿业务来回滚



#### 4.4.2.优缺点



优点：

- 事务参与者可以基于事件驱动实现异步调用，吞吐高
- 一阶段直接提交事务，无锁，性能好
- 不用编写TCC中的三个阶段，实现简单

缺点：

- 软状态持续时间不确定，时效性差
- 没有锁，没有事务隔离，会有脏写

### 4.5.四种模式对比

我们从以下几个方面来对比四种实现：

- 一致性：能否保证事务的一致性？强一致还是最终一致？
- 隔离性：事务之间的隔离性如何？
- 代码侵入：是否需要对业务代码改造？
- 性能：有无性能损耗？
- 场景：常见的业务场景



如图：

![image-20210724185021819](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153793.png)





## 5.高可用

Seata的TC服务作为分布式事务核心，一定要保证集群的高可用性。

### 5.1.高可用架构模型

搭建TC服务集群非常简单，启动多个TC服务，注册到nacos即可。



但集群并不能确保100%安全，万一集群所在机房故障怎么办？所以如果要求较高，一般都会做异地多机房容灾。



比如一个TC集群在上海，另一个TC集群在杭州：

![image-20210724185240957](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153794.png)



微服务基于事务组（tx-service-group)与TC集群的映射关系，来查找当前应该使用哪个TC集群。当SH集群故障时，只需要将vgroup-mapping中的映射关系改成HZ。则所有微服务就会切换到HZ的TC集群了。



### 5.2.实现高可用

具体实现请参考课前资料提供的文档《seata的部署和集成.md》：

![image-20210724172549013](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153775.png)

第三章节：

![image-20220811181654407](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153795.png)









# seata的部署和集成



## 一、部署Seata的tc-server



### 1.下载

首先我们要下载seata-server包，地址在[http](http://seata.io/zh-cn/blog/download.html)[://seata.io/zh-cn/blog/download](http://seata.io/zh-cn/blog/download.html)[.](http://seata.io/zh-cn/blog/download.html)[html](http://seata.io/zh-cn/blog/download.html) 

当然，课前资料也准备好了：

![image-20210622202357640](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153796.png)



### 2.解压

在非中文目录解压缩这个zip包，其目录结构如下：

![image-20210622202515014](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153797.png)

### 3.修改配置

修改conf目录下的registry.conf文件：

![image-20210622202622874](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153798.png)

内容如下：

```properties
registry {
  ## tc服务的注册中心类，这里选择nacos，也可以是eureka、zookeeper等
  type = "nacos"

  nacos {
    ## seata tc 服务注册到 nacos的服务名称，可以自定义
    application = "seata-tc-server"
    serverAddr = "127.0.0.1:8848"
    group = "DEFAULT_GROUP"
    namespace = ""
    cluster = "SH"
    username = "nacos"
    password = "nacos"
  }
}

config {
  ## 读取tc服务端的配置文件的方式，这里是从nacos配置中心读取，这样如果tc是集群，可以共享配置
  type = "nacos"
  ## 配置nacos地址等信息
  nacos {
    serverAddr = "127.0.0.1:8848"
    namespace = ""
    group = "SEATA_GROUP"
    username = "nacos"
    password = "nacos"
    dataId = "seataServer.properties"
  }
}
```





### 4.在nacos添加配置

特别注意，为了让tc服务的集群可以共享配置，我们选择了nacos作为统一配置中心。因此服务端配置文件seataServer.properties文件需要在nacos中配好。

格式如下：

![image-20210622203609227](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153799.png)



配置内容如下：

```properties
## 数据存储方式，db代表数据库
store.mode=db
store.db.datasource=druid
store.db.dbType=mysql
store.db.driverClassName=com.mysql.jdbc.Driver
store.db.url=jdbc:mysql://127.0.0.1:3306/seata?useUnicode=true&rewriteBatchedStatements=true
store.db.user=root
store.db.password=123
store.db.minConn=5
store.db.maxConn=30
store.db.globalTable=global_table
store.db.branchTable=branch_table
store.db.queryLimit=100
store.db.lockTable=lock_table
store.db.maxWait=5000
## 事务、日志等配置
server.recovery.committingRetryPeriod=1000
server.recovery.asynCommittingRetryPeriod=1000
server.recovery.rollbackingRetryPeriod=1000
server.recovery.timeoutRetryPeriod=1000
server.maxCommitRetryTimeout=-1
server.maxRollbackRetryTimeout=-1
server.rollbackRetryTimeoutUnlockEnable=false
server.undo.logSaveDays=7
server.undo.logDeletePeriod=86400000

## 客户端与服务端传输方式
transport.serialization=seata
transport.compressor=none
## 关闭metrics功能，提高性能
metrics.enabled=false
metrics.registryType=compact
metrics.exporterList=prometheus
metrics.exporterPrometheusPort=9898
```



==其中的数据库地址、用户名、密码都需要修改成你自己的数据库信息。==



### 5.创建数据库表

特别注意：tc服务在管理分布式事务时，需要记录事务相关数据到数据库中，你需要提前创建好这些表。

新建一个名为seata的数据库，运行课前资料提供的sql文件：

![image-20210622204145159](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153800.png)

这些表主要记录全局事务、分支事务、全局锁信息：

```mysql
SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- 分支事务表
-- ----------------------------
DROP TABLE IF EXISTS `branch_table`;
CREATE TABLE `branch_table`  (
  `branch_id` bigint(20) NOT NULL,
  `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `resource_group_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `resource_id` varchar(256) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `branch_type` varchar(8) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `status` tinyint(4) NULL DEFAULT NULL,
  `client_id` varchar(64) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime(6) NULL DEFAULT NULL,
  `gmt_modified` datetime(6) NULL DEFAULT NULL,
  PRIMARY KEY (`branch_id`) USING BTREE,
  INDEX `idx_xid`(`xid`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Compact;

-- ----------------------------
-- 全局事务表
-- ----------------------------
DROP TABLE IF EXISTS `global_table`;
CREATE TABLE `global_table`  (
  `xid` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `transaction_id` bigint(20) NULL DEFAULT NULL,
  `status` tinyint(4) NOT NULL,
  `application_id` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_service_group` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `transaction_name` varchar(128) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `timeout` int(11) NULL DEFAULT NULL,
  `begin_time` bigint(20) NULL DEFAULT NULL,
  `application_data` varchar(2000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `gmt_create` datetime NULL DEFAULT NULL,
  `gmt_modified` datetime NULL DEFAULT NULL,
  PRIMARY KEY (`xid`) USING BTREE,
  INDEX `idx_gmt_modified_status`(`gmt_modified`, `status`) USING BTREE,
  INDEX `idx_transaction_id`(`transaction_id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Compact;

SET FOREIGN_KEY_CHECKS = 1;
```



### 6.启动TC服务

进入bin目录，运行其中的seata-server.bat即可：

![image-20210622205427318](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153801.png)

启动成功后，seata-server应该已经注册到nacos注册中心了。



打开浏览器，访问nacos地址：http://localhost:8848，然后进入服务列表页面，可以看到seata-tc-server的信息：

![image-20210622205901450](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153802.png)







## 二、微服务集成seata

### 1.引入依赖

首先，我们需要在微服务中引入seata依赖：

```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
    <exclusions>
        <!--版本较低，1.3.0，因此排除-->
        <exclusion>
            <artifactId>seata-spring-boot-starter</artifactId>
            <groupId>io.seata</groupId>
        </exclusion>
    </exclusions>
</dependency>
<!--seata starter 采用1.4.2版本-->
<dependency>
    <groupId>io.seata</groupId>
    <artifactId>seata-spring-boot-starter</artifactId>
    <version>${seata.version}</version>
</dependency>
```



### 2.修改配置文件

需要修改application.yml文件，添加一些配置：

```yaml
seata:
  registry: ## TC服务注册中心的配置，微服务根据这些信息去注册中心获取tc服务地址
    ## 参考tc服务自己的registry.conf中的配置
    type: nacos
    nacos: ## tc
      server-addr: 127.0.0.1:8848
      namespace: ""
      group: DEFAULT_GROUP
      application: seata-tc-server ## tc服务在nacos中的服务名称
      cluster: SH
  tx-service-group: seata-demo ## 事务组，根据这个获取tc服务的cluster名称
  service:
    vgroup-mapping: ## 事务组与TC服务cluster的映射关系
      seata-demo: SH
```



## 三、TC服务的高可用和异地容灾

### 1.模拟异地容灾的TC集群

计划启动两台seata的tc服务节点：

| 节点名称 | ip地址    | 端口号 | 集群名称 |
| -------- | --------- | ------ | -------- |
| seata    | 127.0.0.1 | 8091   | SH       |
| seata2   | 127.0.0.1 | 8092   | HZ       |

之前我们已经启动了一台seata服务，端口是8091，集群名为SH。

现在，将seata目录复制一份，起名为seata2

修改seata2/conf/registry.conf内容如下：

```nginx
registry {
  ## tc服务的注册中心类，这里选择nacos，也可以是eureka、zookeeper等
  type = "nacos"

  nacos {
    ## seata tc 服务注册到 nacos的服务名称，可以自定义
    application = "seata-tc-server"
    serverAddr = "127.0.0.1:8848"
    group = "DEFAULT_GROUP"
    namespace = ""
    cluster = "HZ"
    username = "nacos"
    password = "nacos"
  }
}

config {
  ## 读取tc服务端的配置文件的方式，这里是从nacos配置中心读取，这样如果tc是集群，可以共享配置
  type = "nacos"
  ## 配置nacos地址等信息
  nacos {
    serverAddr = "127.0.0.1:8848"
    namespace = ""
    group = "SEATA_GROUP"
    username = "nacos"
    password = "nacos"
    dataId = "seataServer.properties"
  }
}
```



进入seata2/bin目录，然后运行命令：

```powershell
seata-server.bat -p 8092
```



打开nacos控制台，查看服务列表：

![image-20210624151150840](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153803.png)

点进详情查看：

![image-20210624151221747](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153804.png)



### 2.将事务组映射配置到nacos

接下来，我们需要将tx-service-group与cluster的映射关系都配置到nacos配置中心。

新建一个配置：

![image-20210624151507072](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181153805.png)

配置的内容如下：

```properties
## 事务组映射关系
service.vgroupMapping.seata-demo=SH

service.enableDegrade=false
service.disableGlobalTransaction=false
## 与TC服务的通信配置
transport.type=TCP
transport.server=NIO
transport.heartbeat=true
transport.enableClientBatchSendRequest=false
transport.threadFactory.bossThreadPrefix=NettyBoss
transport.threadFactory.workerThreadPrefix=NettyServerNIOWorker
transport.threadFactory.serverExecutorThreadPrefix=NettyServerBizHandler
transport.threadFactory.shareBossWorker=false
transport.threadFactory.clientSelectorThreadPrefix=NettyClientSelector
transport.threadFactory.clientSelectorThreadSize=1
transport.threadFactory.clientWorkerThreadPrefix=NettyClientWorkerThread
transport.threadFactory.bossThreadSize=1
transport.threadFactory.workerThreadSize=default
transport.shutdown.wait=3
## RM配置
client.rm.asyncCommitBufferLimit=10000
client.rm.lock.retryInterval=10
client.rm.lock.retryTimes=30
client.rm.lock.retryPolicyBranchRollbackOnConflict=true
client.rm.reportRetryCount=5
client.rm.tableMetaCheckEnable=false
client.rm.tableMetaCheckerInterval=60000
client.rm.sqlParserType=druid
client.rm.reportSuccessEnable=false
client.rm.sagaBranchRegisterEnable=false
## TM配置
client.tm.commitRetryCount=5
client.tm.rollbackRetryCount=5
client.tm.defaultGlobalTransactionTimeout=60000
client.tm.degradeCheck=false
client.tm.degradeCheckAllowTimes=10
client.tm.degradeCheckPeriod=2000

## undo日志配置
client.undo.dataValidation=true
client.undo.logSerialization=jackson
client.undo.onlyCareUpdateColumns=true
client.undo.logTable=undo_log
client.undo.compress.enable=true
client.undo.compress.type=zip
client.undo.compress.threshold=64k
client.log.exceptionRate=100
```

### 3.微服务读取nacos配置

接下来，需要修改每一个微服务的application.yml文件，让微服务读取nacos中的client.properties文件：

```yaml
seata:
  config:
    type: nacos
    nacos:
      server-addr: 127.0.0.1:8848
      username: nacos
      password: nacos
      group: SEATA_GROUP
      data-id: client.properties
```



重启微服务，现在微服务到底是连接tc的SH集群，还是tc的HZ集群，都统一由nacos的client.properties来决定了。

