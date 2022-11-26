#  初识Mysql

## 数据库分类

关系数据库 Sql

- MySql、Oracle、Sql Server
- 通过表和表之间，行和列之间关系进行存储。学员信息表，考勤表

非关系型数据库 NoSql not only sql

- Redis、MongDB
- 对象存储，通过对象的自身属性来决定

DBMS(数据库管理系统)

- 数据库的管理软件，科学有效的管理我们的数据。维护和获取数据
- MySQL，本质上是一个数据库管理系统

## 安装mysql

\1. 下载安装文件 [https://dev.mysql.com/downloads/file/?id=494993](https://dev.mysql.com/downloads/file/?id=494993 )
![img](https://i.loli.net/2021/09/25/GKobN1eYVQpx9ak.png)
\2. 解压下载的安装文件 mysql-8.0.20-winx64.zip 到需要存放的位置，如 E:\mysql-8.0.20-winx64；

\3. 在解压后的目录下新建文件夹 data 用于存放数据库的数据文件，并新建 my.ini 配置文件，如下所示

\4. my.ini 配置文件中写入如下内容：

```
#代码开始
[Client]
#设置3306端口
port = 3306
[mysqld]
#设置3306端口
port = 3306
#设置mysql的安装目录
basedir=E:\mysql-8.0.20-winx64
#设置mysql数据库的数据的存放目录
datadir=E:\mysql-8.0.20-winx64\data
#允许最大连接数
max_connections=200
#服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
#创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
[mysql]
#设置mysql客户端默认字符集
default-character-set=utf8
#代码结束
```

  \5. 配置环境变量

   \1. 新建系统变量 MYSQL_HOME ，并配置其值为 “E:\mysql-8.0.20-winx64”
　　![img](https://i.loli.net/2021/09/25/dicQvoLp137bXl2.png)
     \2. 编辑系统变量 Path，将 ;%MYSQL_HOME%\bin 添加到Path变量值的后面（Windows 7）,直接新增该变量值

　　![img](https://i.loli.net/2021/09/25/THdINerqEXCQPv5.png)
\6. 安装 mysql 服务

```
mysqld install
```

\7. 初始化：

```
mysqld --initialize
```

\8. 开启服务

```
net start mysql
```

\9. 查找初始密码

  mysq在5.7版本以上为root用户默认生成了一个临时登录密码，该密码是生成在数据目录下的.err文件里的；在my.ini配置文件里我写的数据目录是：

```
datadir=D:/db/mysqldata
```

所以找到文件：
![img](https://i.loli.net/2021/09/25/94fZRhmajHiozWp.png)

代开该文件，找到如下红色圈出内容，即为 root 用户的密码。
![img](https://i.loli.net/2021/09/25/lIMDrNXaRdK5Bxu.png)

```
SELECT * FROM stu
```

再输入密码

```
Enter password: ******
```

进入mysql后更改密码

```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';
```

SQLyog 报错2058

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
```

## 连接数据库

```mysql
mysql uroot -p123456        --连接数据库
show databases;                    --查看全部数据库

use school;                            --使用数据库
show tables;                        --查看数据库全部的表
describe student;                --查看数据库中全部的表的信息

create database westos;    --创建一个数据库

exit;                                        --退出连接
```

# 操作数据库

mysql关键字不区分大小写

## 数据库的类型

数值

- tinyint 十分小的数据 1个字节
- smallint. 较小的数据 2个字节
- int 标准 4个字节
- float 浮点数 4个字节
- double 浮点数 8个字节
- decimal 字符串形式的浮点数 金融计算的时候，一般用

字符串

- char 字符串固定大小。0-255
- varchar 可变字符串。 0-65535
- text 文本串 2^16-1

时间日期

- date YYYY-MM-DD
- time. HH:mm:ss
- datetime. YYYY-MM-DD HH:mm:ss **最常用的时间格式**
- timestamp. 时间戳。 1970.1.1到现在的毫秒数

null

- 没有值，未知
- 不要使用NULL进行运算，结果一定为NULL

```sql
每一个表，都必须存在以下五个字段!未来做项目用的，表示-一个记录存在意义!
id			主键
`version` 	乐观锁
is_delete 	伪删除
gmt_create 	创建时间
gmt_update	修改时间
```

## 数据库的字段属性（重点）

Unsigned

- 无符号整数
- 声明该列不能为负数

zerofill

- 0填充

- 不足的位数，使用0来填充

- > int(3)    5      005

auto_increment

- 通常理解为自增，自动在上一条记录的基础上+1
- 通常用来设计唯一的主键index,必须是整数类型
- 可以自定义设计主键自增的起始值

非空 NULL not NULL

- 设置为not NULL,如果不赋值，就会报错

默认：

- 设置默认的值

## 创建数据库表

```sql
--目标:创建一个schoo1数据库

--创建学生表(列,字段)使用SQL 创建

--学号int 登录密码varchar(20)姓名,性别varchar(2),出生日期(datatime)，家庭住址，emai1--注意点，使用英文()，表的名称和字段尽量使用括起来

-- AUTO_ INCREMENT 自增

--字符串使用单引号括起来!

--所有的语句后面加，(英文的)，最后一个不用加

-- PRIMARY KEY 主键，一般- 一个表只有一个唯一 -的主键!

CREATE DATABASE school

CREATE TABLE IF NOT EXISTS `student` (

`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
`sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
`address` VARCHAR(100) DEFAULT NULL COMMENT '家庭住址',
`email` VARCHAR(50) DEFAULT NULL COMMENT '邮箱',
PRIMARY KEY (`id`)

)ENGINE=INNODB DEFAULT CHARSET=utf8
```

格式

```sql
CREATE TABLE IF NOT EXISTS `表名`(
	'字段名'列类型[属性] [索引] [注释]，
    '字段名'列类型[属性] [索引] [注释]，
    '字段名'列类型[属性] [索引] [注释]
)[表类型] [字符集设置] [注释]
```

==**常用的命令**==

```sql
SHOW CREATE DATABASE school -- 查看创建数据库的语句
SHOW CREATE TABLE student -- 查看student数据表的定义语句
DESC student -- 显示表的结构
```

## 数据库表的类型

关于数据库引擎

innodb和myisam

|            | MYISAM         | INNODB              |
| ---------- | -------------- | ------------------- |
| 事务支持   | 不支持         | 支持                |
| 数据行锁定 | 不支持（表锁） | 支持（行锁）        |
| 外键约束   | 不支持         | 支持                |
| 全文索引   | 支持           | 支持                |
| 表空间大小 | 较小           | 较大，约为2倍myisam |

常规使用操作

- MYISAM 节约空间，速度较快，
- INNODB 安全性高，事务处理，多表多用户操作

> 物理空间的位置

所有的数据库文件都存在data目录下，一个文件夹就对应一个数据库

MySQL 引擎在物理文件上的区别

- innoDB 在数据库表中，只有一个*.frm文件，以及上级目录下的ibdata1文件
- MYISAM 对应的文件
  - *.frm - 表结构的定义文件
  - *. MYD -数据文件
  - *.MYI 索引文件

> 设置字符集编码

不设置的话，会是mysql默认的字符集编码-（不支持中文）

可以在my.ini中配置默认的编码

```
character-set-server=utf8
```

## 修改删除表

修改

```sql
-- 修改表名 ALTER TABLE 旧表面 AS 新表名
ALTER TABLE student RENAME  AS student1

-- 增加表的字段 ALTER TABLE 表名 ADD 字段名 列属性
ALTER TABLE student1 ADD age INT(11)

-- 修改表的字段（重命名，修改约束）
ALTER TABLE student1 MODIFY age VARCHAR(11)  -- 修改约束
ALTER TABLE student1 CHANGE age age1 INT(1)  -- 更改列名 和 列类型 (每次都要把新列名和旧列名写上, 即使两个列名没有更改,只是改了类型)

-- 删除表的字段
ALTER TABLE student1 DROP age1
```

删除

```sql
-- 删除表
DROP TABLE IF EXISTS student1
```

==所有的创建和删除操作尽量加上判断，以免报错~==

注意点：

- 字段名，使用这个包裹!
- 注释 -- /**/
- sql关键字大小写不敏感，建议大家写小写

# MYSQL基本语句

```sql
use school;
```

使用school数据库

```sql
SELECT *   //明确想要获得的列
FROM school.stu  //明确想要查询的表
where stuNum = 1; //删选结果
order by MARK 	//排序
```

不能改变语句顺序，否着会使SQL语包的语义语法或者结构不正确。

1、选择子句

```sql
SELECT 
name,
stuNum,
mark+10 AS 'new mark' //新列命名
//查询名字和学号的一列和进行运算的新一列
SELECT DISTINCT mark //防止列中重复
```

2、WHERE子句

```sql
SELECT *
FROM school.stu
-- WHERE mark > 90 
-- where name = '小红'
 where name != '小红' //选择语句的应用
```

3、AND,OR,ONT运算符

> 优先级: ONT > AND > OR

```sql
SELECT *
FROM school.stu
where not(stuNum>1 AND mark<95 )
where mark=90 OR 95	//错误用法
```

or 只能搭配一个判断，判断返回true or false，不能直接和字符串配合使用

4、IN运算符

> in同一个系列比较一个属性
>
> 允许您在 WHERE 子句中指定多个值

```sql
SELECT *
FROM school.stu
where stuNum IN ('2','4')
```

5、between运算符

```sql
SELECT *
FROM school.stu
where stuNum between 2 and 4 //从2到4（包含2）
```

6、LIKE运算符

> 模糊搜索

```sql
SELECT *
FROM school.stu
where mark like '%9%'	//%不限字符
where mark like '_9'	//_表示一个字符
```

7、REGEXP运算符

> 正则表达式

```sql
SELECT *
FROM school.stu
where mark regexp '9'
```

- ^搜索前缀
- $搜索后缀
- |多个搜索模式
- [abc]匹配任意在括号里的单字符
- [a-c]用-表示一个范围

8、IS NULL运算符

> 搜索列中null的一项

```sql
SELECT *
FROM school.stu
where point is null
```

9、order by运算符

> 排序 

```sql
SELECT *
FROM school.stu
order by mark DESC, `point` 	//desc倒序
```

10、limit运算符

```sql
SELECT *
FROM school.stu
limit 3 	//显示前3数据
limit 2,2	//跳过前2条数据后显示2条数据
```

## 连接

1、内连接

```sql
USE school ;
SELECT id,`name`,date 
FROM customers c //名字后面可以用简称
JOIN stu s
	on c.id = s.stuNum;
```

2、跨数据库连接

```sql
use school;
SELECT *
FROM school.stu s
JOIN dd.customers c //跨数据库连接要加数据库前缀
	on s.stuNum = c.id
```

3、自连接

```sql
use school;
SELECT *
FROM school.stu s
JOIN customers c
	ON s.stuNum =c.manager  
```

4、多表连接

```sql
use school;

SELECT *
FROM customers c
JOIN school.stu s
	ON s.stuNum =c.manager  
JOIN ready r
	ON c.id = r.id
```

5、隐式连接

```sql
use school;

SELECT *
FROM customers c,stu s
where c.id = s.stuNum
```

6、外连接

```sql
use school;
SELECT *
FROM school.stu s
LEFT JOIN dd.customers c //显示内容以左表为主
	on s.stuNum = c.id
```

7、多表外连接

```sql
use school;
SELECT *
FROM school.stu s
LEFT JOIN dd.customers c
	on s.stuNum = c.id
left join ready r
	on s.stuNum = r.id
```

8、USING子句

```sql
use school;
SELECT *
FROM customers c
join ready r
	using (id) //当两张表的列名一样时，可以用using简化join on连接
```

9、自然连接（不推荐）

```sql
use school;
SELECT *
FROM stu
natural join customers //由服务器自己连接，随机性大
```

10、交叉连接

> 除了在FROM子句中使用逗号间隔连接的表外，SQL还支持另一种被称为交叉连接的操作，它们都返回被连接的两个表所有数据行的笛卡尔积，返回到的数据行数等于第一个表中符合查询条件的数据行数乘以第二个表中符合查询条件的数据行数。惟一的不同在于，交叉连接分开列名时，使用CROSS JOIN关键字而不是逗号。

```sql
use school;
SELECT *
FROM stu
cross join customers
```

11、联合

```sql
use school;
SELECT *,
	'good'
FROM stu
where mark >'80' 

union  //联合两个表的内容

SELECT *,
	'bad'
FROM stu
where mark <'80' ;
```

# mysql数据管理

## 外键

![image-20210421225229225](https://i.loli.net/2021/09/25/AK41FsL6yN2dnUG.png)

以上的操作都是物理外键，数据库级别的外键，不建议使用! (避免数据库过多造成困扰)
==最佳实践==

- 数据库就是单纯的表，只用来存数据，只有行(数据)和列(字段)
- 我们想使用多张表的数据，想使用外键(程序去实现)

## DML语言

数据库意义：数据存储，数据管理

DML语言：数据操作语言

- Insert

  ```sql
  -- 插入语句（添加）
  -- nsert into 表名（[字段一], [字段二]）values('值1'),('值2')
  INSERT INTO `grade` (`gradename`) VALUES('大四')
   
   
  -- 由于主键自增我们可以省略（如何不写表的字段，他会一一匹配）
  INSERT INTO `grade` VALUES('大三')
  INSERT INTO `grade` (`gradeid`,`gradename`) VALUES ('大三','null')
  
  
  -- 一般写插入语句，我们一定要数据和字段一一对应。
  -- 插入多个字段
  INSERT INTO `grade`(`gradename`) VALUES ('大二'),('大一');
  
  INSERT INTO `student`(`name`) VALUES ('张三')
  
  INSERT INTO `student`(`name`,`pwd`,`sex`) VALUES ('张三','aaaaa','男')
  
  INSERT INTO `student`(`name`,`pwd`,`sex`) 
  VALUES ('李四','aaaaa','男'),('王五','23232','女')
  ```

  **注意事项:**

  1. 字段和字段之间使用英文逗号隔开
  2. 字段是可以省略的，但是后面的值必须要要一一对应， 不能少
  3. 可以同时插入多条数据，VALUES后面的值，需要使用，隔开即可==values('值1'),('值2')==

- update

  ```sql
  -- 修改学员名字
  UPDATE `student` SET `name`='洛依尘' WHERE id =1;
  
  -- 不指定条件的情况下，会改动所有表
  UPDATE `student` SET `name`='233'
  
  -- 语法；
  -- UPDATE 表名 set column_name,[] = value where 条件
  ```

  注意：

  - colnum_ name是数据库的列，尽量带上``
  - 条件，筛选的条件,如果没有指定,则会修改所有的列
  - value, 是-个具体的值，也可以是一一个变量
  - 多个设置的属性之间，使用英文逗号隔开

- delete

```sql
-- 清空表单
TRUNCATE `student`

-- 删除数据 (避免这样写)
DELETE FROM `student`

-- 删除指定
DELETE FROM `student` where id= 1
```

> DELETE 与 TRUNCATE区别

相同点 : 都能删除数据，都不会删除表结构
不同 :

- TRUNCATE重新设置自增列计数器会归零
- TRUNCATE 不会影响事务

# DQL查询数据（最重要）

DQL(Data Query Language) : 数据查询语言

- 所有的查询操作都用它 Select
- 简单的查询，复杂的查询它都能做
- ==数据库中最核心的语言==
- 使用频率最高的语言

##  基本查询

```sql
--查询全部的学生 SELECT字段FROM表
SELECT * FROM student
--查询指定字段
SELECT `StudentNo`,`StudentName`,FROM student
--别名，给结果起一一个名字 AS 可以给字段起别名，也可以给表起别名
SELECT `StudentNo` AS 学号, `StudentName` AS 学生姓名 FROM student AS s
--函数
Concat (a，b)
SELECT CONCAT('姓名:' , StudentName) AS新名字FROM student
```

> 有的时候，列名字不是那么的见名知意。我们起别名 AS

### **去重**

> 作用 ： 去除SELECT查询出来的结果中重复的数据，重复的数据只显示一条

```sql
SELECT DISTINCT `StudentNo` FROM result
```

### **数据库的列(表达式)**

```sql
SELECT VERSION() --查询系统版本 (函 数)
SELECT 100*3-1 AS 计算结果 --用来计算 (表达式)
SELECT @@auto_increment_increment --查询自增的步长 (变量)
--学员考试成绩+ 1分查看
SELECT `StudentNo`,`StudentResult`+1 AS '提分后' FROM result 
```

==数据库中的表达式:文本值, 列，Null, 函数,计算表达式，系统变量...==

select  `表达式` from 表

## 联表查询

join对比 :

| 操作       | 描述                                         |
| ---------- | -------------------------------------------- |
| Inner join | 如果表中至少有一个匹配，就返回行             |
| left join  | 即使左表中没有匹配，也会从左表中返回所有的值 |
| right jion | 即使右表中没有匹配，也会从右表中返回所有的值 |

左连接就是对右边表进行条件的过滤，左边的表完全进行保留，不被条件影响

```sql
======================联表查询 join ==============================
-- 查询参加考试的同学 （学号，姓名，考试编号，分数）

SELECT * FROM student  
SELECT	`studentname` AS 姓名 FROM student

/*
	1.分析需求，分析查询的字段来自哪些表
	2.确定使用哪种连接查询？7种
	确定交叉点（这两个表中哪个数据是相同的）
	判断的条件： 学生表中 studentNo = 成绩表中 studentNo 

*/

-- JION（表） ON （判断的条件）连接查询
-- where 等值查询
SELECT studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
INNER JOIN result AS r
WHERE s.studentNo=r.studentNo

--Right Join
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
RIGHT JOIN result AS r
ON s.studentNo = r.studentNo

--LEFT Join
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
LEFT JOIN result AS r
ON s.studentNo = r.studentNo

--我要查询哪些数据select ...
--从那几个表中查FROM 表XXX Join 连接的表 on 交叉条件
--假设存在一种多张表查询，慢慢来，先查询两张表然后再慢慢增加
SELECT s.studentNo, studentName , SubjectName,`StudentResult`
FROM student s
RIGHT JOIN result r
ON r.studentNo = s. studentNo
INNER JOIN `subject` sub
ON r.SubjectNo = sub.SubjectNo
```

**自连接**

```sql
--查询父子信息:把-张表看为两个-模-样的表
SELECT a.`categoryName` AS '父栏目', b.`categoryName` AS '子栏目'
FROM `category` AS a, `category` AS b
WHERE a.`categoryid` = b.`pid`
```

![image-20210423215801952](https://i.loli.net/2021/09/25/vBo8N7wVtxIhA9M.png)

## 连接

1、内连接

```sql
USE school ;
SELECT id,`name`,date 
FROM customers c //名字后面可以用简称
JOIN stu s
	on c.id = s.stuNum;
```

2、跨数据库连接

```sql
use school;
SELECT *
FROM school.stu s
JOIN dd.customers c //跨数据库连接要加数据库前缀
	on s.stuNum = c.id
```

3。自连接

```sql
use school;
SELECT *
FROM school.stu s
JOIN customers c
	ON s.stuNum =c.manager  
```

4、多表连接

```sql
use school;

SELECT *
FROM customers c
JOIN school.stu s
	ON s.stuNum =c.manager  
JOIN ready r
	ON c.id = r.id
```

5、隐式连接

```sql
use school;

SELECT *
FROM customers c,stu s
where c.id = s.stuNum
```

6、外连接

```sql
use school;
SELECT *
FROM school.stu s
LEFT JOIN dd.customers c //显示内容以左表为主
	on s.stuNum = c.id
```

7、多表外连接

```sql
use school;
SELECT *
FROM school.stu s
LEFT JOIN dd.customers c
	on s.stuNum = c.id
left join ready r
	on s.stuNum = r.id
```

8、USING子句

```sql
use school;
SELECT *
FROM customers c
join ready r
	using (id) //当两张表的列名一样时，可以用using简化join on连接
```

9、自然连接（不推荐）

```sql
use school;
SELECT *
FROM stu
natural join customers //由服务器自己连接，随机性大
```

10、交叉连接

> 除了在FROM子句中使用逗号间隔连接的表外，SQL还支持另一种被称为交叉连接的操作，它们都返回被连接的两个表所有数据行的笛卡尔积，返回到的数据行数等于第一个表中符合查询条件的数据行数乘以第二个表中符合查询条件的数据行数。惟一的不同在于，交叉连接分开列名时，使用CROSS JOIN关键字而不是逗号。

```sql
use school;
SELECT *
FROM stu
cross join customers
```

11、联合

```sql
use school;
SELECT *,
	'good'
FROM stu
where mark >'80' 

union  //联合两个表的内容

SELECT *,
	'bad'
FROM stu
where mark <'80' ;
```

## 分页查询

我们采用limit来实现。limit 当前页，页面的大小

```sql
-- 为什么要分页
-- 缓解数据库压力，给人的体验更好

-- 分页，每页显示五条数据
-- 语法： limit 起始值，页面的大小
-- 网页应用： 当前，总的页数，页面的大小
-- limit 0,5 1-5
-- limit 1,5 2-6
-- limit 6,5

SELECT s.`StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM student s
INNER JOIN `result` r
ON s.`StudentNo`=r.`StudentNo`
INNER JOIN `subject` sub
ON r.`subjectNo`=sub.`subjectNo`
WHERE subjectName='数据结构-1'
ORDER BY StudentResult ASC
LIMIT 0,5

-- 第一页 limit 0,5
-- 第二页 limit 5,5
-- 第三页 limit 10,5
-- 第N页 limit 5*（n-1）,5
--【pageSize:页面大小】
--【(n-1) * pageSize:起始值】
--【n : 当前页】
--【数据总数/页面大小 = 总页数（向上取整）】
```

==语法 ：limit（查询起始下标，pagesize）==

## 子查询

where（这个值是计算出来的）

本质 ：==在where语句里面嵌套另一个子查询语句==

![image-20210423234348411](https://i.loli.net/2021/09/25/bruLAnv2jU5G1c6.png)

## **常用函数**

**一、数学函数**

- `ABS(x)`  返回x的绝对值
- `BIN(x)`  返回x的二进制（OCT返回八进制，HEX返回十六进制）
- `CEILING(x)`  返回大于x的最小整数值
- `EXP(x) ` 返回值e（自然对数的底）的x次方
- `FLOOR(x)`  返回小于x的最大整数值
- `GREATEST(x1,x2,...,xn)`返回集合中最大的值
- `LEAST(x1,x2,...,xn) `   返回集合中最小的值
- `LN(x)  `         返回x的自然对数
- `LOG(x,y)`返回x的以y为底的对数
- `MOD(x,y) `        返回x/y的模（余数）
- `PI()`返回pi的值（圆周率）
- `RAND()`返回０到１内的随机值,可以通过提供一个参数(种子)使RAND()随机数生成器生成一个指定的值。
- `ROUND(x,y)`返回参数x的四舍五入的有y位小数的值
- `SIGN(x) `返回代表数字x的符号的值
- `SQRT(x) `返回一个数的平方根
- `TRUNCATE(x,y) `      返回数字x截短为y位小数的结果

**二、聚合函数(常用于GROUP BY从句的SELECT查询中)**

- `AVG(col)`返回指定列的平均值
- `COUNT(col)`返回指定列中非NULL值的个数
- `MIN(col)`返回指定列的最小值
- `MAX(col)`返回指定列的最大值
- `SUM(col)`返回指定列的所有值之和
- `GROUP_CONCAT(col) `返回由属于一组的列值连接组合而成的结果

**三、字符串函数**

- `ASCII(char)`返回字符的ASCII码值
- `BIT_LENGTH(str)`返回字符串的比特长度
- `CONCAT(s1,s2...,sn)`将s1,s2...,sn连接成字符串
- `CONCAT_WS(sep,s1,s2...,sn)`将s1,s2...,sn连接成字符串，并用sep字符间隔
- `INSERT(str,x,y,instr) `将字符串str从第x位置开始，y个字符长的子串替换为字符串instr，返回结果
- `FIND_IN_SET(str,list)`分析逗号分隔的list列表，如果发现str，返回str在list中的位置
- `LCASE(str)或LOWER(str) `返回将字符串str中所有字符改变为小写后的结果
- `LEFT(str,x)`返回字符串str中最左边的x个字符
- `LENGTH(s)`返回字符串str中的字符数
- `LTRIM(str) `从字符串str中切掉开头的空格
- `POSITION(substr,str)` 返回子串substr在字符串str中第一次出现的位置
- `QUOTE(str) `用反斜杠转义str中的单引号
- `REPEAT(str,srchstr,rplcstr)`返回字符串str重复x次的结果
- `REVERSE(str) `返回颠倒字符串str的结果
- `RIGHT(str,x) `返回字符串str中最右边的x个字符
- `RTRIM(str)` 返回字符串str尾部的空格
- `STRCMP(s1,s2)`比较字符串s1和s2
- `TRIM(str)`去除字符串首部和尾部的所有空格
- `UCASE(str)`或`UPPER(str) `返回将字符串str中所有字符转变为大写后的结果

**四、日期和时间函数**

- `CURDATE()`或`CURRENT_DATE() `返回当前的日期
- `CURTIME()`或`CURRENT_TIME() `返回当前的时间
- `DATE_ADD(date,INTERVAL int keyword)`返回日期date加上间隔时间int的结果(int必须按照关键字进行格式化),如：`SELECTDATE_ADD(CURRENT_DATE,INTERVAL 6 MONTH);`
- `DATE_FORMAT(date,fmt) ` 依照指定的fmt格式格式化日期date值
- `DATE_SUB(date,INTERVAL int keyword)`返回日期date加上间隔时间int的结果(int必须按照关键字进行格式化),如：`SELECTDATE_SUB(CURRENT_DATE,INTERVAL 6 MONTH);`
- `DAYOFWEEK(date)`  返回date所代表的一星期中的第几天(1~7)
- `DAYOFMONTH(date) ` 返回date是一个月的第几天(1~31)
- `DAYOFYEAR(date)`  返回date是一年的第几天(1~366)
- `DAYNAME(date)`  返回date的星期名，如：`SELECT DAYNAME(CURRENT_DATE);`
- `FROM_UNIXTIME(ts,fmt) ` 根据指定的fmt格式，格式化UNIX时间戳ts
- `HOUR(time) ` 返回time的小时值(0~23)
- `MINUTE(time) ` 返回time的分钟值(0~59)
- `MONTH(date) ` 返回date的月份值(1~12)
- `MONTHNAME(date) ` 返回date的月份名，如：`SELECT MONTHNAME(CURRENT_DATE);`
- `NOW() `  返回当前的日期和时间
- `QUARTER(date) ` 返回date在一年中的季度(1~4)，如`SELECT QUARTER(CURRENT_DATE);`
- `WEEK(date) ` 返回日期date为一年中第几周(0~53)
- `YEAR(date) ` 返回日期date的年份(1000~9999)

## **聚合函数**

```sql
--都能够统计表中的数据 (想查询一个表中有多少个记录，就使用这个count () )
SELECT COUNT (`BornDate`) FROM student; 	-- Count(字段)， 会忽略所有的null. 值
SELECT COUNT (*) FROM student; 				-- Count (*)，不会忽略null 值，本质计算行数
SELECT COUNT (1) FROM result; 				-- Count (1)，不会忽略忽略所有的null值本质计算行数

SELECT SUM (`StudentResult`) AS 总和 FROM result
SELECT AVG (`StudentResult`) AS 平均分 FROM result
SELECT MAX (`StudentResult`) AS 最高分 FROM result
SELECT MIN (`StudentResult`) AS 最低分 FROM result
```

## **分组和过滤**

> GROUP BY 语句根据一个或多个列对结果集进行分组。
>
> 在分组的列上我们可以使用 COUNT, SUM, AVG,等函数。
>
> 分组前对数据进行筛选，使用where关键字
>
> 分组后对数据筛选，使用having关键字

```sql
--查询不同课程的平均分，最高分，最低分，平均分大于80
--核心: (根据不同的课程分组)
SELECT subjectName, AVG(StudentResult) AS 平均分, MAX(StudentResu1t) AS 最高分，MIN(StudentResult) AS 最低分
FROM result r
INNER JOIN `subject` sub
ON r.`subjectNo` = sub.`subjectNo`
GROUP BY r. subjectNo --通过什么字段来分组
HAVING 平均分>80
```

 **where和having的区别**

where是在分组（聚合）前对记录进行筛选，而having是在分组结束后的结果里筛选，最后返回整个sql的查询结果。

可以把having理解为两级查询，即含having的查询操作先获得不含having子句时的sql查询结果表，然后在这个结果表上使用having条件筛选出符合的记录，最后返回这些记录，因此，having后是可以跟聚合函数的，并且这个聚集函数不必与select后面的聚集函数相同。

## 数据库级别的MD5加密

```sql
-- 加密 
UPDATE `md5` SET pwd=MD5(pwd)

-- 插入时加密
INSERT INTO `md5` VALUE(5,'xiaoming',MD5('123456'))

-- 如何校验：将用户传递进来的密码，进行md5加密，然后比对加密后的值
SELECT * FROM `md5` WHERE `name` ='xiaoming 'AND pwd=MD5('123456')
```

## select小结

![image-20210424161404464](https://i.loli.net/2021/09/25/QW6aTV2izqPnt1B.png)

# 事务

## 什么是事务

==要么都成功，要么都失败==

![image-20210424162515559](https://i.loli.net/2021/09/25/ThR5KsD4m1atMCE.png)

## 特性（ACID）

**原子性**：事务要么都成功，要么都失败

![image-20210424162941441](https://i.loli.net/2021/09/25/jAqTu6KZhBd7xyG.png)

**一致性**：数据前后，事务的完整性必须保持一致

![image-20210424162839003](https://i.loli.net/2021/09/25/3tnOT6WNbBLlFRA.png)

**持久性**：事务一旦提交就不可被逆转，被持久化在数据库中

![image-20210424163100315](https://i.loli.net/2021/09/25/73Z8RhpDIONixlS.png)

**隔离性**：事务并发执行的过程中，互不干扰

![image-20210424163131988](https://i.loli.net/2021/09/25/fjh145VkNrSYgbR.png)

## 隔离产生的问题

- **脏读**：指一个事务读取了另外一个事务未提交的数据。

![image-20210424163359324](https://i.loli.net/2021/09/25/pRLtnmubZHFJQA4.png)

此时左边读到B的钱是400，右边读到B的钱是300

- **幻读**：是指在一个事务内读取到了别的事务插入的数据，导致前后读取不一致。（一般是行影响，多了一行）

![image-20210424163505633](https://i.loli.net/2021/09/25/UhsDlXJi4xqBpCW.png)

- **不可重复读**：在一个事务内读取表中的某一行数据，多次读取结果不同。（这个不一定是错误，只是某些场合不对）

![image-20210424163443662](https://i.loli.net/2021/09/25/Rfz8EPQwNWpn4yx.png)

## 执行事务

```sql
-- mysql 是默认开启事务自动提交的
SET autocommit = 0 -- 关闭
SET autocommit = 1 -- 开启

-- 手动处理事务
SET autocommit = 0
-- 事务开启
START TRANSACTION -- 标记一个事务的开始，从这个之后的sql都在同一个事务内
 
INSERT xx
INSERT xx
-- 提交 ：持久化（成功）
COMMIT
-- 回滚 ：回到原来的样子（失败）
ROLLBACK
-- 事务结束
SET autocommit = 1

-- 了解
SAVEPOINT 保存点名 -- 设置一个事务的保存点
ROLLBACK TO SAVEPOINT 保存点名 -- 回滚到保存点
RELEASE SAVEPOINT 保存点名 -- 撤销保存点
```

> 案例

```sql
SET autocommit = 0

START TRANSACTION 

UPDATE account SET money = money-500 WHERE `name` = 'A' -- A减少500
UPDATE account SET money = money+500 WHERE `name` = 'B' -- B增加500

COMMIT;
ROLLBACK;

SET autocommit = 1;
```



# 索引

定义：MySQL索引的建立对于MySQL的高效运行是很重要的，索引可以大大提高MySQL的检索速度。

## 索引的分类

- 主键索引 （PRIMARY KEY）
  - 唯一的标识，主键不可重复，只能有一个列作为主键
- 唯一索引 （UNIQUE KEY）
  - 避免重复的列出现，唯一索引可以重复，多个列都可以标识唯一索引
- 常规索引（KEY/INDEX）
  - 默认的，index,key关键字来设置
  - 这是最基本的索引类型，而且它**没有**唯一性之类的限制
- 全文索引（FULLTEXT）
  - 快速定位数据

```sql
-- 索引的使用
-- 1.在创建表的时候给字段增加索引
-- 2.创建完毕后，增加索引

-- 显示所有的索引信息
SHOW INDEX FROM 表

-- 增加一个索引
ALTER TABLE 表 ADD FULLTEXT INDEX 索引名（字段名）

-- id _ 表名 _ 字段名
-- CREATE INDEX 索引名 on 表(字段)
CREATE INDEX id_app_user_name ON app_user(`name`);

-- EXPLAIN 分析sql执行状况
EXPLAIN SELECT * FROM student -- 非全文索引

-- EXPLAIN 分析sq1执行的状况
EXPLAIN SELECT * FROM student; -- 非全文索引
EXPLAIN SELECT * FROM student WHERE MATCH(studentName) AGAINST('刘');
```

索引在小数据的时候，用处不大，但是在大数据的时候，区别十分明显

> 增加100w数据

```sql
CREATE TABLE `app_user` (
`id` BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT,
`name` VARCHAR(50) DEFAULT'' COMMENT'用户昵称',
`email` VARCHAR(50) NOT NULL COMMENT'用户邮箱',
`phone` VARCHAR(20) DEFAULT'' COMMENT'手机号',
`gender` TINYINT(4) UNSIGNED DEFAULT '0'COMMENT '性别（0：男;1:女）',
`password` VARCHAR(100) NOT NULL COMMENT '密码',
`age` TINYINT(4) DEFAULT'0'  COMMENT '年龄',
`create_time` DATETIME DEFAULT CURRENT_TIMESTAMP,
`update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
PRIMARY KEY (`id`)
) ENGINE=INNODB DEFAULT CHARSET=utf8 COMMENT = 'app用户表'

SET GLOBAL log_bin_trust_function_creators=1; -- 开启创建函数功能
/*
  第一个语句 delimiter 将 mysql 解释器命令行的结束符由”;” 改成了”$$”，
  让存储过程内的命令遇到”;” 不执行
*/
DELIMITER $$
CREATE FUNCTION mock_data()
RETURNS INT
BEGIN
	DECLARE num INT DEFAULT 1000000;
	DECLARE i INT DEFAULT 0;
	WHILE i<num DO
		INSERT INTO `app_user`(`name`,`email`,`phone`,`gender`,`password`,`age`)
		VALUES(CONCAT('用户',i),'19224305@qq.com','123456789',FLOOR(RAND()*2),'123456789',18);
		SET i=i+1;
	END WHILE;
	RETURN i;
END;

SELECT mock_data() -- 执行此函数 生成一百万条数据
```

## 索引的原则

- 索引不是越多越好
- 不要对经常变动的数据加索引
- 小数据量的表不需要加索引
- 索引一般加在常用来查询的字段上

## 索引的数据结构

Hash 类型的索引

Btree: 默认innodb 的数据结构

阅读：http://blog.codinglabs.org/articles/theory-of-mysql-index.html

# 权限管理和备份

## 用户管理

![image-20210424230522266](https://i.loli.net/2021/09/25/zYl32wy1EDsceo7.png)

```sql
-- 创建用户   CREATE USER 用户名 IDENTIFIED BY '密码'
CREATE USER luoyichen IDENTIFIED BY '123456'

-- 修改密码（修改当前密码）
ALTER USER "root"@"localhost" IDENTIFIED BY "你的新密码";

-- 重命名  rename user 原名字 to 新名字
RENAME USER sanjin TO luoyichen

-- 用户授权   ALL PRIVILEGES 全部的权限   库，表
-- ALL PRIVILEGES 除了给别人授权，其他都能干
GRANT ALL PRIVILEGES ON *.* TO luoyichen

-- 查询权限
SHOW GRANTS FOR luoyichen  -- 查看指定用户的权限
SHOW GRANTS FOR root@localhost

-- 撤销权限 REVOKE 哪些权限，在哪个库撤销，给谁撤销
REVOKE ALL PRIVILEGES ON *.* FROM luoyichen

-- 删除用户
DROP USER luoyichen
```

## 数据库备份

为什么要备份:

- 保证重要的数据不丢失
- 数据转移

MySQL数据库备份的方式

- 直接拷贝物理文件 

- 在Sqlyog 这种可视化工具中手动导出

  - 在想要导出的表或者库中，右键，选择备份或导出

    ![image-20210424232455651](https://i.loli.net/2021/09/25/aEY6NCvBVxSUyAR.png)

- 使用命令行导出mysqldump 命令行使用

  ```cmd
  # mysq1dump -h主机 -u用户名-p密码数据库 表名1 表名2>物理磁盘位置/文件名
  mysq1dump -h1ocalhost -uroot -p123456 schoo1 student >D:/a.sq1
  
  # 导入
  # 登录的情况下，切换到指定的数据库
  # source备份文件
  source d:/a.sq7
  ```

  假设你要备份数据库，防止数据丢失。
  把数据库个朋友! sq|文件给别人即可! 

# 规范数据库设计

## 思路

当数据库比较复杂的时候，我们就需要设计了
糟糕的数据库设计:
数据冗余，浪费空间
数据库插入和删除都会麻烦、异常[ 屏蔽使用物理外键]

- 程序的性能差

良好的数据库设计:

- 节省内存空间
- 保证数据库的完整性
- 方便我们开发系统



软件开发中，关于数据库的设计

- 分析需求:分析业务和需要处理的数据库的需求
- 概要设计:设计关系图E-R图



设计数据库的步骤: (个人博客)

- 收集信息,分析需求
  。用户表(用户登录注销,用户的个人信息，写博客,创建分类)
  。分类表(文章分类,谁创建的)
  。文章表(文章的信息)
  。评论表
  。友链表(友链信息)
  。自定义表(系统信息,某个关键的字，或者- 些主字段) key : value
  。说说表(发表心情.. id... conten...create_ time)

- 标识实体(把需求落地到每个字段)
- 标识实体之间的关系
  。写博客: user -> blog
  。创建分类: user -> category
  。关注: user ->user
  。友链: links .
  。评论: user-user-blog

## 三大范式

[数据库设计三大范式！](https://www.cnblogs.com/linjiqin/archive/2012/04/01/2428695.html)

**第一范式**（1NF）

 原子性：保证每一列不可再分。

 如果数据库表中的所有字段值都是不可分解的原子值，就说明该数据库表满足了第一范式。

![image-20210425150454293](https://i.loli.net/2021/09/25/jIdsAxLRz9rgaDF.png)

**第二范式**（2NF）

 前提：满足第一范式

 每张表只描述一件事情

 第二范式需要确保数据库表中的每一列都和主键相关，而不能只与主键的某一部分相关（主要针对联合主键而言）。也就是说在一个数据库表中，一个表中只能保存一种数据，不可以把多种数据保存在同一张数据库表中。

![image-20210425150653453](https://i.loli.net/2021/09/25/GnNez2rIF8fQypA.png)

**第三范式**（3NF）

 前提：满足第一范式和第二范式

 第三范式需要确保数据表中的每一列数据都和主键直接相关，而不能间接相关。

![image-20210425150820378](https://i.loli.net/2021/09/25/n4wrJNad8pBiSYG.png)

**规范性和性能的问题**：
关联查询的表不得超过三张表

- 考虑商业化的需求和目标， (成本，用户体验! )数据库的性能更加重要
- 在规范性能的问题的时候，需要适当的考虑一下 规范性!

- 故意给某些表增加一-些冗余的字段。 (从多表查询中变为单表查询)
- 故意增加一些计算列(从大数据量降低为小数据量的查询:索引)

# JDBC（重点）

### 10.1、数据库驱动

驱动:声卡，显卡、数据库

![image-20210305110006726](https://i.loli.net/2021/09/25/1BzUcengrAqPQ6m.png)

我们的程序会通过数据库驱动，和数据库打交道!

### 10.2、JDBC

SUN公司为了简化开发人员的(对数据库的统- -) 操作,提供了一一个(ava操作数据库的)规范,俗称JDBC
这些规范的实现由具体的厂商去做~
对于开发人员来说，我们只需要掌握JDBC接口的操作即可

![image-20210305105335235](https://i.loli.net/2021/09/25/sW8F4qLSEPNfp6Y.png)

```SQL
CREATE DATABASE jdbcstudy CHARACTER SET utf8 COLLATE utf8_general_ci;
USE jdbcstudy;
CREATE TABLE users(
id INT PRIMARY KEY,
NAME VARCHAR (40)，
PASSWORD VARCHAR(40)，
email VARCHAR(60)，
birthday DATE
);
INSERT INTO users (id,NAME,PASSWORD,email,bi rthday)
VALUES(1,'zhansan','123456','zs@sina.com','1980-12-04')，
(2,'lisi','123456','lisi@sina.com','1981-12-04'),
(3,'wangwu','123456','wangwu@sina.com','1979-12-04');
```

### 10、3链接数据库

```java
package com.luo;

import java.sql.*;

public class JDBC {
    public static void main(String[] args)throws ClassNotFoundException, SQLException {
        //1.加载驱动
        Class.forName("com.mysql.cj.jdbc.Driver"); //mysql 8.0版本后的驱动位置
        //2.用户信息url
        String url = "jdbc:mysql://localhost:3306/school?useUnicode=ture&characterEncoding=utf-8&serverTimezone=GMT&useSSL=false"; //school就是你要打开的数据库名字
        /*
        useUnicode=ture     支持中文
        &characterEncoding=utf-8   选择字符 
        &serverTimezone=GMT  设置区时
        &useSSL=false  兼容高版本mysql
         */
        String username = "root";
        String password = "123456";

        //3.连接成功，数据库对象

        Connection conn = DriverManager.getConnection(url, username, password);
        //4.执行SQL的对象
        Statement statement = conn.createStatement();
        //5.执行SQL 的对象去执行SQL，可能存在结果，查看返回结果
        String sql = "SELECT * FROM stu";

        ResultSet resultSet = statement.executeQuery(sql);

        while (resultSet.next()){
            System.out.println("stuNum="+resultSet.getObject("stuNum"));
            System.out.println("name="+resultSet.getObject("name"));
            System.out.println("gender="+resultSet.getObject("gender"));
            System.out.println("age="+resultSet.getObject("age"));
            System.out.println("mark="+resultSet.getObject("mark"));
        }
        //6.释放连接
        resultSet.close();
        statement.close();
        conn.close();
    }
}
```

 ==口诀:贾琏欲执事(加连预执释) 引入依赖,加载驱动 连接数据库 创建预编译语句 设置参数,执行sql 关闭连接,释放资源==

**步骤总结**

1.加载驱动

2.连接数据库 DriverManager

3.获取执行SQL的对象 Statement

4.获得返回的结果集

5.释放连接

## statement对象

 **Jdbc中的statement对象用于向数据库发送SQL语句，想完成对数据库的增删改查，只需要通过这个对象向数据库发送增删改查语句即可。**

 Statement对象的executeUpdate方法，用于向数据库发送增、删、改的sq|语句， executeUpdate执行完后， 将会返回一个整数(即增删改语句导致了数据库几行数据发生了变化)。

 Statement.executeQuery方法用于向数据库发生查询语句，executeQuery方法返回代表查询结果的ResultSet对象。

## preparedstatement对象

> PreparedStatement防止SQL注入的本质，把传递进来的参数当做字符
> 假设其中存在转义字符，比如说 ' 会被直接转义

statement传入sql语句的时候，可以进行sql注入，比如传入的sql语句为

```sql
login("' or '1=1","123456");
```

PreparedStatement 可以防止SQL注入 ，效率更高。

1. 新增

   ```java
   package com.luo;
   
   import com.luo.utils.JdbcUtils;
   
   import java.sql.Connection;
   import java.sql.PreparedStatement;
   import java.sql.SQLException;
   import java.util.Date;
   
   public class Test {
       public static void main(String[] args) {
           Connection connection= null;
           PreparedStatement pstm=null;
           try {
               connection = JdbcUtils.getConnection();
               //区别
               //使用 ？占位符代替参数
               String sql = "insert into users(id,`NAME`,`birthday`) values(?,?,?)";
               //预编译sql，先写sql然后不执行
               pstm = connection.prepareStatement(sql);
               //手动赋值
               pstm.setInt(1,8);				//给第一个问号赋值
               pstm.setString(2,"luoyichen");	//给第二个问号赋值
               //注意点:	sqL.Date 	   数据库	java.sql.Date()
               //		    util. Date 	   Java 	new Date().getTime()  获得时间戳
               pstm.setdate(3,new java.sql.Date(new Date().getTime()));
               //执行
               int i = pstm.executeUpdate();
               if (i>0){
                   System.out.println("插入成功");
               }
           } catch (Exception e) {
               e.printStackTrace();
           }finally {
               try {
                   JdbcUtils.release(connection,pstm,null);
               } catch (SQLException e) {
                   e.printStackTrace();
               }finally {
                   JdbcUtils.release(connection,pstm,null);
               }
           }
       }
   }
   ```

   

2. 删除

3. 查询

   ```java
   package com.luo;
   
   import com.luo.utils.JdbcUtils;
   
   import javax.naming.Name;
   import java.sql.*;
   import java.util.Date;
   
   public class Test {
       public static void main(String[] args) {
           Connection conn = null;
           PreparedStatement st =null;
           ResultSet rs = null;
           try {
               conn = JdbcUtils.getConnection();//获得数据库连接
   
               String sql = "select * from users where id = ?";
   
               st = conn.prepareStatement(sql);
   
               st.setInt(1,1); //传递参数
   
               rs = st.executeQuery(); //执行
   
               if (rs.next()){
                   System.out.println(rs.getString("Name"));
               }
           } catch (Exception e) {
               e.printStackTrace();
           }finally {
                   JdbcUtils.release(conn,st,rs);
           }
       }
   }
   ```

   ​	

## jdbc里的事务

==要么都成功，要么都失败==

> ACID原则

原子性 : 要么全部完成，要么都不完成
一致性 : 总数不变
隔离性 : 多个进程互不干扰
持久性 : 一旦提交不可逆，持久化到数据库了

> 代码实现

1、开启事务 ==conn. setAutoCommit(false)==;
2、一组业务执行完毕，提交事务
3、可以在catch 语句中显示的定义回滚语句，但默认失败就会回滚

```java
    package com.luo;

    import com.luo.utils.JdbcUtils;

    import javax.naming.Name;
    import java.sql.*;
    import java.util.Date;

    public class Test {
        public static void main(String[] args) {
            Connection conn = null;
            PreparedStatement st =null;
            ResultSet rs = null;
            try {
                conn = JdbcUtils.getConnection();//获得数据库连接

                conn.setAutoCommit(false); //关闭数据库自动提交，自动开启事务

                String sql1 = "update account set money = money-100 where name ='A'";
                st = conn.prepareStatement(sql1);
                st.executeUpdate();
                String sql2 = "update account set money = money+100 where name ='B'";
                st = conn.prepareStatement(sql2);
                st.executeUpdate();
                //业务完毕，提交事务
                conn.commit();
                System.out.println("成功！");
            } catch (Exception e) {
                try {
                    conn.rollback();
                } catch (SQLException throwables) {
                    throwables.printStackTrace();
                }
                e.printStackTrace();
            }finally {
                    JdbcUtils.release(conn,st,rs);
            }
        }
    }
```

## 数据库连接池

数据库连接–执行完毕–释放

连接–释放 十分浪费资源

**池化技术： 准备一些预先的资源，过来就连接预先准备好的**

不用频繁的去获取connection链接，像一个池子一样，里面有很多现成的

最小连接数: 10
最大连接数: 15	业务最高承载上限
等待超时: 100ms

> 开源的连接池实现

DBCP、C3P0、Druid: 阿里巴巴

使用了这些数据库连接池之后，我们在项目开发中就不需要编写连接数据库的代码了

