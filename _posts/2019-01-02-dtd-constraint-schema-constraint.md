---
layout: post
title: DTD约束、Schema约束
date: 2019-01-02
Author: gwl
categories: java
tags: [DTD, Schema]
comments: true
toc: true
---

### DTD

> [DTD 菜鸟教程：http://www.runoob.com/dtd/dtd-tutorial.html](http://www.runoob.com/dtd/dtd-tutorial.html)

#### xml文件

```
<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE web-app SYSTEM "web-app_2_3.dtd">
<web-app>
    <servlet>
        <servlet-name></servlet-name>
        <servlet-class></servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name></servlet-name>
        <url-pattern></url-pattern>
    </servlet-mapping>
    <welcome-file-list>
        <welcome-file></welcome-file>
    </welcome-file-list>
</web-app>
```

#### web-app_2_3.dtd 文件

```
<?xml version="1.0" encoding="UTF-8"?>
<!--
	模拟servlet2.3规范，如果开发人员需要在xml使用当前DTD约束，必须包括DOCTYPE。
	格式如下：
	<!DOCTYPE web-app SYSTEM "web-app_2_3.dtd">
-->
<!ELEMENT web-app (servlet*,servlet-mapping* , welcome-file-list?) >
<!ELEMENT servlet (servlet-name,description?,(servlet-class|jsp-file))>
<!ELEMENT servlet-mapping (servlet-name,url-pattern+) >
<!ELEMENT servlet-name (#PCDATA)>
<!ELEMENT servlet-class (#PCDATA)>
<!ELEMENT url-pattern (#PCDATA)>
<!ELEMENT description (#PCDATA)>
<!ELEMENT jsp-file (#PCDATA)>

<!ELEMENT welcome-file-list (welcome-file+)>
<!ELEMENT welcome-file (#PCDATA)>

<!ATTLIST web-app version CDATA #IMPLIED>
```


### Schema

> [Schema 教程:http://www.w3school.com.cn/schema/index.asp](http://www.w3school.com.cn/schema/index.asp)

#### xml文件

```
<?xml version="1.0" encoding="utf-8" ?>
<web-app xmlns="http://www.example.org/web-app_2_5"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.example.org/web-app_2_5 web-app_2_5.xsd"
         version="2.5">
    
    <servlet>
        <servlet-name></servlet-name>
        <servlet-class></servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name></servlet-name>
        <url-pattern></url-pattern>
    </servlet-mapping>
    <welcome-file-list>
        <welcome-file></welcome-file>
    </welcome-file-list>
</web-app>
```

#### web-app_2_5.xsd 文件

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- 
	模拟servlet2.5规范，如果开发人员需要在xml使用当前Schema约束，必须包括指定命名空间。
	格式如下：
	<web-app xmlns="http://www.example.org/web-app_2_5" 
			xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			xsi:schemaLocation="http://www.example.org/web-app_2_5 web-app_2_5.xsd"
			version="2.5">
-->
<xsd:schema xmlns="http://www.w3.org/2001/XMLSchema" 
	targetNamespace="http://www.example.org/web-app_2_5"
	xmlns:xsd="http://www.w3.org/2001/XMLSchema"
	xmlns:tns="http://www.example.org/web-app_2_5" 
	elementFormDefault="qualified">
	
	<xsd:element name="web-app">
		<xsd:complexType>
			<xsd:choice minOccurs="0" maxOccurs="unbounded">
				<xsd:element name="servlet">
					<xsd:complexType>
						<xsd:sequence>
							<xsd:element name="servlet-name"></xsd:element>
							<xsd:element name="servlet-class"></xsd:element>
						</xsd:sequence>
					</xsd:complexType>
				</xsd:element>
				<xsd:element name="servlet-mapping">
					<xsd:complexType>
						<xsd:sequence>
							<xsd:element name="servlet-name"></xsd:element>
							<xsd:element name="url-pattern" maxOccurs="unbounded"></xsd:element>
						</xsd:sequence>
					</xsd:complexType>
				</xsd:element>
				<xsd:element name="welcome-file-list">
					<xsd:complexType>
						<xsd:sequence>
							<xsd:element name="welcome-file" maxOccurs="unbounded"></xsd:element>
						</xsd:sequence>
					</xsd:complexType>
				</xsd:element>
			</xsd:choice>
			<xsd:attribute name="version" type="double" use="optional"></xsd:attribute>
		</xsd:complexType>
	</xsd:element>
</xsd:schema>
```
