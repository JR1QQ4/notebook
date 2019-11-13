## MySql 入门

**数据库**（database）就是存储数据的仓库。为了方便数据的存储和管理，将数据按照特定的规律在磁盘上，通过数据库管理系统，有效地组织和管理存储在数据库中的数据。
**数据库系统**和数据库不是一个概念，数据库系统（DBS），比数据库大很多，由数据库、数据库管理系统，应用开发工具构成。
**数据库管理系统**（DataBase Management System，简称 DBMS），是用来定义数据，管理和维护数据的软件。它是数据库系统的一种重要组成部分。
常见的数据库系统：甲骨文Oracle数据库，IBM的DB2,微软SQL Server、Access，PostgreSql、MySQL。

### MySql 数据库
MySQL数据库特点：开放源代码的数据库，MySQL的跨平台性（Unix、Linux、Windows等)，开源免费，功能强大使用方便。
**SQL**：(Structured Query Language)，结构化查询语句，数据库管理系统通过 SQL 语言来管理数据库中的数据。
SQL 语言组成部分：
* **DDL**(Data Defination Language)，数据定义语言，主要用于定义数据库、表、数据、索引和触发器等，像 DROP、CREATE、ALTER 等语句。
* **DML**(Data Manipulation Language)，主要包括对数据的增删改。INSERT 插入数据、UPDATA 更新数据、DELETE 删除数据。
* **DQL**(Data Query Language)，数据检索语句，用来从表中获得数据，确定数据怎样在应用程序中给出，像 SELECT 查询数据。
* **DCL**(Data Control Language)，数据控制语言，主要用于控制用户的访问权限，像 GRANT、REVOKE、COMMIT、ROLLBACK 等语句。

### 安装与配置
[官网下载](https://dev.mysql.com/downloads/mysql/) 有两个版本，一个是二进制分发版（.msi 安装文件），一个是 免安装版（.zip 压缩文件）。二进制分发版和安装普通软件一样的，在选择需要安装的文件时，如果只是学习 MySql，可以只选择安装 MySQL Server。默认安装路径是：`C:\Program Files\MySQL\MySQL Server 5.6`。8.x 版本的压缩包版本没有 .ini 文件，和 5.x 版本的不一样，配置方式也不一样，以下内容以 5.x 版本为例。

|   目录  |  备注 |   |  |
| --- | --- | --- | --- |
|  bin目录   |  存储可执行文件   |     |     |
|  data 目录   |   存储数据文件  |     |     |
|   include 目录  |   存储包含的头文件  |     |     |
|  lib 目录   |   存储库文件  |     |     |
|  docs 目录   |   文档  |     |     |
|  share 目录   |  错误信息和字符集文字   |     |     |
|   my.ini文件  |  MySQL的配置文件，默认的是 my-default.ini，需要复制并重命名为 my.ini   |   设置字符集  |  客户端字符集[mysql]：default-character-set=utf8   |
|     |     |     |  服务器端字符集[masqld]：character-set-server=utf8   |

运行 MySql 的步骤：
1. 配置环境变量，在 Path 中添加一条数据，即 MySql 的 bin 目录，`C:\Program Files\MySQL\MySQL Server 5.6\bin`
2. 开启 MySql 服务，安装的时候默认会添加一个名为`MySQL56`的服务，开启服务有两个方式，一是打开系统的服务，手动开启；二是在控制台输入：`net start mysql56`，关闭服务是：`net stop mysql56`
3. 配置编码字符集，避免显示乱码。需要在 my.ini 中添加两行：客户端[mysql] `default-character-set=utf8` ，服务器端[mysqld] `character-set-server=utf8`
4. 连接 MySql，需要在控制台输入：`mysql -u root -p`

### 登录与退出
登录命名：`mysql [参数][参数值]`，比如 `mysql -uroot -p`。

|   常用参数  |  备注   |
| --- | --- |
|  -u   |   用户名  |
|  -p   |   密码  |
|  -h   |  服务器名称，-h localhost ，-h 127.0.0.1  |
|  -P   |  端口号，默认安装端口号 `3306`   |
|  -D,--database=name   |   打开指定数据库  |
|  --prompt=name   |  设置命令提示符，--prompt=>>> ，登录之后也可以设置，`prompt \h~\u~\D~\d`，服务器名称~当前用户名~完整的日期~当前数据库  |
|  --delimiter=name   |   指定分隔符，登录之后也可以修改，DELIMITER //，输入语句后以`//`结束，默认分隔符`;`、`\g`  |
|  -V,--version   |  输出版本信息并且退出   |

退出命名：`exit` | `quit` | `\q` 

扩展语句：
* SELECT VERSION();  select v()\g  查看当前数据库版本号，`\g`等同于`;`
* SELECT USER(); 查看当前用户
* SELECT NOW(); 查看当前时间
* SELECT VERSION()\c 不会执行这个命令
* \T C:\Develop\mysql1.txt  输出日志文件到 mysql1.txt ，结束日志`\t`
* SHOW WARNINGS; 查看语句的警告
* SELECT {DATABASE() | SCHEMA()} ：得到当前打开的数据库名称
* help [要查询的内容]，比如 help CREATE DATABASE

### 数据库操作（DDL）
MySql 语句规范：
* 关键字与函数名称全部大写
* 数据库名称、表名称、字段名称等全部小写
* SQL语句必须以分隔号结尾（或\g）
* SQL语句支持折行操作，只要不把单词、标记或引号字符串分割为两部分，可以在下一行继续写
* 数据库名称、表名称、字段名称等尽量不要使用MySQL的保留字，如果需要使用的时候需要用反引号（\`\`）将名称括起来

1.创建数据库，数据库保存在 data 文件夹中
```sql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name [[DEFAULT] CHARACTER SET [=] charset_name]
```
数据库名称：DATABASE 或 SCHEMA；
`{ }`代表必须要出现的，`[ ]`代表可以选的；
db_name表示数据库名称；
CHARACTER SET [=] charset_name 表示编码方式，如 utf8

2.查看当前服务器下的数据库列表：`SHOW {DATABASES | SCHEMAS}`

3.查看制定数据库的定义：`SHOW CREATE {DATABASE | SCHEMA} db_name`

4.修改制定数据库的编码方式：`ALTER {DATABASE | SCHEMA} db_name [DEFAULT] CHARACTER SET [=] character_name`

5.打开指定数据库：`USE db_name`

6.删除指定数据库：`DROP {DATABASE | SCHEMA} [IF EXISTS] db_name`

### 数据表相关操作
**数据表**：
* 是数据库最重要的组成部分之一，是其他对象的基础
* 是存储数据的数据结构
* 是包含了特定实体类型的数据
* 由行（row）和列（column）构成的二维网络
* 一定先有表结构，再有数据
* 至少有一列，可以没有行或者多列
* 数据表名称要求唯一，而且不要包含特殊字符

#### 创建数据表
```sql
CREATE TABLE [IF NOT EXISTS] tbl_name(
字段名称 字段类型 [完整性约束条件]
...
)ENGINE=引擎名称 CHARSET='编码方式';

CREATE TABLE [IF NOT EXISTS] tbl_name(
字段名称 字段类型 [UNSIGNED | ZEROFILL] [NOT NULL] [DEFAULT 默认值] [[PRIMARY] KEY] [UNIQUE [KEY]]
)ENGINE=INNODB CHARSET=UTF8 AUTO_INCREMENT=数值;

CREATE TABLE IF NOT EXISTS `user`(
id SMALLINT,
username VARCHAR(20),
age TINYINT,
sex ENUM('男','女','保密'),
email VARCHAR(50),
addr VARCHAR(20),
birth YEAR,
salary FLOAT(8,2),
tel INT,
# COMMENT 是给字段添加注释
married TINYINT(1) COMMENT '0代表未结婚，非0代表结婚'
)ENGINE=INNODB CHARSET=UTF8;
```
注释：# 注释内容  或者 -- 注释内容

**完整性约束条件**：
*	PRIMARY KEY 主键
*	AUTO_INCREMENT 自增
*	FOREIGN KEY 外键
*	NOT NULL 非空
*	UNIQUE KEY 唯一
*	DEFAULT 默认值
*	ZEROFILL 零填充
*	UNSIGNED 无符号

**字段类型**：查看数据类型`help [数据类型]`或`\h [数据类型]`

*  整数类型：
	* TINYINT ：长度 1 字节，有符号值 -128 到 127（-2^7 到 2^7 - 1），无符号 0 - 255（2^8 - 1）
	* SMALLINT ：2 字节
	* MEDIUMINT ： 3 字节
	* INT ：4 字节
	* BIGINT ：8 字节
	* BOOL，BOOLEAN ：1 字节，等价于 TINYINT(1) ，0 为 false，其余为 true
	
* 浮点类型：
	* FLOAT[(M, D)] ：4 字节，负数取值范围为 -3.40E+38 到 -1.17E-38、0 和 1.175E-38 到 3.40E+38，M 是数字总位数，D 是小数点后面的位数。如果 M 和 D 被省略，根据硬件允许的限制类保存值。单精度浮点数精度大约 7 位小数位。
	* DOUBLE[(M, D)] ：8 字节
	* DECIMAL[(M, D)] ： M+2 字节，和 DOUBLE 一样，`内部以字符串形式存储数值`
	
* 字符串类型：
	* CHAR(M) ：M 个字节，0<=M<=255，CHAR 在保存的时候，前面会用空格填充到指定的长度，在检索的时候后面的空格会去掉
	* VARCHAR(M) : L+1 个字节，其中 L<=M 且 0<=M<=65535，L 为长度，VARCHAR在保存的时候，不进行填充。当值保存和检索时尾部的空格仍保留
	* TINYTEXT ：L+1 字节，其中 L<2^8
	* TEXT ： L+2 字节，其中 L<2^16，只能保存字符数据，而且不能有默认值
	* MEDIUMTEXT ：L+3 字节
	* LONGTEXT ：L+4 字节
	* ENUM('value1', 'value2', ...) ：1 或 2 个字节，取决于枚举值的个数（最多 65535 个值）
	* SET('value1', 'value2', ...) ：1、2、3、4 或 8 个字节，取决于 set 成员的数目（最多 64 个成员）
	
* 日期时间类型：
	* TIME ：3 字节
	* DATE ：3 字节，1000-01-01 ~ 9999-12-31
	* DATETIME ：8 字节，1000-01-01 00:00:00
	* TIMESTAMP ：4字节，1970-01-01 00:00:01 UTC ~ 2038-01-19 03:14:07，一般用整型保存时间戳
	* YEAR ： 1 字节，1901 - 2155
	* 标准时间转为时间戳： $dateline=strtotime($nowtime);
	* 时间戳转为标准时间：$nowtime=date('H:i:s',$dateline);


**存储引擎**
存储引擎就是指表的类型。数据库的存储类型决定了表在计算机中的存储方式。用户可以根据不同的存储方式，是否进行事务处理等来选择合适的存储引擎。

查看数据库的存储引擎：
* 查看支持的存储引擎：`SHOW ENGINES; 或者 SHOW ENGINES\G`
* 查看显示支持的存储引擎信息：`SHOW VARIABLES LIKE 'have%'`
* 查看默认的存储引擎：`SHOW VARIABLES LIKE 'storage_engine'`

常用存储引擎及特点：
* InnoDB ：事务，回滚，多版本并发控制，支持外键约束，表结构存储在 .frm 文件内
* MyISAM ：保存到三个文件中，.frm .MYD .MYI，
* MEMORY ：存储到内存中，hash 索引

#### 查看数据表
1.查看数据库下的数据表：SHOW TABLES
2.查看指定表的表结构：DESC tbl_name, DESCRIBE tbl_name, SHOW COLUMNS FROM tbl_name
3.查看创建表的定义：SHOW CREATE TABLE tbl_name;

#### 修改数据表
1.修改表名：ALTER TABLE tbl_name RENAME [TO | AS] new_name  或者 RENAME TABLE tbl_name TO new_name

2.添加字段：ALTER TABLE tbl_name ADD 字段名称 字段类型 [完整性约束条件] [FIRST | AFTER 字段名称]

3.删除字段：ALTER TABLE tbl_name DROP 字段名称，或者 ALTER TABLE tbl_name DROP 字段1,DROP 字段2,...;

4.修改字段：ALTER TABLE tbl_name MODIFY 字段名称 [完整性约束条件] [FIRST | AFTER 字段名称] ，`主键有自增长不能直接删除主键，需要先去掉自增长，修改字段可以去掉自增长`

5.修改字段名称：ALTER TABLE tbl_name CHANGE 旧字段名称 新字段名称 字段类型 [完整性约束条件] [FIRST | AFTER 字段名称]

6.添加删除默认值：ALTER TABLE tbl_name ALTER 字段名称 SET DEFAULT 默认值 ， ALTER TABLE tbl_name ALTER 字段名称 DROP DEFAULT

7.添加主键：ALTER TABLE tbl_name ADD [CONSTRAINT [symbol]] PRIMARY KEY [index_type] (字段名称, ...)

8.删除主键：ALTER TABLE tbl_name DROP PRIMARY KEY;

9.添加唯一：ALTER TABLE tbl_name ADD [CONSTRAINT [symbol]] UNIQUE [INDEX | KEY] [索引名称](字段名称, ...) ，索引名称不能带有单引号，可以使用反引号。

10.删除唯一：ALTER TABLE tbl_name DROP {INDEX | KEY} index_name

11.修改表的存储引擎：ALTER TABLE tbl_name ENGINE=存储引擎名称

12.设置自增长的值：ALTER TABLE tbl_name AUTO_INCREMENT=值

13.删除数据表：DROP TABLE [IF EXISTS] tbl_name[, tbl_name...]

### 数据的操作（DML）
1.插入数据：
* 不指定具体的字段名：INSERT [INTO] tbl_name VALUES|VALUE(值,...)
* 列出指定字段：INSERT [INTO] tbl_name(字段名称1, ...) VALUES|VALUE(值1,...)
* 同时插入多条记录：INSERT [INTO] tbl_name[(字段名称 ...)] VALUES(值 ...), (值 ...)...
* 通过 SET 形式插入记录：INSERT [INTO] tnl_name SET 字段名称=值,...
* 将查询结果插入到表中：INSERT [INTO] tbl_name[(字段名称, ...)] SELECT 字段名称 FROM tbl_name [WHERE 条件]

2.更新数据：UPDATE tbl_name SET 字段名称=值,... [WHERE 条件] [ORDER BY 字段名称] [LIMIT 限制条数]
* LIMIT 限制条数只能有一个数，不能由两个数包含偏移量

3.删除数据：
* DELETE FROM tbl_name [WHERE 条件] [ORDER BY 字段名称] [LIMIT 条数]，没有条件会删除所有记录，但是`DELETE删除不会重置AUTO_INCREMENT的值`
	* LIMIT 条数只能有一个数，不能包含偏移量
* `彻底清空数据表`： TRUNCATE [TABLE] tbl_name; 

### 查询数据操作（DQL）

#### 普通查询

1.查询记录：
```sql
SELECT select_expr[,select_expr...] 
[
	FROM table_references
	[WHERE 条件]
	[GROUP BY {col_name | position} [ASC | DESC],...分组]
	[HAVING 条件 对分组结果进行二次筛选]
	[ORDER BY {col_name | position} [ASC | DESC],...排序]
	[LIMIT 限制显示条数]
]
```

2.查询表达式：
* 每个表达式表示想要的一列，必须至少有一列，多个列之间以逗号分隔
* `*` 表示所有列，`tbl_name.*` 表示命名表的所有列，`tb_name.tbl_name.*` 表示哪个数据库中的哪个表里的所有列
* 查询表达式可以使用 `[AS]alias_name` 为表赋予别名

3.WHERE 条件：

|  查询条件   |   符号  |
| --- | --- |
|  比较  |   = 、< 、<= 、> 、>= 、!= 、<> 、!> 、!< 、<=> (可以判断是不是 NULL)  |
|  指定范围   |   BETWEEN AND 、NOT BETWEEN AND  |
|  指定集合    |  IN 、 NOT IN   |
|  匹配字符   |  LIKE 、 NOT LIKE (模糊查询，`%`代表0个一个或者多个任意字符，`_`代表1个任意字符)   |
|  是否为空值  |   IS NULL 、 IS NOT NULL  |
|  多个查询条件   |   AND 、 OR  |

4.GROUP BY 查询结果分组
* SELECT * FROM tbl_name GROUP BY 字段1,字段2... ：先按照 字段1 分组，分完组之后再按照 字段2 分组
* 配合 GROUP_CONCAT() 得到分组详情 --- 默认下获取的分组是不全的，只能看到组里的一条记录
	* SELECT id,sex,GROUP_CONCAT(username) FROM cms_user GROUP BY sex;
* 配合聚合函数： 
	* COUNT() ，COUNT(字段) 不统计 NULL 值，COUNT(*)就能统计技术
	* MAX()
	* AVG()
	* SUM()
* 配合 WITH ROLLUP 记录上面所有记录的总和，会在查询到的数据中增加一行数据
	* SELECT * FROM tbl_name GROUP BY 字段名称 WITH ROLLUP

5.HAVING 子句
通过 HAVING 子句对分组结果进行二次筛选，和 WHERE 差不多，只能用于分组之后进行筛选。SELECT * FROM tbl_name GROUP BY 字段名称 HAVING 条件1 [[AND | OR...] 条件2]
如果没有 GROUP BY 进行分组，结果可能和 WHERE 一样的。

6.ORDER BY 排序
ORDER BY 对查询结果进行排序，默认排序是 ASC 升序排序，DESC 是降序排列。SELECT * FROM tbl_name ORDER BY 字段名称 [ASC|DESC]
SELECT * FROM tbl_name ORDER BY RAND(); 随机数排序

7.LIMIT 限制查询结果显示条数
对查询结果，限制显示条数，SELECT * FROM tbl_name LIMIT 条数
SELECT * FROM tbl_name LIMIT 起始条数偏移量(以0开始), 每页显示条数

#### 连接查询
`连接查询`是将两个或两个以上的表按某个条件连接起来，从中选取需要的数据。连接查询是同时查询两个或两个以上的表时使用的，当不同的表中存在相同意义的字段时，可以通过该字段连接这几个表。
```sql
SELECT cms_user.id,username,proName FROM cms_user,provinces
WHERE cms_user.proId=provinces.id;

 SELECT u.id,u.username,u.email,u.sex,p.proName
 FROM cms_user AS u
 INNER JOIN provinces AS p
 ON u.proId=p.id;
 
SELECT u.id,u.username,u.regTime,a.proName,u.sex,COUNT(*) AS totalUsers,GROUP_CONCAT(username)
FROM cms_user AS u
LEFT JOIN
provinces AS a
ON u.proId=a.id
WHERE sex='女'
GROUP BY a.proName
HAVING COUNT(*)>=1
ORDER BY u.id DESC
LIMIT 0,2;
```

1.内连接查询：
* JOIN|CROSS JOIN 、INNER JOIN
* 通过 ON 连接条件
* 显示两个表中符合连接条件的记录

2.外连接查询
* 左外连接： LEFT [OUTER] JOIN ，显示左表的全部记录及右表符合连接条件的记录
* 右外连接： RIGHT [OUTER] JOIN ，显示右表的全部记录以及左表符合条件的记录

3.外键
外键是表的一个特殊字段。被参照的表是主表，外键所在字段的表为子表。设置外键的原则：就是依赖于数据库中已存在的表的主键。外键的作用是建立该表与其父表的关联关系。父表中对记录做操作时，子表中与之对应的信息也应有相应的改变。

外键的作用保持数据的一致性和完整性；可以实现一对一或一对多的关系。

注意：
* 父表和子表必须使用相同的存储引擎，而且禁止使用临时表；
* 数据表的存储引擎只能为InnoDB;
* 外键列和参照列必须具有相似的数据类型。其中数字的长度或是否有符号位必需相同；而字符的长度则可以不同；
* 外键列和参照列必须创建索引。如果外键列不存在索引的话，MYSQL将自动创建索引。

外键约束的参照操作：
* CASCADE : 从父表删除或更新且自动删除或更新子表中匹配的行；
   * `CONSTRAINT 父表_fk_子表 FOREIGN KEY(连接子表字段名称) REFERENCES 父表名(连接父表字段名称) ON DELETE CASCADE ON UPDATE CASCADE;`
* SET NULL : 从父表删除或更新行，并设置子表中的外键列为NULL，如果使用该选项，必须保证子表列没有指定NOT NULL。
   * `CONSTRAINT 父表_fk_子表 FOREIGN KEY(连接子表字段名称) REFERENCES 父表名(连接父表字段名称) ON DELETE SET NULL ON UPDATE SET NULL;`
* RESTRICT : 拒绝对父表的删除或更新操作。
* NO ACTION : 标准SQL的关键字，在MySQL中与RESTRICT相同。

在连接查询中，如果一个字段在父表和子表中有关联，则不能直接用DELETE FROM tbl_name [ WHERE 条件 ]去删除父表中的字段（因为子表还会存在该字段），所以为了彻底删除，此时需要给子表创建一个外键，当需要删除一个字段时，必需先删除子表中的字段才能删除父表中的字段。
```sql
CREATE TABLE IF NOT EXISTS department(
id TINYINT AUTO_INCREMENT KEY,
dep VARCHAR(20) NOT NULL UNIQUE
)ENGINE=INNODB;

CREATE TABLE IF NOT EXISTS employee(
id SMALLINT AUTO_INCREMENT KEY,
username VARCHAR(20) NOT NULL,
depId TINYINT,
CONSTRAINT em_fk_dep FOREIGN KEY(depId) REFERENCES department(id)
)ENGINE=INNODB;
```
4.联合查询：查询的数目要一致
* UNION ：SELECT username FROM tbl_name1 UNION SELECT username FROM tbl_name2;
* UNION ALL ：SELECT username FROM tbl_name1 UNION ALL SELECT username FROM tbl_name2;
* 区别： UNION 去掉相同记录，UNION ALL 是简单的合并

#### 子查询
子查询是将一个查询语句嵌套在另一个查询语句中。内层查询语句的查询结果，可以为外层查询语句提供条件。由内向外执行

引发子查询的情况：
* 使用 [NOT] IN 的字查询
* 使用比较运算符的子查询：=、>、<、>=、<=、<>、!=、<=>
* 使用 [NOT] EXISTS 的子查询，SELCT * FROM tbl_name WHERE EXISTS(SELECT ...) 条件是真才会有结果
* 使用 ANY | SOME 或者 ALL 的子查询

|  运算符   |   ANY  |  SOME   |   ALL  |
| --- | --- | --- | --- |
|  >、>=   |  最小值   |   最小值  |  最大值   |
|  <、<=   |  最大值   |  最大值   |  最小值   |
|  =   |   任意值  |  任意值   |     |
|  <>、!=   |     |     |  任意值   |

将查询结果写入到数据表：
```sql
-- 向已经存在的表中插入数据
INSERT [INTO] tbl_name [(col_name,...)] SELECT ...

INSERT employee(username) 
SELECT username FROM department

-- 在存储过程中向变量插入数据
SELECT value1 INTO var_anem FROM tbl_name
```

创建数据表同时将查询结果写入到数据表：
```sql
CREATE TABLE [IF NOT EXISTS] tbl_name[(create_definition,...)] select_statement

CREATE TABLE test(
id TINYINT UNSIGNED AUTO_INCREMENT KEY,
num TINYINT UNSIGNED
)SELECT id,score FROM student;
```

#### 正则表达式查询
1.REGEXP '匹配模式'
```sql
SELECT * FROM cms_user WHERE username REGEXP '^A';
SELECT * FROM cms_user WHERE username REGEXP '[^ABC]';
```

2.常用匹配方式

|   模式字符  |   含义  |
| --- | --- |
|  ^   |  匹配字符开始的部分   |
|  $  |  匹配字符串结尾部分   |
|  .   |  代表字符串中的任意一个字符，包括回车和换行，相当于 LIKE 语句中的`_`   |
|  [字符集合]   |  匹配字符集合中的任何一个字符   |
|  [^字符集合]   |  匹配除了字符集合以外的任何一个字符   |
|  s1|s2|s3   |  匹配s1、s2、s3中的任意一个字符串   |
|  *   |  代表0个1个或者多个其前的字符，相当于 LIKE 语句中的 `%`   |
|  +   |  代表1个或者多个其前的字符   |
|  String{N}   |  字符串出现 N 次   |
|  字符串{M, N}   |  字符串至少出现 M 次，最多 N 次   |

### 运算符和函数
#### 运算符
1.算数运算符：SELECT 3/0;

|   符号  |  表达式   |  作用   |
| --- | --- | --- |
|   +  |  X1+X2   |  加法   |
|   -  |  X1-X2   |  减法   |
|   *  |  X1*X2   |  乘法   |
|   /  |  X1/X2   |  除法   |
|   DIV  |  X1 DIV X2   |  除法   |
|  %   |  X1 % X2   |  取余   |
|  MOD   |  MOD(X1,X2)   |  取余   |

2.比较运算符：结果只能为真或假，1为真，0为假

|  符号   |  形式   |  作用   |
| --- | --- | --- |
|  =   |   X1=X2  |   判断是否相等  |
|  <>或!=   |   X1<>X2或 X1!=X2   |   判断是否不相等  |
|  <=>   |   X1<=>X2   |   判断是否相等，可以判断是否等于NULL  |
|  >、>=   |   X1>X2或 X1>=X2   |   判断是否大于等于  |
| <、<=    |   X1<X2或 X1<=X2   |  判断是否小于等于  |
| IS NULL或IS NOT NULL    |   X1 IS NULL 或 X1 IS NOT NULL   |  判断是否等于NULL   |
|  BETWEEN AND或NOT BETWEEN AND   |  X1 BETWEEN m AND n   |    判断是否在范围内 |
|  IN 或 NOT IN   |  X1 IN(值,...)   |   判断是否在某一固定范围内  |
|  LIKE 或 NOT LIKE   |  X1 LIKE 表达式   |  判断是否撇配   |
|  REGEXP    |  REGEXP 正则表达式  | 判断是否正则匹配    |

3.逻辑运算符

|  符号   |   形式  |  作用   |
| --- | --- | --- |
|  &&或者AND   | 与   |   并且  |
|  ||或者OR   |  或   |  或者   |
|  !或者NOT   |  非   |  取反   |
|  XOR   |  异或   |  不同为真   |

4.运算符的优先级：通过括号（）改变优先级

|  优先级   |  运算符   |   优先级  |   运算符  |
| --- | --- | --- | --- |
|  1   |   !  |   8  |  |   |
|  2   |  ~   |   9  |   =、<=>、<、<=、>、>=、!=、<>、IN、IS NULL、LIKE、REGEXP  |
|  3   |  ^   |   10  |  BETWEEN AND、CASE、WHEN、THEN、ELSE   |
|  4   |   *、/、DIV、%、MOD  |  11   |  NOT   |
|  5   |  +、-   |  12   |  &&、AND   |
|  6   |  >>、<<  |  13   |  ||、OR、XOR   |
|  7   |  &   |  14   |  ;=   |

#### 函数
1.数学函数

|   名称  |  描述   |
| --- | --- |
|  CEIL()   |   进一取整  |
|  MOD   |   取余数（取模）  |
|  ROUND()   |  四舍五入，SELECT ROUND(3.123,2);  3.12   |
| ABS()   |   取绝对值  |
|  FLOOR()   |  舍一取整   |
|  POWER(X,n)   |  幂运算   |
|   TRUNCATE()  |  数字截取，SELECT TRUNCATE(43.125,1); 43.1   |
|  PI()   |  圆周率   |
|  RAND()和RAND(X)   |  返回0~1之间的随机数，RAND(X),X相同时返回的随机数相同   |
|   SIGN(X)   |  返回X的符号，X为负数、0、正数，分别返回-1和0和1   |
|  EXP(X)    |   计算e的几次方  |

2.字符串函数

|  名称   |  描述   |
| --- | --- |
|  CHAR_LENGTH (S)   |  返回字符串的字符数   |
|  LENGTH   |  返回字符串的长度   |
|   CONCAT (S1,S2,...)  |  将字符串合并为一个字符串   |
|   CONCAT_WS (X,S1,S2,...)  |  以指定分隔符连接字符串   |
|  UPPER (S) /UCASE (S)   |   将字符串转换为大写  |
|  LOWER (S) /LCASE (S)   |  将字符串转换为小写   |
|  LEFT(S,N) /RIGHT(S,N)   |  返回字符串的前/后n个字符   |
|  LPAD (S1,LEN,S2) /RPAD (S1,LEN,S2)   |  将字符串S1用S2填充到指定的LEN  |
|  LTRIM(S)/RTRIM(S)/TRIM(S)   |   去掉字符串中的空格  |
|  TRIM(S1 FROM S)   |  去掉字符串S中开始出现和结尾处的字符串S1   |
|  REPEAT(S,N)   |  重复字符串指定次数   |
|   SPACE(N)  |  返回N个空格   |
|  REPLACE(S,S1,S2)   |   将字符串S中搜索S1替换成S2 ，会区分大小写  |
|  STRCMP(S1,S2)   |   比较字符串，>=<分别返回1，0，-1 ，比较不会区分大小写  |
|   SUBSTRING(S,P,LEN)  |  截取字符串，从第P个位置截取LEN个字符，包括截取字符   |
|   REVERSE(S)  |  反转字符串   |
|  ELT(N,S1,S2)   |  返回指定位置的字符串，字符串起始点从1开始   |

3.日期时间函数

|  名称   |  描述   |
| --- | --- |
|  CURDATE(),CURRENT_DATE()   |   返回当前日期  |
|  CURTIME(),CURRENT_TIME()   |  返回当前时间   |
|  NOW()   |  返回当前日期和时间   |
|  MONTH(D)   |  返回日期中月份的值                 *MONTH(NOW())   |
|   MONTHNAME(D)  |  返回日期中月份名称，January         *MONTHNAME(NOW())   |
|  DAYNAME(D)   |  返回日期是几，Monday               *MONTHNAME(NOW())   |
|  DAYOFWEEK(D)   |  返回一周内的第几天，1代表星期日    *DAYOFWEEK(NOW())   |
|   WEEKDAY(D)  |  返回日期是星期几，0代表是星期一    *WEEKDAY(NOW())   |
|   WEEK(D)  |  一年中的第多少个星期                *WEEK(NOW())   |
|  YEAR(D)   |  返回年份值   |
|  HOUR(T)   |   返回小时值  |
|  MINUTE()   |   返回分钟值  |
|  SECOND(T)   |  返回秒数   |
|   DATEDIFF(D1,D2)  |   计算两个日期之间的相隔的天数  |

4.条件判断函数

|  名称   |  描述   |
| --- | --- |
|  IF(EXPR,V1,V2)   |  如果表达式EXPR成立，返回结果v1；否则v2   |
|  IFNULL (V1,V2)  *IFNULL间没有空格   |   如果v1的不为空，就显示v1的值；否则v2  |
|  CASE WHEN exp1      |  CASE表示函数开始，END表示函数结束。   |
|  THEN v1[ WHEN exp2    |  如果exp1成立时，返回v1。如果表达式exp2成立时，返回v2值。  |
|  THEN v2 ] [ ELSE vn ] END    |  依次类推，最后遇到ELSE时，返回vn的值  |

5.系统函数

|  名称   |  描述   |
| --- | --- |
|   VERSION()  |  返回数据库版本号   |
|   CONNECTION_ID()  |   返回服务器的连接数  |
|  DATABASE(),SCHEMA()   |   返回当前数据库名  |
|  USER(),SYSTEM_USER()   |  返回当前用户   |
|  CURRENT_USER(),CURENT_USER   |  返回当前用户   |
|  CHARSET(STR)   |  返回字符串STR的字符集   |
| COLLATION(STR)    |   返回字符串STR的校验字符集  |
| LAST_INSERT_ID()    |  返回最近生成的AUTO_INCREMENT值   |

6.其他

|  名称   |   描述  |
| --- | --- |
|  MD5(str)   |  信息摘要算法   |
|   PASSWORD(str)  |  密码算法   |
|  ENCODE(str,pwd,str)   |  |  ENCODE(str,pwd,str)   |加密结果是一二进制数，必须使用BLOB类型字段保存|
   |
|  DECODE(crypt_str,pwd_str)   |  对通过ENCODE加密之后的内容解密   |
|   FORMAT(x,n)   |   将数字x进行格式化，将x保留到小数点后n 位  |
|  ASCII(s)    |   返回字符串s的第一个字符的ASCII码  |
|   BIN(x)   |   返回x的二进制编码  |
|   HEX(x)   | 返回x的十六进制编码    |
|   OCT(x)   |  返回x的八进制编码   |
|  CONV(x,f1,f2)    |  将x从f1进制数变成f2进制数   |
|  INET_ATON(IP)    |  将IP地址转换成数字   |
|   INET_NTOA(n)   | 将数字转换成IP地址    |
|   GET_LOCT(name,time)   |   定义锁，IS_FREE_LOCK(name)判断是否使用锁，0表示存在锁，1表示不存在锁  |
|   RELEASE_LOCK(name)   |  解锁   |

### 索引
索引由数据库中一列或多列组合而成，其作用是提高对表中数据的查询速度。优点是可以提高检索数据的速度，缺点是创建和维护索引需要耗费时间，索引可以提高查询速度，会减慢写入速度。

索引分类：
* 普通索引 ：相当于书签
* 唯一索引 ：UNIQUE KEY、PRIMARY KEY是一种特殊的唯一索引
* 全文索引 ：用FULLTEXT,只能创建在CHAR、VARCHAR、text等字符字段上
* 单列索引 ：在一个字段上创建索引
* 多列索引 ：在多个字段上创建索引
* 空间索引 ：搜索引擎为MyISAM ，数据类型GEOMETRY

#### 创建索引
1.创建表的时候创建索引
```sql
CREATE TABLE tbl_name(
字段名称 字段类型 [完整性约束条件],
...,
[UNIQUE | FULLTEXT |SPATIAL] INDEX | KEY [索引名称](字段名称[(长度)]
[ASC | DESC])
);
```
2.在已经存在的表上创建索引
```sql
CREATE [UNIQUE | FULLTEXT | SPATIAL] INDEX 索引名称 ON 表名{字段名称[(长度)] [ASC | DESC] }

ALTER TABLE tbl_name ADD [UNIQUE | FULLTEXT | SPATIAL] INDEX 索引名称(字段名称[(长度)] [ASC | DESC]);
```

#### 删除索引
删除索引
```sql
DROP INDEX 索引名称 ON tbl_name;

ALTER TABLE tbl_name DROP INDEX 索引名称
```

### MySql 编码设定 和 变量

#### 编码设定
1.服务器编码设定：为解决客户端连接乱码
`net start mysql56`开启mysql服务，`mysql -u root -h 127.0.0.1 -p root`打开mysql。

导入数据库：`source 数据库所在路径.数据库名加后缀`，如 source C:/Develop/mysql/test.sql，`\`变为`/`。

查看数据库创建方式`SHOW CREATE TABLE tbl_name`，如果编码方式是`CHARSET=latin1`，在插入中文和在CMD上查看是可以看到，但在客户端连接工具中查看是乱码的。

打开命令窗口，`SHOW VARIABLES LIKE 'CHAR%'`，查看客户端编码方式，如果不是utf8方式则进行修改。在my.ini文件中修改客户端编码 default-character-set=utf8 ，服务端编码 character-set-server=utf8 。
如果配置文件中修改了不能生效，则用下面的方法，但`只在当前状态下有效，当重启数据库服务后失效`：
```sql
SET character_set_client = utf8;
SET character_set_connection = utf8;
SET character_set_database = utf8;
SET character_set_results = utf8;
SET character_set_server = utf8;

或 SET names 'utf8';
```

如果已经修改了my.ini，重启了服务还是不能生效，可以查看服务`可执行文件的路径`：
```
"C:\Program Files\MySQL\MySQL Server 5.6\bin\mysqld.exe" --defaults-file="C:\ProgramData\MySQL\MySQL Server 5.6\my.ini" MySQL56

这里显示my.ini文件不是执行Program Files里添加的，而是ProgramData里的。则有两种方式让自己添加的数据生效。

一、修改ProgramData里的my.ini文件
二、修改服务里的可执行文件的路径，这个需要在运行里输入regedit，打开注册表，找到HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL56，修改ImagePath
```

2.数据表的编码设定：已存在的表
* 更改数据表编码格式：ALTER TABLE  tbl_name CHARACTER SET utf8;
* 更改数据表里列的编码格式：ALTER TABLE tbl_name CHANGE 旧字段名 新字段名 字段类型 CHARACTER SET utf8 NOT NULL，更改前后字段类型要相似
* 解决多张表的字符编码问题:
	1. 导出表结构：mysqldump -u root - p --default-character-set=utf8 -d db_name > 存放路径/文件名.sql
	2. 导出数据表的数据：mysqldump -u root -p --quick --no-create-info --extended-insert --default-character-set=utf8 db_name > 存放路径/文件名.sql
	3. 删除原有的数据库
	4. 以新的编码格式创建数据库：
		* 导入结构：mysql -u root -p test < C:/Develop/mysql/test.sql
		* 导入数据，需要在数据中添加 set names 'utf8' ，mysql -u root -p test < C:/Develop/mysql/test_data.sql
```sql
备份命令：mysqldump -h [ip地址] -P [端口号] -u [用户名] -p [数据库] > [sql脚本文件]

还原命令：mysql -h [ip地址] -P [端口号] -u [用户名] -p [数据库] < [sql脚本文件]
```
**注意**：导入导出不要使用 powershell ，直接使用 cmd。

#### 变量
1.会话变量
* 查看会话变量：
	* SHOW SESSION VARIABLES;  SHOW SESSION VARIABLES LIKE 'auto%';
	* 查看指定的变量：SELECT @@SESSION.变量名
* 设置会话变量：SET @@SESSION.变量名=值  或者 SET 变量名=值

2.全局变量
* 查看全局变量：
	* SHOW global VARIABLES; SHOW GLOBAL VARIABLES;
	* SELECT @@global.变量名;
* 设置全局变量：SET global 变量名=值 或者 SET @@global.变量名=值

3.区别：会话变量只针对当前用户有效，全局变量是针对整个mysql数据库。

### 存储过程
常用的操作数据库语言SQL语句在执行的时候需要先编译，然后执行，而存储过程（Stored Procedure）是一组为了完成特定功能的SQL语句集，经编译后存储在数据库中，用户通过指定的存储过程的名字并给定参数（如果该存储过程带有参数）来调用执行它。

一个存储过程是一个可编程的函数，它在数据库中创建并保存。它可以有SQL语句和一些特殊的控制结构组成。当希望在不同的应用程序或平台上执行相同的函数，或者封装特定功能时，存储过程是非常有用的。数据库中的存储过程可以看做是对编程中的面向对象方法的模拟。它允许控制数据的访问方式。

存储过程的优点：增强了SQL语言的功能和灵活性；存储过程允许标准组件是编程；存储过程能实现较快的执行速度。

1.创建存储过程：
1. 选中一个数据库
2. 改变分隔符，不要让分号`;`作为执行结束的标记，`DELIMITER 新的分隔符`，比如`DELIMITER ~`
3. 创建存储过程：
```sql
CREATE PROCEDURE p_name()
BEGIN
语句1;
语句2;
END~

-- 调用存储过程
CALL p_name~
```
2.参数和变量
* 局部变量：DECLARE 变量名 数据类型 DEFAULT 默认值;
* 三种参数
	* IN ：输入参数，表示该参数的值必须在调用存储过程之前指定，在存储过程中修改的值不能被返回
	* OUT ：输出参数，该值可在存储过程内部改变，并可以返回
	* INOUT ：输入输出参数，该值可以在调用时指定，并可修改和返回
```sql
CREATE PROCEDURE p_vartest1(IN p_var INT)
BEGIN
SELECT p_var;
SET p_var=p_var+1;
SELECT p_var;
END~

-- 创建一个名为@P的变量，没有@符号是不能创建成功的
SET @P=3~

-- 调用存储过程，并传递参数
CALL p_vartest1(@P)~

-- 查看调用存储过程后的@P值，是否有变化
SELECT @P;
```
3.流程控制
* 选择语句（IF ELSEIF ELSE CASE分支）：ELSEIF是挨着写的，在SQL语句中除了IF、CASE，还有IFNULL
```sql
IF search_condition THEN statement_list 
[ELSEIF search_condition THEN statement_list] ... 
[ELSE statement_list] 
END IF

CREATE PROCEDURE p_if(in age INT)
BEGIN
IF age>=18 && age<30 THEN 
	SELECT '成年人';
ELSEIF age>=30 && age<60 THEN 
	SELECT '中年人';
ELSE 
	SELECT '老年人';
END IF;
END~

-- case_value便是条件判断的变量，when_value表示变量的取值
CASE case_value
WHEN when_value THEN statement_list
[WHEN when_value THEN statement_list] ...
[ELSE statement_list]
END CASE;

CREATE PROCEDURE p_case(in salaryId INT)
BEGIN
DECLARE addS INT;
CASE salaryId
WHEN 1001 THEN SET addS = 1500;
WHEN 1002 THEN SET addS = 2000;
WHEN 1003 THEN SET addS = 2500;
ELSE SET addS=1000;
END CASE;
UPDATE salaries SET salary=addS WHERE id=salaryId;
END~
```
* 循环语句
	* while 语句: WHILE 条件 DO ... END WHILE;
	* repeat 语句: REPEAT ... UNTIL 条件 END REPEAT;
	* loop 语句: 循环名称:LOOP ... IF 条件 THEN LEAVE 循环名称; END IF; END LOOP;
```sql
CREATE PROCEDURE p_while()
BEGIN
DECLARE i INT DEFAULT 1;
DECLARE result INT DEFAULT 0;
WHILE i<=100 DO
	SET result=result+i;
	SET i=i+1;
END WHILE;
SELECT result;
END~

CREATE PROCEDURE p_repeat()
BEGIN
DECLARE min_var INT DEFAULT 1;
DECLARE max_var INT DEFAULT 1;
SELECT MIN(id) INTO min_var FROM tbl_name;
SELECT MAX(id) INTO max_var FROM tbl_name;
REPEAT
	IF min_var%2 = 0 THEN
		UPDATE tbl_name SET gender='F' WHERE id=min_var;
	END IF;
	SET min_var = min_var + 1;
	UNTIL min_var > max_var
END REPEAT;
END~

CREATE PROCEDURE p_loop()
BEGIN
DECLARE min_var INT DEFAULT 1;
DECLARE max_var INT DEFAULT 1;
SELECT MIN(id) INTO min_var FROM tbl_name;
SELECT MAX(id) INTO max_var FROM tbl_name;
loop_name:LOOP
	IF min_var%2 = 0 THEN
		UPDATE tbl_name SET gender='F' WHERE id=min_var;
	END IF;
	SET min_var = min_var + 1;
	IF min_var > max_var THEN
	LEAVE loop_name;
	END IF;
END LOOP;
END~
```
4.定义条件和处理
条件的定义和处理可以用来定义过程中遇到问题时相应的处理步骤。
DECLARE CONTINUE HANDLER FOR sqlstate '错误代码值' SET 变量=变量值
```sql
CREATE PROCEDURE p_insert()
BEGIN
DECLARE CONTINUE HANDLER FOR SQLSTATE '42S02' SET @X=1;
INSERT INTO test11(username) VALUES('aaa');
INSERT INTO test2(username,password) VALUES('abc','aab');
END~

ERROR 1146 (42S02):Table 'test11' doesn't exists
-- 错误代码 42S02 是表不存在，添加了CONTINUE就会直接跳过错误向下执行
```
5.存储过程管理
* 查看存储过程：SHOW PROCEDURE STATUS WHERE db='数据库名';
* 查看当前数据库下的存储过程的列表：SELECT  specific_name FROM mysql.proc;
* 查看存储过程的内容：
	* SELECT specific_name,body FROM mysql.proc [WHERE specific_name=存储过程名字]
	* SHOW CREATE PROCEDURE 存储过程名字
* 删除存储过程：DROP PROCEDURE 存储过程名字
* 修改存储过程：ALTER {PROCEDURE | FUNCTION} sp_name [characteristic ...]
	* {CONTAINS SQL | NO SQL | READS SQL DATA | MODIFIES SQL DATA} | SQL SECURITY {DEFINER | INVOKER} | COMMENT 'string'
	* NO SQL表示子程序中不包含SQL语句；READS SQL DATA表示子程序中包含读数据的语句；MODIFIES SQL DATA表示子程序中包含写数据的语句。SQL SECURITY {DEFINER | INVOKER} 指明谁有权限来执行。DEFINER表示只有定义者自己才能够执行；INVOKER表示调用者可以执行。COMMENT 'string'是注释信息。

### 函数
默认函数功能时关闭的，`SHOW VARIABLES LIKE '%fun%'`可以查看到函数功能是否关闭，如果显示OFF，可以设置为ON`SET global log_bin_trust_function_creators=1`。

#### 创建函数
```sql
-- 返回是 RETURNS 不是 RETURN，数据类型和返回的数据类型要一致
CREATE FUNCTION 函数名( 变量1, 变量2,... )
RETURNS 数据类型
BEGIN
	...执行的程序代码
	RETURN 数据;
END;

CREATE FUNCTION add_f(a INT,b INT)
RETURNS INT
BEGIN
	RETURN a + b;
END~

SELECT add_f(3,4)~  -->  7
```
#### 删除函数
DROP FUNCTION [IF EXISTS] 函数名
```sql
DROP FUNCTION IF EXISTS add_f~
```

###  视图
视图是由查询结果形成的一张虚拟表。
如果某个查询结果出现的非常频繁，也就是，要经常拿这个查询结果来做子查询，就可以使用视图。

视图的好处：简化查询语句；可以进行权限控制；大数据表分表的时候，比如某张表的数据由100万条，那么可以将这张表分成四个视图。

#### 创建视图
```sql
CREATE [OR REPLACE] [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
	VIEW view_name [(column_list)]
	AS select_statement
	[WITH [CASCADED | LOCAL] CHECK OPTION]
```
该语句能创建新的视图，如果给定了OR REPLACE子句，该语句还能替换已有的视图。select_statement是一种SELECT语句，它给出了视图的定义。该语句可从基表或其他视图进行选择。
```sql
-- 把一张表分成4个视图，分成四部分查询
CREATE OR REPLACE VIEW view_employee1
AS
SELECT * FROM employees WHERE emp_id % 4 = 0;

CREATE OR REPLACE VIEW view_employee2
AS
SELECT * FROM employees WHERE emp_id % 4 = 1;

CREATE OR REPLACE VIEW view_employee3
AS
SELECT * FROM employees WHERE emp_id % 4 = 2;

CREATE OR REPLACE VIEW view_employee4
AS
SELECT * FROM employees WHERE emp_id % 4 = 3;
```

#### 视图管理
视图存放在 information_schema数据库下的views表里。

1.视图的算法
* Merge：合并的执行方式，每当执行的时候，先将我们视图的SQL语句与外部查询视图的SQL语句，混合在一起，最终执行；
* Temptable：临时表模式，每当查询的时候，将视图所使用的SELECT语句生成一个结果的临时表，再在当前的临时表内进行查询。

对于Merge，会将引用视图的语句的文本与视图定义合并起来，使得视图定义的某一部分取代语句的对应部分。
对于Temptable，视图的结果将被置于临时表中，然后使用它执行语句。
对于UNDEFINED，MySql将选择所要使用的算法。如果可能，它倾向于MERGE而不是TEMPTABLE，这是因为MERGE通常更有效，而且如果使用了临时表，视图是不可更新。

2.查看视图的定义：SHOW table status [FROM 数据库名] [LIKE '匹配']

3.删除视图定义：只能删除视图的定义，不能删除数据，必须有DROP权限
* DROP VIEW [IF EXISTS] view_name [RESTRICT | CASCADE]

4.查看权限：mysql>SELECT Drop_priv FROM mysql.user WHERE USER='root';

5.删除视图
* DROP VIEW IF EXISTS worker_view1;

6.删除多个
* DROP VIEW IF EXISTS department_view1,department_view2;

7.视图更新：某些视图是可更新的。也就是说，可以在诸如UPDATE、DELETE 或 INSERT 等语句中使用它们，以更新基表的内容。对于可更新的视图，在视图中的行和基表汇总的行之间必须具有一对一的关系。还有一些特定的其他结构，这类结构会是的视图不可更新。更具体地讲，如果视图包含下面中的任何一种，那么它就是不可更新的：
* 聚合函数（SUM()，MIN()，COUNT()等）
* DISTINCT
* GROUP BY
* HAVING
* UNSIGNED 或UNION ALL
* 位于选择列表中的子查询
* JOIN
* FROM 子句中的不可更新视图
* WHERE 子句中的子查询，引用FROM子句中的表
* 仅引用文字值（在该情况下，没有要更新的基本表）
* ALGORITHM = TEMPTABLE（使用临时表总会使视图成为不可更新的）

8.with check option的理解和应用：通过视图进行的修改，必须也能通过该视图看到修改后的结果。更新视图的数据，那么必须先满足视图的条件，满足之后才能够更新到基表中。

### 触发器
触发器是一种特殊的存储过程，它在插入、删除或修改特定表中的数据时触发执行，它比数据库本身标准的功能有更精细和更复杂的数据控制能力。

触发器的特性：
* 监视地点：一般就是表名
* 监视时间：update、delete、insert
* 触发事件：after、before
* 触发事件：update、delete、insert

`触发器不能直接被调用，是由数据库主动去执行。`

#### 创建触发器
```sql
CREATE TRIGGER 语法：
CREATE TRIGGER trigger_name trigger_time trigger_event
	ON tbl_name FOR EACH ROW trigger_stmt
```
触发程序是与表有关的命名数据库对象，当表上出现特定事件时，将激活该对象。
触发程序与命名为tbl_name的表相关，tbl_name必须引用永久性表，不能将触发程序与TEMPORARY表或视图关联起来。
trigger_time是触发程序的动作时间。它可以是BEFORE或AFTER，以指明触发程序是在激活它的语句之前或之后触发。
trigger_event指明了激活触发程序的语句的类型。trigger_event可以是下述值之一：
* INSERT：将新行插入表时激活触发程序，例如，通过INSERT、LOAD DATA和REPLACE语句
* UPDATE：更改某一行时激活触发程序，例如，通过UPDATE语句
* DELETE：从表中删除某一行时激活触发程序，例如，通过DELETE和REPLACE语句
注意：trigger_cvent与以表操作方式激活触发程序的SQL语句并不很类似，这点很重要。例如，关于INSERT的BEFORE触发程序不仅能被INSERT语句激活，也能被LOAD DATA语句激活。可能会造成混淆的例子之一是INSERT INTO .. ON DUPLICATE UPDATE ...语法：DEFORE INSERT
触发程序对于每一行激活，后跟AFTER INSERT触发程序，或BEFORE UPDATE和AFTER UPDATE触发程序，具体情况取决于行上是否有重复键。
对于具有相同触发程序动作时间和时间的给定表，不能有两个触发程序。例如，对于某一表，不能有两个BEFORE UPDATE触发程序。但可以有1个BEFORE UPDATE触发程序。
trigger_stmt是当触发程序激活时执行的语句。如果打算执行多个语句，可以使用DEGIN ... END符合语句结构。这样，就能使用存储子程序中允许的相同语句。

特别说明：
* 对于INSERT而言，就插入的行用new来标识，行中的每一列的值用new.列名来表示
* 对于DELETE而言，原本有一行，后来被删除，想引用被删除的这一行，用old来表示，old.列名可以引用被删除的行的值
* 对于update而言，其修改的行，修改前的数据，用old来表示，old.列名引用被修改之前中的值；修改后的数据，用new来表示，new.列名引用被修改之后运行中的值。

```sql
CREATE TRIGGER tr_insert AFTER INSERT
ON employee FOR EACH ROW
BEGIN
	INSERT salaries VALUES(new.emp_no,0,'2019-05-10');
END~

CREATE TRIGGER tr_delete AFTER DELETE
ON employee FOR EACH ROW
BEGIN
	DELETE FROM salaries WHERE emp_no=old.emp.no;
END~
```

#### 触发器的管理
1.查看所有触发器：SHOW TRIGGERS;

2.MYSQL中有一个information_schema.TRIGGERS表，存储所有库中的所有触发器，DESC information_schema.TRIGGERS，可以查看到触发器结构。

3.查看触发器名字：SELECT * FROM information_schema.TRIGGERS WHERE TRIGGER_NAME='触发器名字'\G

4.删除触发器：DROP TRIGGER [schema_name.]trigger_name

### MyISAM表锁
锁是计算机协调对个进程或线程并发访问某一资源的机制。在数据库中，数据也是一种供许多用户共享的资源。如何保证数据并发访问的一致性、有效性是所有数据库必须解决的一个问题，锁冲突也是影响数据库并发访问性能的一个重要因素。从这个角度来说，锁对数据库而言显得尤其重要，也更加复杂。

MYSQL锁机制相比其他数据库，最显著的特点是不同的存储引擎支持不同锁机制。比如MyISAM和MEMORY存储引擎采用的是表级锁（table-level locking）；BDB存储引擎采用的是页面锁（page-level locking），但也支持表级锁；INNODB既支持行级锁（row-level locking），也支持表级锁，但默认是行级锁。
* 表级锁：开销小，加锁块，不会出现死锁；锁粒粒度大，发生锁冲突的概率高，并发度最低
* 行级锁：开销大，加锁慢，会出现死锁；并发度最高
* 页面锁：开销介于之间，会出现死锁，并发度一般。
从锁的角度说，表级锁更适合于以查询为主，只有少量按索引条件更新数据的应用，如WEB应用；而行级锁更适合于有大量按索引条件并发更新少量不同数据，同时又并发查询的应用，比如一些在线事务处理（OLTP）系统。

#### 共享读锁
先把数据库导出，在导出的.sql文件中添加`set storage_engine = MyISAM;`，然后再导入，确保成为MyISAM存储引擎。

MySQL的表级锁有两种模式：表共享读锁（Table Read Lock）和表独占写锁（Table Write Lock）。

对于MyISAM表的读操作，不会阻塞其他用户对同一表的读请求，但会阻塞对同一表的写请求；对于写操作，则会阻塞其他用户对同一表的读和写操作；读操作和写操作之间，以及写操作之间是串行的。

一个SESSION使用LOCK TABLE命令给表加了读锁，这个SESSION可以查询锁定表中的记录，但更新或访问其他表会提示错误；同时，另外一个SESSION可以查询表中的记录，但更新就会出现锁等待。 

1.加共享读锁：LOCK TABLE tbl_name READ;

2.解锁：UNLOCK TABLES;

#### 独占写锁

1.加独占写锁：LOCK TABLE tbl_name WRITE;

2.解锁：UNLOCK TABLES;

#### 并发插入
MyISAM表的读和写是串行的，但就总体而言，在一定条件下，MyISAM表也支持查询和插入操作的并发进行。
该引擎有一个系统变量consurrent_insert，专门用以控制其并发插入的行为，其值分别可以为0、1和2.

* 当为0时，不允许并发插入
* 当为1时，如果MyISAM表中没有空洞（即表的中间没有被删除的行），MyISAM运行在一个进程读表的同时，另一个进程从表尾插入记录。这也是MYSQL的默认设置
* 当为2时，无论MyISAM表中有没有空洞，都允许在表尾并发插入记录

锁调度：一个进程请求读锁，另一个进程请求同一表的写锁；写进程先获得锁。MYSQL任务写请求更重要。MyISAM不适合有大量更新操作和查询操作。
解决方法：执行`set low_priority_updates=1`，使该连接发出的更新请求优先降低，其中insert、delete也可以通过此方法指定。

### 事务
1.查看数据库是否支持事务（INNODB支持）：SHOW ENGINES;
2.查看MYSQL当前默认的存储引擎：SHOW VARIABLES LIKE '%storage_engine%'
3.查看某张表的存储引擎：SHOW CREATE TABLE tbl_name
4.修改表的存储结构：
* CREATE TABLE ... type=InnoDB;
* ALTER TABLE tbl_name type=InnoDB;

#### 创建事务
事务是为了保证数据的一致性，开启事务之后需要提交之后数据才会生效。
START TRANSACTION; 开启事务
COMMIT; 提交

SET AUTOCOMMIT=1; 自动提交

#### 事务的回滚
回到事务发生之前的数据状态，通过 ROLLBACK；
补充：
* commit and chain; 表示提交事务之后重新开启了新的事务。
* rollback and release; 表示事务回滚之后断开和客户端的连接。

还原点:
   Set autocommit=0;
   insert into userinfo values(6,’test1’,’128’);
   savepoint s1;
   insert into userinfo values(6,’test2’,’128’);
   savepoint s2;
   执行完三条插入语句，select * from userinfo可以看到三条。如果你想回滚到最初roolback就是最初什么都没有做的状态。如果你想回到savepoint s1的状态（也就是插入一条test1那里）： rollback to savepoint s1; 。
   
事务更改被锁定： lock table 事务名称 writes;
解锁，让其他客户端可读： start transaction;

事务的4个属性：原子性、一致性、隔离性、持久性，这四个属性通常称为ACID特性。
* 原子性（atomicity）:一个事务是一个不可分割的工作单位，事务中包括的诸操作要么都做，要么都不做；
* 一致性（consistencr）:事务必须是使数据库从一个一致性状态变到另一个一致性状态，一致性与原子性密切相关；
* 隔离性（isolation）：一个事务的执行不能被其他事物干扰。即一个事物内部的操作及使用的数据对并发的他事物是隔离的，并发执行的各个事物之间不能互相干扰；
* 持久性（durability）:持久性也称永久性，指一个事物一旦提交，它对数据库中的数据的改变应该是永久性的。接下来的其他操作或鼓掌不应该对其有任何影响。

### 慢查询
MYSQL 记录下查询超过指定时间的语句，我们将超过指定时间的SQL语句查询成为‘慢查询’。
查看慢查询设定时间：`SHOW VARIABLES LIKE '%long%';`

#### 获取慢查询
SHOW status语句，获取当前数据库运行的时间：
* SHOW status LIKE 'uptime%'
* SHOW status LIKE 'com_Select'
* SHOW status LIKE 'connections'
* SHOW status LIKE 'slow_quries'

#### 启动慢查询
启动慢查询需要以安全模式启动mysql服务，安全模式可以通过日志恢复数据库：`mysql.exe --safe-mode --slow-query-log`

数据库存储日志存放位置可以在my.ini中的datadir=‘...’查看到，然后打开到该文件夹，就能看到ZY-slow.log文件。超过设定时间，通常是5s-10s，就能在.log文件中看到。

#### 配置慢查询
在mysql的配置文件中添加参数：
```sql
-- 文件和文件夹是已经创建好的
log-slow-queries=C:/MySQL/log/mysqld-slow-query.log

-- 慢查询的时间设置
long-query-time=5

-- 及时没有超过时间，但如果没有使用到索引，也会记录SQL语句
log-queries-not-using-indexes
```

### 索引
在关系数据库中，索引是一种与表有关的数据库结构，它可以使对于于表的SQL语句执行更快。

#### 索引的分类
1.主键索引：ALTER TABLE tbl_name PRIMARY KEY(字段名)

2.唯一索引：唯一索引所在的列可以为NULL值；唯一索引所在的列不能为空字符串。注：列名即字段名
CREATE UNIQUE INDEX 索引名称 ON tbl_name(列名)

3.普通索引： CREATE INDEX 索引名称 ON tbi_name(字段名)

4.全文(FULL TEXT)索引： 用于全文搜索，只有MyISAM表类型支持FULL TEXT索引；FULL TEXT索引只可以从CHAR、VARCHAR和TEXT列中创建；整个列都会被编入索引，不支持部分列编索引。
```sql
-- 查看数据表articles中title，body字段中包含database单词的
SELECT * FROM articles WHERE MATCH (title,body) AGAINST ('database');

-- 查看全文匹配度
SELECT id,MATCH(title,body) AGAINST ('Tutorial') FROM articles;
```

#### 索引的管理
1.查看索引：SHOW KEYS FROM tbl_name 或者 SHOW INDEXS FROM tbl_name

2.删除索引：ALTER TABLE tbl_name DROP INDEX 索引名称

3.通过Explain分析具体有没有使用索引，执行低效SQL的执行计划：
EXPLAIN SELECT 索引名称(字段名) FROM tbl_name\G;
EXPLAIN SELECT 字段名 FROM tbl_name\G;

#### 通过索引优化SQL
索引原理：主要通过二叉树去寻找索引文件，效率：log2N         检索10次：2的10次方，1024条记录

索引带来的开销：
* .frm 文件： 表示表的结构
* .myd 文件： 表示数据
* .myi 文件：  表示索引的文件

哪些不适合创建索引：更新非常频繁的字段；唯一性比较差的字段，比如人的性别。

创建索引的条件：肯定在WHERE条件中经常使用到的；该字段的变化不会太频繁。

通过 SHOW PROFILE 分析 SQL 具体消耗时间：
1. 首先查看 mysql 是否支持 SHOW PROFILE       
   SELECT @@HAVE_PROFILING;
2. 如果 PROFILING 是关闭的，可以通过 SET 语句在 SESSION 级别开启 PROFILING  
   SET PROFILING=1;
3. 执行完毕之后，可以通过 SHOW PROFILES; 语句，查看当前 SQL 的 QUERY ID
4. 执行 SELECT COUNT(*) FROM 表名;
5. 通过 SHOW PROFILE FOR QUERY ID;。

### 优化
表的分析、检查、优化：
1.定期分析表：ANALYZE [ LOCAL | NO_WRITE_TO_BINLOG ] TABLE tbl_name [,tbl_name]

2.定期检查表：CHECK TABLE tbl_name [,tbl_name ] [option]
备注：CHECK TABLE 也可以检查视图是否有错误，比如在视图定义中被引用的表已不存在

3.定期优化表：OPTIMIZE [ LOCAL | NO_WRITE_TO_BINLOG ] TABLE tbl_name [,tbl_name]
对于MyISAM表，OPTIMIZE TABLE按如下方式操作：
* 如果表已经删除或分解了行，则修复表；
* 如果未对索引页进行分类，则进行分类
* 如果表的统计数据没有更新（并且通过对索引进行分类不能实现修复），则进行更新

注意：无论是ANALYZER,CHECK还是OPTIMIZE在执行期间将对表进行锁定，因此请注意这些操作要在数据库不繁忙的时候执行。

#### 获取表的相关信息
SHOW TABLE STATUS 获取表的信息
SHOW TABLE STATUS LIKE 'tableName'\G

1.Name：表名称
2.Engine：表的存储引擎
3.Version：版本
4.Row_format：行格式
5.Rows：表中的行数
6.Avg_row_length：平均每行包括的字节数
7.Data_length：整个表的数据量（单位：字节）
8.Max_data_length：表可以容纳的最大数据量
9.Index_length：索引占用磁盘的空间大小
10.Data_free：未使用空间
11.Auto_increment：下一个自增长值
12.Create_time：表创建时间
13.Update_time：表最近更新时间
14.Check_time：使用check table或myisamchk工具检查表的最近时间
15.Collation：表的默认字符集和字符排序规则
16.Checksum：启用则对整个表的内容计算时的检验和
17.Create_options：指表创建时的其他所有选项
18.Comment：包含了其他额外信息

#### 表的分区
当数据量过大的时候，需要将一张表的数据划分几张表存储。一些查询可以得到极大的优化，这主要是有助于满足一个给定WHERE语句的数据可以值保存在一个或多个分区内，这样在查找时就不用查找其他剩余的分区。

查看是否支持分区：SHOW VARIABLES LIKE '%partition%'; yes表示支持分区。

分区的分类：
* RANGE分区：基于属于一个特定连续区间的列值，把多行分配给分区
* LIST分区：类似与按RANGE分区，区别在于它是基于列值匹配一个离散值集合中的某个值来进行选择
* HASH分区：基于用户定义的表达式的返回值来进行选择的分区
* KEY分区：：类似与HASH分区，区别在于它只支持计算一列或多列
```sql
CREATE TABLE employees(
	id INT NOT NULL,
	fname VARCHAR(30),
	lname VARCHAR(30),
	hired DATE NOT NU;; DEFAULT '1970-01-01',
	separated DATE NOT NULL DEFAULT '9999-12-31',
	job_code INT NOT NULL,
	store_id INT NOT NULL
)

partition BY RANGE(store_id)(
	partition p0 VALUES LESS THAN(6),
	partition p1 VALUES LESS THAN(11),
	partition p2 VALUES LESS THAN(16),
	partition p3 VALUES LESS THAN MAXVALUE
);

-- 查看分区
SHOW CREATE TABLE employees\G
```
分区的删除：ALTER TABLE 表名 DROP PARTITION 分区名

增加分区：ALTER TABLE 表名 ADD PARTITION(PARTITION 分区名字 VALUES LESS THEN 具体的某个值)

#### 内存优化
myisam内存优化：
1.key_buffer_size设置，决定索引块缓存区的大小，一般的myisam数据库，建议用1/4可用内存分配给key_buffer_size：
key_buffer_size=2G
2.read_buffer_size，经常顺序扫描myisam表，就需要设置，该值是每个session独占的，如果默认值设置太大，就会造成内存浪费。
3.read_rnd_buffer_size，需要做排序的myisam表查询，如带有order by子句的sql，适当增加该值。但需要注意，该值是每个session独占的，设置太大内存浪费。

innodb内存优化：
1.innodb_buffer_pool_size，决定表数据和索引数据的最大缓存区大小
2.innodb_log_buffer_size，决定innodb重做日志缓存的大小，对应有大量更新记录的事务，增加该值大小，可以避免在事务提交前就执行不必要的日志写入磁盘操作。

mysql并发参数：
1.max_connections，提高并发连接
2.thread_cache_size，加快连接数据库的速度，控制mysql缓存客户服务线程的数量
3.innodb_lock_wait_timeout，控制innodb事务等待行锁的时间

#### 应用程序优化
1.访问数据库采用连接池优化，就是连接数据库的客户端放在一个连接池里。

2.采用缓存减少对mysql的访问：
* 避免对同一数据做重复检索，尽可能选择多个字段
* 使用查询缓存，比如一条SQL查询除了字段名和表明不一样，其他都一样，mysql就会把SQL语句1缓存，发给SQL2语句
* 缓存参数的配置
	* query_cache_type：是否打开缓存，大小写要一样，以下是可选项
		* OFF ：关闭
		* ON：总是打开
		* DEMAND：只有明确写了SQL_CACHE的查询才会吸入缓存
	* query_cache_size：缓存使用的总内存大小空间，单位字节，必须是1024的整数倍，否则MYSQL实际分配可能跟这个数值不同
	* query_cache_min_res_unit：分配内存块时的最小单位大小
	* query_cache_limit：MYSQL能够缓存的最大结构，如果超出则增加query_not_cached的值，并删除查询结果
	* query_cache_wlock_invalidate：如果某个数据表被锁住，是否仍然从缓存中返回数据，默认是OFF，便是仍然返回

3.负载均衡（读写分离）：一个主MYSQL服务器（MASTER）服务器与多个从属MYSQL服务器（STAVE）建立复制（replication）连接，主服务器与从属服务器实现一定程度上的数据同步，多个从属服务器存储相同的数据副本，实现数据冗余，提供容错功能。部署开发应用系统时，对数据库操作代码进行优化，将写操作（如UPDATE、INSERT）定向到主服务器，把大量的查询操作（SELECT）定向到从属服务器，实现集群的负载均衡功能。

如果主服务器发生故障，从属服务器将转换角色成为主服务器，是应用系统为终端用户提供不剪短的网络服务；主服务器恢复运行后，将其转换为从属服务器，存储数据库副本，继续对终端用户提供数据查询检索服务。

#### 账号管理
查看用户：
mysql>USE mysql;
mysql>SELECT host,user,password FROM user;

1.GRANT命令使用

对于ZY用户，赋予SELECT的权限，能查看所有数据库和所有数据表
GRANT SELECT ON *.* TO ZY@'localhost' IDENTIFIED BY 'PWD' WITH GRANT OPTION;;

对应YZ用户，赋予test下索引数据表的索引权限
GRANT ALL PRIVILEGES ON test.* TO YZ@'localhost' IDENTIFIED BY 'PWD' WITH GRANT OPTION;;
*  ALL PRIVILEGES ：表示多有权限，你也可以使用SELECT、UPDATE等提到的权限
*  ON ：用来指定权限针对哪些库和表
*  test.* ：test数据库下的所有表
*  TO ：表示将权限赋予给哪个用户
*  YZ@'localhost' ：表示test用户，@后面接限制的主机，可以是IP、IP段、域名以及%，%表示任何地方，但有的版本不包括本地，如果不包括需要再加一个localhost的用户
*  IDENTIFIED BY ：指定用户的登录密码
*  WITH GRANT OPTION ：表示该用户可以将自己拥有的权限

2.查看用户的权限：
SHOW GRANTS FOR ‘root’@'localhost'  

3.删除用户，不仅仅要删除用户的名称，还要删除用户拥有权限。
使用DELETE删除，并不能删除权限，新建同名用户后会继承以前的权限，正确的做法是使用DROP命令：
DROP USER ‘zy’@'localhost' ;

4.修改密码
SET PASSWORD FOR 'ty'@'localhost'=password('123');

5.对账号权限的资源设置
GRANT SELECT ON employees.* TO test@localhost IDENTIFIED BY 'pwd' WITH max_queries_per_hour 5 max_user_connections 6;
* 设置test用户对employees数据库的权限，每小时查询的次数小于5次，最多有6个用户进行并发连接

#### MYSQL监控
随着软件后期的不断升级，mysql的服务器数量越来越多，软硬件故障的发生概率也越来越高。这个时候需要一套监控系统，当主机发生异常时，此时通过监控系统发现和处理。

1.常见监控方式的分类：下面语句没有分号`;`
* 自己写程序或者脚本控制
	* 监控mysql是否提供正常的服务：mysqladmin -uroot -proot -hlocalhost ping，输出：mysql is alive
	* 获取当前的几个状态值：mysqladmin -uroot -proot -hlocalhost status
	* 获取数据库当前的连接信息：mysqladmin -uroot -proot -hlocalhost processlist
	* 获取当前数据库的连接数：mysql -uroot -proot -BNe "select host,count(host) from processlist group by host;" information_schema
	* 检查修复分析优化：mysqlcheck -u root -proot --all-databases
	* 在客户端执行以下命令
		* 检查临时表是否过多：SHOW STATUS LIKE 'Created_tmp%'
		* 锁定状态：SHOW STATUS LIKE "%lock%"
		* Inonodb_log_waits反应Innodb Log Buffer空间不足造成等待的次数：SHOW STATUS LIKE 'Innodb_log_waits'
* 监控采用商业解决方案
* 监控开源软件

#### 定时维护
mysql 设置定时器，从5.1开始才支持event的。查看版本SELECT VERSION();
1.查看是否开启event与开启event
* 查看evevt的状态：SHOW VARIABLES LIKE '%sche%'
* 开启evevt功能：SET GLOBAL event_scheduler=1;

2.创建定时器，创建事件test_event：
```sql
DROP EVENT IF EXISTS test_event;
CREATE EVENT test_event
ON schedule every 1 second
ON completion preserve disable
DO CALL p_test_proce();

-- 当为on completion preserve的时候，当event到期了，event会被disable，但该event还会存在

-- 当为on completion not preserve的时候，当event到期时，该event会被自动删除

-- p_test_proce是一个存储过程的名字
```
* 开启事件test_event：ALTER EVENT test_event ON completion preserve enable;
* 关闭事件test-event：ALTER EVENT test_event ON completion preserve disable;

#### 备份与还原
1.备份：
* 通过mysqldump命令备份：
	* 备份单个数据库：mysqldump -u username -p dbname [table1 table2] > backupName.sql
		* dbname 表示数据库的名称，table1 table2表示备份表名称，backupName.sql参数表设计备份文件的名称
	* 备份多个数据库：mysqldump -u username -p --databases dbname1 dbname2 >backup.sql
	* 备份所有数据库：mysqldump -u username -p -all-databases > bakcupName.sql
* 直接复制整个数据库目录
* 使用mysqlhotcopy工具快速备份

2.还原
* 使用mysql命令还原mysqldump备份的数据库：
	* mysql -u root -p [dbname] < backupName.sql