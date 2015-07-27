---
author: fangrenbin
comments: true
date: 2013-08-28 06:26:16+00:00
layout: post
slug: build-apk-no-such-file-or-directory
title: ' apk打包时aapt，提示No such file or directory'
wordpress_id: 531
categories:
- linux
---

系统fedora16 
使用ant构建apk的时候，运行到appt的时候一直提示No such file or directory，我的路径没有任何错误。最后我切到目录下面直接运行appt，提示少一些依赖。 
解决方法，查找包，然后install 

    
    
    yum whatprovides ld-linux.so.2  
    yum install -y glibc-2.12-1.107.el6.i686  
    


参考文章：http://michaelzqm.iteye.com/blog/1881576
