---
author: fangrenbin
comments: true
date: 2013-10-31 06:23:21+00:00
layout: post
slug: create-j2ee-application
title: 创建j2ee应用
wordpress_id: 580
categories:
- wordpress
---

需要：
1、struts2
2、spring
3、Hibernate和JDBC
流程：
web.xml功能：
1、载入spring配置文件application-*.xml文件
2、载入log配置文件
3、struts2配置文件：maven直接打包的时候会载入/src/main/resources目录下面的struts.xml文件，这个文件可以include其它的struts的配置。
使用xml来配置系统参数，比如：数据库连接信息、上传文件路径、sql语句、mongoDB的JS配置文件。
使用maven的xdoclet插件来生成hibernate的映射文件。
请求地址重写：urlrewrite
单元测试使用testng，载入的配置资源文件在/src/test/resource目录下面。

项目缺陷管理系统JIRA。
