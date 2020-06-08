---
layout: post
title: Sequel Pro登录失败
date: 2018-12-27
Author: gwl
categories: 
tags: [Sequel]
comments: false
toc: true
---


使用Mac下的sequel Pro链接数据库时，出现如下问题：

>  **Connection failed!**
>
>  > 
>  > Unable to connect to host 127.0.0.1, or the request timed out.
>  > 
>  > Be sure that the address is correct and that you have the necessary privileges, or try increasing the connection timeout (currently 10 seconds).
>  > 
>  > MySQL said: Authentication plugin 'caching_sha2_password' cannot be loaded: dlopen(/usr/local/lib/plugin/caching_sha2_password.so, 2): image not found

问题描述：就是在链接数据库时不能加载 `caching_sha2_password` 这个插件，也就是不能对身份验证。

### 解决方案：

1.打开系统偏好设置，找到mysql，点击Initialize Database。

![img](https://github.com/mouos/mouos.github.io/raw/master/images/articleImages/2018-12-27-login-failed-01.jpg)

2.输入你的新密码，记住这个密码，用于后期链接数据库的登陆使用，选择‘Use legacy password‘。

![img](https://github.com/mouos/mouos.github.io/raw/master/images/articleImages/2018-12-27-login-failed-02.jpg)

3.重启mysql服务，使用sequel Pro链接。

![img](https://github.com/mouos/mouos.github.io/raw/master/images/articleImages/2018-12-27-login-failed-03.jpg)