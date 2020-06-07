---
layout: post
title: Windows下MySQL安装
date: 2019-01-15
Author: gwl
categories: MySQL
tags: [MySQL]
comments: true
toc: true
---

> [MAC下MySQL下载、安装、卸载](https://swiftprimer.com/mac-mysql-download-installation-uninstall/)

### 下载MySQL

[MySQL下载地址：https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

选择对应的操作系统和版本下载，Looking for previous GA versions? 选择旧版本（5.7.24）

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-01.jpg)

解压下载的文件到mysql目录 （D:\mysql），解压后的目录结构为

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-02.jpg)

在 D:\mysql\mysql-5.7.25-winx64 目录下新建my.ini文件，复制如下内容

```
[mysqld]
 
#设置3306端
 
port = 3306
 
# 设置mysql的安装目录
 
basedir=D:\mysql\mysql-5.7.25-winx64
 
# 设置mysql数据库的数据的存放目录
 
datadir=D:\mysql\mysql-5.7.25-winx64\data
 
# 允许最大连接数
 
max_connections=200
 
# 服务端使用的字符集默认为8比特编码的latin1字符集
 
character-set-server=utf8
 
# 创建新表时将使用的默认存储引擎
 
default-storage-engine=INNODB
 
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
 
[mysql]
 
# 设置mysql客户端默认字符集
 
default-character-set=utf8
```

### 配置

右键点击 我的电脑->属性->高级系统设置->环境变量->系统变量，编辑 Path－将mysql的路径 D:\mysql\mysql-5.7.25-winx64\bin 添加进去（;分开）－确定

### 安装MySQL

开始菜单，搜索cmd，右键以管理员身份运行cmd，进入mysql的bin目录，执行安装命令

```
mysqld --install
```

如果安装失败，提示如下，则网上下载 msvcr120.dll 文件，放在C:\Windows\System32目录下，或者直接下载 [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/zh-CN/download/details.aspx?id=40784) 安装

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-03.jpg)

如果已存在mysql，则提示

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-04.jpg)

可执行删除命令移除，成功后再次运行安装命令 mysqld --install

```
mysqld --remove
```

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-05.jpg)

安装成功

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-06.jpg)

生成data目录

```
mysqld --initialize
```

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-07.jpg)

启动服务

```
net start mysql
```

如果启动服务失败，遇到如下情况，则 右键点击 我的电脑->属性->高级系统设置->环境变量->系统变量，编辑 Path－将 C:\Windows\System32 添加进去（;分开）－确定

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-08.jpg)

关闭cmd，重新以管理员身份运行，cd到bin目录下重新执行 net start mysql

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-09.jpg)

停止服务

```
net stop mysql
```

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-10.jpg)

开启无密码的MySQL Server

```
mysqld --skip-grant-tables
```

先停止服务再执行开启无密码，不然出现以下错误

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-11.jpg)

新开一个终端，输入mysql -u root -p进入mysql，回车键无需敲入密码

```
mysql -u root -p
```

![img](https://github.com/mouos/image-hosting-service/raw/master/images/2019-01-15-windows-mysql-install-12.jpg)

 然后更新root账户的密码为'123456'

```
update mysql.user set authentication_string=password("123456") where user="root";
```

执行刷新权限

```
flush privileges;
```

执行 quit; 退出MySQL，再次执行 mysql -u root -p 即可输入密码进入

再次就改密码为

```
SET PASSWORD = PASSWORD('new password');

ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;

flush privileges;
```