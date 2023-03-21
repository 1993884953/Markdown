​                                                                                                                                                                                     

# 数据库基础

数据库(Database, DB)，顾名思义就是存放数据的仓库，可以将大量的数据保存起来，并进行高效的访问

用来管理数据库的计算机系统称为`数据库管理系统` (Database Management System, DBMS)

`关系型数据库`是目前应用 最广泛的数据库，是由一张张的表格组成，每张表格有`行`和`列`，如下图所示

为了高效的管理这些数据，我们需要学习一种`结构化查询语言`(Structured Query Language, SQL)

> 不同的数据库管理系统，都支持标准SQL，例如下面列出的这些常见关系型数据库：
>
> - Oracle 甲骨文公司关系型数据库产品
> - SQL Server 微软公司的关系型数据库产品
> - MySQL 甲骨文公司开源关系型数据库产品
> - PostgreSQL 加州大学计算机系开发的开源关系型数据库

## SQL基础







> 为了高效的管理这些数据，我们需要学习一种`结构化查询语言`(Structured Query Language, SQL)



| 编号 | 标题   | 作者   | 出版社             | 售价  | 页数 |
| ---- | ------ | ------ | ------------------ | ----- | ---- |
| 1    | 呐喊   | 鲁迅   | 陕西师范大学出版社 | 22.00 | 297  |
| 2    | 西游记 | 吴承恩 | 群言出版社         | 44.50 | 645  |

> 表的列(垂直方向)称为字段，表的行(水平方向)称为记录，它相当于一条数据，关系数据库以`行`为单位进行数据操作

### 常用的数据类型

不同的列，可能有不同的数据类型，例如、数字、字符串、日期时间等等，常用的数据类型如下:

| 类型         | 存储占用空间  | 用途                                         |
| ------------ | ------------- | -------------------------------------------- |
| tinyint      | 1字节         | 较小的整数值(-128, 127)                      |
| int          | 4字节         | 整数值(-2147483648, 2147483647)              |
| decimal(m,n) | 变长          | 小数值，例如书的售价(共m位数字，其中小数n位) |
| char(n)      | 取决于n的大小 | 固定长度字符串                               |
| varchar(n)   | 取决于n的大小 | 变长字符串                                   |
| text         | 变长          | 长文本数据                                   |
| date         | 4字节         | 日期值，例如1949-10-01                       |
| datetime     | 8字节         | 年月日时分秒                                 |

> 上面这个表格并不完整，不同的数据库所支持的数据类型也有差别，这里先记住这些常用的类型。tinyint和int都可用于存放整数，我们在设计数据表的时候，在满足需求的情况下，尽量选择占用存储空间小一些的数据类型

```
CURRENT_TIMESTAMP   //當前时间戳
```

另外，有一个特殊的值，叫`null` ，用于表示“无”或“空缺”的意思，不同于数字`0`或`空字符串`

#### 方法演示

字段名在数据库中通常用选择使用有意义的英文单词，我们下面来设计表结构，用来存放书籍数据:

| 字段名    | 数据类型     | 备注   |
| --------- | ------------ | ------ |
| id        | int          | 编号   |
| title     | varchar(100) | 标题   |
| author    | varchar(50)  | 作者   |
| publisher | varchar(50)  | 出版社 |
| price     | decimal(8,2) | 售价   |
| page      | int          | 页数   |

表名使用`book`作为表名，到在线练习平台的数据库中，去创建这个表，见下图：

#### INSERT INTO 	增加数据

INSERT INTO	+ 表名 + (列名) + VALUES +	(各个值)				
表示插入数据到表中，括号中写上字段名，多个用`英文逗号`分隔，与列名对应的`值

```
INSERT INTO book (id, title, author, publisher, price, page) VALUES (1, "呐喊", "鲁迅", "陕西师范大学出版社", 22, 297)
```

#### SELECT * FROM 查询数据

SELECT * FROM + 表名

`SELECT`关键字表示查询数据，`*` 表示查出所有的字段(列),`FROM`关键字后面，写上我们的表名，就能查询出该表中，所有数据

```javascript
SELECT * FROM book
```

#### UPDATE ++ SET 修改数据

UPDATE + 表名 + SET + 列名=值+ WHERE+指定条件

> 不指定条件会全部更改

```
UPDATE book SET price = 45 WHERE id = 1
```

#### DELETE FROM	删除数据

DELETE FROM + 表名 +WHERE + 指定条件

```
DELETE FROM book WHERE id = 1
```

## 使用Python操作数据库

#### 新建一张表

在python界面输入数据库各种信息

```
CREATE TABLE `user` (
  `id` int NOT NULL AUTO_INCREMENT  PRIMARY KEY ,
  `username` varchar(50) NOT NULL COMMENT '帐号',
  `password` varchar(50) NOT NUL COMMENT '密码',
  `created_at` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='用户';
```

#### 连接到MySQL

```javascript
import pymysql.cursors

# 连接数据库
connection = pymysql.connect(host='改为你的数据库host',
                             user='你的数据库用户名',
                             password='你的数据库密码',
                             database='你的数据库名称',
                             cursorclass=pymysql.cursors.DictCursor)
# 获取游标
cursor= connection.cursor()
```

> 上面的代码执行完后，没有报错，就说明能连接到数据库

#### 执行SQL语句

连接成功后，继续写代码，让Python到数据中去执行SQL语句

```
# 新增一条
sql = "INSERT INTO user (username, password) VALUES (%s, %s)"
cursor.execute(sql, ['jack', '123456'])
connection.commit()
```

>执行之后，如果没有报错，到数据库中检查一下，是否有数据了

#### 查询数据

获取一条数据

```python
sql = "SELECT * FROM user WHERE username=%s"
cursor.execute(sql, ['jack'])
result = cursor.fetchone()
print(result['username'])
```

获取多条数据

```python
# 获取多条数据
sql = "SELECT * FROM user order by id desc limit 3"
cursor.execute(sql)
result = cursor.fetchall()
for u in result:
    print(u['username'])
```

## 聚合查询

```
--  查询单价小于20的数据条数
SELECT COUNT(*) FROM book WHERE price < 20

-- 查询平均单价
SELECT AVG(price) FROM book

-- 查询最大单价
SELECT MAX(price) FROM book

-- 查询最小单价
SELECT MIN(price) FROM book

-- 库存数量总和
SELECT SUM(quantity) FROM book
```

## 分页和排序

#### 对查询结果进行排序

```javascript
-- 通过价格列从低到高排序 (ASC可以省略)
SELECT * FROM book ORDER BY price ASC

-- 通过价格列从高到低排序
SELECT * FROM book ORDER BY price DESC

-- 通过价格列从高到低排序，针对价格相同的数据，按id列从小到大
SELECT * FROM book ORDER BY price DESC, id ASC
```

#### 分页返回数据

```javascript
-- 每页5条数据，返回第1页
SELECT * FROM book LIMIT 0,5
SELECT * FROM book LIMIT 5

-- 每页5条数据，返回第2页(跳过5条，返回5条)
SELECT * FROM book LIMIT 5,5

-- 每页5条数据，返回第3页(跳过前10条，返回5行)
SELECT * FROM book LIMIT 10,5
```

#### 一些复杂的查询条件

```javascript
-- 书名任意位置包含java的记录
SELECT * FROM book WHERE name LILE '%java%'

-- 书名以java开头的记录
SELECT * FROM book WHERE name LIKE 'java%'

-- 单价在10到20元之间的记录
SELECT * FROM book WHERE price >= 10 AND price <= 20
SELECT * FROM book WHERE price BETWEEN 10 AND 20

-- 查询id为1,2,3,6,7的记录
SELECT * FROM book WHERE id = 1 or id = 2 or id = 3 or id = 6 or id = 7
SELECT * FROM book WHERE id in (1,2,3,6,7)
```

> WHERE、ORDER BY、LIMIT 同时使用，注意顺序问题(WHERE在最前、LIMIT在最后)

```javascript
SELECT * FROM book WHERE price >= 10 ORDER BY id DESC LIMIT 3
```

#### java操作数据库

```
// 准备SQL语句
String sql = "SELECT * FROM book WHERE name LIKE ? ORDER BY id DESC LIMIT ?";
stmt = conn.prepareStatement(sql);

// 绑定占位符的值
//%1%两个百分号表示模糊搜索
stmt.setString(1,"书");   // 新版本驱动直接支持MySQL中的utf8mb4字符集
stmt.setInt(2, 5);

```

```java
package com.example;

import com.example.entity.Book;
import com.example.dao.BookDao;

import java.util.List;

public class App {
    //1、建包、域名+项目名
    //架包如果找不到就把lib里的文件夹添加为库
    //dao 为数据访问对象
    //book 为数据结构
    public static void main(String[] args) {

        Book book =new Book("图书名11",1213,"22.22","1223");
        BookDao bookDao=new BookDao();
        bookDao.create(book);
//        BookDao bookDao=new BookDao();
//        List<Book>books =bookDao.findBooks("图书",3);
//       for (Book obj:books){
//           System.out.println(obj.getId()+"\t"+obj.getName()+"\t"+obj.getPrice()+"\t"+obj.getPrice()+"\t"+obj.getIsbn());
//       }


    }
}

```

```java
package com.example.dao;

import com.example.entity.Book;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;


//数据访问包
public class BookDao {
    //Connection：返回一个链接
    private Connection getConnection(){
        Connection conn=null;
        try {
            // 加载驱动类 (mysql-connector-java-5.x)
            Class.forName("com.mysql.jdbc.Driver");

            // 如果mysql-connector-java-8.x 则使用下面的驱动类，最低要求Java8+
            // Class.forName("com.mysql.cj.jdbc.Driver");

            // 连接到本机(127.0.0.1)的test数据库，使用Unicode字符集UTF-8编码，不使用SSL，时区为东8区
            String url = "jdbc:mysql://127.0.0.1:3306/book?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai";
            conn = DriverManager.getConnection(url, "root", "");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return conn;
    }
    //创建book类，并且上传到MySql
    public void create(Book book) {

        // 操作数据库需要用到 java.sql 包中的三个类
        Connection conn = getConnection();         // 连接对象
        PreparedStatement stmt = null;  // 预处理对象
        ResultSet rs = null;            // 结果集对象

        try {
            // 准备SQL语句
            String sql = "INSERT INTO book (name, quantity) VALUES (?, ?)";
            stmt = conn.prepareStatement(sql);

            // 绑定占位符的值
            stmt.setString(1, book.getName());   // 新版本驱动直接支持MySQL中的utf8mb4字符集
            stmt.setInt(2, book.getQuantity());

            // 执行SQL
            stmt.execute();

            // 获取MySQL自增id
            rs = stmt.executeQuery("SELECT LAST_INSERT_ID()");
            int id;
            if (rs.next()) {
                id = rs.getInt(1);
                System.out.println("ID:" + id);
            }

            // 释放资源，关闭连接
            rs.close();
            stmt.close();
            conn.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //查找返回list类型数据
    public <list> List<Book> findBooks(String name, int size) {

        // 操作数据库需要用到 java.sql 包中的三个类
        Connection conn = getConnection();         // 连接对象
        PreparedStatement stmt = null;  // 预处理对象
        ResultSet rs = null;            // 结果集对象
        List<Book> bookList=new ArrayList<>();
        try {
            // 准备SQL语句
            String sql = "SELECT * FROM book WHERE name LIKE ? ORDER BY id DESC LIMIT ?";
            stmt = conn.prepareStatement(sql);

            // 绑定占位符的值
            //%1%两个百分号表示模糊搜索
            stmt.setString(1, "%"+name+"%");   // 新版本驱动直接支持MySQL中的utf8mb4字符集
            stmt.setInt(2, size);

            // 执行SQL
            stmt.execute();

            // 执行查询类型的SQL
            rs = stmt.executeQuery();

            System.out.println("id\tname\tquantity");

            // 循环输出结果集，next是移动到下一条记录，如果后面没有记录则返回false
            while (rs.next()) {
                Book book =new Book(rs.getInt("id"),rs.getString("name"),rs.getInt("quantity"),rs.getString("price"),rs.getString("isbn"));
//                book.setId(rs.getInt("id"));
//                book.setName(rs.getString("name"));
//                book.setQuantity(rs.getInt("quantity"));
//                book.setPrice(r s.getString("price"));
//                book.setIsbn(rs.getString("isbn"));
                bookList.add(book);
            }


            // 释放资源，关闭连接
            rs.close();
            stmt.close();
            conn.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
        return bookList;
    }
}
```

```java
package com.example.entity;

//建一个类储存可以被new出来的数据
public class Book {
    //创建与表相同的数据
    private  int id;
    private String name;
    private int quantity;
    private String price;
    private String isbn;

    public Book() {
    }

    public Book(String name, int quantity) {
        this.name = name;
        this.quantity = quantity;
    }

    public Book(int id, String name, int quantity, String price, String isbn) {
        this.id = id;
        this.name = name;
        this.quantity = quantity;
        this.price = price;
        this.isbn = isbn;
    }

    public Book(String name, int quantity, String price, String isbn) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
        this.isbn = isbn;
    }

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", quantity=" + quantity +
                ", price='" + price + '\'' +
                ", isbn='" + isbn + '\'' +
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

    public int getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }

    public String getPrice() {
        return price;
    }

    public void setPrice(String price) {
        this.price = price;
    }

    public String getIsbn() {
        return isbn;
    }

    public void setIsbn(String isbn) {
        this.isbn = isbn;
    }
}

```

# MySQL进阶

安装服务(开机自启动)，最后一个mysql表示服务名，如果不指定默认就是mysql

```
D:\MySQL\bin\mysqld --install mysql
```

启动服务

```
net start mysql
```

## **一、进入MySQL终端**

输密码时直接回车(默认密码为空)

```
winpty mysql -uroot -p
```

```
D:\MySQL\bin\mysql -uroot -p
```

我们在远和维护MySQL时，经常需要在终端下操作，这一节我们来熟悉并掌握这些内容

```javascript
# 连接到本机的MySQL
$ mysql -uroot -p
# 显示有哪些数据库
mysql> show databases;
# 创建一个叫test的数据库
mysql> create database  test;
# 进入到test数据库中
mysql> use test;
# 显示有哪些表
mysql> show tables;
# 创建一个user表
mysql> create table user (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50),
  created_at DATETIME
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
# 查看user表的字段信息
mysql> desc user;
# 查看user表的建表语句
mysql> show create table user;
# 删除user表
mysql> drop table user;
# 删除test数据库
mysql> drop database test;
# 退出MySQL
mysql> exit;
```

```
 create table user (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,username VARCHAR(50),created_at DATETIME) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 二、mysql数据备份与恢复

mysqldump 用于备份数据库到一个SQL文件中，下面示范将 `test`数据库，备份到 `test.sql`文件中，假设你数据库用户名为 `root`，密码为`12345`

```javascript
$ mysqldump -uroot -p12345 test > test.sql
```

如果需要将备份的数据恢复到MySQL中，使用下面的语句：

```javascript
# 先删除test数据库，从新创建一个空的 test库，再执行下面的语句
$ mysql -uroot -p12345 test < test.sql
```

```
 mysqldump -uroot -p test >test.sql
```

```
 mysql -uroot -p test< test.sql
```

准备一个50万数据的表，备份该数据库，耗时为多少？

将50万记录，恢复到数据库中，耗时为多少？

如何更快的导出和恢复数据?

## 三、事物

事务（Transaction）在计算机术语中是指访问并可能更新数据库中各种数据项的一个程序执行单元。事务由事务开始(begin transaction)和事务结束(end transaction)之间执行的全体操作组成。

事务应该具有4个属性：原子性、一致性、隔离性、持久性。这四个属性通常称为`ACID特性`。

-   原子性（atomicity） 一个事务是一个不可分割的工作单位，事务中包括的操作`要么都做`，`要么都不做`
-   一致性（consistency） 事务必须是使数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的
-   隔离性（isolation） 一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰
-   持久性（durability） 持久性也称永久性（permanence），指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的，接下来的其他操作或故障不应该对其有任何影响

接下来，用一个实例，来讲解事务:

一个转帐操作，从帐户1，扣款100元，然后将金额加到帐户2，相关SQL如下:

```mysql
UPDATE account SET balance = balance - 100 WHERE id = 1;

UPDATE account SET balance = balance + 100 WHERE id = 2;
```

如果在执行完第一句SQL之后，由于网络故障或其它原因，导致第二句SQL未执行，这就会发生数据不一致，用帐户1钱被扣了，但帐户2并没有收到从帐户1转帐过来的钱

我们如何利用事务机制，来避免这种情况呢？只需要将两条SQL，放在同一个事务中就行：

```mysql
BEGIN;

	UPDATE account SET balance = balance - 100 WHERE id = 1;

	UPDATE account SET balance = balance + 100 WHERE id = 2;

COMMIT;
```

`BEGIN`语句标记一个事务开始，`COMMIT`为提交事务。一个事务，只有提交成功(COMMIT)，数据变更才会被保留下来。在这个过程中，如果发生了意外情况，事务在没有提交前连接中断了，这个事务会被自动回滚，就像什么事也没有发生一样

例如，执行了 `BEGIN`语句，和第一条`UPDATE` 语句后，网络故障故障了，连接中断，MySQL就会立即将这个事务回滚掉，帐户1就不会被扣款

如果我们在事务过程中，由于业务需要，想手动回滚事务，在没有COMMIT之前，可以执行 `ROLLBACK `来完成

牢牢记住，开启一个事务后(BEGIN)，要么提交(COMMIT)，要么回滚(ROLLBACK)。开发中，千万不要忘记COMMIT或ROLLBACK

## 四、MySQL高级查询

### 1.1、普通多表关联查询

不易维护

>   查php 85分及以上的员的学生id，学生名，老师名，班级名，分数

```mysql
select
	stu.id, stu. name, grade . name, teacher .name, score . php
from
	stu, score, grade, teacher
where
	score.stu_id = stu.id and
	stu.grade_id = grade.id and
	grade.teacher_id = teacher.id and
	score.php>=85
```

>   as关健字可以省略为空格

```mysql
select
	stu.id, stu.name as stu_ name, grade .name as grade_ name, teacher .name as
	feacher_ name, score.php
from
	stu, score, grade , teacher
where
	score.stu_id = stu.id and
	stu.grade_id = grade.id and
	grade.teacher_id = teacher.id and
	score.php >=85
```

### 1.2、Json查询

>    同条件是score.php>=85,score表作为主表

![](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143927.png)



```mysql
select
	stu.id, stu.name as stu_ name, grade.name as grade_ name, teacher .name as
	teacher_ name, score.php
from score
	left join stu on score.stu_id = stu.id
	left join grade on stu.grade_id = grade.id
	left join teacher on grade.teacher_id = teacher.id
where
	score.php >=85
```

#### 1、**1eft inner (左右内外)**

>   left  join 在一张表的数据为空时会输出null ,推荐使用
>
>   inner join 会当被做废数据，直写join是inner join

```mysql
select score.*,stu.name from score inner join stu on score.stu_id = stu.id
select score.*,stu.name from score left join stu on score.stu_id = stu.id
```

>   *是全部查找

#### 2.显示所有参加了考式的学员姓名和成绩

```
select stu. name , score . html, score . php
from score
inner join stu on score.stu_id = stu.id
```

#### 3.显示所有的学员，和考试成功(没有参加考试的学员，也要显示)

```
select *
from stu
left join score on score.stu id = stu.id;
```

####  4.显示s05班级， htm1和php的平均成绩

```mysql
select
	avg(html) html_avg，avg(php) php_avg
from score
	left join stu on score.stu_id = stu.id
	left join grade on stu.grade_id = grade.id
where grade.name='s05';
```

#### 5.显示所有班级的平均成绩(班级id和平均分)

>   **GROUP BY** 语句用于结合聚合函数，根据一个或多个列对结果集进行分组

```mysql
select
grade_id,avg(html), avg(php)
from score
left join stu on stu.id = score.stu_ id;


select
	grade_ id, avg(htm1),avg(php)
from score
	inner join stu on stu.id = score.stu_ _id
group by grade_ id;
```

#### 6.显示所有班级的平均成绩(班级name、班级id、和平均分)

```mysql
select
	grade.name, avg(html),avg(php)
from score
	inner join stu on stu.id = score.stu_ _id
	inner join grade on stu.grade_ _id = grade.id
group by grade .name;
```

>   用了group by,select后只能用聚合函数或group by的字段

#### 7.php平均成绩小于85分的班级名称、和php平均成绩

```mysql
select 
	grade . name ,avg(php) as php_ _avg
from score
	inner join stu on stu.id = score.stu_ _id
	inner join grade on stu.grade_id = grade.id
group by grade . name
having php_ avg<85;
```

>   having用于分组之后加条件,where条件在分组前起作用
>
>   先执行where条件，后执行having

#### 8.查询显示班级名称，每个班级 邇过人数和未通过人数

```mysql
drop table if exists student;
CREATE TABLE student(
	name VARCHAR(50) DEFAULT '', /*学员姓名*/
	grade VARCHAR(50) DEFAULT '', /* 班级名称*/
	score INT DEFAULT 0   		  /*考试成绩*/
)ENGINE =MyISAM DEFAULT CHARSET = UTF8;
insert into student (name , grade ,score) values
('jack' ,'S05' ,90), .
('lily', 'S05',80),
('user1','S05' , 80),
( 'user3','S05' ,59),
('user2','S06' ,90), .
( 'user4' , 'S06',55),
('mary','S06',50);
```

```mysql
select grade ,
	sum(case when score<60 then 1 else 0 end) NO, 
	sum(case when score>=60 then 1 else 0 end) YES
from student
	group by grade;
```

![](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143928.png)

1.3、内外左右连接

交叉连接： 不适用任何匹配条件。生成笛卡尔积。

```
 select * from employee,department;
```

内连接： 只取两张表的共同部分

```
select * from employee inner join department on employee.dep_id = department.id;
```

左连接: 在内连接的基础上保留左表的记录（如果右表有左表没有会不显示右表有而左表没有的部分）

```
select * from employee left join department on employee.dep_id = department.id
```

右连接： 在内连接的基础上保留右表的记录（和左连接相反，如果左表有右表没有会不显示左表有而右表没有的部分））

```
select * from employee right join department on employee.dep_id = department.id
```

全外连接： 在内连接的基础上保留左右两表没有对应关系的记录（就是左右连接的合体，两者相互没有的都进行保留）

```
select * from employee left join department on employee.dep_id = department.id
union
select * from employee right join department on employee.dep_id = department.id
```

## 五、MySQL索引实验

我们给name列，加上`索引`，索引的名字为`ind_name`，SQL如下：

```javascript
ALTER TABLE t1 ADD INDEX ind_name (name);
```

先在你的数据库中，创建一张`t1`表：

| 字段名 | 数据类型    | 说明       |
| ------ | ----------- | ---------- |
| id     | int         | 主键、自增 |
| name   | varchar(50) | 不能为null |

建表SQL如下：

```javascript
CREATE TABLE `t1` (
  `id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(50)  NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

在这个表中的`name`字段，插入随机姓名数据，500万条

查询name为 `张三` 的数据，观察SQL执行时间，多执行几次，平均执行时间是多少？

接下来，我们给name列，加上`索引`，索引的名字为`ind_name`，SQL如下：

```javascript
ALTER TABLE t1 ADD INDEX ind_name (name);
```

在50万(或500万)条数据的情况下，为name列添加索引，耗时为多少毫秒？

现在有了索引，再执查询name为 `张三` 的数据，观察SQL执行时间，多执行几次，平均执行时间是多少？

MySQL索引的建立对于MySQL的高效运行是很重要的，索引可以大大提高MySQL的检索速度

接下来，我们试一下另一种情况，查询出所有姓 `张`的人，有多少条数据，观察耗时 

```mysql
SELECT * FROM t1 WHERE name LIKE '张%'
```

查询姓名中，任意位置包含`张`的，有多少条数据，观察耗时

```mysql
 SELECT * FROM t1 WHERE name LIKE '%张%'
```

总结：如果LIKE语句，以`%`开头，将无法利用到索引

我们平常开发时，怎么知道什么SQL用不到索引呢？

使用 `EXPLAIN` 或 `DESC` 令命，就可以观察MySQL的执行计划

```mysql
EXPLAIN SELECT * FROM t1 WHERE name LIKE '张%' \G

EXPLAIN SELECT * FROM t1 WHERE name LIKE '%张%' \G
```

EXPLAIN 输出的各列解释如下:

```http
table：查询的数据表

type：这是重要的列，显示连接使用了何种类型。从最好到最差的连接类型为const、eq_reg、ref、range、index和all。`如果是all，说明查询效率很低，需要做全表扫描

possible_keys：显示可能应用在这张表中的索引。如果为空，没有可能的索引。可以为相关的域从where语句中选择一个合适的语句

key： 实际使用的索引。如果为null，则没有使用索引。很少的情况下，mysql会选择优化不足的索引。这种情况下，可以在select语句中使用use index（indexname）来强制使用一个索引或者用ignore index（indexname）来强制mysql忽略索引

key_len：使用的索引的长度。在不损失精确性的情况下，长度越短越好

ref：显示索引的哪一列被使用了，如果可能的话，是一个常数

rows：mysql认为必须检查的用来返回请求数据的行数，mysql完成此请求扫描的行数

extra：关于mysql如何解析查询的额外信息
```

## 六、数据库的三大范式



**三大范式**是指数据库设计的基础标准

* 要求数据库表的每一列都是不可分割的原子数据项

* 在1NF的基础上，需要确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关
* 在2NF的基础上，非主键列必须直接依赖于主键，不能存在传递依赖

![image-20211206104116546](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143929.png)

#### 第一范式

可以具体的分割区域方便查找数据		

![image-20211206104315427](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143930.png)

#### 第二范式

主键为订单编号和产品编号，单独的订单编号和产品编号不能作为主键，所以把订单编号和产品编号联合在一起作为组合主键

![image-20211206104410794](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143931.png)

把一张表拆成三个表

![image-20211206110116502](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143932.png)

#### 第三范式

![image-20211206110330214](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143933.png)

## mysql简单查询

### 一 、任务卡 #1021 SQL简单查询

`user` 表数据如下

```
id    username    created_at
1    jack          2021-01-19 09:48:54
2    mary          2021-01-19 09:49:12
3    lily          2021-01-19 09:49:48
```

请查询出 id 为 2 的 username 和 created_at 两个字段的值，输出如下：

```
Username    CreatedAt
mary          2021-01-19 09:49:12
```

```mysql
SELECT
    user.username AS Username ,
    user.created_at AS CreatedAt 
FROM 
    user 
WHERE id = 2
```

### 二、 任务卡 #1023 SQL两表连查

题目描述

`category` 分类表部份数据如下

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |
| 2    | 网络协议 |

`book` 图书表部份数据如下

| id   | name               | category_id | quantity | price | isbn          | status |
| ---- | ------------------ | ----------- | -------- | ----- | ------------- | ------ |
| 1    | 深入理解计算机系统 | 4           | 100      | 22    | 9787111544937 | 1      |
| 2    | Java编程思想       | 1           | 100      | 33    | 3987111213826 | 1      |
| 4    | C语言程序设计      | 1           | 100      | 24    | 9687111213827 | 1      |
| 5    | Java并发编程之美   | 5           | 100      | 34    | 6687111213820 | 1      |

查询图书名、分类名、单价，按图书id倒序排，如果分类id不存在，该条图书数据不需要，返回部份结果例示如下：

| BookName       | CategoryName | Price |
| -------------- | ------------ | ----- |
| 汇编语言       | 编程语言     | 28    |
| Python科学计算 | 综合         | 83    |
| 现代编译原理   | 微服务       | 24    |
| 数据结构与算法 | 编程语言     | 55    |

```mysql
SELECT
    book.name AS BookName,
    category.name AS CategoryName,
    book.price AS Price	
FROM category
    inner join book on book.category_id = category.id
ORDER BY book.id DESC
```



###  三、任务卡 #1024 SQL查询在售图书库存数...

题目描述

`category` 分类表部份数据如下：

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |
| 2    | 网络协议 |

`book` 图书表部份数据如下：

| id   | name               | category_id | quantity | price | isbn          | status |
| ---- | ------------------ | ----------- | -------- | ----- | ------------- | ------ |
| 1    | 深入理解计算机系统 | 4           | 100      | 22    | 9787111544937 | 1      |
| 2    | Java编程思想       | 1           | 100      | 33    | 3987111213826 | 1      |
| 4    | C语言程序设计      | 1           | 100      | 24    | 9687111213827 | 1      |
| 5    | Java并发编程之美   | 5           | 100      | 34    | 6687111213820 | 1      |

status字段:1表示在售 2表示下架。

查询`在售`图书库存数量最多的2个分类，显示分类id和库存数量，按数量降序排，如下：

| category_id | sum  |
| ----------- | ---- |
| 3           | 433  |
| 4           | 200  |

```mysql
SELECT                                       
    category_id,
    SUM(quantity) AS sum
FROM book
WHERE status = 1 
	group by category_id
ORDER BY SUM(quantity) DESC LIMIT 2
```



###  四、 任务卡 #1025 SQL分组后筛选

题目描述

`category` 分类表部份数据如下：

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |
| 2    | 网络协议 |

`book` 图书表部份数据如下：

| id   | name               | category_id | quantity | price | isbn          | status |
| ---- | ------------------ | ----------- | -------- | ----- | ------------- | ------ |
| 1    | 深入理解计算机系统 | 4           | 100      | 22    | 9787111544937 | 1      |
| 2    | Java编程思想       | 1           | 100      | 33    | 3987111213826 | 1      |
| 4    | C语言程序设计      | 1           | 100      | 24    | 9687111213827 | 1      |
| 5    | Java并发编程之美   | 5           | 100      | 34    | 6687111213820 | 1      |

status字段:1表示在售 2表示下架。

`在售`图书库存总数量大于等于200的分类，显示分类id和总数量，升序排，最多返回2条，示例如下：

| category_id | sum  |
| ----------- | ---- |
| 4           | 200  |
| 1           | 500  |

```mysql
SELECT
    category_id,
    SUM(quantity) AS sum
FROM book
WHERE status = 1
group by category_id
having SUM(quantity)>=200

ORDER BY SUM(quantity) ASC LIMIT 2
```

### 五、 任务卡 #1026 SQL分组排序

题目描述

`category` 分类表部份数据如下：

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |
| 2    | 网络协议 |

`book` 图书表 部份数据如下：

| id   | name               | category_id | quantity | price | isbn          | status |
| ---- | ------------------ | ----------- | -------- | ----- | ------------- | ------ |
| 1    | 深入理解计算机系统 | 4           | 100      | 22    | 9787111544937 | 1      |
| 2    | Java编程思想       | 1           | 100      | 33    | 3987111213826 | 1      |
| 4    | C语言程序设计      | 1           | 100      | 24    | 9687111213827 | 1      |
| 5    | Java并发编程之美   | 5           | 100      | 34    | 6687111213820 | 1      |

status字段:1表示在售 2表示下架。

每个分类下`在售`图书的总金额，显示分类名称和金额，按金额倒序排，返回示例如下：

| name     | sum   |
| -------- | ----- |
| 微服务   | 17901 |
| 综合     | 10500 |
| 编程语言 | 5700  |
| 网络协议 | 1600  |

```mysql
SELECT
    category.name AS name,
    SUM(quantity*price) AS sum
FROM book 
    inner join category  on category.id = book.category_id
    WHERE status = 1
    group by category_id
ORDER BY SUM(quantity*price) DESC  
```

### 六、任务卡 #1027 SQL子查询

题目描述

`category` 分类表部份数据如下：

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |
| 2    | 网络协议 |

`book` 图书表 部份数据如下：

| id   | name               | category_id | quantity | price | isbn          | status |
| ---- | ------------------ | ----------- | -------- | ----- | ------------- | ------ |
| 1    | 深入理解计算机系统 | 4           | 100      | 22    | 9787111544937 | 1      |
| 2    | Java编程思想       | 1           | 100      | 33    | 3987111213826 | 1      |
| 4    | C语言程序设计      | 1           | 100      | 24    | 9687111213827 | 1      |

查询出图书id为 在1到5之间（包含5）这些图书的分类名称(分类id不存在的不需要返回)，显示分类id和分类名称（不能重复），id升序排，返回示例如下：

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |
| 4    | 综合     |

```mysql
SELECT
     id,name
FROM category  
    WHERE id  IN (SELECT category_id FROM book WHERE id BETWEEN 1 AND 5)
ORDER BY id
```

```mysql
SELECT
     book.name AS name, category_id
FROM book  
    left join category on book.category_id=category.id
WHERE  isnull(category.id)
```

### 七、任务卡 #1028 SQL左连接查询

题目描述

`category` 分类表部份数据如下：

| id   | name     |
| ---- | -------- |
| 1    | 编程语言 |

`book` 图书表 部份数据如下：

| id   | name               | category_id | quantity | price | isbn          | status |
| ---- | ------------------ | ----------- | -------- | ----- | ------------- | ------ |
| 1    | 深入理解计算机系统 | 4           | 100      | 22    | 9787111544937 | 1      |
| 6    | HTTP权威指南       | 2           | 100      | 16    | 9787121185632 | 1      |

查询分类id不存在的图书，显示图书名称和分类id，返回示例如下：

| name         | category_id |
| ------------ | ----------- |
| HTTP权威指南 | 2           |

```
SELECT 
    book.name AS name,
    book.category_id AS category_id
FROM book
LEFT  join category on category.id = book.category_id
WHERE isnull(category.id) ;
```



# mysql基础格式

```mysql
  需要查询出的数据
select ...
	( *,book.id,category.*,)

from...
	(from+主表)

//联合条件
join..
	( left join category on book.category_id=category.id)

//条件可以写子查询，isnull
where....
	WHERE id  IN (SELECT category_id FROM book WHERE id BETWEEN 1 AND 5)
	WHERE  isnull(category.id)

//分组前排序
group by...

//分组后排序
having...

//id倒序和升序
order by id DESC/ASC..

//跳过前五条,返回10条
limit [offset,] (rows)/limit 5,10
	
执行顺序：from... where...group by... having.... select ... order by... limit
```

```mysql
SELECT
	DISTINCT goods.id, 
	goods.`name`, 
	goods.`describe`, 
	goods.price, 
	goods.discount,
	
	goods_pic_info.pic_url, 
	

	goods_analyze.cart_count, 
	goods_analyze.sales_count,
	goods_analyze.favorite_count, 
	
	goods_analyze.cart_count*1+goods_analyze.sales_count*2+goods_analyze.favorite_count*3 AS heat 
FROM goods 
	LEFT JOIN goods_analyze ON 
		goods.id = goods_analyze.goods_id
	LEFT JOIN goods_pic_info ON 
		goods.id = goods_pic_info.goods_id
WHERE  goods.sellout = 0
	AND	(goods_pic_info.is_master IN (1) OR ISNULL(goods_pic_info.is_master))
	AND (goods.`name`LIKE '%西瓜%' OR goods.`describe`LIKE '%西瓜%') 
ORDER BY
 heat   							  	 -- 根据热度
-- 	goods_analyze.cart_count,    -- 根据加购
-- 	goods_analyze.sales_count,   -- 根据销量
-- 	goods_analyze.favorite_count -- 根据收藏

DESC LIMIT 0,100 
```





# MySQL安装

Windows系统安装MySQL可参考：

>   http://www.daimaku.net/post/view/10706

Linux 系统MySQL，可参考：

>   http://www.daimaku.net/post/view/10863

macOS系统MySQL，可参考：

>   https://www.cnblogs.com/nickchen121/p/11145123.html

#### windows系统

##### 一、下载

通过如下链接从官方网站下载MySQL

https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.13-winx64.zip

##### 二、解压

解压`mysql-5.7.13-winx64.zip`到 `D:\MySQL`

##### 三、管理员身份打开命令提示符

在系统的开始菜单上，单击鼠标右键，选择命令提示符(管理员)

![管理员运行.png](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143934.png)

也可以这样操作：`所有应用`->`Windows系统`中找到`命令提示符`，然后这时候在`命令提示符`上单击鼠标`右键`，选择以`管理员身份打开命令提示符`

##### 四、初始化数据库目录并安装服务

初始化数据目录 (如果报错，先安装 `Microsoft Visual C++2013`)

```
D:\MySQL\bin\mysqld --initialize-insecure --console
```

安装服务(开机自启动)，最后一个mysql表示服务名，如果不指定默认就是mysql

```
D:\MySQL\bin\mysqld --install mysql
```

启动服务

```
net start mysql
```

##### 五、终端连接

进入MySQL终端，输密码时直接回车(默认密码为空)

```
D:\MySQL\bin\mysql -uroot -p
```

如果需要可视化客户端，Windows下可以下载 `SQLyog`

##### 六、卸载

如果我们不再需要MySQL或是想要更换其它版本，可通过下面的方法，删除MySQL的服务

```
net stop mysql
D:\MySQL\bin\mysqld -remove mysql
```

#### Ubuntu 20.4 安装

##### 一、准备环境

```
$ cat /etc/issue
Ubuntu 20.04.2 LTS

# 安装MySQL依赖包
$ apt install  -y libaio1 libncurses*
```

##### 二、下载软件

从MySQL官网下载编译好的Linux二进制包

```
$ wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz
```

你也可以在本地电脑中提前下载好，通过scp等方式，上传到Linux中

##### 三、解压

解压到 /usr/local/ 目录中

```
$ tar -zxvf mysql-5.7.13-linux-glibc2.5-x86_64.tar.gz -C /usr/local/
```

进入 `/usr/local/`目录，将 `mysql-5.7.13-linux-glibc2.5-x86_64` 重命名为 `mysql/`

```
$ cd /usr/local/
$ mv mysql-5.7.13-linux-glibc2.5-x86_64 mysql/
```

##### 四、初始化数据库目录

创建一个叫做`mysql`的系统帐号

```
$ useradd -s /bin/false -M mysql

# 删除系统中默认MySQL配置文件
$ rm -f /etc/my.cnf /etc/mysql/my.cnf /usr/local/mysql/etc/my.cnf ~/.my.cnf

# 初始化数据库目录，执行成功后，在/usr/local/mysql中，将新产生一个data目录
$ /usr/local/mysql/bin/mysqld --initialize-insecure --user=mysql

[Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
[Warning] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
```

##### 五、启动服务

```
/usr/local/mysql/bin/mysqld_safe --user=mysql &
```

##### 六、测试连接

进入MySQL(默认空密码，直接回车)

```
$ /usr/local/mysql/bin/mysql -uroot -p

Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.7.13 MySQL Community Server (GPL)

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

建库建表

```
mysql> create database test;
Query OK, 1 row affected (0.00 sec)

mysql> use test;
Database changed

mysql> create table t1 (id int primary key auto_increment, name varchar(50)) engine=innodb default charset=utf8mb4;
Query OK, 0 rows affected (0.00 sec)
```

插入数据

```
mysql> insert into t1 (name) values ('jack');
Query OK, 1 row affected (0.01 sec)

#  查询数据
mysql> select * from t1;
+----+------+
| id | name |
+----+------+
|  1 | jack |
+----+------+
1 row in set (0.00 sec)
```

退出MySQL

```
mysql> exit
```

##### 七、常见错误解决

error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory

```
$ apt install -y libaio1
```

error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory

```
$ apt install  -y libncurses*
```

#### macos安装

目录

-   [一、安装](https://www.cnblogs.com/nickchen121/p/11145123.html#一、安装)
-   二、环境变量
    -   [2.1 MySQL服务的启停和状态的查看](https://www.cnblogs.com/nickchen121/p/11145123.html#21-mysql服务的启停和状态的查看)
-   [三、启动](https://www.cnblogs.com/nickchen121/p/11145123.html#三、启动)
-   四、初始化设置
    -   [4.1 退出sql界面](https://www.cnblogs.com/nickchen121/p/11145123.html#41-退出sql界面)
-   五、配置
    -   [5.1 检测修改结果](https://www.cnblogs.com/nickchen121/p/11145123.html#51-检测修改结果)


MySQL完整教程目录：https://www.cnblogs.com/nickchen121/p/14709373.html



##### 一、安装

第一步：打开网址，[https://www.mysql.com](https://www.mysql.com/) ，点击downloads之后跳转到https://www.mysql.com/downloads 选择Community选项

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143935.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-01.png?x-oss-process=style/watermark)

第二步： 第一步结束后程序会跳转到https://dev.mysql.com/downloads/ 网址，点击MySQL Community Server进入下面的页面，再点击5.6版本的数据库

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143936.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-02.png?x-oss-process=style/watermark)

第三步：mac操作系统 点击5.6版本之后会跳转到https://dev.mysql.com/downloads/mysql/5.6.html#downloads 网址，页面如下，确认好要下载的版本和操作系统，点击Download

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143937.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-03.png?x-oss-process=style/watermark)

第四步：可以不用登陆或者注册，直接点击`No thanks,just start my download`就可以下载了。

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143938.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-04.png?x-oss-process=style/watermark)

第五步：双击下载好的dmg文件，会弹出pkg弹框，再双击pkg图标，进入安装界面

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143939.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-05.png?x-oss-process=style/watermark)

第六步：在安装界面上一路继续，最后就安装成功了。

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143940.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-06.png?x-oss-process=style/watermark)

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143941.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-07.png?x-oss-process=style/watermark)

##### 二、环境变量

第一步 ：在终端切换到根目录，编辑./.bash_profile文件



```shell
$ cd ~
$ vim ./.bash_profile
```

第二步 ：进入vim 编辑环境。 按下i 进入 insert 模式 ，输入



```shell
export PATH=$PATH:/usr/local/mysql/bin
export PATH=$PATH:/usr/local/mysql/support-files
```

第三步 ：按下esc 退出 insert 模式，输入:wq保存配置文件。



```shell
:wq
```

第四步 ：在终端界面下输入以下命令，让配置文件的修改生效，并查看环境变量是否设置成功



```shell
$ source ~/.bash_profile 
$ echo $PATH
```

###### 2.1 MySQL服务的启停和状态的查看



```shell
停止MySQL服务
sudo mysql.server stop

重启MySQL服务
sudo mysql.server restart

查看MySQL服务状态
sudo mysql.server status
```

##### 三、启动

第一步 ：终端界面下输入



```shell
sudo mysql.server start
```

第二步 ：启动mysql服务,启动成功后继续输入



```shell
mysql -u root -p
```

第三步 ：直接回车进入数据库，看到下列欢迎页面

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143942.jpeg)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-08.png?x-oss-process=style/watermark)

##### 四、初始化设置

设置初始化密码，进入数据库mysql数据库之后执行下面的语句，设置当前root用户的密码为root。



```sql
set password = password('root');
```

[![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143943.png)](https://imgmd.oss-cn-shanghai.aliyuncs.com/Python从入门到放弃/195-Mac安装MySQL-09.png?x-oss-process=style/watermark)

###### 4.1 退出sql界面



```shell
exit
```

##### 五、配置

进入到 /usr/local/mysql/support-files 目录。里面有个文件:my-default.cnf

将其复制到桌面上，改名为my.cnf，将内容替换为。



```default
[mysqld]
default-storage-engine=INNODB
character-set-server=utf8
port = 3306

[client]
default-character-set=utf8
```

将修改后的文件my.cnf复制到 /etc 目录下。

重启mysql

###### 5.1 检测修改结果

​    

```sql
$mysql>>>show variables like '%char%';
```

至此数据库就可以愉快的使用啦！

###

# InnoDB储存引擎

 

```shell
#开始事务
mysql> begin;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from user;
+----+------+----------+
| id | name | email    |
+----+------+----------+
|  4 | jack | test@111 |
+----+------+----------+
1 row in set (0.00 sec)


#开启事务无法立即查询
mysql> select * from user;
+----+------+----------+
| id | name | email    |
+----+------+----------+
|  4 | jack | test@111 |
+----+------+----------+
1 row in set (0.00 sec)

#开启事务查询最新数据
mysql> select * from user for update;
mysql> select * from user lock in share mode;
+----+------+----------+
| id | name | email    |
+----+------+----------+
|  4 | jack | test@222 |
+----+------+----------+
1 row in set (0.00 sec) 

```





## mysql事务

==事务在mysql高阶讲过==

MySQL 事务主要用于处理操作量大，复杂度高的数据。

- 在 MySQL 中只有使用了 Innodb 数据库引擎的数据库或表才支持事务。
- 事务处理可以用来维护数据库的完整性，保证成批的 SQL 语句要么全部执行，要么全部不执行。
- 事务用来管理 insert,update,delete 语句

事务是必须满足4个条件（ACID）：：原子性（**A**tomicity，或称不可分割性）、一致性（**C**onsistency）、隔离性（**I**solation，又称独立性）、持久性（**D**urability）。

> 在 MySQL 命令行的默认设置下，事务都是自动提交的，即执行 SQL 语句后就会马上执行 COMMIT 操作。因此要显式地开启一个事务务须使用命令 BEGIN 或 START TRANSACTION，或者执行命令 SET AUTOCOMMIT=0，用来禁止使用当前会话的自动提交。

### 事务控制语句

1、用 BEGIN, ROLLBACK, COMMIT来实现

- **BEGIN** 开始一个事务
- **ROLLBACK** 事务回滚
- **COMMIT** 事务确认

2、直接用 SET 来改变 MySQL 的自动提交模式:

- **SET AUTOCOMMIT=0** 禁止自动提交
- **SET AUTOCOMMIT=1** 开启自动提交



> 使用保留点 SAVEPOINT

savepoint 是在数据库事务处理中实现“子事务”（subtransaction），也称为嵌套事务的方法。事务可以回滚到 savepoint 而不影响 savepoint 创建前的变化, 不需要放弃整个事务。

ROLLBACK 回滚的用法可以设置保留点 SAVEPOINT，执行多条操作时，回滚到想要的那条语句之前。

使用 SAVEPOINT

```
SAVEPOINT savepoint_name;    // 声明一个 savepoint

ROLLBACK TO savepoint_name;  // 回滚到savepoint
```

删除 SAVEPOINT

保留点再事务处理完成（执行一条 ROLLBACK 或 COMMIT）后自动释放。

MySQL5 以来，可以用:

```
RELEASE SAVEPOINT savepoint_name;  // 删除指定保留点
```

## InnoDB架构

### 概念区分

数据库：存储数据的物理操作系统文件或其他形式文件的集合
数据库实例：MySql数据库实例由后台线程以及一个共享内存区组成，负责操作数据库文件。
MySql是一个单进程多线程架构的数据库，MySql数据库实例在系统上表现就是一个进程。

### MySql架构

![preview](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143944.jpg)





## ==mysql储存引擎正式版==

**[show engines\g](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html)**  (查看储存引擎)



* InnoDB	
  * 支持事务、行级锁定和外键
    * 事务安全（符合 ACID）
    * 支持MVCC
    * 全文索引
* MyISAM
  * 基于哈希，存储在内存中，对临时表很有用
    * MyISAM不支持MVCC所以不支持事务
* MEMORY
  * 基于哈希，存储在内存中，对临时表很有用
* CSV 
  * CSV storage engine       

```shell
mysql> show engines\g;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
9 rows in set (0.00 sec)
```



MYISAM5.5版本吧之前的

从mysql 5.5.5开始InnoDB作为默认的储存引擎

- [`InnoDB`](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html): MySQL 5.7 中的默认存储引擎。 `InnoDB`是用于 MySQL 的事务安全（符合 ACID）存储引擎，具有提交、回滚和崩溃恢复功能以保护用户数据。 `InnoDB`行级锁定（不升级到更粗粒度的锁定）和 Oracle 风格的一致非锁定读取提高了多用户并发性和性能。`InnoDB`将用户数据存储在聚集索引中，以减少基于主键的常见查询的 I/O。为了维护数据完整性， `InnoDB`还支持`FOREIGN KEY`引用完整性约束。有关 的更多信息`InnoDB`，请参阅 [第 14 章，*InnoDB 存储引擎*](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html)。
- [`MyISAM`](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html)：这些表占用空间小。 [表级锁定](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_table_lock) 限制了读/写工作负载的性能，因此它通常用于 Web 和数据仓库配置中的只读或以读取为主的工作负载。
- [`Memory`](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html)：将所有数据存储在 RAM 中，以便在需要快速查找非关键数据的环境中快速访问。该发动机以前称为`HEAP`发动机。它的用例正在减少；`InnoDB`它的缓冲池内存区域提供了一种通用且持久的方式来将大部分或所有数据保存在内存中，并 `NDBCLUSTER`为庞大的分布式数据集提供快速的键值查找。
- [`CSV`](https://dev.mysql.com/doc/refman/5.7/en/csv-storage-engine.html): 它的表格实际上是带有逗号分隔值的文本文件。CSV 表允许您以 CSV 格式导入或转储数据，以便与读取和写入相同格式的脚本和应用程序交换数据。由于 CSV 表没有索引，因此您通常`InnoDB`在正常操作期间将数据保存在表中，并且仅在导入或导出阶段使用 CSV 表。
- [`Archive`](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html)：这些紧凑的、未编制索引的表旨在存储和检索大量很少引用的历史、归档或安全审计信息。
- [`Blackhole`](https://dev.mysql.com/doc/refman/5.7/en/blackhole-storage-engine.html): Blackhole 存储引擎接受但不存储数据，类似于 Unix`/dev/null`设备。查询总是返回一个空集。这些表可用于复制配置，其中 DML 语句被发送到副本服务器，但源服务器不保留自己的数据副本。
- [`NDB`](https://dev.mysql.com/doc/refman/5.7/en/mysql-cluster.html)（也称为 [`NDBCLUSTER`](https://dev.mysql.com/doc/refman/5.7/en/mysql-cluster.html)）：此集群数据库引擎特别适用于需要尽可能高的正常运行时间和可用性的应用程序。
- [`Merge`](https://dev.mysql.com/doc/refman/5.7/en/merge-storage-engine.html)：使 MySQL DBA 或开发人员能够对一系列相同的`MyISAM`表进行逻辑分组并将它们作为一个对象引用。适用于 VLDB 环境，例如数据仓库。
- [`Federated`](https://dev.mysql.com/doc/refman/5.7/en/federated-storage-engine.html)：提供链接不同的 MySQL 服务器以从多个物理服务器创建一个逻辑数据库的能力。非常适合分布式或数据集市环境。
- [`Example`](https://dev.mysql.com/doc/refman/5.7/en/example-storage-engine.html)：这个引擎作为 MySQL 源代码中的一个示例，说明了如何开始编写新的存储引擎。它主要是开发人员感兴趣的。存储引擎是一个 不做任何事情的“存根” 。您可以使用此引擎创建表，但无法在其中存储或检索任何数据。

建表语句，指定引擎为InnoDB 不指定，默认为InnoDB

**表 15.1 存储引擎功能摘要**

| 特征                    | MyISAM     | **Memory**   | InnoDB     | **Archive** | **NDB**    |
| :---------------------- | :--------- | :----------- | :--------- | :---------- | :--------- |
| B-tree索引              | 是的       | 是的         | 是的       | 不          | 不         |
| 备份/时间点恢复（注 1） | 是的       | 是的         | 是的       | 是的        | 是的       |
| 集群数据库支持          | 不         | 不           | 不         | 不          | 是的       |
| 聚集索引                | 不         | 不           | 是的       | 不          | 不         |
| 压缩数据                | 是（注2）  | 不           | 是的       | 是的        | 不         |
| 数据缓存                | 不         | 不适用       | 是的       | 不          | 是的       |
| 加密数据                | 是（注 3） | 是（注 3）   | 是（注 4） | 是（注 3）  | 是（注 3） |
| 外键支持                | 不         | 不           | 是的       | 不          | 是（注 5） |
| 全文检索索引            | 是的       | 不           | 是（注 6） | 不          | 不         |
| 地理空间数据类型支持    | 是的       | 不           | 是的       | 是的        | 是的       |
| 地理空间索引支持        | 是的       | 不           | 是（注 7） | 不          | 不         |
| 哈希索引                | 不         | 是的         | 否（注 8） | 不          | 是的       |
| 索引缓存                | 是的       | 不适用       | 是的       | 不          | 是的       |
| 锁定粒度                | Table      | Table        | Row        | Row         | Row        |
| MVCC                    | 不         | 不           | 是的       | 不          | 不         |
| 复制支持（注 1）        | 是的       | 有限（注 9） | 是的       | 是的        | 是的       |
| 存储限制                | 256TB      | 内存         | 64TB       | 没有任何    | 384EB      |
| T-树索引                | 不         | 不           | 不         | 不          | 是的       |
| 交易                    | 不         | 不           | 是的       | 不          | 是的       |
| 更新数据字典的统计信息  | 是的       | 是的         | 是的       | 是的        | 是的       |

**指定引擎**

![image-20220606153825515](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143945.png)

### InnoDB记录结构

Mysql 5.7 参考手册 / InnoDB存储引擎 /InnoDB行格式

https://dev.mysql.com/doc/refman/5.7/en/innodb-row-format.html

将数据存入Mysql时，最小单位是行（ROW），一行就是一条记录

| 行格式                 | 紧凑的存储特性 | 增强的可变长度列存储 | 大索引键前缀支持 | 压缩支持 | 支持的表空间类型                | 所需文件格式          |
| :--------------------- | :------------- | :------------------- | :--------------- | :------- | :------------------------------ | :-------------------- |
| `REDUNDANT`            | No             | No                   | No               | No       | system, file-per-table, general | Antelope or Barracuda |
| `COMPACT`(压缩)        | Yes            | No                   | No               | No       | system, file-per-table, general | Antelope or Barracuda |
| `DYNAMIC`(基于compact) | Yes            | Yes                  | Yes              | No       | system, file-per-table, general | Barracuda             |
| `COMPRESSED`           | Yes            | Yes                  | Yes              | Yes      | file-per-table, general         | Barracuda             |

![image-20220606152523842](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143946.png)



```
show table status\g;
使用不了
```

![image-20220606154447780](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143947.png)

```
f3 f4 列  允许为NULL

insert into t1 (f1,f2,f3,f4) valuses ('AAAA','B','CC',NULL);
长度 
```

![image-20220606155445707](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143948.png)

记录头信：删除标记(数据库隐藏数据假删)、下一行记录的位置、等等
隐藏列：

* DB ROW ID、

  * 数据库自己的主键id(如果表内字段无主键)

* DB TRX ID、

  * 事务id

* DB ROLL_PTR

  * 回滚指针

   

  ![image-20220606160139000](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143949.png) 



### InnoDB数据页结构

是InnoDB管理储存空间的基本单位，一个页的大小是16KB

主键为链表进行存放 

![image-20220606160342541](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143950.png)

## 索引

![image-20220606160817671](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143951.png)



> B+tree

![image-20220606161244976](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143952.png)

> 聚簇索引（一级索引）

-   所有完整的数据都存放在这个聚簇索引的叶子结点处
-   聚簇索引只能在搜索条件是主键值时才能发挥作用，因为B+树中的数据都是按照主键进行排序的

> 二级索引

![ ](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143953.png)

![image-20220606161552513](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143954.png)

一级索引可以单独存在，二级索引不能单独存在，必须依附于一级索引，这叫做回表

![image-20220606161753196](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143955.png)

如果只查id和age，就是`索引覆盖`（select后的字段，能少点就少）



二级索引是指定字段与主键的映射，主键长度越小，普通索引的叶子结点就越小，二级索引上占用的空间就越小，   所以要避免使用过长的字段作为主键 （一般尽量用整数作为主键）



数据加载单位（以Page为单位加载，减少硬盘访问次数），数据变化写盘同样以Page为单位

![image-20220606162123273](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143956.png)





> 启动参数

```java
--innodb_buffer_pool_size=3G
//缓冲池的大小
```





## 事务



### 事务特性

[MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/) / [The InnoDB Storage Engine](https://dev.mysql.com/doc/refman/5.7/en/innodb-storage-engine.html) / InnoDB and the ACID Model

https://dev.mysql.com/doc/refman/5.7/en/mysql-acid.html

The following sections discuss how MySQL features, in particular the `InnoDB` storage engine, interact with the categories of the ACID model:

- **A**: atomicity.
- **C**: consistency.
- **I**: isolation.
- **D**: durability.

### 隔离级别



[MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/) / [...](https://dev.mysql.com/doc/refman/5.7/en/innodb-transaction-isolation-levels.html) / Transaction Isolation Levels	

https://dev.mysql.com/doc/refman/5.7/en/innodb-transaction-isolation-levels.html



> 不同隔离级别带来的数据操作问题：

1.脏读(读未提交)：

两个事务，t1事务可以读取到t2事务正在做更 改的数据的中间状态(t2事务执行过程中)，而这个数据的更改有可能不会被持久化(commit)，而是rollback，导致t1在同一事务内的两次读取同一行数据得到结果不同。

2.不可重复读：

t1事务在整个事务执行过程中读取某一条记录多次，发现读取的此条记录不是每次都一样。

3.幻读：

t1事务在整个事务执行过程中读取某一范围内的数据 ，在第二次读取时发现多了几行或者少了几行。





> READ UNCOMMITTED  ->脏读

```java
read uncommited--读未提交 (A可以读取B事务未提交的数据)
 该隔离级别指即使一个事务的更新语句没有提交,但是别的事务可以读到这个改变，几种异常情况都可能出现。极易出错，没有安全性可言，基本不会使用。
```



> READ COMMITTED  ->不可重复读

```java
read committed --读已提交 (未提交则查不到)
 该隔离级别指一个事务只能看到其他事务的已经提交的更新，看不到未提交的更新，消除了脏读和第一类丢失更新，这是大多数数据库的默认隔离级别，如Oracle,Sqlserver。
```



> REPEATABLE READ ->可重复读 出现幻读问题mysql默认

```java
repeatable read --可重复读 (事务查到什么就是什么,查询时删除数据 )
 该隔离级别指一个事务中进行两次或多次同样的对于数据内容的查询，得到的结果是一样的，但不保证对于数据条数的查询是一样的，只要存在读改行数据就禁止写，消除了不可重复读和第二类更新丢失，这是Mysql数据库的默认隔离级别。
```



> SERIALIZABLE ->串行化 没有并发

```java
serializable --序列化读
 意思是说这个事务执行的时候不允许别的事务并发写操作的执行.完全串行化的读，只要存在读就禁止写,但可以同时读，消除了幻读。这是事务隔离的最高级别，虽然最安全最省心，但是效率太低，一般不会用。
```

### mysql事务实现原理

- redo log (异常恢复)
- undo log (回滚) 
- MVCC （多版本并发控制）解决读写冲突，使用隐藏队列
- 快照读 
- 当前读



redo log

磁盘顺序写入，不要每次都刷一页的数据到磁盘（修改的数据未必要一个页中，还会导致大量随机写）



这个参数对性能影响较大



```mysql
mysql> show variables like 'innodb_flush_log_at_trx_commit';
+--------------------------------+-------+
| Variable_name                  | Value |
+--------------------------------+-------+
| innodb_flush_log_at_trx_commit | 1     |
+--------------------------------+-------+
1 row in set, 1 warning (0.54 sec)

innodb_flush_log_at_trx_commit = 0 每秒写一次日志（写的时候直接刷到硬盘不利用os的缓存），极端的情况是丢失1秒的数据变更 flush + fsync
innodb_flush_log_at_trx_commit = 1 就是实时写日志（不利用os的缓存），最安全，性能很低 flush + fsync

innodb_flush_log_at_trx_commit = 2 每次事务写日志，但利用os的文件缓存机制，MYSQL挂了只要os不挂，就不会丢数据  只做 fsync
```

MYSQL中日志缓存叫：log buffer(flush,将Mysql中的日志缓存区内容写到文件中)

操作系统文件缓存中：os cache （fsync，让操作系统把文件缓存中的内容写盘）



undo log 回滚日志，保证事务原子性，实现数据多版本

![image-20220606172243504](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143957.png)

MVCC Read VIew

活跃事务列表，最小事务ID，最大事务ID



- 快照读 
  -  查询回滚日志之前的数据
  -  当前读



- 当前读

  - FOR UPDATE

  - LOCK IN SHARE MOODE

  - DELETE

  - UPDATE

  - INSET

    

## 锁

[MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/) / [...](https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html) / InnoDB Locking

https://dev.mysql.com/doc/refman/5.7/en/innodb-locking.html

#### 共享锁和独占锁

* lock inshare mode   (**读锁S **可共享,其他不可)

  > select from user where name='cc' for update;

  * for update 	(**写锁X**)



`InnoDB` implements standard row-level locking where there are two types of locks, [shared (`S`) locks](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_shared_lock) and [exclusive (`X`) locks](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_exclusive_lock).

- A [shared (`S`) lock](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_shared_lock) permits the transaction that holds the lock to read a row.
- An [exclusive (`X`) lock](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_exclusive_lock) permits the transaction that holds the lock to update or delete a row.

![image-20220606094549349](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143958.png)

select @@tx_isolation

```shell
+-----------------+
| @@tx_isolation  |
+-----------------+
| REPEATABLE-READ |
+-----------------+
```

```shell
#两个cmd终端,session对全局线程生效,global对当前线程生效
set global transaction isolation level Read committed;
set session transaction isolation level Read committed;
```



![image-20220606095144344](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143959.png)

![image-20220606095610044](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143960.png)

#### 间隙锁 Gap locks

> 表空的时候会锁住整条数据

![image-20220606100716810](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143961.png)

![image-20220606101235164](images/220-InnoDB/image-20220606101235164.png

> 二级索引也会被锁住 (索引会影响锁)
>
> 二级索引之间的字符集排序也会被锁住
>
> 如果没有索引会锁全表(全表死锁)

![image-20220606101701103](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143962.png)

#### 锁冲突

  当2个数据同时进行转账时,会导致锁住



# 特殊查询

## mysql 查询当天、本周,本月,上一个月的数据

 更新时间：2018年01月29日 15:53:42  作者：沐浴春风  

这篇文章主要介绍了mysql 查询当天、本周,本月,上一个月的数据的sql代码，在文中还给大家提到了mysql如何查询当天信息，具体内容详情大家参考下本文



**今天**

```
select` `* ``from` `表名 ``where` `to_days(时间字段名) = to_days(now());
```

**昨天**

```
SELECT` `* ``FROM` `表名 ``WHERE` `TO_DAYS( NOW( ) ) - TO_DAYS( 时间字段名) <= 1
```

**近7天**

```
SELECT` `* ``FROM` `表名 ``where` `DATE_SUB(CURDATE(), INTERVAL 7 ``DAY``) <= ``date``(时间字段名)
```

**近30天**

```
SELECT` `* ``FROM` `表名 ``where` `DATE_SUB(CURDATE(), INTERVAL 30 ``DAY``) <= ``date``(时间字段名)
```

**本月**

```
SELECT` `* ``FROM` `表名 ``WHERE` `DATE_FORMAT( 时间字段名, ``'%Y%m'` `) = DATE_FORMAT( CURDATE( ) , ``'%Y%m'` `)
```

**上一月**

```
SELECT` `* ``FROM` `表名 ``WHERE` `PERIOD_DIFF( date_format( now( ) , ``'%Y%m'` `) , date_format( 时间字段名, ``'%Y%m'` `) ) =1
```

**查询本季度数据**

```
select` `* ``from` ``ht_invoice_information` ``where` `QUARTER(create_date)=QUARTER(now());
```

**查询上季度数据**

```
select` `* ``from` ``ht_invoice_information` ``where` `QUARTER(create_date)=QUARTER(DATE_SUB(now(),interval 1 QUARTER));
```

**查询本年数据**

```
select` `* ``from` ``ht_invoice_information` ``where` `YEAR``(create_date)=``YEAR``(NOW());
```

**查询上年数据**

```
select` `* ``from` ``ht_invoice_information` ``where` `year``(create_date)=``year``(date_sub(now(),interval 1 ``year``));
```

**查询当前这周的数据**

```
SELECT` `name``,submittime ``FROM` `enterprise ``WHERE` `YEARWEEK(date_format(submittime,``'%Y-%m-%d'``)) = YEARWEEK(now());
```

**查询上周的数据**

```
SELECT` `name``,submittime ``FROM` `enterprise ``WHERE` `YEARWEEK(date_format(submittime,``'%Y-%m-%d'``)) = YEARWEEK(now())-1;
```

**查询上个月的数据**

```
select` `name``,submittime ``from` `enterprise ``where` `date_format(submittime,``'%Y-%m'``)=date_format(DATE_SUB(curdate(), INTERVAL 1 ``MONTH``),``'%Y-%m'``)``select` `* ``from` `user` `where` `DATE_FORMAT(pudate,``'%Y%m'``) = DATE_FORMAT(CURDATE(),``'%Y%m'``) ; ``select` `* ``from` `user` `where` `WEEKOFYEAR(FROM_UNIXTIME(pudate,``'%y-%m-%d'``)) = WEEKOFYEAR(now()) ``select` `* ``from` `user` `where` `MONTH``(FROM_UNIXTIME(pudate,``'%y-%m-%d'``)) = ``MONTH``(now()) ``select` `* ``from` `user` `where` `YEAR``(FROM_UNIXTIME(pudate,``'%y-%m-%d'``)) = ``YEAR``(now()) ``and` `MONTH``(FROM_UNIXTIME(pudate,``'%y-%m-%d'``)) = ``MONTH``(now()) ``select` `* ``from` `user` `where` `pudate ``between` `上月最后一天 ``and` `下月第一天
```

**查询当前月份的数据**

```
select` `name``,submittime ``from` `enterprise ``where` `date_format(submittime,``'%Y-%m'``)=date_format(now(),``'%Y-%m'``)
```

**查询距离当前现在6个月的数据**

```
select` `name``,submittime ``from` `enterprise ``where` `submittime ``between` `date_sub(now(),interval 6 ``month``) ``and` `now();
```

**PS:下面看下mysql如何查询当天信息？**

原来不是太熟悉SQL查询语句，什么都是用到了再去查去找，还好网络提供给我们很多支持。今天又用到了一个语句，一时间真想不出怎么解决，到网上看了看，感觉就有一个，怎么那么简单啊。需要积累的东西真是太多了。

今天就把我这个简单的问题记录下来吧!算是一个积累：

mysql查询当天的所有信息：

```
select` `* ``from` `test ``where` `year``(regdate)=``year``(now()) ``and` `month``(regdate)=``month``(now()) ``and` `day``(regdate)=``day``(now())
```

这个有一些繁琐，还有简单的写法：

```
select` `* ``from` `table` `where` `date``(regdate) = curdate();
```

date()函数获取日期部分, 扔掉时间部分，然后与当前日期比较即可

## mysql 行转列与列转行

mysql 中行转列我们用的是内部函数实现过， 就是 cast when then else end 这种列转行使用 union 关键字把多个 select 语句结果捏合到一个结果来实现  

![image-20220616192642170](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143963.png)

## mysql 查询重复数据

比如 A 表有字段 id， pid， sname，

```sql
#查询重复数据： 
select * from A
where pid in 
(select pid from A group by pid having count(pid) > 1);  
```



# mysql 查询语句的优化

### mysql 查询语句的优化

```sql
#对查询进行优化， 应尽量避免全表扫描， 首先应考虑在 where 及 order by 涉及的列上建立索引。  

#应尽量避免在 where 子句中使用!=或<>操作符， 否则引擎将放弃使用索引而进行全表扫描。

#应尽量避免在 where 子句中对字段进行函数操作， 这将导致引擎放弃使用索引而进行全表扫描

#应尽量避免在 where 子句中对字段进行 null 值判断， 否则将导致引擎放弃使用索引而进行全表扫描， 如：
select id from t where num is null #错误格式
select id from t where num=0 #可以在 num 上设置默认值 0 ,确保表中 num 列没有 null 值

#应尽量避免在 where 子句中使用 or 来连接条件， 否则将导致引擎放弃使用索引而进行全表扫描， 如： 
select id from t where num=10 or num=20  #错误格式
select id from t where num=10 union all select id from t where num=20

#以%开头的模糊查询也会导致全表扫描： 
select id from t where name like '%abc%' # 如果要提高效率的话， 可以考虑全文检索来解决。

#in 和 not in 也要慎用， 否则会导致全表扫描， 如： 
select id from t where num in(1,2,3)  #错误格式
select id from t where num between 1 and 3  #对于连续的数值， 能用 between 就不要用 in 了

#应尽量避免在 where 子句中对字段进行表达式操作， 这将导致放弃使用索引而进行全表扫描。 如： 
select id from t where num/2=100 	#错误格式
select id from t where num=100*2
```

##  批量插入 5000 条数据如何优化？

• 第一种方法：
合并 sql 插入语句， 合并后日志量减少， 降低日志刷盘的数据量和频率， 从而提高效率， 通过合并 SQL 语句，同时也能减少 SQL 语句解析的次数， 减少网络传输的 IO

```mysql
INSERT INTO table(uid,content, type) VALUES ('userid_0', 'content_0', 0); #d
# 改为：
INSERT INTO table (uid,content, type) VALUES ('userid_0', 'content_0', 0), ('userid_1','content_1',1);
```

• 第二种方法：
在同一个事务中进行插入处理这是因为进行一个 INSERT 操作时， MySQL 内部会建立一个事务， 在事务内才进行真正插入处理操作。 通过使用同一个事务可以减少创建事务所消耗的时间， 所有插入都在执行后才统一进行提交操作。  



# MySQL 之全文索引

## 概念

通过数值比较、范围过滤等就可以完成绝大多数我们需要的查询，但是，如果希望通过关键字的匹配来进行查询过滤，那么就需要基于相似度的查询，而不是原来的精确数值比较。全文索引就是为这种场景设计的。

你可能会说，用 like + % 就可以实现模糊匹配了，为什么还要全文索引？like + % 在文本比较少时是合适的，但是对于大量的文本数据检索，是不可想象的。全文索引在大量的数据面前，能比 like + % 快 N 倍，速度不是一个数量级，但是全文索引可能存在精度问题。

你可能没有注意过全文索引，不过至少应该对一种全文索引技术比较熟悉：各种的搜索引擎。虽然搜索引擎的索引对象是超大量的数据，并且通常其背后都不是关系型数据库，不过全文索引的基本原理是一样的。

## 版本支持

开始之前，先说一下全文索引的版本、存储引擎、数据类型的支持情况

1. MySQL 5.6 以前的版本，只有 MyISAM 存储引擎支持全文索引；
2. MySQL 5.6 及以后的版本，MyISAM 和 InnoDB 存储引擎均支持全文索引;
3. 只有字段的数据类型为 char、varchar、text 及其系列才可以建全文索引。

测试或使用全文索引时，要先看一下自己的 MySQL 版本、存储引擎和数据类型是否支持全文索引。

## 操作全文索引

索引的操作随便一搜都是，这里还是再啰嗦一遍。

## 创建

1.创建表时创建全文索引

```sql
create table fulltext_test (
    id int(11) NOT NULL AUTO_INCREMENT,
    content text NOT NULL,
    tag varchar(255),
    PRIMARY KEY (id),
    FULLTEXT KEY content_tag_fulltext(content,tag)  // 创建联合全文索引列
) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```

2.在已存在的表上创建全文索引

```sql
create fulltext index content_tag_fulltext
    on fulltext_test(content,tag);
```

3.通过 SQL 语句 ALTER TABLE 创建全文索引

```sql
alter table fulltext_test
    add fulltext index content_tag_fulltext(content,tag);
```

## 修改

修改个 O，直接删掉重建。

## 删除

1.直接使用 DROP INDEX 删除全文索引

```sql
drop index content_tag_fulltext
    on fulltext_test;
```

2.通过 SQL 语句 ALTER TABLE 删除全文索引

```sql
alter table fulltext_test
    drop index content_tag_fulltext;
```

## 使用全文索引

和常用的模糊匹配使用 like + % 不同，全文索引有自己的语法格式，使用 match 和 against 关键字，比如

```sql
select * from fulltext_test  where match(content,tag) against('xxx xxx');
```

**注意：** match() 函数中指定的列必须和全文索引中指定的列完全相同，否则就会报错，无法使用全文索引，这是因为全文索引不会记录关键字来自哪一列。如果想要对某一列使用全文索引，请单独为该列创建全文索引。

## 测试全文索引

## 添加测试数据

有了上面的知识，就可以测试一下全文索引了。

首先创建测试表，插入测试数据

```sql
create table test (
    id int(11) unsigned not null auto_increment,
    content text not null,
    primary key(id),
    fulltext key content_index(content)
) engine=MyISAM default charset=utf8;

insert into test (content) values ('a'),('b'),('c');
insert into test (content) values ('aa'),('bb'),('cc');
insert into test (content) values ('aaa'),('bbb'),('ccc');
insert into test (content) values ('aaaa'),('bbbb'),('cccc');
```

按照全文索引的使用语法执行下面查询

```sql
select * from test where match(content) against('a');
select * from test where match(content) against('aa');
select * from test where match(content) against('aaa');
```

根据我们的惯性思维，应该会显示 4 条记录才对，然而结果是 1 条记录也没有，只有在执行下面的查询时

```sql
select * from test where match(content) against('aaaa');
```

才会搜到 *aaaa* 这 1 条记录。

为什么？这个问题有很多原因，其中最常见的就是 **最小搜索长度** 导致的。另外插一句，使用全文索引时，测试表里至少要有 4 条以上的记录，否则，会出现意想不到的结果。

MySQL 中的全文索引，有两个变量，最小搜索长度和最大搜索长度，对于长度小于最小搜索长度和大于最大搜索长度的词语，都不会被索引。通俗点就是说，想对一个词语使用全文索引搜索，那么这个词语的长度必须在以上两个变量的区间内。

这两个的默认值可以使用以下命令查看

```sql
show variables like '%ft%';
```

可以看到这两个变量在 MyISAM 和 InnoDB 两种存储引擎下的变量名和默认值

```sql
// MyISAM
ft_min_word_len = 4;
ft_max_word_len = 84;

// InnoDB
innodb_ft_min_token_size = 3;
innodb_ft_max_token_size = 84;
```

可以看到最小搜索长度 MyISAM 引擎下默认是 4，InnoDB 引擎下是 3，也即，MySQL 的全文索引只会对长度大于等于 4 或者 3 的词语建立索引，而刚刚搜索的只有 *aaaa* 的长度大于等于 4。

## 配置最小搜索长度

全文索引的相关参数都无法进行动态修改，必须通过修改 MySQL 的配置文件来完成。修改最小搜索长度的值为 1，首先打开 MySQL 的配置文件 /etc/my.cnf，在 [mysqld] 的下面追加以下内容

```text
[mysqld]
innodb_ft_min_token_size = 1
ft_min_word_len = 1
```

然后重启 MySQL 服务器，并修复全文索引。注意，修改完参数以后，一定要修复下索引，不然参数不会生效。

两种修复方式，可以使用下面的命令修复

```sql
repair table test quick;
```

或者直接删掉重新建立索引，再次执行上面的查询，*a、aa、aaa* 就都可以查出来了。

但是，这里还有一个问题，搜索关键字 *a* 时，为什么 *aa、aaa、aaaa* 没有出现结果中，讲这个问题之前，先说说两种全文索引。

## 两种全文索引

## 自然语言的全文索引

默认情况下，或者使用 in natural language mode 修饰符时，match() 函数对文本集合执行自然语言搜索，上面的例子都是自然语言的全文索引。

自然语言搜索引擎将计算每一个文档对象和查询的相关度。这里，相关度是基于匹配的关键词的个数，以及关键词在文档中出现的次数。在整个索引中出现次数越少的词语，匹配时的相关度就越高。相反，非常常见的单词将不会被搜索，如果一个词语的在超过 50% 的记录中都出现了，那么自然语言的搜索将不会搜索这类词语。上面提到的，测试表中必须有 4 条以上的记录，就是这个原因。

这个机制也比较好理解，比如说，一个数据表存储的是一篇篇的文章，文章中的常见词、语气词等等，出现的肯定比较多，搜索这些词语就没什么意义了，需要搜索的是那些文章中有特殊意义的词，这样才能把文章区分开。

## 布尔全文索引

在布尔搜索中，我们可以在查询中自定义某个被搜索的词语的相关性，当编写一个布尔搜索查询时，可以通过一些前缀修饰符来定制搜索。

MySQL 内置的修饰符，上面查询最小搜索长度时，搜索结果 ft_boolean*_*syntax 变量的值就是内置的修饰符，下面简单解释几个，更多修饰符的作用可以查手册

- **+** 必须包含该词
- **-** 必须不包含该词
- **>** 提高该词的相关性，查询的结果靠前
- **<** 降低该词的相关性，查询的结果靠后
- **(\*)星号** 通配符，只能接在词后面

对于上面提到的问题，可以使用布尔全文索引查询来解决，使用下面的命令，*a、aa、aaa、aaaa* 就都被查询出来了。

```sql
select * test where match(content) against('a*' in boolean mode);
```

## 总结

好了，差不多写完了，又到了总结的时候。

MySQL 的全文索引最开始仅支持英语，因为英语的词与词之间有空格，使用空格作为分词的分隔符是很方便的。亚洲文字，比如汉语、日语、汉语等，是没有空格的，这就造成了一定的限制。不过 MySQL 5.7.6 开始，引入了一个 ngram 全文分析器来解决这个问题，并且对 MyISAM 和 InnoDB 引擎都有效。

事实上，MyISAM 存储引擎对全文索引的支持有很多的限制，例如表级别锁对性能的影响、数据文件的崩溃、崩溃后的恢复等，这使得 MyISAM 的全文索引对于很多的应用场景并不适合。所以，多数情况下的建议是使用别的解决方案，例如 Sphinx、Lucene 等等第三方的插件，亦或是使用 InnoDB 存储引擎的全文索引。

## 几个注意点

1. 使用全文索引前，搞清楚版本支持情况；
2. 全文索引比 like + % 快 N 倍，但是可能存在精度问题；
3. 如果需要全文索引的是大量数据，建议先添加数据，再创建索引；
4. 对于中文，可以使用 MySQL 5.7.6 之后的版本，或者第三方插件。

# 使用全文索引

## 一：概念

全文索引与普通的索引不是一回事，在查找上方面其效率是普通模糊（like）查询和N倍，是MySQL专门提供用作搜索引擎的

## 二：版本支持

Mysql 5.6之前版本，只有MyISAM支持全文索引，5.6之后，Innodb和MyISAM均支持全文索引

另外，只有字段的数据类型为 char、varchar、text 及其系列才可以建全文索引

## 三：ngram解析器

5.6之后MySQL自带ngram解析器，可以解析中日韩三国文字，如果不使用ngram解析器，则MySQL默认使用空格与符号作为分隔符（对于英文自然够用了，但对于中日韩文字就不好用了，所以才需要ngram解析器）

## 四：开始使用

**1：创建索引**

用可视化工具创建就好了

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143964.jpg)

**2：查询语句**

全文索引有专用的查询语法：match(字段) against(关键字)

```text
如：select * from answer where match(content) against("测试表")
```

**3：为了更好的搜索效果，通常会配置最小搜索长度**

全文索引的相关参数都无法进行动态修改**，必须通过修改MySQL的配置文件来完成**。通常修改最小搜索长度的值为2，首先打开MySQL的配置文件 （MySQL8.0的配置文件为：my.ini），在 [mysqld] 的下面追加以下内容

```text
// MyISAM
ft_min_word_len = 4; 默认值
ft_max_word_len = 84; 默认值

// InnoDB
innodb_ft_min_token_size = 3; 默认值
innodb_ft_max_token_size = 84; 默认值

//ngram解析器令牌长度----即against()中字符串切分的最小字符长度
ngram_token_size = 2~10 ; 默认值

一般设定：（以下例子均是假定设置如下）
在 [mysqld]的下面追加：
innodb_ft_min_token_size = 2
ft_min_word_len = 2
ngram_token_size = 2
```

**查看该变量的语法：**

```text
show variables like "%ft%"
show variables like "%ngram%"
```

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143965.jpg)

![img](https://raw.githubusercontent.com/1993884953/PicGo-Photo/master/PigCo/202303181143966.jpg)

在配置完参数之后，然后重启 MySQL 服务器，（不会重启，这里我用了最土的方法，直接重启电脑）并删除原先的索引，重新创建

**注意，修改完参数以后，一定要重启电脑（或重启MySQL）并重新创建（或修复）索引，不然参数不会生效**

## 五：三种全文搜索模式

**1：自然语言模式（IN NATURAL LANGUAGE MODE，默认情况下为该模式）**

```text
例：
SELECT * FROM user WHERE MATCH(userName) AGAINST (‘张三’ );
如果最小搜索长度为1的话，则查找包含张，或三，或张三的记录；与布尔搜索模式中的‘+张三’结果相同
```

**2：布尔搜索模式（IN BOOLEAN MODE）**

- 【+】----------必须包含此字符串
- 【-】----------必须不包含此字符串
- 【“ ”】--------双引号内作为整体不能拆词
- 【> 】--------提高该词的相关性，查询的结果靠前
- 【< 】--------降低该词的相关性，查询的结果靠后
- 【*】---------通配符，只能接在词后面
- 等

```text
例：
SELECT * FROM user WHERE MATCH(userName) AGAINST (’+“美女” & +“动人”’ IN BOOLEAN MODE);
查询有‘美女’的又有‘动人’的记录
```

**3：查询扩展搜索**

较少使用，没有细了解