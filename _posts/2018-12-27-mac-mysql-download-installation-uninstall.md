---
layout: post
title: MAC下MySQL下载、安装、卸载
date: 2018-12-27
Author: gwl
categories: MySQL
tags: [MySQL]
comments: true
---

> [Windows下MySQL安装](https://my.oschina.net/gwlCode/blog/3001993)

### 安装

[MySQL下载地址：https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-01.jpg?raw=true)

选择系统版本下载，点击Looking for previous GA versions?可下载旧版本，选择5.7.24即可，6.0后的收费

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-02.jpg?raw=true)

选择No thanks, just start my download.直接下载，打开下载的文件安装

安装成功后提示：

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-03.jpg?raw=true)

localhost:后为默认的密码。系统偏好设置查看MySQL

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-04.jpg?raw=true)

点击后, 启动MySQL 

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-05.jpg?raw=true)

### 修改数据库密码

启动完成后,打开终端

```
alias mysql=/usr/local/mysql/bin/mysql
```

```
alias mysqladmin=/usr/local/mysql/bin/mysqladmin
```

把上面两条指令复制到终端当中运行,给两个地址给一个临时别名

目的是下一次执行可以直接执行mysql或者mysqladmin

不需要再去来回切换目录

接下来修改数据库密码,执行以下命令

```
mysqladmin -u root -p password root123
```

root123是我的新密码,自行修改成自己想要设置的密码

按回车后, 提示输入密码,此时让输入的密码不是你电脑的密码，而是数据库的密码。

在5.7之前都是有默认用户名和密码的,都为root

但是从5.7之后, 只有默认的用户名P:root

默认的密码会自动给你分配,在安装的时候就会给你自动分配。

我们也可以从mac通知栏当中来去查看，下图当中就是自动生成一个数据库密码

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-06.jpg?raw=true)

看到如下信息,修改成功

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-07.jpg?raw=true)

接下来执行以下指令:

```
mysql -u root -p
```

会让你输入密码, 此时的密码就是你在上面修改的密码（root123）

看到如下信息,全部说明已经进入数据库当中

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2018-12-27-mac-mysql-download-installation-uninstall/2018-12-27-mac-mysql-download-installation-uninstall-08.jpg?raw=true)


### 卸载

先停止所有mysql有关进程。

```
1 sudo rm /usr/local/mysql
2 sudo rm -rf /usr/local/mysql*
3 sudo rm -rf /Library/StartupItems/MySQLCOM
4 sudo rm -rf /Library/PreferencePanes/My*
5 vim /etc/hostconfig  (and removed the line MYSQLCOM=-YES-)
6 rm -rf ~/Library/PreferencePanes/My*
7 sudo rm -rf /Library/Receipts/mysql*
8 sudo rm -rf /Library/Receipts/MySQL*
9 sudo rm -rf /var/db/receipts/com.mysql.*
```