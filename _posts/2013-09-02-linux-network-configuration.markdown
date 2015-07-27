---
author: fangrenbin
comments: true
date: 2013-09-02 09:27:07+00:00
layout: post
slug: linux-network-configuration
title: ' linux系统网络设置'
wordpress_id: 534
categories:
- linux
tag:
- linux
- network
---

与网络配置相关的文件： 

    
    
    #1.IP配置信息文件
    /etc/sysconfig/network-scripts/ifcfg-eth0  
    #2.网关主机名配置文件
    /ect/init.d/network  
    #3.DNS配置文件
    /etc/resolv.conf   
    #添加格式：nameserver x.x.x.x(注：一般添加两条) 
    


注：我当时配置的服务器第一块网卡不工作，我设置的第二块网卡，设置时需要将eth0的网卡停掉(ONBOOT=no)，然后配置eth1的网卡信息(ONBOOT=yes)， 
我的配置如下（注：如果网关在IP配置信息文件里面也就是ifcfg-eth0里面配置过，network就不需要配置了）：
#我的ifcfg-eth1配置信息

    
    
    DEVICE=eth1  
    HWADDR=00:13:72:67:2F:33  
    ONBOOT=yes  
    HOTPLUG=no  
    IPADDR=122.1.27.90  //ip地址  
    NETMASK=255.255.255.0  
    GATEWAY=192.168.1.1  
    


参考文章： 
1.测试网卡的是否正常工作：http://redking.blog.51cto.com/27212/15574/ 
2.两块网卡死马当活马医：http://www.linuxidc.com/Linux/2010-10/29054.htm
