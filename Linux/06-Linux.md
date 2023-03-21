# Linux操作系统基础

一套免费使用和自由传播的类UNIX操作系统

### 安装vmwa Tools

```
sudo su 切换成超级管理员
```

```
apt-get install open-vm-tools-desktop -y
```

报错 `E：Could not get lock /var/lib/dpkg/lock-frontend - open`

先尝试：

```
killall apt apt-get
```

如果还是不行，则：

```
rm /var/lib/apt/lists/lock
rm /var/cache/apt/archives/lock
rm /var/lib/dpkg/lock*
```

最后：
```sudo apt update```

### 如果浏览器没有网络

1.关闭虚拟机器

2.点击vmware的编辑 

3.点击虚拟网络编辑器  

4.点击更改设置 

5.点击还原默认值

6.重启ubuntu



### 更换镜像源

备份文件

```
sudo cp  /etc/apt/sources.list /etc/apt/sources.list.bak
```

编辑文件

```
sudo gedit /etc/apt/sources.list
```

更换镜像源

### 安装gcc

```
sudo apt install gcc 
```

检查是否安装成功

```
gcc -v
```

出现版本号则表示安装成功



# 远程连接SSL

## mac系统安装ssh

```
ip addr    				获取虚拟机ip地址192.1.1.123为例
ping 192.1.1.123        物理机测试网络状态
ctrl+c					网络通畅，结束
ssh 用户名@192.1.1.123   物理机连接
	sudo service ssh start   虚拟机创建连接，输入密码
		sudo apt install -y openssh-server 直接安装ssh
			sudo apt update				如果报错，先执行更新
			sudo apt install -y openssh-server  再安装ssh
	sudo service ssh start   虚拟机创建连接，输入密码
确认连接密钥，连接完成

ls 查询桌面位置
cd Desktop/ 	切换到桌面
ls				查询桌面文件

scp 文件 用户名@192.1.1.123:虚拟机路径（pwd查询路径）  	  拷贝到虚拟机
scp 用户名@192.1.1.123:路径名文件						拷贝到物理机
```



![image-20210927164204354](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20210927164204354.png)=======================================================================================

![image-20210927145914801](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20210927145914801.png)例

## windows使用GIT进行安装

```
ip addr    				获取虚拟机ip地址192.1.1.123为例
ping 192.1.1.123        物理机测试网络状态
Git Bash Here	鼠标右键桌面打开git软件
ssh 用户名@192.1.1.123   物理机连接
	后同mac
	
Git Bash Here	鼠标右键桌面打开git软件

```

![image-20210927152740993](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20210927152740993.png)例：

# 编辑器vi的使用

### vi状态: 命令模式和编辑模式

进入后默认是命令模式，只能输入**特定的命令**或**移动光标**，不能编辑文件内容

<img src="C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20210927115813933.png" alt="image-20210927115813933" style="zoom:33%;" />例：



> 命令模式用 a 跳转到编辑模式，编辑模式用 esc 跳转到命令模式

```
vi index.php	如果文件不存在，则新建文件

a 进入编辑页面
        <?php
        echo 'hello world';
        
ESC 返回命令界面
       :Wq   存盘并退出(write and quit)
        :W    存盘
        :q    退出
        :q!   不存盘强制退出
        :wq!  强制存盘退出
```

### 命令模式移动光标

![image-20210927134800300](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20210927134800300.png)H左L右K上J下

### 命令模式快速定位

```
:set nu		显示行号
:15 		跳到第15行
G			定位到最后一行
gg			到第一行
/str		搜索str字符串，按n键到下一处
```

### 常用的编辑操作

```
dd		删除一行 (剪切)
5dd		删除5行(剪切)
yy		复制
5yy		复制5行
p		粘贴
U		撤销
ctrl+r  恢复上一步撤销操作
```

# Linux常用命令

## ~ Home目录 与执行文件

```
`~` 表示宿主目录/家(Home)目录,对应侧边栏的文件夹

./       			 执行文件命令
./welcome
```

## 变量与函数

```
变量名 = 值
pi = 3.1415926

函数名（）{}	例：
show()
{
echo ==============
echo
}
show			直接调用时不需要加括号快捷
```

## 打印/输出到控制台

```
echo 内容            打印

echo "hello&world"
& 是特殊字符需要用引号包起来
echo $pi 打印变量需要加 $符号

echo "">>文件
例：echo "123456">>readme.txt

echo $PATH 寻找命令
```

## 目录和文件操作

```
pwd			打印当前工作目录	 print working directory
```

```
cd			切换目录			change directory
    cd ~	宿主目录 或直接cd
    cd -	上次的目录
    cd ..	上级目录( .代表当前目录)
```

## Linux命令的选项与参数

```
ls					list 		命令
ls -l -a /etc		-l -a -la	选项
ls -la /etc			/etc		参数

ls 		列出当前目录文件
ls -a 	显示所有隐藏的
ls -l 	显示权限
ls -F	按类型区分
```

## 列出目录内容与权限

```
ls			列出目录中的文件	 list

    ls -1	详细信息
    ls -a	显示所有文件(包含以点开头的文件)
    ls -F	在目录后加斜线显示
    ls -1h 	人性化单位显示大小
-rw-r--r-- 1 root root 26 Feb 20 16:44 /etc/issue
	第一个字符文件类型 d目录 -文件  l链接			日期是最后修改时间
	
	chmod u+x 文件名字   给文件加权限  
			u 指的是所有者 x执行权限
```

## 创建文件与删除

```
mkdir		创建目录 			make directory
touch		创建一个空文件
```

```
rm				删除remove
    rm -r		删除目录
    rm -i		删除前提示(Centos默认)
    rm -f		删除文件不提示
    rm -rf		删除目录(不提示) (rm -r -f)|
    rm -rf ./* 	删除当前目录所有文件
```

## 复制与移动(重命名)

```
mv		移动move (重命名也是这个命令)
		目录也可以移动
mv 文件 文件夹		   	（移动文件）
mv 文件夹/ 文件夹2/		（移动文件夹）
```

```
cp		复制		copy
    cp /etc/issue ./		将/etc/issue文件复制到当前目录
    cp -r递归复制目录	
```

```
mv 文件名 新的文件名

如将/test1目录下的file1移动到/test3 目录，并将文件名改为file2,可输入以下命令：
mv /test1/file1 /test3/file2
    
如将/test1目录下的file1复制到/test3目录，并将文件名改为file2,可输入以下命令：
cp /test1/file1 /test3/file2
```

## 查找

```
find搜索
    find /etc -name init		在/etc目录精确查找init文件
    find /etc -name 'init*'		在/etc目录找init开头的文件
    find /etc -name '?init'		在/etc目录找以init结尾，前面只有一个字符
	find /usr/bin -size +3M		在/use/bin目录查找大于3M的文件
```

```
which显示命令路径
	which python3
```

## 查看内容

```
cat显示文件内容 少量
	cat /etc/issue
more		大量
    more /etc/services 			 查看/etc/services文件
   
        空格	翻页
        回车	下一行
        b	  上一页
        q	  退出

    
head	查看文件头几行
	head -n 5 /etc/services
tain		查看文件最后几行
	tail -n 5 /etc/services		显示/etc/services文件最后5行
tail -f		监视文件变化
```

## 链接

```
1n创建链接	
	1n -s 源文件 新文件	(创建软链接)
		例子：touch readme.txt
                echo "123456" >>readme.txt
                    ln -s readme.txt install.txt 
                        对源文件的增加不影响新文件，但删除会影响
	In 源文件  新文件		(创建硬链接)
		例子： touch setup.sh
				echo "123456" >>setup.sh
					in setup.sh	setup2.sh
							不会指向，文件删改会互相影响，不能跨文件系统
```

![image-20210927195930877](C:\Users\十六夜咲夜\AppData\Roaming\Typora\typora-user-images\image-20210927195930877.png)

> 文件夹后面数值代表子目录数量，硬链接代表有多少被连接的文件

## 快捷（ctrl）

```
code 加文件  启动visual code
ctrl+l 清屏
ctrl+insert	复制	
ctrl+c		终止
shift+insert 粘贴
上下键   查找历史代码
部分前称+tab 快捷补全
tab+tab   快捷查找
```

# Linux下的文件打包与解压

## tar格式：打包目录和解压文件

```
    z -->	zip 		压缩
    v -->	view 		解压的文件的目录,可不写,耗性能 
    c -->	create 	创建
    X -->	extract 	提取
    f -->	file 		文件
```

``` 
打包目录：
    tar -zcf 压缩后的文件 需要解压的目录
       tar -zvcf 压缩后的文件 需要解压的目录
   	   例：	tar -zcf test.tar.gz test  
```

```
解压文件：
    tar -zxf 文件名
       例：	tar -zxf test.tar.gz 
```

## bz2格式：打包目录和解压文件

``` 
打包目录：
    tar -jcf 压缩后的文件 需要解压的目录 
        例：	tar -jcf demo.bz2 demo 
```

```
解压文件：
    tar -jxf 文件名
        例：	tar -xjf demo.bz2 
```



## ZIP格式：打包目录和解压文件

```
zip安装
    zip						（没安装会报错）
  	  apt install zip		（安装zip）
  	  	apt update			（更新软件源）
  		  apt install zip	（安装zip）
```



``` 
打包目录：
    zip -r 压缩后的文件 需要解压的目录 
        例：	zip -r demo.zip demo 
```

```
解压文件：
    unzip 压缩后的文件 
    	例：	unzip demo.zip
```


### 查看文件的类型

```
file 压缩后的文件名
```

# 服务器上部署前端项目

## 下载nginx

```
wget http://nginx.org/download/nginx-1.20.1.tar.gz
```

## 解压nginx

```
tar -zxvf nginx-1.20.1.tar.gz
```

## 下载OpenSSL

```
wget https://www.openssl.org/source/openssl-1.1.1l.tar.gz
```

## 解压OpenSSL

```
tar -zxvf openssl-1.1.1l.tar.gz
```

## 编译nginx

进入nginx目录

```
cd ./nginx-1.20.1
```

## 安装编译nginx需要的工具

```
apt install -y gcc make libpcre3-dev zlib1g-dev
apt-get update
```

## 设置配置

```
./configure --with-http_ssl_module --with-openssl=../openssl-1.1.1l
```

![image-20220310092236852](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181145502.png)



```
./configure --help	帮助
```



## 编译

```
make
```

```
make install
```

## 启动nginx服务

进入编译好的nginx目录

```
cd /usr/local/nginx
```

启动服务

```
/usr/local/nginx/sbin/nginx
```

查看端口是否启动成功

```
netstat -tnulp | grep 80
```

结果如下说明成功

```
tcp  0  0 0.0.0.0:80  0.0.0.0:*   LISTEN  50909/nginx: master 
```


# 部署阿里云服务器

## 什么是云服务器？

阿⾥云提供的云服务器ECS，拥有独⽴操作系统和公⽹IP地址，我们可以⾃由在该服务器上安装软件， 正式上线部署我们的项⽬。根据配置不同，价格也不相同： 
标准型1核CPU+1G内存+40G硬盘，约47元/⽉ 
标准型1核CPU+2G内存+40G硬盘，约74元/⽉ 
突发型1核CPU+2G内存+40G硬盘，约59.6元/⽉
**带宽1M，⼀个⽉费⽤约23元**
如果选⽤：突发型1核CPU+2G内存+40G硬盘，1M带宽，⼀个⽉费⽤约82.6元。



## 如何购买云服务器？

学习期间使⽤，我们可以使⽤下⾯的推⼴链接，购买到新⽤户专享的ECS服务器，⾜够我们整个学习期 间使⽤了。

https://www.aliyun.com/minisite/goods?userCode=5olcxcaq

### 地域可选华东或华北 

### 操作系统选择公共镜像 Ubuntu 18.04 64位

### 安全组将80、443、22端⼝打开

# Linux进阶-用户权限和进程管理

## 一.用户与权限管理

### 1.Linux权限概述(*)

#### **Linux文件权限**

-  **r**ead         可读 	    数字编号4   
-  **w**rite        可写	     数字编号2    
-  e**x**ecute   可执行      数字编号1    

| 代表字符 | 权限     | 对文件的含义                                      | 对目录的含义               |
| -------- | -------- | ------------------------------------------------- | -------------------------- |
| **r**    | 读权限   | 可以查看文件内容(可以使用cat tail more等查看命令) | 可以列出目录中的内容(ll)   |
| **w**    | 写权限   | 可以修改文件内容(可以vi编辑)                      | 可以再目录中创建、删除文件 |
| **x**    | 执行权限 | 可以执行文件                                      | 可以进入目录               |

#### **用户三大类(u g o)**

- user(owner)     所有者
- group               所属组  一个文件归到一个组中,组成员拥有一个共同的权限
- other                 其他人

三三组合就有九种情况

```
-rw-r--r--   第一个字符为"d" 代表目录
-	   普通文件
rw-    u 属用户
r-- 	 g 属组
r--	  o 其他人 
```

#### 用户管理命令

- **groupadd**          添加用户组
- **groupdel**           删除用户组

useradd                     添加用户

​			-g 				   添加用户组

​			-m 				  自动创建宿主文件目录(ubuntu)  CentOS 默认会创建   /Home/jack               自动生成jack宿主目录

userdel

​			 -r					连同宿主目录一起删除

​			 -password	修改用户密码(没有参数时修改自己的密码)

#### 权限操作命令

chown  jack 	testfile		改变文件所有者	

chgrp    group1   testfile		修改文件所属组

chmod  u+x 		./start.sh     修改文件权限

chmod  -R  777  /data/www

#### 实例

>创建2个小组
>
>​		python
>
>​		php
>
>创建四个用户
>
>​		python组: jack    mary
>
>​		php组:	lily		tom
>
>创建目录
>
>​		/data/python
>
>​		/data/php
>
>配置权限
>
>​		python  组的同事允许在	/data/python 目录下工作
>
>​		php 组的同事允许在 	/data/php 目录下工作
>
>在ubuntu内

1. 先获取管理员权限

2. 

3. 创建两个小组 python php

   ```
   groupadd python
   groupadd php
   ```

4. 创建4个用户 python组：jack mary ；php组：lily tom

   ```
   useradd -m -g python jack
   useradd -m -g python mary
   useradd -m -g php lily
   useradd -m -g php tom
   ```

   ```
   id jack
   uid=1007(jack) gid=(1008)(python) groups=1008(python)
   ```

5. 创建目录 /data/python /data/php

   ```
   mkdir /data/python -p
   mkdir /data/php -p
   ```

   ```
   cd /data/
   ls -l 查看权限
   passwd jack 给jack设置密码
   ```

6. 配置权限 python组的同事允许在/data/python目录下工作 php组的同事允许在/data/php目录下
   工作  
   以putty链接ip 以jack登录

  ```
pwd =========》/home/j$ pwd
/home/jack
$ ls -l
total 0
$ cd /data
$ pwd
/data
$ ls -l
total 8
drwxr-xr-x 2 root root 4096 Sep 29 20:29 php

drwxr-xr-x 2 root root 4096 Sep 29 20:29 python <===============other有
读，执行权限
$ cd python
$ ls
$ touch 1.py
touch: cannot touch '1.py': Permission denied <================jack没
有写的权限因此被拒绝
  ```

  想要写入可以在root端将权限转让给他

  ```
root@iZuf6j9jkgkabhxwraxiccZ:~# cd /data/
root@iZuf6j9jkgkabhxwraxiccZ:/data# chown jack python/ <=============将
权限转移给jack
root@iZuf6j9jkgkabhxwraxiccZ:/data# ls -l
total 8
drwxr-xr-x 2 root root 4096 Sep 29 20:29 php
drwxr-xr-x 2 jack root 4096 Sep 29 20:29 python <==============
所有者已改为jack
  ```

  当将文件所有权转让后就只能让一个人拥有所有者权限，所有考虑使用组权限

  ```
root@iZuf6j9jkgkabhxwraxiccZ:/data# chgrp python python 将python文件改到
python组里
root@iZuf6j9jkgkabhxwraxiccZ:/data# ls -l
total 8
drwxr-xr-x 2 root root 4096 Sep 29 20:29 php
drwxr-xr-x 2 jack python 4096 Sep 30 09:45 python <===========所属组依
旧没有写权限
root@iZuf6j9jkgkabhxwraxiccZ:/data#
root@iZuf6j9jkgkabhxwraxiccZ:/data# chmod g+w python/ <============加入组
写权限
  ```

  jack给自己加文件执行权限

  ```
-rw-r--r-- 1 jack python 0 Sep 30 09:45 1.py
$ chmod u+x 1.py <=================给当前用
户增加执行权限
$ ls -l
total 0
-rwxr--r-- 1 jack python 0 Sep 30 09:45 1.py
快速给所有人加所有权限
chmod 777 1.py
  ```

### 2.Linux用户与用户组

**用户分类**
user(owner) 所有者
group 所属组
一个文件归到一个组中，组成员拥有一个共同的权限
other 其他

## 二.Linux的进程管理和系统状态

### 程序和进程

#### 程序

- 程序 是指令和数据的有序集合 是一个静态的概念
- 进程 代表一个正在运行的程序的实例
- 线程 通常在一个进程中可以包含多个线程



- 在命令末尾加上&符合，就可以让程序在后台运行
- 程序正在前台运行，可以使用Ctrl+Z把程序暂停
- jobs查看运行的程序
- bg 把暂停的程序放到后台运行
- fg 把一个程序调到前台运行

#### 查看进程

**查看所有端口**

```
方法1 netstat -ano | findstr *
方法2 netstat -ano
```

##### **查看占用端口进程**

```
netstat -ano | findstr 80  //为空就是没被占用  
tasklist|findstr 端口号

使用ntsd -c q -p PID命令杀掉占用端口的进程，其中PID为占用端口的进程号，上一步查找到的端口号，也可以使用taskkill
/PID PID 命令杀掉进程。
```

```ABAP
  1：协议 2：本地地址 3： 外部地址 4： 状态 5： PID
  
  TCP    0.0.0.0:7680           0.0.0.0:0              LISTENING       5712
  TCP    0.0.0.0:49664          0.0.0.0:0              LISTENING       980
  TCP    192.168.1.80:139       0.0.0.0:0              LISTENING       4
  TCP    192.168.1.80:49417     40.90.189.152:443      ESTABLISHED     5024
  TCP    192.168.1.80:51602     20.43.70.166:443       ESTABLISHED     11040
  TCP    192.168.1.80:55880     142.250.157.188:5228   ESTABLISHED     14824
  TCP    192.168.1.80:58620     51.104.164.114:443     TIME_WAIT       0
  TCP    192.168.1.80:58621     104.44.88.24:443       TIME_WAIT       0
  TCP    192.168.1.80:58622     20.150.95.132:443      TIME_WAIT       0
  TCP    192.168.1.80:58624     203.208.43.66:443      ESTABLISHED     14824
  TCP    192.168.1.80:58629     104.111.211.185:80     ESTABLISHED     4544
  TCP    192.168.1.80:58630     115.231.33.1:80        ESTABLISHED     4544
  TCP    192.168.1.80:58631     20.44.229.112:443      ESTABLISHED     1584
  TCP    192.168.1.80:58632     115.231.33.1:80        ESTABLISHED     4544
  TCP    192.168.1.80:58633     104.208.16.88:443      ESTABLISHED     15556
  TCP    192.168.1.80:58803     40.90.189.152:443      ESTABLISHED     15556
  TCP    192.168.1.80:60919     183.3.224.139:443      ESTABLISHED     2860
  TCP    [::]:7680              [::]:0                 LISTENING       5712
  TCP    [::]:49664             [::]:0                 LISTENING       980
  UDP    192.168.1.80:137       *:*                                    4
  UDP    192.168.1.80:138       *:*                                    4
  UDP    192.168.1.80:1900      *:*                                    6072
  UDP    192.168.1.80:52640     *:*                                    6072
  UDP    [fe80::c8:d52a:46ef:c06%9]:1900  *:*                                    6072
  UDP    [fe80::c8:d52a:46ef:c06%9]:52635  *:*                                    6072
  UDP    [fe80::515f:8ae8:7e52:3b5f%20]:1900  *:*                                    6072
  UDP    [fe80::515f:8ae8:7e52:3b5f%20]:52633  *:*                                    6072
  UDP    [fe80::80e1:89de:31e6:7ea5%19]:1900  *:*                                    6072
  UDP    [fe80::80e1:89de:31e6:7ea5%19]:52634  *:*                                    6072
  UDP    [fe80::c169:6964:ae00:a031%17]:1900  *:*                                    6072
  UDP    [fe80::c169:6964:ae00:a031%17]:52632  *:*                                    6072
```

**其他进程**

电脑里进程很多，有系统进程，有用户进程
-e 是显示所有的

```
root@iZuf6j9jkgkabhxwraxiccZ:~# ps -ef
UID PID PPID C STIME TTY TIME CMD
root 1 0 0 Sep29 ? 00:00:04 /sbin/init noibrs splash
root 2 0 0 Sep29 ? 00:00:00 [kthreadd]
root 4 2 0 Sep29 ? 00:00:00 [kworker/0:0H]
root 6 2 0 Sep29 ? 00:00:00 [mm_percpu_wq]
root 7 2 0 Sep29 ? 00:00:01 [ksoftirqd/0]
root 8 2 0 Sep29 ? 00:00:16 [rcu_sched]
root 9 2 0 Sep29 ? 00:00:00 [rcu_bh]
```

- UID 该程序被uid所拥有
- PID 就是这个程序的进程ID
- PPID 则是其上级父程序的进程ID
- C 表示CPU使用的资源百分比
- STIME 表示进程的启动时间
- TTY 登入者的终端机位置
- TIME 使用掉的CPU时间
- CMD所下达的指令为何

使用grep指令过滤输出，将ps -ef输出的内容 进行搜索

```
root@iZuf6j9jkgkabhxwraxiccZ:~# ps -ef | grep httpd
root 29490 27663 0 10:33 pts/0 00:00:00 grep --color=auto httpd
```

**另一种查看进程的方法**

```
root@iZuf6j9jkgkabhxwraxiccZ:~# ps aux
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.4 77652 8628 ? Ss Sep29 0:04 /sbin/init
noibrs splash
root 2 0.0 0.0 0 0 ? S Sep29 0:00 [kthreadd]
root 4 0.0 0.0 0 0 ? I< Sep29 0:00 [kworker/0:0H]
root 6 0.0 0.0 0 0 ? I< Sep29 0:00 [mm_percpu_wq]
```

- USER 行程拥有者

- PID pid

- %CPU 占用cpu使用率

- %MEM 占用的记忆体使用率

- VSZ 占用虚拟记忆体大小

- RSS 占用记忆体大小

- TTY 终端的次要装置号码(minor device number of tty)

- STAT 该行程的状态，linux有5种状态：

  1. D不可中断

  2. R运行

  3. S中断

  4. T停止

  5. 僵死

  6. 注：其他状态还包括W(无驻留页)，<( 高优先级进程)，N(低优先级进程)，L(内存锁业)

- START 行程开始时间
- TIME 执行的时间
- COMMAND 所执行的指令

**top命令**

```
top - 10:46:05 up 17:44, 3 users, load average: 2.00, 2.20, 2.00
		^ 			^ 	 ^ 						 ^ 		^ 	  ^
		| 			| 	登录的人数 				  | 	5分钟 15分钟
	当前时间 	最近的开机时间内 			当前1分钟内的平均负载
Tasks: 88 total, 3 running, 55 sleeping, 1 stopped, 0 zombie
%Cpu(s): 99.3 us, 0.7 sy, 0.0 ni, 0.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st
KiB Mem : 1957500 total, 1395132 free, 105432 used, 456936 buff/cache
KiB Swap: 0 total, 0 free, 0 used. 1686240 avail Mem

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
28937 jack 20 0 28732 8336 5488 R 49.5 0.4 11:58.63 test.py
28887 jack 20 0 28732 8412 5572 R 49.2 0.4 12:47.68 test.py
1053 root 10 -10 137952 25224 14252 S 0.3 1.3 7:34.63 AliYunDun
1 root 20 0 77652 8628 6508 S 0.0 0.4 0:04.91 systemd
2 root 20 0 0 0 0 S 0.0 0.0 0:00.00 kthreadd
4 root 0 -20 0 0 0 I 0.0 0.0 0:00.00 kworker/0:0H
```

![image-20211203151346926](C:\Users\LIN\AppData\Roaming\Typora\typora-user-images\image-20211203151346926.png)

#### 查看硬盘空间

```
root@iZuf6j9jkgkabhxwraxiccZ:~# df -h
Filesystem  Size  	Used 	Avail  Use%  Mounted on
udev 		933M       0 	933M	 0%  /dev
tmpfs 		192M 	2.9M 	189M 	 2%  /run
```

#### 查看内存的占用

```
root@iZuf6j9jkgkabhxwraxiccZ:~# free -m
		total   used 	free	 shared buff/cache available
Mem:    1911 	97 		1366 		2    447		 1651
Swap:    0 		0 		0
```

### 计划任务

计划任务，就是让操作系统定期执行我们指定的程序，来完成一些自动化任务。例如，我们希望每天1点20分，执行一次`ls`命令，格式如下：

```
20  1  *  *  *  ls
```

```
*    *    *    *    *    command
-    -    -    -    -    -
|    |    |    |    |    + 需要执行的命令
|    |    |    |    +----- 星期中星期几 (0 - 6) (星期天 为0)
|    |    |    +---------- 月份 (1 - 12) 
|    |    +--------------- 一个月中的第几天 (1 - 31)
|    +-------------------- 小时 (0 - 23)
+------------------------- 分钟 (0 - 59)
```

这个计划任务，编写在什么地方呢？输出如下命令后回车:

```
crontab -e
```

```
执行这个命令后，会打开了个vi编辑器，我们在里面，输入相应的计划任务，然后ESC，按wq保存退出，计划任务就生效了
```

```
下面我们列举一些实例:
# 每一分钟执行一次 ls
* * * * * ls

# 每五分钟执行一次 ls
*/5 * * * * ls

# 每小时的 30分钟，执行一次ls
30  * * * * * ls

# 每天凌晨1点20分，执行一次ls
20  1  *  *  *  ls

# 每周1，凌晨2点20分执行一次ls
20 2 * * 1  ls
```





