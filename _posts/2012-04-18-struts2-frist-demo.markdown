---
author: fangrenbin
comments: true
date: 2012-04-18 04:34:41+00:00
layout: post
slug: struts2-frist-demo
title: struts2环境搭建和第一个struts2应用
wordpress_id: 329
categories:
- struts2
---

struts2下载地址
[http://apache.etoak.com/struts/binaries/](http://apache.etoak.com/struts/binaries/)

找到开发struts2应用需要使用到的jar文件
编写struts2的配置文件struts.xml
在web.xml中加入Struts2 MVC框架启动配置

具体操作步骤：



	
  1. 创建web项目

	
  2. 导入Jar文件

	
  3. 编写struts2配置文件，struts.xml开发阶段放在src目录下面，配置文件的模板可以从struts2包的例子里面烤，也可以从文档里面烤。例子在apps目录下面，解压下面的包，\apps\struts2-blank\WEB-INF\classes目录下面就有struts.xml文件了。

	
  4. 在WEB-INF文件夹下面新建web.xml，加入代码。


第一个struts2应用：

	
  * 新建Action类和编写execute方法

	
  * 新建jsp文件，定义视图


