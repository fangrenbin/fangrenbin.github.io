---
author: fangrenbin
comments: false
date: 2014-06-26 08:35:47+00:00
layout: post
slug: maven-building-exclude-file
title: maven构建时排除特定的文件
wordpress_id: 613
categories:
- maven
- wordpress
tag:
- exclude
- maven
- profiles
---

最近开发一个web模块，这个web模块是与其它模块一起共用一套用户登陆系统共享session。
此web模块需要添加一个拦截器，项目中使用的是Spring MVC拦截器，在xml文件中配置。
想要达到的目的是，在dev环境下面排除这个拦截器的配置文件，所以在构建项目时需要使用到maven的profiles。
所以在项目的超级pom.xml文件中配置如下：

    
    
    <profile>
        <id>dev</id>
        <activation>
            <activebydefault>true</activebydefault>
        </activation>
        <build>
            <resources>
                <resource>
                    <directory>src/main/resources</directory>
                    <filtering>true</filtering>
                    <excludes>
                        <exclude>**/applicationContext-interceptor.xml</exclude>
                    </excludes>
                </resource>
            </resources>
            <testresources>
                <testresource>
                    <directory>src/test/resources</directory>
                    <filtering>true</filtering>
                </testresource>
            </testresources>
        </build>
    </profile>
    


然后每次在构建dev的时候，拦截器的xml配置文件就不会在项目里面了。
