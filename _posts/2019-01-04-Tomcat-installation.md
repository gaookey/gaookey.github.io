---
layout: post
title: Tomcat安装
date: 2019-01-04
Author: gwl
categories: java
tags: [Tomcat]
comments: true
---


> [Tomcat安装: https://gwl.xyz/Tomcat-installation/](https://gwl.xyz/Tomcat-installation/)
> [IntelliJ IDEA配置Tomcat: https://gwl.xyz/IntelliJ-IDEA-configuration-Tomcat/](https://gwl.xyz/IntelliJ-IDEA-configuration-Tomcat/)
> [eclipse配置Tomcat: https://gwl.xyz/Eclipse-configuration-Tomcat/](https://gwl.xyz/Eclipse-configuration-Tomcat/)


### 下载

登录Apache Tomcat官网，地址 [http://tomcat.apache.org](http://tomcat.apache.org) ，选择需要下载的版本。 

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-01.jpg?raw=true)

把下载下来的包解压到合适的位置

### MAC安装方式

#### 启动Tomcat

打开终端输入（切换到我们Tomcat的bin目录）

```
cd /Users/mac/apache-tomcat-9.0.14/bin
```

终端输入

```
./startup.sh
```

出现 Permission denied 则操作失败，缺少权限，赋予超级管理员权限

```
sudo chmod 755 *.sh
```

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-02.jpg?raw=true)

再次启动

```
./startup.sh
```

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-03.jpg?raw=true)

#### 关闭Tomcat

终端输入

```
./shutdown.sh
```

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-04.jpg?raw=true)


### Windows安装方式

#### 配置Tomcat环境变量

计算机 -> 属性 -> 高级系统设置 -> 高级 -> 环境变量，在系统变量中添加 TOMCAT_HOME 和 CATALINA_HOME

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-05.jpg?raw=true)

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-06.jpg?raw=true)

修改系统变量Path，在末尾添加如下内容
`;%TOMCAT_HOME%\bin;%CATALINA_HOME%\lib`

#### 启动Tomcat服务器

在cmd命令窗口下输入 `startup` 回车，运行如下图所示

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-07.jpg?raw=true)

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-08.jpg?raw=true)

如下图显示，则是未安装jdk

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-09.jpg?raw=true)

#### 验证

打开我们的浏览器，然后网址输入 [http://localhost:8080/](http://localhost:8080/)，如果出现下图页面，则证明配置成功 

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Tomcat-installation/2019-01-04-Tomcat-installation-10.jpg?raw=true)





