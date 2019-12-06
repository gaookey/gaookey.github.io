---
layout: post
title: IntelliJ IDEA配置Tomcat
date: 2019-01-08
Author: gwl
categories: java
tags: [Tomcat, IDEA]
comments: true
---

> [Tomcat安装及eclipse配置参见：https://my.oschina.net/gwlCode/blog/2996915#h1_11](https://my.oschina.net/gwlCode/blog/2996915#h1_11) 


#### 创建工程

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-01.jpg?raw=true)

#### 配置Configurations

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-02.jpg?raw=true)

#### 添加Tomcat

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-03.jpg?raw=true)

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-04.jpg?raw=true)

#### 配置Tomcat

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-05.jpg?raw=true)

> tip：若不出现Application context：此项，也不可下拉，则放大此窗口

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-06.jpg?raw=true)

配置完成，控制台显示如下

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-07.jpg?raw=true)

启动服务，浏览器出现如下，则成功

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-08.jpg?raw=true)

显示内容为index.jsp文件内容

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-09.jpg?raw=true)


### 工程添加到Tomcat

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-10.jpg?raw=true)

设置Output directory路径，在Tomcat/webapps文件夹下拼接上存放工程的文件名

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-11.jpg?raw=true)

### Servlet测试

#### 导入servlet-api.jar

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-12.jpg?raw=true)

#### 配置文件web.xml

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
        <url-pattern>/abc</url-pattern>
    </servlet-mapping>
    <welcome-file-list>
        <welcome-file></welcome-file>
    </welcome-file-list>
</web-app>
```

#### Test

```
import javax.servlet.*;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Test implements Servlet {
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {

        HttpServletResponse response = (HttpServletResponse) servletResponse;
        response.getWriter().write("My First IDEA Server");
    }

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }


    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```

运行服务或在浏览器输入 [http://localhost:8080/untitled_war_exploded/abc](http://localhost:8080/untitled_war_exploded/abc)，显示如下则成功

![img](https://github.com/mouos/mouos.github.io/blob/master/images/article_images/2019-01-08-IntelliJ-IDEA-configuration-Tomcat/2019-01-08-IntelliJ-IDEA-configuration-Tomcat-13.jpg?raw=true)
