---
author: fangrenbin
comments: true
date: 2014-05-12 08:37:11+00:00
layout: post
slug: spring-data-jpa-null-point
title: spring data jpa null point
wordpress_id: 600
categories:
- spring
- wordpress
---

Spring data jpa在单元测试的时候没有任何问题，当在TOMCAT中启动项目以后，抛空指针，原来是在jpa的配置文件中没有加


    
    
    <context:component-scan base-package="name.frb.wechat.**.repository"></context:component-scan>
    


加入就可以了。
