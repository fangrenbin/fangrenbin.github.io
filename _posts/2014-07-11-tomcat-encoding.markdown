---
author: fangrenbin
comments: true
date: 2014-07-11 05:15:04+00:00
layout: post
slug: tomcat-encoding
title: tomcat中文乱码解决方法
wordpress_id: 641
categories:
- Java
---

修改文件server.xml

    
    
    /apache-tomcat-6.0.41/conf/server.xml
    


在标签中加入

    
    
    URIEncoding="UTF-8"
    
