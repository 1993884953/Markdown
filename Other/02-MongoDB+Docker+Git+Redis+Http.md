# HTML

## 第一个HTML页面

建议开发环境Chrone + visual Studio Code,标准html5模板如下:

```html
<!DOCTYPE html>
<html>
    <head>
        <mate charset="utf-8">
        <title>HTML</title>
    </head>
        <h1>hellow world<h1>
    <bady>
    </bady>
</html>
 HTML标签
HTML元素(Element)通过标签的形式书写，标签内可包含属性(Attribute)
●属性的名称后写- -个等号，等号后是属性值，用引号包围(双引号或单引号均可)
●在属性与元素名称之间需要有空格，多个属性之间也需要有空格
```




| 元素名称          | 描述                           | 重要属性                                                     |
| :---------------- | ------------------------------ | ------------------------------------------------------------ |
| fieldset          | 框线                           |                                                              |
| h1-6              | 标题                           |                                                              |
| p                 | 段落                           |                                                              |
| br                | 换行                           |                                                              |
| b                 | 粗体                           |                                                              |
| i                 | 斜体                           |                                                              |
| ul、li            | 无序列表                       |                                                              |
| ol、li            | 有序列表                       |                                                              |
| dl、dt、dd        | 定义列表                       |                                                              |
| table、tr、td、th | 表格                           | border  框线，colspan，rowspan                               |
| img               | 图片                           | src，width，height，title，alt                               |
| a                 | 超链接                         | href 新建页面，target  链接                                  |
| form              | 表单                           | action 提交，method  （get /post浏览器隐藏），entype         |
| input             | 输入控件                       | name，type 类型，value 可改值，placeholder 隐藏提示、id、readonly 只读状态，disabled 禁用，checked选中 |
| label             | 标记                           | for                                                          |
| select、option    | 选择控件                       | name、value、selected                                        |
| textarea          | 多行文本键                     | name、rows、cols                                             |
| button            | 按钮                           |                                                              |
| div               | 将不同的内容分隔开（独占一行） | class、style                                                 |
| span              | 将不同的内容分隔开（行类）     |                                                              |



## input的常用type值

| type值   | 描述     | 注意事项                                    |
| -------- | -------- | ------------------------------------------- |
| text     | 账号框   |                                             |
| password | 密码框   |                                             |
| radio    | 单选按钮 | 同一组radio的name相同                       |
| checkbox | 复选框   |                                             |
| file     | 文件选择 | method="post"  entype="multipart/form-data" |
| hidden   | 隐藏     |                                             |
|          |          |                                             |

## 相对路径

./当前目录

../上级目录

## HTML 实体符号

| 显示结果 | 描述              | 实体名称 | 实体编号 |
| -------- | ----------------- | -------- | -------- |
|          | 空格              | &nbsp；  | &#160 ;  |
| <        | 小于号            | &lt ;    | &#60 ;   |
| >        | 大于号            | &gt ;    | &#62 ;   |
| &        | 和号              | &amp ;   | &#38 ;   |
| "        | 双引号            | &quot ;  | &#34 ;   |
| '        | 单引号            | &apos ;  | &#39 ;   |
| ©        | 版权（copyright） | &copy ;  | &#169 ； |

# CSS基础入门



## ⼀、基础语法 

Cascading Style Sheets 层叠样式表，简称CSS，⽤于对⽹⻚的样式进⾏调整 

CSS基础语法 代码规范 不区分⼤⼩写，推荐⽤⼩写 每条⽤英⽂分号隔开，简单的规则可以合并为⼀⾏ 注释： /* */

        <style type="text/css">
         选择器 {
         属性1: 值1;
         属性2: 值2;
         }
        </style>

> 代码规范：推荐⽤⼩写 每条⽤英⽂分号隔开；简单的规则可以合并为⼀⾏ ；注释： /* */

## ⼆、常⽤的样式

### 颜⾊

```color 
     color
     opacity: 0.5 透明级别
```

### 字体

``` 
    font-size: 		字体⼤⼩
    font-weight: 粗细 bold(粗体)
    font:bold 12px/1.5 宋体; (缩写时font-size和font-family是不可忽略的，例如"12px 宋体")
        粗体 12px ⾏⾼为 字体的1.5倍 宋体
```

### 文本 

``` 
    line-height:25px;
    text-align:left/right/center 				对齐方式（居中，居左，居右）
    align-items: center;						元素居中
    text-decoration:underline/line-through/none ⽂本修饰：下划线、删除线、⽆
    text-shadow: 4px 4px 0 red 					阴影偏移(上右下左)
    text-indent:2em 							⽂本向右缩进两个汉字宽度
    letter-spacing:3px; 						⽂字之间距离
    word-spacing:20px;						    英⽂单词之间的间隔
    white-space:nowrap 							(强制不换⾏) 规定如何处理空⽩
    word-break:break-all;						单词超出自动换行
```

### 背景

``` 
    background-color	（背景颜色）rgb(x,y,z) #f8ead1 进制
    background-image	（背景图片）
    (background: url(image/logo.png) no-repeat;)
    background-repeat:repeat-x|repeat-y|no-repeat
    background-position:
        -20px 0px
        30% 50%
        left | center | right | top | bottom
    background:red url(../imgs/bg.png) repeat-x top
```

#### background-size

值为cover、100%和contain的区别

正如属性意义一样，三者都是来定义背景图显示尺寸大小的，但是三者还是有一点区别的：

```
cover：是按照等比缩放铺满整个区域。如果显示如果显示比例和显示区域的比例相差很大某些部分会不显示，比如长度比宽度大很多，则宽度左侧会有一部分不显示。

100%：长宽100%显示，可能会拉升图片。

contain：也是等比缩放，按照某一边来覆盖显示区域的，会有白边
```

#### background-repeat

```
background-repeat：repeat ，也就是全部覆盖
background-repeat:repeat-x; 是只是横向的
background-repeat:repeat-y;只是 纵向的
background-repeat:no-repeat; 不重复
```

### 边框

``` 
    border-width			
    border-style
        none|solid|dashed    {实线，虚线}
    border-color
    border-top|right|bottom|left
    border:1px solid red;
    border-top:1px solid red;
    border-radius: 5px;      （圆角）

```

### ⽤户界⾯ 

``` 
    cursor:pointer ⿏标⼩⼿
    outline:2px solid #f00
    zoom:1;	
```

### 表格 

``` 
	border-collapse：collapse 边框合并在⼀起，实现单线边框
```

### 列表样式 

``` 
    list-style-type:none|disc实圆|circle空圆|square实正⽅|decimal数字    list-style:none				去除类型
```

### 尺⼨与补⽩

``` 
width	（宽度）    
height	（高度）					    
	min-height    max-height    min-width    min-height        
外间距margin 				    	
	# 调节边距    margin-top[right/bottom/left] 		
	#上边距    margin:5px 10px 15px 20px; 			
	#上右下左    margin: 0 auto;						
	#自动        
内填充padding    padding-top|right|bottom|left    
padding:0px 5px 10px 15px;        
	实际占位：元素⼤⼩+填充+边框+边距
```

## 三、元素选择符

``` 
*标签选择符(元素选择器)    
*类选择符(同⼀元素，可以指定多个className)    
*ID选择符(注意⻚⾯ID的唯⼀性)    
*关系选择符    	
	包含选择符(E F)    	⼦选择(E>F)    
*伪类选择符    	
a:hover{}光标移到超连接上(⿏标悬停时)    		
    font-weight: bold;（字体加粗）    		
    color:red； (字体变颜色)    			
还可以组合选择    	多个选择符之间，⽤逗号分隔    	    	
	class="first"    	.first    	ID ="first"    	#first
```

## 四、如何应⽤样式

``` 
三种⽅式    
1.内部样式表    
	<style></style>    
2.外部样式表(注意外部样式表中，使⽤图⽚时，以css⽂件所在⽬录为当前⽬录)    	
	<link rel="stylesheet" href="sytle.css" />    
3.⾏内样式		
	<div style=""></div>    
样式优先级        
	⾏内 > 内部 > 外部 (就近原则)        
ID选择器 > 类选择器 > 标签选择器        
	!important 强制改变优先级
```

## 五、定位与布局

### 定位

``` 
position   absolute/relative/fixed
(绝对定位，相对自身定位)
z-index						(层级)
left
top
right
bottom

```

### 布局

``` 
    显示
        display:none	(不占位隐藏)	
                display： inline-block； （在一行里面的快捷元素）
                display:block   (将div中a，标签a成块级元素)
                display:flex         弹性布局
                justify-content: space-around; 居中分割
                flex:1
                
                display:flex; 				两端对齐
                align-items:center; 
                justify-content:space-between;
```

```
        visibility:hidden		（占位隐藏）
        overflow:hidden （超出内容隐藏）
    float浮动
        块级元素浮动后，失去独占⼀⾏的特性
        浮动元素将紧贴上⼀个同⽅向浮动或⽗级元素的边框，如果宽度不够将换⾏
        浮动元素将占据⾏内元素的空间

    清除浮动
    clear:left|right|both|none
```



> 弹性盒⼦(  Flex,box)

### 倒三角旋转属性

```
. calendar . month .icon {
display: inline-block;
width: 5px;
height: 5px;
border-right: 1px solid red;
border-bottom: 1px soLid red;
trans form: rotate ( 45deg) ;
}

```

### input图片插入

```
border: none;
outline: none;
background-image:url("./imgs/search/search.png") ;
background-repeat: no-repeat;
background-position: left;
background-size: 30px;
padding-left: 30px;
```

### 逐渐展开动画

```
transition: height .5s linear;
```

### 半透明模式

```
background: linear-gradient(red 10%, green 85%, blue 90%)
```

# Http 

## HTTP简介

HTTP协议（HyperText Transfer Protocol，超文本传输协议）是因特网上应用最为广泛的一种网络传输协议

HTTP协议是建立在TCP协议基础之上的，是一种`无状态`的协议，默认使用`80`端口

当我们在浏览器中，输入一个网址，按下回车之后，实际上就是浏览器给服务器发送了一个HTTP的`GET`请求

### TCP

传输控制协议（TCP，Transmission Control Protocol）是一种面向连接的、可靠的、基于字节流的传输层通信协议，由IETF的RFC 793 [1] 定义。

TCP旨在适应支持多网络应用的分层协议层次结构。 连接到不同但互连的计算机通信网络的主计算机中的成对进程之间依靠TCP提供可靠的通信服务。TCP假设它可以从较低级别的协议获得简单的，可能不可靠的数据报服务。 原则上，TCP应该能够在从硬线连接到分组交换或电路交换网络的各种通信系统之上操作。

### 发送请求给服务器

例如，我们访问`http://playground.it266.com/hello`页面，浏览器会显示 `Hello World!`

实际上，浏览器是将类似下面的`HTTP协议`内容，发给了服务器：

```http
GET /hello HTTP/1.0
Host: playground.it266.com
User-Agent: Mozilla/4.0(MSIE8.0;WindowsNT6.0)
```

### 服务器返回消息

服务器，则返回了类似如下信息：

```javascript
HTTP/1.1 200 OK
Server: nginx/1.18.0
Date: Sat, 17 Apr 2021 11:56:17 GMT
Content-Type: text/html; charset=UTF-8
Connection: close

<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
    <title>Hello</title>
</head>
<body>
    <h1>Hello World!</h1>
</body>
</html>
```

### 命令行操作

下载网址 http://eternallybored.org/misc/netcat/   netcat1.12版本

解压以后把nc.exe复制到C:windows/system32/

通过`nc`命令(或telnet命令)，我们可以向指定服务器，发送HTTP协议内容。使用下面的命令，连上服务器的80端口：

进入到存储文件的目录内

```javascript
 nc playground.it266.com 80
```

然后输入下面内容，最后按两次回车

```
GET /hello HTTP/1.0
Host: playground.it266.com
```

我们发送给服务器的信息中，第一行分为3段内容：

- GET    	/hello        HTTP/1.0
- 请求方式为 `GET`
- 请求URI为 `/hello`
- 协议版本为 `HTTP/1.0`

服务器返回的HTTP协议第一行，表示所使用HTTP协议的版本号和状态码，例如`HTTP/1.1 200 OK`，则表示版本为`HTTP/1.1`，状态码为`200`.

- HTTP/1.1 200 OK													 头信息
- Server: nginx/1.18.0                                                服务器信息
- Date: Sat, 17 Apr 2021 11:56:17 GMT                  服务器时间
- Content-Type: text/html; charset=UTF-8             响应内容的类型和字符编码方式
- Connection: close                                                    发送完数据后，连接将关闭

报文头信息后面，是一个空行，再往后是`报文主体`，浏览器会根据报文主体中的内容显示网页

## URL

### 定义

URL (Uniform Resource Locator,统一资源定位器），它是WWW的统一资源定位标志，就是指网络地址

### 组成结构

```ABAP
scheme:  // login:password  @  address :port  /path/to/resource  ?query_string   #fragment
```

### scheme(): (协议)

这个字段表示传输协议 

常见的协议有：

>file ：访问本机的文件
>
>ftp：访问ftp服务器的协议 
>
>https ：通过SSL协议的HTTP访问WEB服务器资源 
>
>mailto：访问资源属于电子邮箱地址，通过SMTP协议访问，打开当前计算机系统中默认的电子邮件客户端ed2k,flashget,thunde等，通过支持专用下载协议的p2p软件访问资源

**SSL**

(Secure Sockets Layer [安全套接字协议](https://baike.baidu.com/item/安全套接字协议)),及其继任者[传输层安全](https://baike.baidu.com/item/传输层安全)（Transport Layer Security，TLS）是为[网络通信](https://baike.baidu.com/item/网络通信/9636548)提供安全及[数据完整性](https://baike.baidu.com/item/数据完整性/110071)的一种安全协议。TLS与SSL在[传输层](https://baike.baidu.com/item/传输层/4329536)与[应用层](https://baike.baidu.com/item/应用层/16412033)之间对网络连接进行加密。

### //

URL层级URL标记符号

 根据RFC 1738规定的语法，在授权信息之前，每个层级结构的URL中都会包括固定的”//“符号

 非层级结构的URL：http

```
http://www.example.com
```

非层级结构的URL：mailto

```
非层级结构的URL不包含 //
<a href="mailto:1111111@qq.com"> 发送邮件</a>
```

### login:password

访问资源的身份验证的URL中,身份验证属于可选项,在向服务器申请资源时,在某些情况下,需要指定一个用户名和密码.如果没有身份验证字段,浏览器默认以匿名的方式访问网站.它与域名之间用@连接(如果有login:password才使用@符号)

### address

域名 完整的层级URL，必须有一个域名，ipv4或者IPV6地址作为服务器的位置。域名不区分大小写，ipv6需要括在方括号中

### :port

端口号 （默认为80） 基本上浏览器支持的协议都会关联的默认服务接口，不过默认接口可以在URL中进行修改

### /path/to/resource

（路径） URL的这部分被称为层级文件路径，这一结构源自于UNIX目录语义保留了对 /../ ,/ ./的支持

### ?query_string

 查询字符串是一个非必须的字段，只要负责将一系列非层级格式的任意参数传给服务器。可同时传递多个参数，参数之间用`&`符号连接，每个参数名与值用=隔开 

例子： 

```
www.baidu.com?uid=777&qqq=666
```

### \#fragment

 片段ID是应用有别于普通字符串 就是锚点，当你打开网站的某个连接的时候，自动跳到网站的某一个锚点（就是光标默认在哪里），该属性应用于客户端，并不会上传到服务器端

```http
以[http://www.example.com:80/news/index.html?id=250&page=1]
(http://www.example.com/news/index.html?id=250&page=1) 为例, 其中：

- http 是协议
- [www.example.com](http://www.example.com/) 是服务器域名(或IP地址)
- 80 是服务器上的默认网络端口号，默认80不显示
- /news/index.html 是路径（URI：直接定位到对应的资源）
- ?id=250&page=1 是查询参数 (QueryString)
```

### 特殊字符

需要编码 (urlencode)，常见特殊字符如下：

| 空格 | !    | #    | $    | %    | +    | @    | :    | =    | ?    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| %20  | %21  | %23  | %24  | %25  | %2B  | %40  | %3A  | %3D  | %3F  |

## 请求方法

### http1.0

HTTP 1.0版本中，定义了三种请求方法，分别是：

- GET: 用来向服务器请求数据
- HEAD: HEAD方法与GET几乎一样，区别在于使用HEAD方法时，服务器不返回报文主体，只返回头信息
- POST: 用来向服务器发送数据，例如提交一个活动报名表单

```javascript
<h1>技术交流活动报名表</h1>
<form method="POST"  action="http://playground.it266.com/signup">
    <div>姓名 <input name="name" type="text"></div>
    <div>邮箱 <input name="email" type="email"></div>
    <div><input type="submit" value="提交"></div>
</form>
```

我们点击表单的提交按扭时，浏览器向服务器发送的HTTP协议内容格式如下：

```javascript
POST /signup HTTP/1.0
Host: playground.it266.com
User-Agent: Mozilla/4.0(MSIE8.0;WindowsNT6.0)
Content-Type: application/x-www-form-urlencoded
Content-Length: 34

name=jack&email=jack%40example.com
```

表单中的内容，会被编码，然后放到请求头的后面，发送给服务器

`Content-Type`用于指定内容的编码类型，form表单对POST请求，编码方式默认使用`application/x-www-form-urlencoded`，如果需要使用其它编码方试，则通过`enctype`属性指定，例如通过表单上传文件，则需要使用`enctype="multipart/form-data"`）

**enctype三种编码方式**

>application/x-www-form-urlencoded
>
>multipart/form-data  可以上传字符串 ,也可以上传文件,如图片 
>
>text/plain

由于使用的是`application/x-www-form-urlencoded`编码方式，所以特殊字符需要编码，例如`@`被编码为`%40`

`Content-Length`是请求体的长度，服务端可以根据这个值，判断数据是否已接收完整

### http1.1

HTTP1.1版本,新增了五个请求方式

- PUT:请求服务器存储一个资源

- DELETE:请求服务器删除标识的资源

- OPTIONS:请求查询服务器的性能,或者查询与资源相关的选项和需求

- TRACE:请求服务器回收到的请求信息,主要用于测试或诊断

- CONNECT:保留将来使用


方法名称是区分大小写的。当某个请求所针对的资源不支持对应的请求方法的时候，服务器应当返回状态码405（Method Not Allowed），当服务器不认识或者不支持对应的请求方法的时候，应当返回状态码501（Not Implemented）。

HTTP服务器至少应该实现GET和HEAD方法，其他方法都是可选的。当然，所有的方法支持的实现都应当匹配下述的方法各自的语义定义。此外，除了上述方法，特定的HTTP服务器还能够扩展自定义的方法。例如PATCH（由 RFC 5789 指定的方法）用于将局部修改应用到资源。

## 状态码

所有HTTP响应的第一行都是状态行，依次是当前HTTP版本号，3位数字组成的状态代码，以及描述状态的短语，彼此由空格分隔。

>状态代码的第一个数字代表当前响应的类型：
>
>1xx消息——请求已被服务器接收，继续处理 
>
>2xx成功——请求已成功被服务器接收、理解、并接受 
>
>3xx重定向——需要后续操作才能完成这一请求 
>
>4xx请求错误——请求含有词法错误或者无法被执行 
>
>5xx服务器错误——服务器在处理某个正确请求时发生错误
>
>虽然 RFC 2616 中已经推荐了描述状态的短语，例如"200 OK"，"404 Not Found"，但是WEB开发者仍然能够自行决定采用何种短语，用以显示本地化的状态描述或者自定义信息。

|      | 分类                           | 分类描述                         |
| ---- | ------------------------------ | -------------------------------- |
| 1XX  | Informational(信息性状态码)    | 接收的请求正在处理               |
| 2XX  | Success(成功状态码)            | 请求正常处理完毕                 |
| 3XX  | Redirection(重定向状态码)      | 需要进一步的操作以完成请求       |
| 4XX  | Client Error(客户端错误状态码) | 请求包含语法错误或无法完成请求   |
| 5XX  | Server Error(服务端错误状态码) | 服务器在处理请求的过程发生了错误 |

### 

常用状态码：

```ABAP
101： 转换协议（例如WebScoket连接成功后需要切换协议）
200： 服务端成功响应
301： 永久重定向


302： 临时重定向
401： 未授权（需要登录）
403： 请求被拒绝（权限不够）
404： 服务端找不到请求的资源
500： 处理请求时出错
503： 服务不可用
504： 网关超时  (服务器作为网关或代理，从上游服务器收到无效响应。)
```

## 实现HttpServer

tcp包的最大传输单元1500字节

### get与post的区别

get请求传递的参数时在url地址中

post请求传递的参数在正文中

### 重定向

```
HTTP/1.1 302
Location:https://www.baidu.com/
```

### 设置COOKIE

```http
HTTP/1.1 302
Set-Cookie: SESSID=ff21f3da21;
max-age=86000; 
path=/admin
Location:https:www.baidu.com/
```

>path:请求/admin的时候把SESSID发送给服务器
>
>max-age:SESSID保存的时间

### 控制台post请求

```
curl -XPOST -i http://loacalhost:8200 -d "username=jack&password=123456"
```



### 无状态

服务端没有记录客户端记录,即没有保留客户端状态,每一次请求都是全新的.

## 实现一个 HTTP Server

node.js fs模板

curl --http0.9   "http://localhost:8200/hello.html"

实现一个 HTTP Server，监听8001端口，客户端使用`curl`、`postman`或`浏览器`来交互

GET [http://localhost:8001](http://localhost:8001/)

```
响应: 
    HTTP状态码:200 
    Content-Type: text/html  
    内容: <h1>welcome</h1><a href="/admin">进入管理后台</a>
```

GET http://localhost:8001/admin

```
找不到sessid时
响应:
    HTTP状态码:302
    让浏览器转到 /login
```

GET http://localhost:8001/login

```
显示一个登录表单，输入用户名username 和密码password，点击提交按扭，将信息以post方式，提交到http://localhost:8001/login
```

POST http://localhost:8001/login

```
获取 body中的 username 和 password，如果username值为admin 密码为123456，说明登录成功
登录成功后，随成一个随机字符串(假设为5d9d6922a7fee) ，用这个字符串作为文件名，将username的值写入该文件中
在浏览器cookie中放入刚生成的随机字符串格式为 SESSID=5d9d6922a7fee ，并让浏览器重定向到/admin
```

GET http://localhost:8001/admin

```
如果cookie中存在 SESSID，如果存在，将对应的内容取出来， 检查是否存在对应的文件，如果不存在，跳转到 /login，如果存在，则显示该文件中的内容在浏览器上
```

11min

```js
const net = require('net')

var fs = require('fs'); // 引入fs模块

const port = 8001 // 端口

const server = net.createServer()

server.listen(port) // 监听8000端口

// 全局唯一标识符（GUID,UUID）的方法
function guid() {
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
        var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}

// 查找头信息中的SESSID
function findSESSID(header) {
    let SESSID = ""
    for (const data of header) {
        if (data.includes("Cookie:")) {

            // Cookie:lang=zh-CN; SESSID=qwiiiiiiiiiiiiiihsjkadksnakdbjwvdwvgds;

            let cookieDataString = data.split(":")[1]
            let cookieDataArr = cookieDataString.split(";");
            for (const cookieData of cookieDataArr) {
                if (cookieData.trim().startsWith("SESSID=")) { // 以SESSID=开头
                    SESSID = cookieData.split("=")[1];
                    break
                }
            }
        }
    }
    return SESSID
}

server.on("connection", function (socket) {
    // socket添加接收到数据事件
    socket.on("data", function (data) {
        console.log(data.toString())
        let header = data.toString().split("\r\n") 
        
        // header="请求方式 url HTTP/1.0"

        let method = header[0].split(" ")[0]  // 请求方法
        let url = header[0].split(" ")[1]  // url
        
        // 首页
        if (url === "/") {
            socket.write(`HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=UTF-8\r\n\r\n<h1>welcome</h1><a href="/admin">进入管理后台</a>`)
            socket.end()
            return
        }
 
        // 后台管理
        else if (url === "/admin" && method.toLocaleUpperCase() === "GET") {
            // 查找头信息中的SESSID 
            let SESSID = findSESSID(header)

            // 不存在重定向登录页
            if (!SESSID) {
                socket.write(`HTTP/1.1 302\r\nLocation:/login`)
                socket.end()
                return
            }
            // 读取文件
            fs.readFile(`./${SESSID}.txt`, 'utf-8', function (err, data) {
                // 报错返回登录页
                if (err) {
                    console.log("找不到文件");
                    socket.write(`HTTP/1.1 302\r\nLocation:/login`)
                    socket.end()
                    return
                }

                // 返回文件内容至客户端
                socket.write(`HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=UTF-8\r\n\r\n<h1>${data}</h1>`)
                socket.end()
                return
            });
        }

        // 登录验证
        else if (method === "POST" && url === "/login") {
            let paramsArr = data.toString().split("\r\n\r\n").pop().split("&")
            username = paramsArr[0].split("=")[1]
            password = paramsArr[1].split("=")[1]
            // 失败返回登录页
            if (username !== "admin" || password !== "123456") {
                socket.write(`HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=UTF-8\r\n\r\n
                <h1>用户名和密码不匹配</h1>
                <form action="http://localhost:8001/login" method="POST">
                <label name="username">用户名称：<input name="username" type="text"/></label>
                <br>
                <label name="password">用户密码：<input name="password" type="password"/></label>
                <br>
                <input type="submit">
                </form>`)
                socket.end()
                return
            }

            // 成功则写入文件并重定向到admin
            let fileName = guid();
            fs.writeFile(`./${fileName}.txt`, username, function (err) { if (err) { throw err } })
            console.log("fileName", fileName);
            socket.write(`HTTP/1.1 302\r\nContent-Type: text/html; charset=UTF-8\r\nSet-Cookie: SESSID=${fileName}; max-age=86400;\r\nLocation:/admin`)
            socket.end()
            return
        }
	
        // 登录界面
        else if (method === "GET" && url === "/login") {
            socket.write(`HTTP/1.1 200 OK\r\nContent-Type: text/html; charset=UTF-8\r\n\r\n
            <form action="http://localhost:8001/login" method="POST">
                <label name="username">用户名称：<input name="username" type="text"/></label>
                <br>
                <label name="password">用户密码：<input name="password" type="password"/></label>
                <br>
                <input type="submit">
            </form>`)
            socket.end()
                return
        }
    })
})
```

## java操作http

```java
package com;

import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Objects;

public class Server {
    public Server() {
        try {
            ServerSocket ss = new ServerSocket(8000);
            System.out.println("The server is waiting your input...");
            while (true) {
                Socket socket = ss.accept();

                BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
                String line = in.readLine();

                System.out.println("you input is : " + line);
                //out.println("you input is :" + line);

                String method = line.split(" ")[0];  // 请求方法
                String url = line.split(" ")[1];  // 请求方法

                if (Objects.equals(method, "GET") && Objects.equals(url, "/")) {
                    out.write("HTTP/1.1 200 OK\n" +
                            "Content-Type: text/html; charset=UTF-8\n" +
                            "\r\n" +
                            "<h1>welcome</h1><a href=\"/admin\">进入管理后台</a>"
                    );
                }
                

                out.close();
                in.close();
                socket.close();

                if (line.equalsIgnoreCase("quit") || line.equalsIgnoreCase("exit")) {
                    break;
                }
            }

            ss.close();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        new Server();
    }
}  
```

### 随机生成uuid

```
    //随机生成32位UUID
    public static String  guid(){
        return UUID.randomUUID().toString();
       
    }
```

```
package com;

import java.util.UUID;
/**
 * 通过UUID随机生成36位、32位唯一识别码（唯一字符串）
 * @author 【J.H】
 *
 */

public class Test {

    public static void main(String[] args) {
        int i = 0;
        while (i<10) {
            String a = UUID.randomUUID().toString();
            System.out.println(a);
            System.out.println(a.length());
            String b = a.replaceAll("-","");
            System.out.println(b);
            System.out.println(b.length());
            System.out.println("*******************************");
            i++;
        }
    }
}
```



### 写入读取文件

```
package com;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.UUID;

public class ObjectFileTrans {
    /*文件写入路径*/
    public static final String LOACLFILEPATH_STRING = "./";

    //    /*文件写入日期*/
//    static Date date = new Date();
//    static SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyyMMddHH");
//    static String nowTimeHour = simpleDateFormat.format(date);
//
//随机生成32位UUID
    public static String guid() {
        return UUID.randomUUID().toString();
    }

    /*文件写入*/
    public static void writeObject(String infoStr, String dealTime) {
        try {
            File inforFile = new File(ObjectFileTrans.LOACLFILEPATH_STRING + dealTime + ".txt");
            FileWriter fileWriter = new FileWriter(inforFile, true);
            fileWriter.write(infoStr);
            fileWriter.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    /*文件读取*/
    public static String readObject(String textName) {
        StringBuffer buffer = new StringBuffer();
        try {
            /*文件读取路径*/
            FileReader fileReader = new FileReader(".\\"+textName +".txt");
            /*文件读取缓冲区*/
            char[] chs = new char[1024];
            while (fileReader.read(chs) != -1) {
                System.out.println(chs);
                buffer.append(chs);

            }
            System.out.println();
        } catch (IOException e) {
//            e.printStackTrace();
            System.out.println("false");
        }
        return buffer.toString();
    }

    public static void main(String[] args) {
        ObjectFileTrans objectFileTrans = new ObjectFileTrans();
        /*文件读取测试*/
        String infoString = objectFileTrans.readObject("textName");
        /*文件写入测试*/
        objectFileTrans.writeObject(infoString, "textName");

    }

}
```

```
获取浏览器信息


package com;


import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.ArrayList;
import java.util.List;

public class App {
    public static final int port = 8000;


    public static void main(String[] args) {
        try {
            // 创建服务端socket
            ServerSocket serverSocket = new ServerSocket(port);


            //循环监听等待连接
            while (true) {
                //监听客户端
                // 创建客户端socket
                Socket socket = serverSocket.accept();
                DataInputStream input = new DataInputStream(socket.getInputStream());
//                System.out.println(input.readLine());
                do {
                    String line = input.readLine();
                    System.out.print("server said:");
                    System.out.println(line);
                } while (true);

            }

        } catch (IOException e) {
            e.printStackTrace();
        }

    }

}

```



# Redis基础

## 一.Redis安装

Redis 是一个基于**内存**的分布式**键值对(**Key-Value)存储数据库，使用C语言开发，性能优良，互联网项目中大量使用，这一节我们的任务是在Linux下编译安装Redis

```java
$ wget https://download.redis.io/releases/redis-6.2.4.tar.gz
$ tar xzf redis-6.2.4.tar.gz
$ cd redis-6.2.4
$ make
$ ./src/redis-server    # 启动服务
$ ./src/redis-cli       # 进入控制台
redis> set foo bar
OK
redis> get foo
"bar"
```

## 二.Redis数据类型

掌握以下数据类型相关命令：

- String 字符串
- Hash 散列 （类似Map）
- List 列表
- Set 集合（不重复）
- Sorted Set 有序集合

### String 常用命令：

```javascript
redis> set name jack
redis> get name
redis> setnx                     # 不存在才写入 (not exist)
redis> setex name 5 jack         # 指定过期时间  expires
redis> incr num                  # 将 num 自增 1（不存在 num 时，当作 0 处理，自增后是 1） increase
redis> incrby num 3              # 将 num 自增 3
```

### Hash 常用命令：

```redis
redis> hset user1 name jack
redis> hset user1 age 18

redis> del user1  删除user1

redis> hget user1 name
redis> hget user1 age

redis> hmset user2 name lily age 18
redis> hmget user2 name age

redis> hgetall user2

redis> HINCRBY user2 age 1   指定增量
```

#### Redis Hincrby

Redis Hincrby 命令用于为哈希表中的字段值加上指定增量值。

增量也可以为负数，相当于对指定字段进行减法操作。

如果哈希表的 key 不存在，一个新的哈希表被创建并执行 HINCRBY 命令。

如果指定的字段不存在，那么在执行命令前，字段的值被初始化为 0 。

对一个储存字符串值的字段执行 HINCRBY 命令将造成一个错误。

本操作的值被限制在 64 位(bit)有符号数字表示之内。

### List 常用命令：

```javascript
redis> lpush mylist hello     # 从左放入
redis> lpush mylist world

redis> llen mylist            # 查看长度
redis> lrange mylist 0 -1     # 查看全部

redis> rpush mylist haha      # 从右放入
redis> rpop mylist            # 从右取出
redis> lpop mylist			   # 从左取出

redis> ltrim mylist 0 2       # 只留下左边的 3 条（下标 0 到 2）
```

### Set 常用命令： 

（Set是无序的，数据不能重复，List是有序的，数据可重复）

```javascript
redis> sadd myset1 a
redis> sadd myset1 b
redis> sadd myset1 c

redis> smembers myset1    # 查看全部

redis> srem myset1 b      # 删除

redis> spop  myset1       # 随机出一个

redis> sdiff  set1 set2 setn  # 差集   difference
redis> sinter  # 交集    intersection
redis> sunion  # 并集		Union
```

### Sorted Set 常用命令：

 （可排序 Set 集合)

#### Redis Zincrby 命令

Redis Zincrby 命令对有序集合中指定成员的分数加上增量 increment

可以通过传递一个负数值 increment ，让分数减去相应的值，比如 ZINCRBY key -5 member ，就是让 member 的 score 值减去 5 。

当 key 不存在，或分数不是 key 的成员时， ZINCRBY key increment member 等同于 ZADD key increment member 。

当 key 不是有序集类型时，返回一个错误。

分数值可以是整数值或双精度浮点数。

## 三.java中操作Redis

掌握在 SpringBoot 中使用 RedisTemplate 操作Redis，如果你在Windows下，可以直接使用Windows移植版本 https://github.com/tporadowski/redis/releases

代码参考： http://www.daimaku.net/post/view/12613

使用postman http://localhost:8080/test

需要打开D盘 Redis-x64-5.0.14 文件内的 redis-cli.exe 与 redis-server.exe

**添加依赖**

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

**配置类**

```java
import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.JsonTypeInfo;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.jsontype.impl.LaissezFaireSubTypeValidator;
import org.springframework.cache.annotation.CachingConfigurerSupport;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.*;
import org.springframework.data.redis.serializer.*;

@Configuration
public class RedisConfig extends CachingConfigurerSupport {

    /**
     * RedisTemplate 默认配置的是使用 Java JDK 的序列化，如果是对象，在Redis里查看时不直观
     * key 使用 String， value 列序列化 json
     */
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {

        RedisTemplate<String, Object> template = new RedisTemplate<>();

        // 连接工厂
        template.setConnectionFactory(factory);

        // key 使用 StringRedisSerializer 来序列化
        StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
        template.setKeySerializer(stringRedisSerializer);
        template.setHashKeySerializer(stringRedisSerializer);

        // value 采用 json 序列化
        Jackson2JsonRedisSerializer<Object> jsonRedisSerializer = jsonSerializer();
        template.setValueSerializer(jsonRedisSerializer);
        template.setHashValueSerializer(jsonRedisSerializer);

        template.afterPropertiesSet();

        return template;
    }

    /**
     * 序列化器
     */
    private Jackson2JsonRedisSerializer<Object> jsonSerializer() {

        Jackson2JsonRedisSerializer<Object> jsonRedisSerializer = new Jackson2JsonRedisSerializer<>(Object.class);

        // 对象映射
        ObjectMapper om = new ObjectMapper();

        // 序列化所有字段和修饰符范围
        om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);

        // 将类名序列化到json中 {"@class":"model.User", "id":"1", "name":"hello"}
        // 否则不能反序列化 {"id":"1", "name":"hello"}
        om.activateDefaultTyping(LaissezFaireSubTypeValidator.instance, ObjectMapper.DefaultTyping.NON_FINAL, JsonTypeInfo.As.PROPERTY);

        jsonRedisSerializer.setObjectMapper(om);

        return jsonRedisSerializer;
    }
}
```

**数据操作示例**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.HashMap;
import java.util.Map;

@RestController
public class TestController {

    @Autowired
    private RedisTemplate<String, Object> redisTemplate;

    @GetMapping("/test")
    public String test() {

        // string
        redisTemplate.opsForValue().set("foo", "hello");
        redisTemplate.opsForValue().set("bar", 100);

        String foo = (String) redisTemplate.opsForValue().get("foo");
        System.out.println(foo);  // hello

        String noData = (String) redisTemplate.opsForValue().get("noData");
        System.out.println(noData); // null

        redisTemplate.opsForValue().increment("bar");
        int bar2 = (int) redisTemplate.opsForValue().get("bar"); // 101
        System.out.println(bar2);

        // hash
        User user = new User(3, "Jack");
        redisTemplate.opsForValue().set("user1", user);
        User obj = (User) redisTemplate.opsForValue().get("obj");
        System.out.println(obj);  //null

        Map<String, Object> map = new HashMap<>();
        map.put("name", "Mary");
        map.put("age", 18);
        redisTemplate.opsForHash().putAll("user2", map);

        Map<Object, Object> user3 = redisTemplate.opsForHash().entries("user2");
        System.out.println(user3); 

        // list
        redisTemplate.opsForList().leftPush("names", "jack");
        redisTemplate.opsForList().leftPush("names", "mary");
        redisTemplate.opsForList().leftPush("names", "lily");


        System.out.println(redisTemplate.opsForList().rightPop("names"));  // jack
        System.out.println(redisTemplate.opsForList().rightPop("names"));  // mary
        System.out.println(redisTemplate.opsForList().rightPop("names"));  // lily
        System.out.println(redisTemplate.opsForList().rightPop("names"));  // null


        return "ok";
    }

    public static class User {
        private int id;
        private String name;

        public User() {
        }

        public User(int id, String name) {
            this.id = id;
            this.name = name;
        }

        @Override
        public String toString() {
            return "User{" +
                    "id=" + id +
                    ", name='" + name + '\'' +
                    '}';
        }

        public int getId() {
            return id;
        }

        public void setId(int id) {
            this.id = id;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
}
```

**连接配置信息**

```java
# Redis服务器地址 (默认127.0.0.1)
spring.redis.host=127.0.0.1
# Redis服务器连接端口 (默认6379)
spring.redis.port=6379
# Redis数据库索引 (默认为0)
spring.redis.database=0
# Redis服务器连接密码 (默认为空)
spring.redis.password=
```

## 四.秒杀

在设计秒杀业务之前，我们先了解一下数据库的性能

MySQL处理数据的性能 (以一台4核CPU、8G内存、SSD硬盘为例)：

- 最大连接数约：6000
- 最大IOPS约： 20000

`IOPS`：(Input/Output operations Per Second,既每秒处理I/O的请求次数)

如果我们想要得到更好的性能，就可以使用Redis这样的内存数据库，来承载高并发。单机Redis就可以轻松达到10万QPS

设计基于Redis的秒杀业务场景，核心思想为：

- 将需要秒杀的商品id和库存数量，在秒杀开始前存入Redis中
- 秒杀过程中，使用 `incrby` 相关原子自增（自减）指令，扣减库存
- 将已参加秒杀的用户id，存入 `set` 中，可以高效的防止同一用户多次抢购
- 将已抢购成功的数据，放入 list 中
- 异步将Redis中的数据，存入MySQL，生成订单



# Git

## 一、git基础命令

```json
git --version    查看版本
useradd -m git   创建用户
passwors git      密码
```

```json
git init --bare project.git				//初始化仓库
git clone git@192.168.88.176:project.git     //仓库克隆回来

git clone http://xueba.it266.com:3000/ethan/cashier-h5
  //克隆地址

git config --global user.email "1993884953@qq.com"
git config --global use.name "cheng"

git status   
git add .    添加
git commit -m "cheng“   提交
git push origin master    提交远端仓库

git pull origin master    远程仓库拉取回来
```

![image-20220402135402542](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140171.png)

## 二、命令进阶

![image-20220909120600832](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140172.png)

查看本地分支

```shell
git branch
```

查看远程分支

```shell
git branch -r
```

删除本地`test`分支

```shell
git branch -D master
```

远程删除git服务器上的`tes

```shell
git push origin -d test
```

拉取远程`test`分支并创建本地分支

```shell
git fetch
git branch -r
git checkout -b dev origin/dev
```

切换到某个commit Id

```shell
git log                      ## 找到你的日志commit号 例如22dfb
git checkout 22dfb           ## 切换到这个commit下
git checkout -b dev 22dfb    ## 在本地新建一个dev分支，并切到22dfb
git push origin dev          ## 将本地dev分支推到远程
```

## 二、流程

github **建仓库**

```json
/*报错应该是代理的问题，可以参考-----异常错误、五*/ 
```

**clone**

>   1、初始化仓库

```json
git init --bare project.git
```

>   2、git clone 

```json
git clone https://github.com/1993884953/fictional-train.git
```

```json
    /*不成功则更换代理*/
git config --global http.https://github.com.proxy socks5://127.0.0.1:10809
git config --global https.https://github.com.proxy socks5://127.0.0.1:10809
```

```json
/*取消代理*/
git config --global --unset http.proxy
git config --global --unset https.proxy
```

**pull**

>   查看有无其他更新-------无错误直接进行push

```json
git pull origin master
```

```json
/*先检查是否进入工作目录，有错误进行*/ 
git remote rm origin
git remote add origin XXXX  
/*返回空值设置用户*/ 
git config --global user.email "1993884953@qq.com"
git config --global use.name "cheng"
```

**push**

>   push上传文件

```json
git status   
git add .   
git commit -m "cheng"
git push origin master  
```

```json
git remote set-url origin https://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@github.com/1993884953/fictional-train.git
```

```
git remote set-url origin https://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@github.com/1993884953/notes.git/
```



## Git SSL公钥密钥生成

步骤：

```
git config --global credential.helper 'cache --timeout=360000'
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
```



```
git config --global user.name "1993884953" 
git config --global user.email "1993884953@qq.com"
ssh-keygen -t rsa -C  "1993884953@qq.com"    
```

\1. git config --global user.name "1993884953"  （写用户名）

\2. git config --global user.email "1993884953@qq.com"  （ 写用户邮箱）

\3. ssh-keygen -t rsa -C  "1993884953@qq.com"       （写上邮箱） 生成密钥

4.运行命令: 生成对应的key，然后系统会有英文提示你输入文件名，密码，确认密码，可以全部ente

5.结束后，对应的key就生成到.ssh目录了

*查看秘钥文件夹位置（路径地址）*

\1. 输入 cd ~/.ssh 进入到.ssh 文件夹

2.输入 ls 查看.ssh 文件夹里面有 id_rsa id_rsa.pub known_hosts 文件

3.输入pwd 查看.ssh 文件路径位置地址

找到.ssh目录将生成的名为 **id_rsa.pub** 的[公钥](https://so.csdn.net/so/search?q=公钥&spm=1001.2101.3001.7020)复制粘贴到GitHub上增加一串密钥

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181136527.png)

 

 

 

如果出错---执行Git命令时出现各种 [SSL](https://so.csdn.net/so/search?q=SSL&spm=1001.2101.3001.7020) certificate problem 的解决办法：

缺失一些环境输入命令 git config --global http.sslVerify false

把忽略证书错误的设置限定在特定的仓库，避免扩大该设置的适用范围而引起的潜在安全风险。

# Docker容器化技术

## 1.Docker简介

Docker 是一个开源的应用容器引擎，基于 [Go 语言](https://www.runoob.com/go/go-tutorial.html) 并遵从 Apache2.0 协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

### Docker 的优点

Docker 是一个用于开发，交付和运行应用程序的开放平台。Docker 使您能够将应用程序与基础架构分开，从而可以快速交付软件。借助 Docker，您可以与管理应用程序相同的方式来管理基础架构。通过利用 Docker 的方法来快速交付，测试和部署代码，您可以大大减少编写代码和在生产环境中运行代码之间的延迟。

#### 1、快速，一致地交付您的应用程序

Docker 允许开发人员使用您提供的应用程序或服务的本地容器在标准化环境中工作，从而简化了开发的生命周期。

容器非常适合持续集成和持续交付（CI / CD）工作流程，请考虑以下示例方案：

- 您的开发人员在本地编写代码，并使用 Docker 容器与同事共享他们的工作。
- 他们使用 Docker 将其应用程序推送到测试环境中，并执行自动或手动测试。
- 当开发人员发现错误时，他们可以在开发环境中对其进行修复，然后将其重新部署到测试环境中，以进行测试和验证。
- 测试完成后，将修补程序推送给生产环境，就像将更新的镜像推送到生产环境一样简单。

#### 2、响应式部署和扩展

Docker 是基于容器的平台，允许高度可移植的工作负载。Docker 容器可以在开发人员的本机上，数据中心的物理或虚拟机上，云服务上或混合环境中运行。

Docker 的可移植性和轻量级的特性，还可以使您轻松地完成动态管理的工作负担，并根据业务需求指示，实时扩展或拆除应用程序和服务。

#### 3、在同一硬件上运行更多工作负载

Docker 轻巧快速。它为基于虚拟机管理程序的虚拟机提供了可行、经济、高效的替代方案，因此您可以利用更多的计算能力来实现业务目标。Docker 非常适合于高密度环境以及中小型部署，而您可以用更少的资源做更多的事情。



### Docker 包括三个基本概念:

- **镜像（Image）**：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
- **容器（Container）**：本质是进程,镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。



- **仓库（Repository）**：仓库可看成一个代码控制中心，用来保存镜像。

Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。

Docker 容器通过 Docker 镜像来创建。

容器与镜像的关系类似于面向对象编程中的对象与类。

## 2.Docker安装(linux)

[docker官网](https://docs.docker.com/engine/install/ubuntu/)

**要安装 Docker Engine，您需要以下 Ubuntu 版本之一的 64 位版本：**

- Ubuntu 小鬼 21.10
- Ubuntu 多毛 21.04
- Ubuntu 焦点 20.04 (LTS)
- Ubuntu 仿生 18.04 (LTS



**卸载旧版本**

> 旧版本的 Docker 被称为`docker`,`docker.io`或`docker-engine`. 如果安装了这些，请卸载它们：

```shell
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

**设置存储库**

> 1.更新`apt`包索引并安装包以允许`apt`通过 HTTPS 使用存储库：

```shell
$ sudo apt-get update

$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

> 2.添加 Docker 的官方 GPG 密钥：

```shell
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

> 3.使用以下命令设置**稳定**存储库。要添加 **nightly**或**test**存储库，请在以下命令中的单词之后添加单词`nightly`或`test`（或两者） 。[了解](https://docs.docker.com/engine/install/)[**夜间**](https://docs.docker.com/engine/install/)[和](https://docs.docker.com/engine/install/)[**测试**](https://docs.docker.com/engine/install/)[频道](https://docs.docker.com/engine/install/)。`stable`

```shell
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**安装 Docker 引擎**

> 更新`apt`包索引，安装*最新版本*的Docker Engine和containerd，或者进入下一步安装特定版本：

```shell
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

>  要安装*特定版本*的 Docker Engine，请在 repo 中列出可用版本，然后选择并安装一种。列出您的存储库中可用的版本：

```shell
 $ apt-cache madison docker-ce
```

> 使用第二列中的版本字符串安装特定版本，例如`5:18.09.1~3-0~ubuntu-xenial`.

```shell
$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io

sudo apt-get install docker-ce=5:20.10.17~3-0~ubuntu-focal docker-ce-cli=5:20.10.17~3-0~ubuntu-focal containerd.io
```

>  `hello-world` 通过运行映像来验证 Docker 引擎是否已正确安装

```shell
$ sudo docker run hello-world
#查看版本号
$ docker --version
#查看更多信息
$ docker info 
#查看帮助文档
$ docker --help 
```



```shell
#停止服务
$ service docker stop 
#开启服务
$ service docker start 
#重启服务
$ service docker restart
#如果不想被访问时自动启动服务
#sudo systemctl stop docker.socket
```

 

## 3.Docker镜像管理

[阿里云镜像加速器](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

```shell
#下载慢可以直接在控制台输入
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://ltxqztkw.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

[ubuntu镜像搜索地址](https://hub.docker.com/search?q=ubuntu&type=image)

```shell
#下载最新版本镜像
$ docker pull alpine
#获取指定版本镜像
#docker pull alpine:20.04 
```

```shell
#查看所有命令
$ docker image
```

```shell
#查看拉取的所有镜像
$ docker image ls
#等价于
$ docker images
```

```shell
#拉取测试镜像
$ docker image pull hello-world
#删除测试镜像
$ docker image rm hello-world
```

> 删除不成功

```shell
#1.查看正在使用的镜像容器号
# docker ps -a -q

#2.停止container，这样才能够删除其中的images：
#docker stop $(docker ps -a -q)

#3.如果想要删除所有container的话再加一个指令：
#docker rm $(docker ps -a -q)

#4.查看当前有些什么images    
#docker images

#通过image的id来指定删除谁
#docker rmi IMAGE_ID
#要删除全部image的话
#docker rmi $(docker images -q)
```



## 4.Docker容器管理

**获取container帮助**

```shell
$ docker container
```

```shell
#展示所用的容器
$ docker images
#让容器执行命令(如果容器不存在会直接拉取回来)
$ docker container run alpine echo "hello docker"
#可省略container
$ docker run alpine echo "hello docker"
#hello docker#(在镜像说打印的)

#列出所有容器
$ List containers

#删除容器
$ docker container rm CONTAINER_ID

#在终端ping百度
$ docker run alpine ping www.baidu.com
#-d 在后台运行
$ docker run -d alpine ping www.baidu.com

#查看正在运行的容器
$ docker ps

#会顶灯该等待10秒时间
$ docker stop CONTAINER_ID

#查看已保存的容器
$ docker ps -a

#运行已保存的容器
$ docker start CONTAINER_ID

#运行结束后自动删除这个容器
$ docker run --rm alpine echo "abc"
```

**docker container 常用命令**

> $ docker container

```http
Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Run a command in a new container
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes
```



## 5.Docker数据卷

**目录映射**

> -v 将物理机的目录映射到容器中去,实现文件的长久保存 

```shell
#--rm 容器不保存

$  docker run --rm -v /root:/data alpine touch /data/
#/root 冒号是物理机的文件路径
#/data 冒号后面是容器目录

#查看创建的文件
$  ls /root   #test.txt
```

**当前目录映射**

> "$(pwd)"

```shell
#获取当前所在目录
$ pwd  #/root

#$(pwd)--保存到当前目录,不用写绝对路径
$ docker run --rm -v $(pwd):/data alpine touch /data/test1.txt
#目录有空格,需要加上引号
$ docker run --rm -v "$(pwd)":/data alpine touch /data/test2.txt

#在当前目录成功创建文件
$ ls 	#test1.txt  test2.txt  test.txt
```

**只读挂载**

> "$(pwd)":/data:ro   :ro readonly 只读文件系统

```shell
#在容器目录后面加:ro 
$ docker run --rm -v "$(pwd)":/data:ro alpine touch /data/test2.txt

#touch: /data/test2.txt: Read-only file system#
```



## 6.Docker服务端口映射

[Nginx 的官方版本镜像](https://hub.docker.com/_/nginx)

**Supported tags and respective `Dockerfile` links**

- [`1.21.6`, `mainline`, `1`, `1.21`, `latest`](https://github.com/nginxinc/docker-nginx/blob/6f0396c1e06837672698bc97865ffcea9dc841d5/mainline/debian/Dockerfile)
- [`1.21.6-perl`, `mainline-perl`, `1-perl`, `1.21-perl`, `perl`](https://github.com/nginxinc/docker-nginx/blob/6f0396c1e06837672698bc97865ffcea9dc841d5/mainline/debian-perl/Dockerfile)
- [`1.21.6-alpine`, `mainline-alpine`, `1-alpine`, `1.21-alpine`, `alpine`](https://github.com/nginxinc/docker-nginx/blob/6f0396c1e06837672698bc97865ffcea9dc841d5/mainline/alpine/Dockerfile)
- [`1.21.6-alpine-perl`, `mainline-alpine-perl`, `1-alpine-perl`, `1.21-alpine-perl`, `alpine-perl`](https://github.com/nginxinc/docker-nginx/blob/6f0396c1e06837672698bc97865ffcea9dc841d5/mainline/alpine-perl/Dockerfile)
- [`1.20.2`, `stable`, `1.20`](https://github.com/nginxinc/docker-nginx/blob/b0e153a1b644ca8b2bd378b14913fff316e07cf2/stable/debian/Dockerfile)
- [`1.20.2-perl`, `stable-perl`, `1.20-perl`](https://github.com/nginxinc/docker-nginx/blob/b0e153a1b644ca8b2bd378b14913fff316e07cf2/stable/debian-perl/Dockerfile)
- [`1.20.2-alpine`, `stable-alpine`, `1.20-alpine`](https://github.com/nginxinc/docker-nginx/blob/b0e153a1b644ca8b2bd378b14913fff316e07cf2/stable/alpine/Dockerfile)
- [`1.20.2-alpine-perl`, `stable-alpine-perl`, `1.20-alpine-perl`](https://github.com/nginxinc/docker-nginx/blob/b0e153a1b644ca8b2bd378b14913fff316e07cf2/stable/alpine-perl/Dockerfile)

**下载镜像**

```shell
#nginx版本比较大,nginx:alpine版本只是操作系统不同
$ docker pull nginx:alpine

#出现REPOSITORY为nginx时表示下载成功
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        alpine    cc44224bfe20   2 months ago   23.5MB
alpine       latest    c059bfaa849c   3 months ago   5.59MB
```

**启动容器服务**

```shell
# nginx是一种服务,容器在启动后默认会启动nginx,nginx不会被退出,会一直提供服务,所以会卡住
$ docker run --rm nginx:alpine
```

> -d 以后台服务的方式运行镜像

```shell
#打印出容器完整的id,以后台的方式启用nginx容器
$ docker run -d --rm nginx:alpine
#f489b3f6d24cdc6f7df762552c79531645ae8e90eb05068f44e09e0af9eab90b

#出现tcp协议的80端口,直接访问会报错,未开放80端口,未封闭
$ docker ps -a
#f489b3f6d24c   nginx:alpine   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp    zen_hypatia#

#在不重复的情况下,只用输出前几位字符就行
$ docker kill f4
#再次查询 f4 开头的容器id 已经被关闭
$ docker ps -a 
```

> -P 随机暴露一个端口给物理机

```shell
#docker是一个封闭的环境,直接从外部无法访问虚拟的内部信息
$ docker run --rm -d -P nginx:alpine
a7c1f3394b0c0264c8e6072868ade3c9ea6f2483f5656b662275bc196b690390


#49153就是被暴露的端口号,175.24.118.73:49153
#公网ip 冒号 被暴露的端口号 就可以直接访问nginx 代理的内容
$ docker ps 	#0.0.0.0:49153->80/tcp  
#a7c1f3394b0c   nginx:alpine   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:49153->80/tcp, :::49153->80/tcp   inspiring_villani
```

> /-p  固定暴露一个端口给物理机

```shell
#将指定的端口号暴露给物理机访问,  175.24.118.73:8080->80/tcp
$ docker run --rm -d -p 8080:80 nginx:alpine
9275ff04f8a8c879fbe37e4d68e2643d13c1f567a80fd946c578e2785f1ca412
#9275ff04f8a8   nginx:alpine   "/docker-entrypoint.…"   6 minutes ago   Up 6 minutes   0.0.0.0:8080->80/tcp, :::8080->80/tcp   cool_darwin
```



## 7.构建镜像

**查看帮助**

> 需要从dockerfile构建镜像-

```shell
#直接输入docker build获取帮助文档
$ docker build  #Build an image from a Dockerfile
#查看帮助文档
$ docker build -help
```

[**常用命令**](https://docs.docker.com/engine/reference/builder/)

* **FROM**  

  > 用于指定基础镜像

* **RUN**

  > 用于指定在构建过程中需要执行的命令

* **CMD**

  > 用于指定容器启动过程中默认要执行的命令

* **LABEL**

  > 用于添加一些扩展的信息到镜像之中(版本,维护者)

* **COPY**

  > 用于将文件打包到镜像之中

* **WORKDIR**

  > 用于设置命令的工作目录

**编辑文件 DockerFile文件**

```shell
#切换到~目录
$ cd ~
```

> vi app.py	

```python
print("hello python")
```



> vi Dockerfile 

```dockerfile
#制作一个基础镜像,可以指定系统
#FROM ubuntu:16.04 
FROM alipne

#添加标签,各种说明,可以多个
LABEL version="1.0"
LABEL description="my first image"


# 在 alipne 的基础之上执行,不是在当前机器执行,可以使用 && 连接命令
#RUN apt update && apt -y install xxxxx  ubuntu需要安装的对象
RUN apk update && apk add python3		#做一个更新,安装python3   

#将当前目录( . )所有文件 拷贝到 镜像目录的( /code )中
COPY . /code 

#设置镜像启动之后的工作目录
WORKDIR /code

#指定使用的容器 等于cd到/code目录  使用 python3 执行 app.py 
CMD ["python3","app.py"]
```

**构建并运行**

> docker build  构建一个新的镜像

```shell
#构建一个新的镜像 -t(tag)打一个myapp的标签	.在当前目录
$ docker build -t myapp . 		
#再次修改需要重新构建,成功输出以下
#Successfully built 27cb04a1b911 Successfully tagged myapp:latest#

#查看是否含有镜像
$ docker images
#myapp        latest    27cb04a1b911   8 minutes ago   54.1MB#
```

> 运行myapp 这个新的镜像

```shell
#运行镜像 
$ docker run --rm myapp

#RUN和CMD只会在构建的时候执行,在后面的命令是启动命令,会覆盖Dockerfile里的CMD的启动命令
$ docker run --rm myapp echo "hi"

#查看镜像的更多的详细信息
$ docker inspect myapp
```



## 8.多容器实战

[**1.准备redis镜像**](https://hub.docker.com/search?q=redis&type=image)

```shell
#先创建一个redis的镜像容器,尽量一个镜像只使用一个容器
$ docker pull redis:alpine

#redis会暴露一个6379的端口,用来进行通讯
$ docker inspect redis:alpine

#物理机创建redis的缓存目录,用来映射当前容器,存放数据
$ mkdir ./redis_data

#-d(启动服务),--name(设置服务名字,方便管理),-v(将/redis-data 目录挂载到/data 目录)
$ docker run -d --name redis -v /root/redis_data:/data redis:alpine

#查看正在运行的容器
$ docker ps
#d864a841253e   redis:alpine   "docker-entrypoint.s…"   11 seconds ago   Up 10 seconds   6379/tcp   redis
```

![image-20220313163106108](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140173.png)

![image-20220313163137897](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140175.png)

**2.开发web页面**

```shell
#创建一个myweb的文件夹
$ mkdir myweb
$ cd myweb/
$ ls
#编辑myweb/app.py文件
$ vi app.py
```

> myweb/app.py信息

```python
#常用的框架是flask和Django
#引入flask的核心类 
from flask import Flask
#引入redis
import redis

#引入flask提供的功能
app = Flask(__name__)
#连接redis容器,监听6397端口
rd =redis.Redis(host="redis",port=6379)

#让函数相应web请求
@app.route('/')
def hello():
    #调用redis的自增
    count = rd.incr("hits")
    return "Hello World!{}".format(count)

#监听主机和端口号
if __name__ =="__main__":
    app.run(host="0.0.0.0",port=5000)                                                   
```

[**3.配置Dockerfile文件**](https://hub.docker.com/search?q=python&type=image) 

>  docker有alpine的python镜像

![image-20220313174519043](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140176.png)

> vi Dockerfile

```dockerfile
#使用alpine制作的镜像
FROM python:alpine
#将当前目录的代码文件拷贝到/code文件目录
COPY . /code
#执行pip的安装flask redis  官方redis里面不是pip3
RUN pip install flask redis
#把工作目录设置到/code目录下
WORKDIR /code
#把5000端口暴露出来
EXPOSE 5000
#使用python执行app.py文件
CMD ["python","app.py"]
```

**4.构建启动myweb镜像**

```shell
#查看目录位置,需要在Dockerfile文件目录下
$ ls 	#app.py Dockerfile 

#-t myweb (设置镜像名myweb), 	.(在当前目录下构建镜像)
$ docker build -t myweb .  

#将80端口绑定5000端口 运行 myweb这个应用 通过公网ip:80端口即可访问
$ docker run --rm -p 80:5000 myweb 
```

![image-20220313192050327](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140177.png)



> 由于容器与容器之间是相互隔离的 ,需要配置连接参数

```shell
# --link redis 连接其他容器的上
$ docker run -d --rm --link redis -p 80:5000 myweb
```

> 2个容器都启动成功,并且进行了连接的操作

![image-20220313181554532](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140178.png)

> 测试redis在配置了redis-data文件目录时会不会持久化保存

```shell
#停止redis容器 如果直接kill可能会丢失近期数据
$ docker stop redis
#删除redis容器
$ docker rm redis
#重新启动redis容器 在redis-data数据目录挂载
$ docker run -d --name redis -v /redis-data:/data redis:alpine 
```

> 已经持久化保存到物理机的redis-data目录下的dump.rdb文件

![image-20220313182102505](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140179.png)













# MongoDB

```shell
db —— 显示当前的数据库表
use xxxx —— 进入xxx数据库
show dbs —— 显示所有数据库
show tables —— 显示当前数据库的所有集合
db.xxx.find() —— 显示xxx集合的所有信息
db.dropDatabase() —— 进入某个数据库后执行则删除该数据库
db.xxx.drop() —— 删除xxx集合
```



## 1.MongoDB安装

MongoDB 是由C++语言编写的，是一个基于分布式文件存储的开源数据库系统。旨在为WEB应用提供可扩展的高性能数据存储解决方案。MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象

[**官网下载**](https://www.mongodb.com/try/download/community)

如果是Windows系统推荐下载`zip`包，Linux系统可以选择`tgz`包。Windows7系统选择4.2版本(4.3不支持Windows7了)。

> [window](https://fastdl.mongodb.org/windows/mongodb-windows-x86_64-5.0.6-signed.msi)

将下载的文件包解压 C:\mongodb，然后创建w一个目录用于存放数据，例如：

```shell
C:\mongo-data

#D:\code\mongodb\data
```



使用下面的命令启动 MongoDB的服务

```shell
C:\mongodb\bin\mongod.exe --dbpath C:\mongo-data

#D:\code\mongodb\bin\mongod.exe --dbpath D:\code\mongodb\data
```

```
D:\code\mongodb\bin\mongod.exe  --logpath D:\code\mongodb\log\mongodb.log --logappend --dbpath D:\code\mongodb\data --directoryperdb --serviceName MongoDB -install
```

再开一个命令行，使用下面的命令启动客户端

```shell
C:\mongodb\bin\mongo

#D:\code\mongodb\bin\mongo
```

这样就进入到MongoDB的管理后台，下面学习常用命令



```javascript
// 查看数据库版本
> version()
4.2.14

// 查看当前所在的数据库
> db
test
 
// 切换到新的数据库，例如users (不需要事先创建)
> use users
switched to db users

// 在users数据库中，保存一条数据
> db.users.insert({"name":"jack", "age": 18})
WriteResult({ "nInserted" : 1 })

// 再保存一条
> db.users.insert({"name":"mary", "age": 20})

// 查询users中的所有数据
> db.users.find()
{ "_id" : ObjectId("60d43c7ec9eb5a8624ca3277"), "name" : "jack", "age" : 18 }
{ "_id" : ObjectId("60d43cd7c9eb5a8624ca3278"), "name" : "mary", "age" : 20 }

// 修改jack的年龄为22 (如果有多个叫jack的记录，会一起改掉)
> db.users.update({"name": "jack"}, {$set:{"age": 22}}, {multi:true})

> db.users.find()

// 删除name叫mary的数据
> db.users.remove({"name": "mary"})
WriteResult({ "nRemoved" : 1 })

// 列出所有数据库
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
users   0.000GB
```



到此，我们已了解MongoDB基础使用，更多内容参考官方文档 https://docs.mongoing.com/



优点

------

- 文档结构的存储方式，能够更便捷的获取数据
- 内置GridFS，支持大容量的存储
- 海量数据下，性能优越
- 动态查询
- 全索引支持,扩展到内部对象和内嵌数组
- 查询记录分析
- 快速,就地更新
- 高效存储二进制大对象 (比如照片和视频)
- 复制（复制集）和支持自动故障恢复
- 内置 Auto- Sharding 自动分片支持云级扩展性，分片简单
- MapReduce 支持复杂聚合

------

缺点

- 不支持事务操作
- MongoDB 占用空间过大 （不过这个确定对于目前快速下跌的硬盘价格来说，也不算什么缺点了）
- MongoDB没有如MySQL那样成熟的维护工具
- 无法进行关联表查询，不适用于关系多的数据
- 复杂聚合操作通过mapreduce创建，速度慢
- 模式自由,自由灵活的文件存储格式带来的数据错
- MongoDB 在你删除记录后不会在文件系统回收空间。除非你删掉数据库。但是空间没有被浪费

本节练习已完成



已完成

## 2.在SpringBoot中操作MongoDB

Spring boot 针对 mongodb 提供了 starter ，使用非常方便



```javascript
<!-- 添加依赖 -->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```



在配置文件 application.properties 添加如下配置



```javascript
spring.data.mongodb.uri=mongodb://127.0.0.1:27017/users

# 用户名为root 密码为example，则使用下面的连接串
# spring.data.mongodb.uri=mongodb://root:example@127.0.0.1:27017/users?authSource=admin&authMechanism=SCRAM-SHA-1
```



```javascript
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private long id;
    private String name;
}
```



```javascript
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class TestController {
    @Autowired
    MongoTemplate mongoTemplate;

    @GetMapping("/save")
    public User save() {

        User user = new User(2, "Jack");
        return mongoTemplate.save(user);
    }

    @GetMapping("/find")
    public List<User> find() {
        return mongoTemplate.findAll(User.class);
    }
}
```

接下来，完成对MongoDB中数据的增删改查



使用详情

```java
package com.example.mongodb;

import com.mongodb.client.result.DeleteResult;
import com.mongodb.client.result.UpdateResult;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.data.mongodb.core.query.Criteria;
import org.springframework.data.mongodb.core.query.Query;
import org.springframework.data.mongodb.core.query.Update;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class TestController {
    @Autowired
    MongoTemplate mongoTemplate;

    @GetMapping("/save")
    public User save(User user) {
        return mongoTemplate.save(user);
    }

    @GetMapping("/find")
    public String find(User user) {
        //查找所有
        System.out.println("查找所有结果-----------");
        System.out.println(mongoTemplate.findAll(User.class));
        //分页查询
        System.out.println("分页查询结果-----------");
        Query query = new Query();
        query.skip(0).limit(2);
        System.out.println(mongoTemplate.find(query, User.class));



        //条件查询1，多条件is("值")后面可以加and("字段2").is("值2")
        System.out.println("条件查询结果-----------");
        query = new Query(Criteria.where("name").is(user.getName()));
        System.out.println(mongoTemplate.find(query, User.class));


        System.out.println("条件gte大于 lte小于-----------");
        //条件查询2，gte大于 lte小于
        Criteria criteria = Criteria.where("id").gte(1).lte(10);
        System.out.println(mongoTemplate.find(query.addCriteria(criteria),User.class));


        return mongoTemplate.getCollectionName(User.class);
    }


    @GetMapping("/delete")
    public DeleteResult delete(int id) {
        Query query = new Query(Criteria.where("_id").is(id));
        return mongoTemplate.remove(query, User.class);
    }

    @GetMapping("/update")
    public UpdateResult update(User user) {
        Query query = new Query(Criteria.where("id").is(user.getId()));
        Update update = Update.update("name", user.getName());
        return mongoTemplate.updateFirst(query, update, User.class);
    }

}
```

![image-20220314165600356](../%25E5%25AD%25A6%25E4%25B9%25A0%25E5%258E%2586%25E7%25A8%258B/images/200-MongoDB/image-20220314165600356.png)

## 3.springboot 整合mongoTemplate的 Query Criteria 用法

1.通过注解注入 mongoTemplate

```java
@Autowired
private MongoTemplate mongoTemplate;
```

2.获取Query 和 Criteria 对象

```java
 Query query = new Query();
 Criteria criteria = new Criteria();
```

3.多参数动态查询。criteria 有两种写法，一种是criteria.and().is();另一种是criteria.where().is(),两种方式不能混合使用，否则不生效。

```java
if(runningStatus != null){
    criteria.and("runningStatus").is(runningStatus);
}
```

4.根据日期时间进行范围查询

```java
SimpleDateFormat format =  new SimpleDateFormat( "yyyy-MM-dd HH:mm:ss" );
criteria.and("createTime").gt(format.parse(createTime));
criteria.and("endTime").lte(format.parse(endTime));
```

5.模糊查询

```java
Pattern pattern=Pattern.compile("^.*"+taskTypeCode+".*$", Pattern.CASE_INSENSITIVE);
criteria.and("taskTypeCode").regex(pattern);
```

6.将查询条件装载到query中

```java
query.addCriteria(criteria);
```

7.排序 通过参数 sord 判断排序方向，sortBy 为排序字段

```java
query.with(new Sort(sord.length() == 3 ? Direction.ASC : Direction.DESC, sortBy));
```

8.分页，有两种方式，一种是通过pageable 一种是 limit().skip();limit表示查询多少数据，skip表示从哪条数据查起

```java
//第一种
query.with(pageable);
long totoal = this.mongoTemplate.count(query, TaskMongo.class);
List<TaskMongo> listTaskMongo = this.mongoTemplate.find(query , TaskMongo.class);

//第二种
query.limit(5000).skip(5000);
List<TaskMongo> listTaskMongo = this.mongoTemplate.find(query , TaskMongo.class);
```

9.一个模糊关键字匹配多个字段

```java
Pattern pattern=Pattern.compile("^.*"+pattern_name+".*$", Pattern.CASE_INSENSITIVE);
criatira.orOperator(Criteria.where("name").regex(pattern),
                    Criteria.where("sex").regex(pattern),
                    Criteria.where("age").regex(pattern), 
                    Criteria.where("class").regex(pattern));
```

10. 查询指定的字段通过 Field这个类，通过findFields.include()方法设置查询字段

```java
Query query = new Query(criteria);
Field findFields = query.fields();
findFields.include("id");
```

 

# Spring Cloud



## 1.RestTemplate



什么是`单体应用`？一个项目一套代码，一个数据库，如下图，就是单体架构：



![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181137586.png!l)





为了更好的扩展性和支持更高的并发，逐渐发展成`微服务`架构，一些重要的模块，被独立成一个单独的项目，叫一个服务，使用独立的数据库。如下图：



![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181137864.png!l)

预览



服务与服务之间，使用HTTP或RPC进行调用，请搭建一个这样的微服务架构项目，在OrderService 中使用`RestTemplate`调用UserService

### [RestTemplate](https://so.csdn.net/so/search?q=RestTemplate&spm=1001.2101.3001.7020) 简介

RestTemplate 是从 Spring3.0 开始支持的一个 HTTP 请求工具，它提供了常见的REST请求方案的模版，例如 GET 请求、POST 请求、PUT 请求、DELETE 请求以及一些通用的请求执行方法 exchange 以及 execute。RestTemplate 继承自 InterceptingHttpAccessor 并且实现了 RestOperations 接口，其中 RestOperations 接口定义了基本的 RESTful 操作，这些操作在 RestTemplate 中都得到了实现。

> 前端一般采用`Ajax`或`Axios`来调用后端的接口获取数据，而后端调用接口的方式有很多，这里介绍基于Spring[框架](https://so.csdn.net/so/search?q=框架&spm=1001.2101.3001.7020)的`RestTemplate`。

[RestTemplate官网](https://i.csdn.net/#/user-center/collection-list?type=1)

### RestTemplate | 使用详解



23 篇文章2 订阅

订阅专栏

> 在学习与工作中，常常遇见需要调用他人写好的`API`接口的情况，前端一般采用`Ajax`或`Axios`来调用后端的接口获取数据，而后端调用接口的方式有很多，这里介绍基于Spring[框架](https://so.csdn.net/so/search?q=框架&spm=1001.2101.3001.7020)的`RestTemplate`。



### 文章目录

- - [RestTemplate的使用](https://blog.csdn.net/Ares___/article/details/121620150#RestTemplate_10)
  - - [getForObject的使用](https://blog.csdn.net/Ares___/article/details/121620150#getForObject_26)
    - [getForEntity 的使用](https://blog.csdn.net/Ares___/article/details/121620150#getForEntity__48)
    - [postForObject 的使用](https://blog.csdn.net/Ares___/article/details/121620150#postForObject__95)
    - [postForEntity的使用](https://blog.csdn.net/Ares___/article/details/121620150#postForEntity_155)
    - [exchange的使用](https://blog.csdn.net/Ares___/article/details/121620150#exchange_182)

**常见的HTTP客户端请求工具：**



- `JDK HttpURLConnection`
- `http client`
- `OkHttp`
- `Spring 家族 RestTemplate`

**`RestTemplate` 是一个同步的 Rest API 客户端。下面我们就来介绍下`RestTemplate` 的常用功能。**

### 自己的练习

> 用户模块(第一个项目)

```java
package com.example.springcloud.service;

import com.example.springcloud.entity.User;
import com.example.springcloud.mapper.UserMapper;
import org.springframework.stereotype.Service;
import org.springframework.web.bind.annotation.*;

import javax.annotation.Resource;

@Service
@CrossOrigin
@RestController
public class UserService {
    @Resource
    UserMapper userMapper;

    @GetMapping("/get/{id}")
    public User findById(@PathVariable Long id) {
        return userMapper.findById(id);
    }

    @PostMapping("/post")
    public User post(@RequestBody User user) {
        System.out.println(user);
        return userMapper.findById(user.getId());

    }
}

```

> 订单模块(第二个项目)

```java
/** 枚举类 */
public enum ApiEnum {
    get(ApiEnum.host + "get/{id}"),
    post(ApiEnum.host +"post")
    ;
    static final String host = "http://localhost:8000/";
    public final String url;

    ApiEnum(String url) {
        this.url = url;
    }
}
```

```java
/** 业务逻辑 */
import com.example.springcloud.api.ApiEnum;
import com.example.springcloud.entity.Order;
import com.example.springcloud.entity.User;
import com.example.springcloud.mapper.OrderMapper;
import com.example.springcloud.utils.SnowflakeIdUtils;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

import javax.annotation.Resource;
import java.io.IOException;

@Service
public class OrderService {
    @Resource
    OrderMapper orderMapper;

    //get请求获取数据
    public static User get(Long id) {
        RestTemplate restTemplate = new RestTemplate();
        //Get请求获取数据
        //User getForObject = restTemplate.getForObject(ApiEnum.findById.url + id, User.class);
        User getForObject = restTemplate.getForObject(ApiEnum.get.url, User.class, id);
        //Get请求获取响应状态
        //ResponseEntity<User> getForEntity = restTemplate.getForEntity(ApiEnum.findById.url+ id, User.class);
        ResponseEntity<User> getForEntity = restTemplate.getForEntity(ApiEnum.get.url, User.class, id);

        return getForEntity.getBody();
    }

    //post传参
    public static User post(User user) {
        RestTemplate restTemplate = new RestTemplate();
        //post 请求传参,接收参数需要
        // User postForObject = restTemplate.postForObject(ApiEnum.post.url, user, User.class);
        //可以获取
        ResponseEntity<User> postForEntity = restTemplate.postForEntity(ApiEnum.post.url, user, User.class);

        System.out.println(postForEntity.getBody());

        return postForEntity.getBody();
    }


    //创建订单
    public Order create(Order order) throws IOException {
        // User user = get(order.getUserId());
        User user = post(User.builder().id(order.getUserId()).build());
        if (user == null) {
            throw new IOException("未查找到用户");
        }
        order.setAddr(user.getAddr());
        order.setUsername(user.getUsername());
        order.setOrder(new SnowflakeIdUtils(1, 1).nextId());
        order.setId(orderMapper.create(order));
        return order;
    }
}
```

```java
/** 雪花id */
/**
 * Twitter_Snowflake<br>
 * SnowFlake的结构如下(每部分用-分开):<br>
 * 0 - 0000000000 0000000000 0000000000 0000000000 0 - 00000 - 00000 - 000000000000 <br>
 * 1位标识，由于long基本类型在Java中是带符号的，最高位是符号位，正数是0，负数是1，所以id一般是正数，最高位是0<br>
 * 41位时间截(毫秒级)，注意，41位时间截不是存储当前时间的时间截，而是存储时间截的差值（当前时间截 - 开始时间截)
 * 得到的值），这里的的开始时间截，一般是我们的id生成器开始使用的时间，由我们程序来指定的（如下下面程序IdWorker类的startTime属性）。41位的时间截，可以使用69年，年T = (1L << 41) / (1000L * 60 * 60 * 24 * 365) = 69<br>
 * 10位的数据机器位，可以部署在1024个节点，包括5位datacenterId和5位workerId<br>
 * 12位序列，毫秒内的计数，12位的计数顺序号支持每个节点每毫秒(同一机器，同一时间截)产生4096个ID序号<br>
 * 加起来刚好64位，为一个Long型。<br>
 * SnowFlake的优点是，整体上按照时间自增排序，并且整个分布式系统内不会产生ID碰撞(由数据中心ID和机器ID作区分)，并且效率较高，经测试，SnowFlake每秒能够产生26万ID左右。
 */
public class SnowflakeIdUtils {

    // ==============================Fields===========================================
    /** 开始时间截 (2015-01-01) */
    private final long twepoch = 1420041600000L;

    /** 机器id所占的位数 */
    private final long workerIdBits = 5L;

    /** 数据标识id所占的位数 */
    private final long datacenterIdBits = 5L;

    /** 支持的最大机器id，结果是31 (这个移位算法可以很快的计算出几位二进制数所能表示的最大十进制数) */
    private final long maxWorkerId = -1L ^ (-1L << workerIdBits);

    /** 支持的最大数据标识id，结果是31 */
    private final long maxDatacenterId = -1L ^ (-1L << datacenterIdBits);

    /** 序列在id中占的位数 */
    private final long sequenceBits = 12L;

    /** 机器ID向左移12位 */
    private final long workerIdShift = sequenceBits;

    /** 数据标识id向左移17位(12+5) */
    private final long datacenterIdShift = sequenceBits + workerIdBits;

    /** 时间截向左移22位(5+5+12) */
    private final long timestampLeftShift = sequenceBits + workerIdBits + datacenterIdBits;

    /** 生成序列的掩码，这里为4095 (0b111111111111=0xfff=4095) */
    private final long sequenceMask = -1L ^ (-1L << sequenceBits);

    /** 工作机器ID(0~31) */
    private long workerId;

    /** 数据中心ID(0~31) */
    private long datacenterId;

    /** 毫秒内序列(0~4095) */
    private long sequence = 0L;

    /** 上次生成ID的时间截 */
    private long lastTimestamp = -1L;

    //==============================Constructors=====================================
    /**
     * 构造函数
     * @param workerId 工作ID (0~31)
     * @param datacenterId 数据中心ID (0~31)
     */
    public SnowflakeIdUtils(long workerId, long datacenterId) {
        if (workerId > maxWorkerId || workerId < 0) {
            throw new IllegalArgumentException(String.format("worker Id can't be greater than %d or less than 0", maxWorkerId));
        }
        if (datacenterId > maxDatacenterId || datacenterId < 0) {
            throw new IllegalArgumentException(String.format("datacenter Id can't be greater than %d or less than 0", maxDatacenterId));
        }
        this.workerId = workerId;
        this.datacenterId = datacenterId;
    }

    // ==============================Methods==========================================
    /**
     * 获得下一个ID (该方法是线程安全的)
     * @return SnowflakeId
     */
    public synchronized long nextId() {
        long timestamp = timeGen();

        //如果当前时间小于上一次ID生成的时间戳，说明系统时钟回退过这个时候应当抛出异常
        if (timestamp < lastTimestamp) {
            throw new RuntimeException(
                    String.format("Clock moved backwards.  Refusing to generate id for %d milliseconds", lastTimestamp - timestamp));
        }

        //如果是同一时间生成的，则进行毫秒内序列
        if (lastTimestamp == timestamp) {
            sequence = (sequence + 1) & sequenceMask;
            //毫秒内序列溢出
            if (sequence == 0) {
                //阻塞到下一个毫秒,获得新的时间戳
                timestamp = tilNextMillis(lastTimestamp);
            }
        }
        //时间戳改变，毫秒内序列重置
        else {
            sequence = 0L;
        }

        //上次生成ID的时间截
        lastTimestamp = timestamp;

        //移位并通过或运算拼到一起组成64位的ID
        return ((timestamp - twepoch) << timestampLeftShift) //
                | (datacenterId << datacenterIdShift) //
                | (workerId << workerIdShift) //
                | sequence;
    }

    /**
     * 阻塞到下一个毫秒，直到获得新的时间戳
     * @param lastTimestamp 上次生成ID的时间截
     * @return 当前时间戳
     */
    protected long tilNextMillis(long lastTimestamp) {
        long timestamp = timeGen();
        while (timestamp <= lastTimestamp) {
            timestamp = timeGen();
        }
        return timestamp;
    }

    /**
     * 返回以毫秒为单位的当前时间
     * @return 当前时间(毫秒)
     */
    protected long timeGen() {
        return System.currentTimeMillis();
    }

    //==============================Test=============================================
    /** 测试 */
    public static void main(String[] args) {
        SnowflakeIdUtils idWorker = new SnowflakeIdUtils(0, 0);

        for (int i = 0; i < 100; i++) {
            long id = idWorker.nextId();
            System.out.println(Long.toBinaryString(id));
            System.out.println(id);
        }
    }
}
```



### [RestTemplate](https://so.csdn.net/so/search?q=RestTemplate&spm=1001.2101.3001.7020)的使用

`RestTemplate` 支持所有 `Restful` 风格方法，你可以根据需要进行选择，这里我们只介绍一些常用的方法。所有方法都支持`URI`模板和`URI`参数，支持下面这种写法：

```css
类似 spring mvc 中的 @PathVariable
https://api.apiopen.top/{method}
```

restTemplate提供了如下[API](https://so.csdn.net/so/search?q=API&spm=1001.2101.3001.7020)：
![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140180.png)
上面的方法我们大致可以分为三组：

- `getForObject --- optionsForAllow` 分为一组，这类方法是常规的 Rest API（GET、POST、DELETE 等）方法调用；
- `exchange`：接收一个 `RequestEntity` 参数，可以自己设置 HTTP method，URL，headers 和 body，返回 `ResponseEntity`；
- `execute`：通过 `callback` 接口，可以对请求和返回做更加全面的自定义控制。
  一般情况下，我们使用第一组和第二组方法就够了。

### getForObject的使用

<img src="https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140181.png" alt="image-20220314203551044" style="zoom:67%;" />



```java
restTemplate.getForObject(要访问的URL, 用于接受结果的类型.class, 入参）`
入参可以使用Map的形式，也可以以可变参数的形式，定义：
可变参数：
//restTemplate会对参数进行URI编码
String result = template.getForObject( "url/{count}/{page}", String.class, "5", "1"); 
```

案例：(随机口吐莲花)

```java
/**
     * getForObject
     */
public static String getForObject(){
    String api1 = "https://nmsl.shadiao.app/api.php?level=min&lang=zh_cn"; //随机生成一句口吐莲花
    RestTemplate restTemplate = new RestTemplate();
    HashMap<String, Object> uriParams = new HashMap<>();//空参
    String res = restTemplate.getForObject(api1,String.class,uriParams);
    return res;
}
```

![在这里插入图片描述](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140182.png)

### getForEntity 的使用

> 此方法有3个重载 方法参数同`getForObject`。
> 唯一区别是：
>
> - 返回值是`ResponseEntity<T>`类型
> - `ResponseEntity<T>` 包含了HTTP响应的头信息`header`

通过`header`可以获取到响应的头信息,比如status 状态码,`ContentType` 响应类型等等
`body`则是响应数据通过`HttpMessageConverte`r转换的数据.

```java
public static void getForEntity() {
    RestTemplate restTemplate = new RestTemplate();
    String url = "https://api.apiopen.top/getImages?page={page}&count={count}"; //获取几张小姐姐的照片看
    HashMap<String,Object> uriParams = new HashMap<>();
    uriParams.put("page",1);
    uriParams.put("count",2);
    ResponseEntity<String> responseEntity = restTemplate
        .getForEntity(url,String.class,uriParams);
    String body = responseEntity.getBody();
    System.out.println(body);
}

/**{
	"code": 200,
	"message": "成功!",
	"result": [{
		"id": 674,
		"time": "2020-02-16 04:00:00",
		"img": "https://img.lijinshan.site/images/70def23833844b0fa0e6e74041421e37"
	}, {
		"id": 675,
		"time": "2020-02-16 04:00:00",
		"img": "https://img.lijinshan.site/images/999cf7f9728b45deacc0740de53aaff1"
	}]
}*/
```

除了获取body，还可以用下面的方式获取响应类型和响应状态码：

```java
//获取响应类型 application/json;charset=UTF-8
MediaType contentType = responseEntity.getHeaders().getContentType();
//获取响应状态码 200 OK
HttpStatus statusCode = responseEntity.getStatusCode();
```

### postForObject 的使用

<img src="https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140183.png" alt="image-20220314203651676" style="zoom:67%;" />

> 此方法有3个重载与 `getForObject`相比多了一个`Object request`参数。其他参数作用和`getForObject`相同
> Object request可以使用以下值作为参数:
>
> 1. `org.springframework.util.MultiValueMap`
> 2. `org.springframework.http.HttpEntity`

1 `org.springframework.util.MultiValueMap`
通过`MultiValueMap`携带多个参数

> 在大多数情况下，您不必为每个部件指定Content-Type。内容类型是根据`HttpMessageConverter`所选内容类型自动确定的，不指定Content-Type以便基于文件扩展名的情况下进行自动选择。

```java
public static void postForObject(){
    RestTemplate template = new RestTemplate();

    MultiValueMap<String, Object> parts = new LinkedMultiValueMap<>();
    //字符串值
    parts.add("fieldPart", "fieldValue");
    //图片文件
    parts.add("filePart", new FileSystemResource("...logo.png"));
    //json
    parts.add("jsonPart", new Person("Jason"));
    //  手动指定类型,并添加xml
    String xmlValue = "<user><name>hoody</name><sex>male</sex></user>";
    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_XML);
    parts.add("xmlPart", new HttpEntity<>(xmlValue, headers));

    String result = new RestTemplate().postForObject(
        "https://example.com/{class}/user", //String url
        parts, //Object request
        String.class, //Class<T> responseType
        "1");  //Object... uriVariables
}
```

2.`org.springframework.http.HttpEntity`

```java
/**
     * PostForObject
     */
public static void postForObject(){
    RestTemplate restTemplate = new RestTemplate();
    //header类型
    HttpHeaders httpHeaders = new HttpHeaders();
    httpHeaders.setContentType(MediaType.APPLICATION_JSON);
    //JSON String
    String param = "{\"type\":\"student\"}";
    //创建请求参数
    HttpEntity<String> entity = new HttpEntity<String>(param, httpHeaders);
    //调用
    String result = new RestTemplate().postForObject(
        "https://example.com/{class}/user", //String url
        entity, //Object request
        String.class, //Class<T> responseType
        "1");  //Object... uriVariables

    System.out.println(result);
}
```

### postForEntity的使用

> 此方法有3个重载 方法参数同`postForObject` 唯一区别是返回值是`ResponseEntity`类型 `ResponseEntity` 包含了HTTP响应的头信息`header`

```java
RestTemplate template = new RestTemplate();
//JSON String
String param = "{\"type\":\"student\"}";
//create request header 创建请求头
HttpHeaders headers = new HttpHeaders()
    headers.setContentType(org.springframework.http.MediaType.APPLICATION_JSON_UTF8)
    //创建请求参数
    HttpEntity<String> entity = new HttpEntity<String>(param, headers)
    //调用
    ResponseEntity<String> result = new RestTemplate().postForObject(
    "https://example.com/{class}/user", //String url
    entity, //Object request
    String.class, //Class<T> responseType
    "1")  //Object... uriVariables

    //获取返回值
    String body = entity.getBody();
//获取响应类型
MediaType contentType = entity.getHeaders().getContentType();
//获取响应状态码
HttpStatus statusCode = entity.getStatusCode();
```

### exchange的使用

该方法是通用的请求方式，支持 GET, HEAD, POST, PUT, PATCH, DELETE, OPTIONS, TRACE，当上面的方式不能满足你可采用该方式定制，该方式提供了更加灵活的 API，比如你可以定制 GET 方法的请求头，放入 `Jwt Token`等操作，这是`getForObject` 无法比拟的。

**例子:**
使用exchange 发起GET请求

设置请求头header:
设置user-agent
设置接收数据类型为JSON

```java
RestTemplate template = new RestTemplate();
//创建header
HttpHeaders headers = new HttpHeaders();
//设置user-agent
headers.add(HttpHeaders.USER_AGENT, "Mozilla/5.0 (Windows NT 10.0; Win64; x64) " +
            "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36");
//添加接收数据媒体类型,JSON
List<MediaType> acceptableMediaTypes = new ArrayList<>();
acceptableMediaTypes.add(MediaType.APPLICATION_JSON_UTF8)
    headers.setAccept(acceptableMediaTypes)
    //创建请求体
    HttpEntity<HttpHeaders> entity = new HttpEntity<>(headers)
    //发出请求
    ResponseEntity<String> responseEntity = restTemplate.exchange(
    "https://example.com/hotels/{hotel}/bookings/{booking}",
    HttpMethod.GET,
    entity,
    String.class,
    "42","21"
)
    //获取返回值
    String body = entity.getBody();
//获取响应类型
MediaType contentType = entity.getHeaders().getContentType();
//获取响应状态码
HttpStatus statusCode = entity.getStatusCode();
```



## 2.Eureka注册中心



在上一节，我们学习了微服务架构，掌握了使用RestTemplate来进行服务之间的调用。为了让我们项目能够支持更大的并发，通常需要将服务部署多个实列，如下图所示



![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181140184.png!l)

预览



调整之后，在OrderService中，想要调用UserService，就需要知道有哪些UserService，以及的IP和端口号，数量小的时候，我们还可以手工配置，如果UserService部署实例较多，或是需要调整时，将UserService的IP和端口硬编码到程序中，或是写在程序的配置文件中，都会带来很大的维护量。



如何简化这个流程呢？如果每个服务启动后，都能自动将自己的IP和端口注册到一个统一的地方，我们只需要去这个地方，就能获取到某个服务的IP列表，服务与服务之间相互调用就变得容易了。如下图所示



![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181136874.png!l)

预览



Eureka就是这样的注册中心，这一节，我们新建一个服务，使用Eureka，用为注册中心，让每个服务，都能注册到Eureka，操作步骤如下：

### [注册中心Eureka](http://www.daimaku.net/post/view/10520)

新建一个工程，叫做`spring-cloud-demo`

父pom

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-cloud-demo</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.8.RELEASE</version>
        <relativePath/>
    </parent>
  
    <properties>
        <java.version>1.8</java.version>
        <spring-cloud.version>Hoxton.SR9</spring-cloud.version>
    </properties>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

      <build>
      <plugins>
        <plugin>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
      </plugins>
  </build>

</project>
```

创建注册中心模块 `registry` 的pom文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>spring-cloud-demo</artifactId>
        <groupId>com.example</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>registry</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
    </dependencies>

</project>
```

启动类

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@EnableEurekaServer
@SpringBootApplication
public class RegistryApplication {
    public static void main(String[] args) {
        SpringApplication.run(RegistryApplication.class, args);
    }
}
```

配置文件 `application.yml`

```yaml
spring:
  application:
    name: registry
server:
  port: 8761
eureka:
  instance:
    hostname: eureka01
    instance-id: ${eureka.instance.hostname}:${server.port}
    prefer-ip-address: true # 使用IP
  server:
    enable-self-preservation: false # 关闭自我保护
    wait-time-in-ms-when-sync-empty: 0
```

构建jar包，上传到服务器，并启动后，访问服务器对应端口，验证Eureka是否启动成功

```
http://your-server-ip:8761/
```



### [将微服务注册到Eureka](http://www.daimaku.net/post/view/10521)

大A2021-02-24 10:45:36标签:文章001

新建一个微服务Module，名叫`foo-svc`

pom依赖

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
</dependencies>
```

主启动类

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
@EnableEurekaClient
public class FooApplication {
    public static void main(String[] args) {
        SpringApplication.run(FooApplication.class, args);
    }

    @GetMapping("/version")
    public String version() {
        return "foo v1";
    }
}
```

application.yml

```yaml
server:
  port: 8001

spring:
  application:
    name: foo-service

eureka:
  instance:
    hostname: foo01
    instance-id: ${eureka.instance.hostname}:${server.port}
    prefer-ip-address: true # 使用IP
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://your-eureka-server-ip:8761/eureka/
```

注意替换 `your-eureka-server-ip`为你真实的Eureka服务器IP

构建jar包上传到服务器，并启动后，到注册中心查看是否注册成功





## 3.Ribbon客户端负载均衡

Ribbon客户端负载均衡



在上一节我们完成了注册中心，接下来，我们如何通过`注册中心`获取想要调用的服务信息呢？Ribbon能自动帮我们完成这个过程，请参考下面的方式，配置Ribbon对RestTemplate进行增强，实现客户端负载均衡



### [Ribbon客户端负载均衡](http://www.daimaku.net/post/view/10522)

大A2021-02-24 10:51:17标签:文章000

新建一个微服务Module，名叫`bar-svc`

pom依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

application.yml

```yaml
server:
  port: 8002

spring:
  application:
    name: bar-service

eureka:
  instance:
    hostname: bar01
    instance-id: ${eureka.instance.hostname}:${server.port}
    prefer-ip-address: true
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://your-eureka-server-ip:8761/eureka/
```

使用LoadBalanced增强RestTemplate，能解析服务名，并进行负载均衡

```java
package com.example;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.loadbalancer.LoadBalanced;
import org.springframework.context.annotation.Bean;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

@SpringBootApplication
@RestController
public class BarApplication {
    public static void main(String[] args) {
        SpringApplication.run(BarApplication.class, args);
    }

    // 对RestTemplate进行增强
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }

    @Autowired
    RestTemplate restTemplate;

    @GetMapping("/demo")
    public String demo() {
        // 调用 FOO-SERVICE 服务的 /version, serviceId不区分大小写,不要端口号
        ResponseEntity<String> res = restTemplate.getForEntity("http://FOO-SERVICE/version", String.class);
        return "[bar-service] foo.version: " + res.getBody();
    }
}
```

## 4.Zuul网关



`网关`是微服务的流量入口，可以做负载均衡，例如我们常用的 nginx。但 nginx 只是流量网关，不方便在 nginx 上做业务编程，`Zuul` 是Java语言实现的可编程网关，可以在Zuul网关层做统一登录拦截，权限校验等等。操作接下来，我们掌握Zuul网关使用



### [Zuul网关](http://www.daimaku.net/post/view/10525)

大A2021-02-26 09:35:15标签:文章002

创建一个gateway的Module

pom

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
</dependency>
```

application.yml

```yaml
server:
  port: 8000

spring:
  application:
    name: gateway
eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://your-eureka-ip:8761/eureka/
  instance:
    prefer-ip-address: true
```

启动类

```java
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.zuul.EnableZuulProxy;

@EnableZuulProxy
@SpringBootApplication
public class GatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(GatewayApplication.class,args);
    }
}
```

application.yml中，提定url也服务之间的映射关系

```yaml
zuul:
  ignored-services: "*"    # 关闭自动映射
  routes:
    foo:
      path: /foo/**
      strip-prefix: true # 默认为true，表示服务中的url没有这个前缀，需要去掉之后调用服务
      service-id: foo-service
    bar:
      path: /bar/**
      service-id: bar-service
```

通过网关访问微服务：

```shell
http://your-gateway-ip:8000/foo/xxx

http://your-gateway-ip:8000/bar/xxx
```

过滤器

```java
package com.example.filter;

import com.netflix.zuul.ZuulFilter;
import com.netflix.zuul.context.RequestContext;
import com.netflix.zuul.exception.ZuulException;
import org.springframework.stereotype.Component;

import javax.servlet.http.HttpServletResponse;

@Component
public class TokenFilter extends ZuulFilter {

    @Override
    public String filterType() {
        return "pre";
    }

    @Override
    public int filterOrder() {
        return 0;
    }

    @Override
    public boolean shouldFilter() {
        return true;
    }

    @Override
    public Object run() throws ZuulException {

        RequestContext requestContext = RequestContext.getCurrentContext();
        HttpServletResponse response = requestContext.getResponse();

        // 从请求头中获取token
        String token = requestContext.getRequest().getHeader("token");
        if (token == null) {
             Map<String, String> map = new HashMap<>();
             map.put("code", "ERROR");
             map.put("message", "INVALID_TOKEN");
             map.put("data", null);
             stop(requestContext, map);  // 停止
            return null;
        }

        // todo 通过token获取当前用户信息
       String userId = "1";
       requestContext.addZuulRequestHeader("current-user-id", userId);

        return null;
    }

    private void stop(RequestContext requestContext, Map map) {

        // 对其它过滤器都不会被执行了，直到  SendResponseFilter，输出Response的内容
        requestContext.setSendZuulResponse(false);

        HttpServletResponse response = requestContext.getResponse();
        response.setHeader("content-type", "application/json;charset=UTF-8");

        response.setHeader("Access-Control-Allow-Origin", "*");
        response.setHeader("Access-Control-Allow-Headers", "*");
        response.setHeader("Access-Control-Allow-Methods", "*");

        requestContext.setResponseStatusCode(200);
        requestContext.setResponseBody(objToStr(map));
    }

    public static <T> String objToStr(T obj) {
        try {
            return new ObjectMapper().writeValueAsString(obj);
        } catch (Exception e) {
            throw new RuntimeException(e.getMessage());
        }
    }

}
```

在微服务中，直接在Http请求头中获取当前用户ID，例如 foo-svc中添加一个控制器

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;

@RestController
public class DemoController {

    @GetMapping("/demo/test")
    public String test(HttpServletRequest request) {
        String userId = request.getHeader("current-user-id");
        return userId;
    }
}
```

你可以用以下两种方式访问

```shell
# 直接访问foo-svc的端口8001访问
http://your-foo-svc-ip:8001/demo/test

# 通过网关访问（需要加上前缀）
http://your-gateway-ip:8000/foo/demo/test
```

## 5.Feign



`Feign`是声明式、模板化的HTTP客户端， Feign可以帮助我们更快捷、优雅地调用HTTP API。Spring Cloud 对Feign进行了增强，使Feign支持了 Spring MVC 注解，并整合了 Ribbon 和 Eureka，从而让 Feign 的使用更加方便



### [Feign](http://www.daimaku.net/post/view/10529)

大A2021-02-26 15:46:03标签:文章110

#### 新建模块

新建一个叫`foo-api`的module

#### 添加依赖

在xml中添加如下依赖

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-openfeign</artifactId>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <skip>true</skip>
            </configuration>
        </plugin>
    </plugins>
</build>
```

#### 添加interface

FooClient接口代码如下

```java
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;

@FeignClient(name = "FOO-SERVICE")
public interface FooClient {
    @GetMapping("/version")
    String version();
}
```

接下来，我们关注`调用方`

#### 调用方添加依赖

在xml中添加如下依赖

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>foo-api</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

#### 启动类中

在启动类中，添加注解

```java
import org.springframework.cloud.openfeign.EnableFeignClients;

@EnableFeignClients()
@SpringBootApplication
public class BarApplication {
    public static void main(String[] args) {
        SpringApplication.run(BarApplication.class, args);
    }
}
```

#### API调用

使用FooClient进行API调用

```java
@RestController
public class DemoController {

    @Autowired
    FooClient fooClient;

    @GetMapping("/demo2")
    public String demo2() {
        String version = fooClient.version();
        return "[bar-service] foo.version: " + version;
    }
}
```

## 6.Hystrix



Hystrix 提供延迟和容错功能，隔离远程系统、访问和第三方程序库的访问点，防止级联失败，保证复杂的分布系统在面临不可避免的失败时，仍能有其弹性。



### [Hystrix](http://www.daimaku.net/post/view/10530)



大A2021-02-27 15:56:10标签:文章100

引入pom依赖

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
```

启动类

```java
@EnableCircuitBreaker
@SpringBootApplication
@EnableFeignClients
public static void main(String[] args) {
    SpringApplication.run(BarApplication.class, args);
}
```

服务类

```java
package com.example;

import com.netflix.hystrix.contrib.javanica.annotation.HystrixCommand;
import com.netflix.hystrix.contrib.javanica.annotation.HystrixProperty;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class BarService {

    @Autowired
    FooClient fooClient;

    @HystrixCommand(
            fallbackMethod = "fallback",
            commandProperties = {
                    @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "2000")
            },
            threadPoolKey = "fooServiceThreadPool",
            threadPoolProperties = {
                    @HystrixProperty(name = "coreSize", value = "30"),
                    @HystrixProperty(name = "maxQueueSize", value = "10")
            }
    )
    public String callFoo() {
        return fooClient.version(); // 去 foo-service 中模拟随机超过2秒的高延时
    }

    private String fallback() {
        return "降级内容";
    }
}
```

控制器

```java
@RestController
class TestController{
    @Autowired
    BarService barService;

    @GetMapping("/test")
    public String test() {
        return barService.callFoo();  
    }
}
```













