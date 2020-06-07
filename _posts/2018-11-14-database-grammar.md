---
layout: post
title: 数据库语法
date: 2018-11-14
Author: gwl
categories: 
tags: [Database]
comments: true
toc: true
---

### 数据库操作

```
创建用户
    create user gwl identified  by 'root123'
root为用户gwl授权，用户gwl可以操作数据库mydatabase下的所有表
    grant all on mydatabase.* to gwl

创建数据库
    格式:
    create database 数据库名;
    create database 数据库名 character set 字符集;

创建数据库，数据库中数据的编码采用的是安装数据库时指定的默认编码 utf8
    CREATE DATABASE mydatabase;
创建数据库 并指定数据库中数据的编码
    CREATE DATABASE mydatabase CHARACTER SET utf8;

查看数据库

查看数据库MySQL服务器中的所有的数据库:
    show databases;

查看某个数据库的定义的信息:
    show create database 数据库名;
例如:
    show create database mydatabase;

删除数据库
    drop database 数据库名称;
例如:
    drop database mydatabase;

其他的数据库操作命令
切换数据库:
    use 数据库名;
例如:
    use mydatabase;

查看正在使用的数据库:
    select database();
```

### 表结构相关语句

#### 创建表

```
格式:
    create table 表名 (
        字段名 类型(长度) 约束,
        字段名 类型(长度) 约束
    );

例如:
    CREATE TABLE mytable (
        sid INT,
        sname VARCHAR(100)
    );

    CREATE TABLE mytable

解决乱码问题
    CREATE TABLE mytable(name VARCHAR(20)) DEFAULT CHARSET = utf8

    CREATE TABLE mytable (
        id INT PRIMARY KEY AUTO_INCREMENT,
        pname VARCHAR(100) NOT NULL,
        price DOUBLE
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

#### 主键约束

```
主键是用于标识当前记录的字段。它的特点是非空，唯一。在开发中一般情况下主键是不具备 任何含义，只是用于标识当前记录。
格式:
1.在创建表时创建主键，在字段后面加上 primary key
    create table tablename (
        id int primary key,
        .......
    )
2.在创建表时创建主键，在表创建的最后来指定主键
    create table tablename(
        id int,
        ...,
        primary key(id)
    )
3.删除主键:alter table 表名 drop primary key;
    alter table tablename drop primary key;
4.主键自动增长:一般主键是自增长的字段，不需要指定。 实现添加自增长语句,主键字段后加auto_increment(只适用MySQL)
例如: 创建分类表
    CREATE TABLE tablename (
        sid INT PRIMARY KEY auto_increment,
        sname VARCHAR(100)
    );
```

#### 查看表

```
查看数据库中的所有表:
    格式:show tables;

查看表结构:
格式:desc 表名;
    例如:desc tablename;
```

#### 删除表

```
格式:drop table 表名;
    例如:drop table tablename;
```

#### 修改表结构格式

```
alter table 表名 add 列名 类型(长度) 约束; 作用:修改表添加列.
例如: 为分类表添加一个新的字段为 分类描述 varchar(20)
    ALTER TABLE sort ADD sdesc VARCHAR(20);

alter table 表名 modify 列名 类型(长度) 约束;作用:修改表修改列的类型长度及约束.
例如: 为分类表的分类名称字段进行修改，类型varchar(50) 添加约束 not null
    ALTER TABLE sort MODIFY sname VARCHAR(50) NOT NULL;

alter table 表名 change 旧列名 新列名 类型(长度) 约束; 作用:修改表修改列名.
例如: 为分类表的分类名称字段进行更换 更换为 snamesname varchar(30)
    ALTER TABLE sort CHANGE sname snamename VARCHAR(30);

alter table 表名 drop 列名; 作用:修改表删除列.
例如: 删除分类表中snamename这列
    ALTER TABLE sort DROP snamename;

rename table 表名 to 新表名; 作用:修改表名
例如: 为分类表sort 改名成category
    RENAME TABLE sort TO category;

alter table 表名 character set 字符集; 作用:修改表的字符集
例如: 为分类表category 的编码表进行修改，修改成gbk
    ALTER TABLE category CHARACTER SET gbk;

格式：alter table 表名 change 字段名 字段名 varchar(50) character set utf8 not null; 作用:修改字段的编码
例如：alter table account change name name varchar(50) character set utf8 not null;
```

#### 插入表记录

```
向表中插入某些列
    insert into 表 (列名1,列名2,列名3..) values (值1,值2,值3..);
向表中插入所有列
    insert into 表 values (值1,值2,值3..);

注意:
    1.插入的数据应与字段的数据类型相同
    2.数据的大小应该在列的长度范围内
    3.在values中列出的数据位置必须与被加入列的排列位置相对应。
    4.除了数值类型外，其它的字段类型的值必须使用引号引起。
    5.如果要插入空值，可以不写字段，或者插入 null。
    6.对于自动增长的列在操作时，直接插入null值即可。

例如:
    INSERT INTO sort(sid,sname) VALUES('s001', '电器');
    INSERT INTO sort VALUES ('s003', '化妆品');

批量插入
    INSERT INTO product (pname,price) VALUES ('洗衣机77',4432.23),
    ('洗衣机88',442.223),('洗衣机99',442334.23)
```

#### 更新表记录

```
用来修改指定条件的数据，将满足条件的记录指定列修改为指定值
语法:
    update 表名 set 字段名=值,字段名=值;
    update 表名 set 字段名=值,字段名=值 where 条件;

注意:
    1.列名的类型与修改的值要一
    2.修改值得时候不能超过最大长度
    3.值如果是字符串或者日期需要加‘’

例如:
    将指定的sname字段中的值 修改成 日用品
        UPDATE sort SET sname = '日用品';
    将sid为s002的记录中的sname改成 日用品
        UPDATE sort SET sname='日用品' WHERE sid='s002';

UPDATE product SET pname = '黑白显示器',price = 100 WHERE id = 3
UPDATE product SET pname = '黑白显示器',price = 100 WHERE id IN (1,2,3,4)
```

#### 删除记录

```
语法:
    delete from 表名 [where 条件];
    DELETE FROM product WHERE id = 4
或者
    truncate table 表名;

delete和truncate:
    删除表中所有记录使用delete from 表名; 还是用truncate table 表名;
    删除方式: delete 一条一条删除，不清空auto_increment记录数。
            truncate 直接将表删除，重新建表，auto_increment将置为零，从新开始。
```

#### DOS操作数据乱码解决

```
我们在dos命令行操作中文时，会报错
    insert into user(username,password) values(‘张三’,’123’);
    ERROR 1366 (HY000): Incorrect string value: '\xD5\xC5\xC8\xFD' for column 'username' at row 1
原因:因为mysql的客户端编码的问题我们的是utf8,而系统的cmd窗又编码是gbk
解决方案(临时解决方案):修改mysql客户端编码。
    show variables like 'character%'; 查看所有mysql的编码

client connetion result 和客户端相关
database server system 和服务器端相关
将客户端编码修改为gbk.
    set character_set_results=gbk; / set names gbk;

以上操作，只针对当前窗又有效果，如果关闭了服务器便失效。如果想要永久修改，通过以下 方式:
在mysql安装目录下有my.ini文件
    default-character-set=gbk 客户端编码设置
    character-set-server=utf8 服务器端编码设置
注意:修改完成配置文件，重启服务
```


### SQL查询语句

> 表结构
>>    CREATE TABLE zhangwu (
>>        id INT PRIMARY KEY AUTO_INCREMENT,
>>        name VARCHAR(200),
>>        money DOUBLE,
>>    );

#### 查询的语法

```
查询指定字段信息
    select 字段1,字段2,...from 表名;
例如:
    select id,name from zhangwu;

查询表中所有字段 select * from 表名;
例如:
    select * from zhangwu;
注意:使用"*"在练习、学习过程中可以使用，在实际开发中，不推荐使用。原因，要查询的字段信息不明确，若字段数量很多，会导致查询速度很慢。

distinct用于去除重复记录
    select distinct 字段 from 表名;
例如:
    select distinct money from zhangwu;

别名查询，使用的as关键字，as可以省略的.
别名可以给表中的字段，表设置别名。 当查询语句复杂时，使用别名可以极大的简便操作。
表别名格式:
    select * from 表名 as 别名;
或
    select * from 表名 别名;

列别名格式:
    select 字段名 as 别名 from 表名;
或
    select 字段名 别名 from 表名;

例如
表别名:
    select * from zhangwu as zw;
列别名:
    select money as m from zhangwu;
或
    select money m from zhangwu;

我们在sql语句的操作中，可以直接对列进行运算。
例如:将所有账务的金额+10000元进行显示.
    select pname,price+10000 from product;
```

#### 条件查询

```
where语句表条件过滤。满足条件操作，不满足不操作，多用于数据的查询与修改。 格式 :select 字段 from 表名 where 条件;
while条件的种类如下:
    <
    >
    <=
    >=
    =                   等于
    <>                  不等于
    BETWEEN ...AND...   显示在某一区间的值(含头含尾)
    IN(set)             显示在in列表中的值，例:in(100,200)
    LIKE 通配符          模糊查询，like语句中有两个通配符:
                        % 用来匹配多个字符;例first_name like ‘a%’;
                        _ 用来匹配一个字符。例first_name like ‘a_’;
    IS NULL             判断是否为空 is null: 判断为空; is not null: 判断不为空
    and                 多个条件同时成立
    or                  多个条件任一成立
    not                 不成立，例:where not(salary>100);

例如
    SELECT * FROM zhangwu WHERE money >1000;

    SELECT * FROM zhangwu WHERE money >=2000 AND money <=5000;
    SELECT * FROM zhangwu WHERE money BETWEEN 2000 AND 5000;

    SELECT * FROM zhangwu WHERE money =1000 OR money =5000 OR money =3500;
    SELECT * FROM zhangwu WHERE money IN(1000,5000,3500);

    查询出账务名称包含”支出”的账务信息。
    SELECT * FROM zhangwu WHERE name LIKE "%支出%";

    查询出账务名称中是无五个字的账务信息  五个下划线 _
    SELECT * FROM gjp_ledger WHERE ldesc LIKE "_____";

    查询出账务名称不为null账务信息
    SELECT * FROM zhangwu WHERE name IS NOT NULL;
    SELECT * FROM zhangwu WHERE NOT (name IS NULL);
```

### 排序、聚合函数...

```
/*
 查询，对结果集进行排序
 升序(ASC)
 降序(DESC)
 默认升序
 */

/*
 升序排列
 */
SELECT *FROM product ORDER BY price
SELECT *FROM product ORDER BY price ASC

/*
 降序排列
 */
SELECT *FROM product ORDER BY price DESC

/*
 先过滤条件，再排序
 */
SELECT *FROM product WHERE pname LIKE '%本%' ORDER BY price DESC


使用聚合函数查询计算
/*
 count 求和
 */
SELECT COUNT(*) FROM product
SELECT COUNT(*) AS 'count' FROM product

/*
 sum 求和
 */
SELECT SUM(price) FROM product
SELECT SUM(price) FROM product WHERE pname LIKE '%记%'

/*
 最大
 */
SELECT MAX(price) FROM product
SELECT MAX(price) FROM product WHERE pname LIKE '%记%'

/*
 最小
 */
SELECT MIN(price) FROM product
SELECT MIN(price) FROM product WHERE pname LIKE '%记%'

/*
 平均值
 */
SELECT AVG(price) FROM product
SELECT AVG(price) FROM product WHERE pname LIKE '%记%'

/*
 分组查询
 select 查询的时候，被分组的列，要出现在select选择列的后面
 */
SELECT SUM(price) , pname FROM product GROUP BY pname

SELECT SUM(price) , pname FROM product WHERE pname LIKE '%记%' GROUP BY pname ORDER BY SUM(price)

/*
 改名字为 getsum
 降序
 */
SELECT SUM(price) AS 'getsum', pname FROM product WHERE pname LIKE '%记%'
GROUP BY pname
ORDER BY SUM(price) DESC

/*
 分组后再次过滤 关键字 HAVING
 */
SELECT SUM(price) AS 'getsum', pname FROM product WHERE pname LIKE '%记%'
GROUP BY pname
HAVING getsum > 100
```

> 记录，便于查询