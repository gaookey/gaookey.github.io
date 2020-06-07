---
layout: post
title: MySQL插入中文时编码错误：ERROR 1366 (HY000): Incorrect string value: '' for column '' at row 1
date: 2019-01-22
Author: gwl
categories: 
tags: [MySQL]
comments: true
---

插入数据时

```
insert into account values(null,'名字',5000);
```

提示如下错误

```
ERROR 1366 (HY000): Incorrect string value: '\xE5\x90\x8D\xE5\xAD\x97' for column 'name' at row 1
```

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-22-mysql-inserting-chinese-code-error/2019-01-22-mysql-inserting-chinese-code-error-01.jpg?raw=true)

查看数据表编码

```
show create table account;
```

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-22-mysql-inserting-chinese-code-error/2019-01-22-mysql-inserting-chinese-code-error-02.jpg?raw=true)

修改数据表编码

```
alter table account character set utf8;
```

查看修改后的编码

```
show create table account;
```

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-22-mysql-inserting-chinese-code-error/2019-01-22-mysql-inserting-chinese-code-error-03.jpg?raw=true)

此时表编码已修改为utf8，但name仍未lantin1，插入数据仍会出现如上错误，需要修改字段编码

格式：alter table 表名 change 字段名 字段名 varchar(50) character set utf8 not null;

```
alter table account change name name varchar(50) character set utf8 not null;
```

修改后如下

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-22-mysql-inserting-chinese-code-error/2019-01-22-mysql-inserting-chinese-code-error-04.jpg?raw=true)
