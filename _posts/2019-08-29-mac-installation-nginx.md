---
layout: post
title: mac下安装nginx
date: 2019-08-29
Author: gwl
categories: 
tags: [nginx]
comments: false
toc: true
---


安装工具
[homebrew](https://brew.sh/index_zh-cn.html)

安装nginx

```
brew update
```

```
brew search nginx
```

```
brew info nginx
```

![img](https://github.com/mouos/mouos.github.io/raw/master/images/articleImages/2019-08-29-mac-installation-nginx-01.png)

```
brew install nginx
```

启动

```
nginx
```

浏览器输入 [http://localhost:8080/](http://localhost:8080/)

![img](https://github.com/mouos/mouos.github.io/raw/master/images/articleImages/2019-08-29-mac-installation-nginx-02.png)

nginx的配置文件地址:

```
/usr/local/etc/nginx/nginx.conf
```
