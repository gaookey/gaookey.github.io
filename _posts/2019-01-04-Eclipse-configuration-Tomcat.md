---
layout: post
title: eclipse配置Tomcat
date: 2019-01-04
Author: gwl
categories: java
tags: [eclipse, Tomcat]
comments: true
---


> [Tomcat安装: https://gwl.xyz/Tomcat-installation/](https://gwl.xyz/Tomcat-installation/)

> [IntelliJ IDEA配置Tomcat: https://gwl.xyz/IntelliJ-IDEA-configuration-Tomcat/](https://gwl.xyz/IntelliJ-IDEA-configuration-Tomcat/)

> [eclipse配置Tomcat: https://gwl.xyz/Eclipse-configuration-Tomcat/](https://gwl.xyz/Eclipse-configuration-Tomcat/)


### eclipse和tomcat绑定

创建Dynamic Web Project项目

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-01.jpg?raw=true)

配置如下

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-02.jpg?raw=true)

创建的新工程目录结构如下

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-03.jpg?raw=true)

选择 eclipse -> Preferences -> Server -> Runtime Environments -> Add

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-04.jpg?raw=true)

选择Apache版本，勾选 Create a new local server（也可不勾选后期配置） 

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-05.jpg?raw=true)

选择文件夹目录

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-06.jpg?raw=true)

eclipse切换至java EE，右上角选择java EE，控制台显示如下

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-07.jpg?raw=true)

双击Tomcat，配置

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-08.jpg?raw=true)

开启Tomcat

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-09.jpg?raw=true)

打开我们的浏览器，然后网址输入 [http://localhost:8080/](http://localhost:8080/)，出现那只猫，则成功。


### 使用eclipse发布工程

#### 第一种方法：

右击控制台Tomcat，点击Add and Remove

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-10.jpg?raw=true)

选择项目添加或移除

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-11.jpg?raw=true)

#### 第二种方法：

选中工程右键选择Run As -> Run on Server

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-12.jpg?raw=true)

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-13.jpg?raw=true)

> WebContent目录下index.html文件
>> ![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-14.jpg?raw=true)

运行成功，默认访问的index.html文件

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-15.jpg?raw=true)

以上两种方法添加后的项目则出现在Tomcat目录下webapps文件里，只拷贝WebContent目录

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-16.jpg?raw=true)

### servlet测试

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-17.jpg?raw=true)

配置文件web.xml

> Schema参见 [https://my.oschina.net/gwlCode/blog/2995818](https://my.oschina.net/gwlCode/blog/2995818)

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://www.example.org/web-app_2_5"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.example.org/web-app_2_5 web-app_2_5.xsd"
         version="2.5">
    
    <servlet>
        <servlet-name>Test</servlet-name>
        <servlet-class>Test</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>Test</servlet-name>
        <!-- http议访问时 资源的虚拟的路径 以/开始 -->
        <url-pattern>/abc</url-pattern>
    </servlet-mapping>
    <welcome-file-list>
        <welcome-file></welcome-file>
    </welcome-file-list>
</web-app>
```

Test

```
import java.io.IOException;

import javax.servlet.Servlet;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletResponse;

public class Test implements Servlet {

	@Override
	public void service(ServletRequest arg0, ServletResponse arg1) throws ServletException, IOException {
		// 专门向客户端提供响应的方法
		HttpServletResponse response = (HttpServletResponse) arg1;
        // 中文        
        // response.setContentType("text/html;charset=UTF-8");
		response.getWriter().write("My First Server");
	}

	@Override
	public void destroy() {
		// TODO Auto-generated method stub
		
	}

	@Override
	public ServletConfig getServletConfig() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public String getServletInfo() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public void init(ServletConfig arg0) throws ServletException {
		// TODO Auto-generated method stub
		
	}
}
```

在浏览器输入 [http://localhost:8080/Demo/abc](http://localhost:8080/Demo/abc)

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-04-Eclipse-configuration-Tomcat/2019-01-04-Eclipse-configuration-Tomcat-18.jpg?raw=true)