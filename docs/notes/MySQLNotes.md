# MySQL Notes



# 连接

- 默认端口：3306

- 使用MySQL自带的命令行工具（MySQL 8.0 Command Line Client - Unicode）连接MySQL

- 使用cmd连接MySQL：

  1. 将MySQLbin目录配置到环境变量`C:\Program Files\MySQL\MySQL Server 8.0\bin`

  2. cmd指令：

     ```powershell
     mysql [-h 127.0.0.1] [-P 3306] -u root -p
     
     参数：
     	-h : MySQL服务所在的主机IP
     	-P : MySQL服务端口号， 默认3306
     	-u : MySQL数据库用户名
     	-p ： MySQL数据库用户名对应的密码
     ```



# SQL

## 通用语法

1. SQL语句可以单行或多行书写，以分号结尾

2. SQL语句可以使用空格/缩进来增强语句的可读性

3. MySQL数据库的SQL语句不区分大小写，关键字建议使用大写

4. 注释：

   单行注释：-- 注释内容 或 # 注释内容

   多行注释：/* 注释内容 */

## SQL分类

|分类 |全称| 说明|
|--|--|--|
|DDL |Data Definition Language |数据定义语言，用来定义数据库对象(数据库，表，字段)|
|DML |Data Manipulation Language| 数据操作语言，用来对数据库表中的数据进行增删改|
|DQL |Data Query Language |数据查询语言，用来查询数据库中表的记录|
|DCL |Data Control Language |数据控制语言，用来创建数据库用户、控制数据库的访问权限|

## DDL

### 数据库操作

| 命令                                                         | 作用           |
| ------------------------------------------------------------ | -------------- |
| `show databases;`                                            | 查询所有数据库 |
| `select database();`                                         | 查询当前数据库 |
| `create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则]; ` | 创建数据库     |
| `drop database [if exists] 数据库名;`                        | 删除数据库     |
| `use 数据库名;`                                              | 切换数据库     |

### 表操作

#### 查询创建

- 查询当前数据库所有表：`show tables; `

- 查询指定表结构：`desc 表名；`

- 查询指定表的建表语句：`show create table 表名;`

- 创建表结构：

  ```sql
  CREATE TABLE 表名(
      字段1 字段1类型 [COMMENT 字段1注释],
      字段2 字段2类型 [COMMENT 字段2注释],
      字段3 字段3类型 [COMMENT 字段3注释],
      ...... 字段n
      字段n类型 [COMMENT 字段n注释]
  ) [COMMENT 表注释] ;
  ```


#### 数据类型

> 文档（仅本地打开）：[MySQL数据类型](MySQL数据类型.xlsx)

**数值类型：**

| 类型         | 大小    | 有符号(SIGNED)范围                                    | 无符号(UNSIGNED)范围                                      | 描述               |
| ------------ | ------- | ----------------------------------------------------- | --------------------------------------------------------- | ------------------ |
| TINYINT      | 1 byte  | (-128，127)                                           | (0，255)                                                  | 小整数值           |
| SMALLINT     | 2 bytes | (-32768，32767)                                       | (0，65535)                                                | 大整数值           |
| MEDIUMINT    | 3 bytes | (-8388608，8388607)                                   | (0，16777215)                                             | 大整数值           |
| INT或INTEGER | 4 bytes | (-2147483648，2147483647)                             | (0，4294967295)                                           | 大整数值           |
| BIGINT       | 8 bytes | (-2^63，2^63-1)                                       | (0，2^64-1)                                               | 极大整数值         |
| FLOAT        | 4 bytes | (-3.402823466 E+38，3.402823466351 E+38)              | 0 和 (1.175494351 E-38，3.402823466 E+38)                 | 单精度浮点数值     |
| DOUBLE       | 8 bytes | (-1.7976931348623157 E+308，1.7976931348623157 E+308) | 0 和 (2.2250738585072014 E-308，1.7976931348623157 E+308) | 双精度浮点数值     |
| DECIMAL      |         | 依赖于M(精度)和D(标度)的值                            | 依赖于M(精度)和D(标度)的值                                | 小数值(精确定点数) |

**字符串类型：**

| 类型       | 大小               | 描述                         |
| ---------- | ------------------ | ---------------------------- |
| CHAR       | 0-255 bytes        | 定长字符串                   |
| VARCHAR    | 0-65535 bytes      | 变长字符串                   |
| TINYBLOB   | 0-255 bytes        | 不超过255个字符的二进制数据  |
| TINYTEXT   | 0-255 bytes        | 短文本字符串                 |
| BLOB       | 0-65535 bytes      | 二进制形式的长文本数据       |
| TEXT       | 0-65535 bytes      | 长文本数据                   |
| MEDIUMBLOB | 0-16777215 bytes   | 二进制形式的中等长度文本数据 |
| MEDIUMTEXT | 0-16777215 bytes   | 中等长度文本数据             |
| LONGBLOB   | 0-4294967295 bytes | 二进制形式的极大文本数据     |
| LONGTEXT   | 0-4294967295 bytes | 极大文本数据                 |

**日期时间类型：**

| 类型      | 大小 | 范围                                       | 格式                | 描述                     |
| --------- | ---- | ------------------------------------------ | ------------------- | ------------------------ |
| DATE      | 3    | 1000-01-01 至 9999-12-31                   | YYYY-MM-DD          | 日期值                   |
| TIME      | 3    | -838:59:59 至 838:59:59                    | HH:MM:SS            | 时间值或持续时间         |
| YEAR      | 1    | 1901 至 2155                               | YYYY                | 年份值                   |
| DATETIME  | 8    | 1000-01-01 00:00:00 至 9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 4    | 1970-01-01 00:00:01 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |

**案例：**

设计一张员工信息表，要求如下：

1. 编号（纯数字）

2. 员工工号 (字符串类型，长度不超过10位) 

3. 员工姓名（字符串类型，长度不超过10位）

4. 性别（男/女，存储一个汉字）

5. 年龄（正常人年龄，不可能存储负数）

6. 身份证号（二代身份证号均为18位，身份证中有X这样的字符）

7. 入职时间（取值年月日即可）

```sql
create table emp(
    id int comment '编号',
    workno varchar(10) comment '工号',
    name varchar(10) comment '姓名',
    gender char(1) comment '性别',
    age tinyint unsigned comment '年龄',
    idcard char(18) comment '身份证号',
    entrydate date comment '入职时间'
) comment '员工表';
```

#### 修改

- 添加字段：`ALTER TABLE 表名 ADD 字段名 类型 (长度) [COMMENT 注释] [约束]; `
- 修改数据类型：`ALTER TABLE 表名 MODIFY 字段名 新数据类型 (长度); `
- 修改字段名和字段类型：`ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型 (长度) [COMMENT 注释] [约束]; `
- 删除字段：`ALTER TABLE 表名 DROP 字段名; `
- 修改表名：`ALTER TABLE 表名 RENAME TO 新表名;`

#### 删除

- 删除表：`DROP TABLE [IF EXISTS] 表名;`
- 删除指定表, 并重新创建表（格式化表）：`TRUNCATE TABLE 表名;`

## DML

### 添加数据

- 给指定字段添加数据：`INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...);`

- 给全部字段添加数据：`INSERT INTO 表名 VALUES (值1, 值2, ...);`

- 批量添加数据：

  `INSERT INTO 表名 (字段名1, 字段名2, ...) VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);`

  `INSERT INTO 表名 VALUES (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);`

注意事项:

- 插入数据时，指定的字段顺序需要与值的顺序是一一对应的
- 字符串和日期型数据应该包含在引号中
- 插入的数据大小，应该在字段的规定范围内

### 修改数据

- 修改数据的具体语法为：`UPDATE 表名 SET 字段名1 = 值1 , 字段名2 = 值2 , .... [WHERE 条件];`

注意事项:

- DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据
- DELETE 语句不能删除某一个字段的值(可以使用UPDATE，将该字段值置为NULL即可)

### 删除数据

- 删除数据的具体语法为：`DELETE FROM 表名 [WHERE 条件];`

注意事项:

- DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据
- DELETE 语句不能删除某一个字段的值(可以使用UPDATE，将该字段值置为NULL即可)

## DQL

### 基本语法

- DQL 查询语句，语法结构如下：

  ```sql
  SELECT
  	字段列表
  FROM
  	表名列表
  WHERE
  	条件列表
  GROUP BY
  	分组字段列表
  HAVING
  	分组后条件列表
  ORDER BY
  	排序字段列表
  LIMIT
  	分页参数
  ```

### 基础查询

- 查询多个字段：`SELECT 字段1, 字段2, 字段3 ... FROM 表名;`

- 查询所有字段：`SELECT * FROM 表名;`

- 字段设置别名（AS可以省略）：

  `SELECT 字段1 [AS 别名1] , 字段2 [AS 别名2] ... FROM 表名;`

  `SELECT 字段1 [别名1] , 字段2 [别名2] ... FROM 表名;`
  
- 去除重复记录：`SELECT DISTINCT 字段列表 FROM 表名;`

### 条件查询

- 语法：`SELECT 字段列表 FROM 表名 WHERE 条件列表;`

- 条件：

  |比较运算符| 功能|
  |--|--|
  |`>` |大于|
  |`>=`| 大于等于|
  |`<` |小于|
  |`=` |小于等于|
  |`=` |等于|
  |`<> 或 !=` |不等于|
  |`BETWEEN ... AND ...` |在某个范围之内(含最小、最大值)|
  |`IN(...)` |在in之后的列表中的值，多选一|
  |`LIKE 占位符`| 模糊匹配(_匹配单个字符, %匹配任意个字符) |
  |`IS NULL` |是NULL|
  
  |逻辑运算符 |功能|
  |--|--|
  |`AND 或 &&` |并且 (多个条件同时成立)|
  |`OR 或 ||` |或者 (多个条件任意一个成立)|
  |`NOT 或 !` |非 , 不是|

### 聚合函数

- 将一列数据作为一个整体，进行纵向计算

- 常见的聚合函数：

  |函数 |功能|
  |--|--|
  |count| 统计数量|
  |max |最大值|
  |min |最小值|
  |avg |平均值|
  |sum |求和|

- 语法：`SELECT 聚合函数(字段列表) FROM 表名;`

- 注意：NULL值是不参与所有聚合函数运算的

### 分组查询

- 语法：`SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件]; `

- where与having区别：

  执行时机不同：where是分组之前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤

  判断条件不同：where不能对聚合函数进行判断，而having可以

- 注意事项:

  分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义

  执行顺序: where > 聚合函数 > having

  支持多字段分组, 具体语法为 : group by columnA,columnB

### 排序查询

- 语法：`SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1 , 字段2 排序方式2;`

- 排序方式：

  ASC : 升序(默认值)

  DESC: 降序

- 注意事项：

  如果是升序, 可以不指定排序方式ASC

  如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序

### 分页查询

- 语法：`SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数;`

- 注意事项：

  起始索引从0开始，起始索引 = （查询页码 - 1）* 每页显示记录数

  分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT

  如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10

### 案例：

```sql
# 查询年龄为20,21,22,23岁的员工信息
select * from emp where age in(20,21,22,23);

# 查询性别为 男 ，并且年龄在 20-40 岁(含)以内的姓名为三个字的员工
select * from emp where gender = '男' and (age between 20 and 40) and name like '___';

# 统计员工表中, 年龄小于60岁的 , 男性员工和女性员工的人数
select gender, count(*) from emp where age < 60 group by gender;

# 查询所有年龄小于等于35岁员工的姓名和年龄，并对查询结果按年龄升序排序，如果年龄相同按入职时间降序排序
select name, age from emp where age <= 35 order by age, entrydate desc;

# 查询性别为男，且年龄在20-40 岁(含)以内的前5个员工信息，对查询的结果按年龄升序排序，年龄相同按入职时间升序排序
select * from emp where gender = '男' and age between 20 and 40  order by age, entrydate desc limit 5;
```

### 执行顺序

- 编写顺序：

  ```sql
  SELECT
  	字段列表 --> 5
  FROM
  	表名列表 --> 1
  WHERE
  	条件列表 --> 2
  GROUP BY
  	分组字段列表 --> 3
  HAVING
  	分组后条件列表 --> 4
  ORDER BY
  	排序字段列表 --> 6
  LIMIT
  	分页参数 --> 7
  ```

- 执行顺序

  ```sql
  FROM
  	表名列表
  WHERE
  	条件列表
  GROUP BY
  	分组字段列表
  HAVING
  	分组后条件列表
  SELECT
  	字段列表
  ORDER BY
  	排序字段列表
  LIMIT
  	分页参数
  ```

## DCL

### 管理用户

- 查询用户：`select * from mysql.user;`
- 创建用户：`CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';`
- 修改用户密码：`ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';`
- 删除用户：`DROP USER '用户名'@'主机名';`

注意事项：

- 在MySQL中需要通过用户名@主机名的方式，来唯一标识一个用户
- 主机名可以使用`%`通配，表示可以在任意主机访问
- 这类SQL开发人员操作的比较少，主要是DBA（Database Administrator 数据库管理员）使用

### 权限控制

- MySQL中定义了很多种权限，但是常用的就以下几种：

  |权限 |说明|
  |--|--|
  |ALL,ALL PRIVILEGES |所有权限|
  |SELECT |查询数据|
  |INSERT |插入数据|
  |UPDATE |修改数据|
  |DELETE |删除数据|
  |ALTER| 修改表|
  |DROP| 删除数据库/表/视图|
  |CREATE |创建数据库/表|
  
  上述只是简单罗列了常见的几种权限描述，其他权限描述及含义，可以直接参考[官方文档](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html)
  
- 查询权限：`SHOW GRANTS FOR '用户名'@'主机名';`

- 授予权限：`GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';`

- 撤销权限：`REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';`

注意事项：

- 多个权限之间，使用逗号分隔
- 授权时，数据库名和表名可以使用`*`进行通配，代表所有



# 函数

## 字符串函数

- MySQL中内置了很多字符串函数，常用的几个如下：

  |函数| 功能|
  |--|--|
  |CONCAT(S1,S2,...Sn) |字符串拼接，将S1,S2,...Sn拼接成一个字符串|
  |LOWER(str) |将字符串str全部转为小写|
  |UPPER(str) |将字符串str全部转为大写|
  |LPAD(str,n,pad) |左填充，用字符串pad对str的左边进行填充，达到n个字符串长度|
  |RPAD(str,n,pad) |右填充，用字符串pad对str的右边进行填充，达到n个字符串长度|
  |TRIM(str) |去掉字符串头部和尾部的空格|
  |SUBSTRING(str,start,len) |返回从字符串str从start位置起的len个长度的字符串|

- 演示如下：

  ```sql
  # concat : 字符串拼接 以下输出HelloMySQL
  select concat('Hello', 'MySQL');
  
  # lower : 全部转小写 以下输出hello
  select concat('Hello');
  
  # upper : 全部转大写 以下输出MYSQL
  select upper('MySQL');
  
  # lpad : 左填充 以下输出---01
  select lpad('01', 5, '-');
  
  # rpad : 右填充 以下输出01---
  select rpad('01', 5, '-');
  
  # trim : 去除空格 以下输出Hello MySQL
  select trim(' Hello MySQL ');
  
  # substring : 截取子字符串 以下输出Hello
  select substring('Hello MySQL', 1, 5);
  
  # 由于业务需求变更，企业员工的工号，统一为5位数，目前不足5位数的全部在前面补0。比如：1号员工的工号应该为00001
  update emp set workno = lpad(workno, 5, '0');
  ```

## 数值函数

- 常见的数值函数如下：

  |函数 |功能|
  |--|--|
  |CEIL(x) |向上取整|
  |FLOOR(x)| 向下取整|
  |MOD(x,y) |返回x/y的模|
  |RAND()| 返回0~1内的随机数|
  |ROUND(x,y) |求参数x的四舍五入的值，保留y位小数|

- 演示如下：

  ```sql
  # ceil：向上取整 以下输出2
  select ceil(1.1);
  
  # floor：向下取整 以下输出1
  select floor(1.9);
  
  # mod：取模 以下输出3
  select mod(7, 4);
  
  # rand：获取随机数 以下输出0-1任意数
  select rand();
  
  # round：四舍五入 以下输出2.35
  select round(2.345, 2);
  
  # 通过数据库的函数，生成一个六位数的随机验证码
  # 获取随机数可以通过rand()函数，但是获取出来的随机数是在0-1之间的，所以可以在其基础上乘以1000000，然后舍弃小数部分，如果长度不足6位，补0
  select lpad(round(rand()*1000000, 0), 6, '0');
  ```

## 日期函数

- 常见的日期函数如下：

  |函数 |功能|
  |--|--|
  |CURDATE() |返回当前日期|
  |CURTIME() |返回当前时间|
  |NOW() |返回当前日期和时间|
  |YEAR(date) |获取指定date的年份|
  |MONTH(date) |获取指定date的月份|
  |DAY(date) |获取指定date的日期|
  |DATE_ADD(date, INTERVAL exprtype) |返回一个日期/时间值加上一个时间间隔expr后的时间值|
  |DATEDIFF(date1,date2) |返回起始时间date1 和 结束时间date2之间的天数|

- 演示如下：

  ```sql
  # curdate：当前日期 2023-02-16
  select curdate();
  
  # curtime：当前时间 14:56:06
  select curtime();
  
  # now：当前日期和时间 2023-02-16 14:56:28
  select now();
  
  # YEAR , MONTH , DAY：当前年、月、日
  select year(now());
  select month(now());
  select day(now());
  
  # date_add：增加指定的时间间隔
  select date_add(now(), interval 30 day);
  
  # datediff：获取两个日期相差的天数
  select datediff('2023-2-1', '2022-1-1');
  
  # 查询所有员工的入职天数，并根据入职天数倒序排序。
  # 思路：入职天数，就是通过当前日期 - 入职日期，所以需要使用datediff函数来完成
  select emp.name, datediff(curdate(), emp.entrydate) as 'entrydays' from emp order by entrydays desc ;
  ```

## 流程函数

- 流程函数也是很常用的一类函数，可以在SQL语句中实现条件筛选，从而提高语句的效率

- 常见的流程函数如下：

  |函数| 功能|
  |--|--|
  |IF(value, t, f) |如果value为true，则返回t，否则返回f|
  |IFNULL(value1, value2) |如果value1不为空，返回value1，否则返回value2|
  |CASE WHEN [val1] THEN [res1] ... ELSE [default] END |如果val1为true，返回res1，... 否则返回default默认值|
  |CASE [expr] WHEN [val1] THEN [res1] ... ELSE [default] END |如果expr的值等于val1，返回res1，... 否则返回default默认值|

- 演示如下：

  ```sql
  # if 以下返回'NO'
  select if(false, 'OK', 'NO');
  
  # ifnull 以下分别返回'Ok'、''、'Default'
  select ifnull('Ok','Default');
  select ifnull('','Default');
  select ifnull(null,'Default');
  
  # case when then else end
  # 需求: 查询emp表的员工姓名和工作地址 (北京/上海 ----> 一线城市 , 其他 ----> 二线城市)
  select
      name,
      (case workaddress when '北京' then '一线城市' when '上海' then '一线城市' else '二线城市' end) as '工作地址'
  from emp;
  
  # 案例: 统计班级各个学员的成绩，展示的规则如下:
  # >= 85，展示优秀
  # >= 60，展示及格
  # 否则，展示不及格
  select
      id,
      name,
      (case when math >= 85 then '优秀' when math >= 60 then '及格' else '不及格' end) as '数学',
      (case when english >= 85 then '优秀' when english >= 60 then '及格' else '不及格' end) as '英语',
      (case when chinese >= 85 then '优秀' when chinese >= 60 then '及格' else '不及格' end) as '语文'
  from score;
  ```



# 约束

