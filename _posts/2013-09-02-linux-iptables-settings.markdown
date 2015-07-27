---
author: fangrenbin
comments: true
date: 2013-09-02 05:20:07+00:00
layout: post
slug: linux-iptables-settings
title: ' linux防火墙设置'
wordpress_id: 528
categories:
- linux
tag:
- iptables
- linux
---

安装一些服务，以后需要添加端口到防火墙配置文件中。

    
    
    sudo vim /etc/sysconfig/iptables 
    #复制系统自带的ssh的22端口，然后改成自己想穿过防火墙的端口
    



启动防火墙：

    
      
    sudo /sbin/service iptables start/stop/restart  
    
