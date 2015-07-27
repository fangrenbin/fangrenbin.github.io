---
author: fangrenbin
comments: true
date: 2013-08-25 09:18:55+00:00
layout: post
slug: apache-virtual-directory-settings
title: apache虚拟目录设置
wordpress_id: 525
categories:
- linux
---

1st.编辑apache配置文件

    
    
    sudo vim /etc/httpd/conf/httpd.conf
    #配置文件中已经存在/icons/这个虚拟路径了，仿照例子根据自己的路径来写一个就可以了 
    


2nd.设置文件夹权限 
    然后可以去根据自己设定的虚拟路径去访问你设定的文件夹下面的文件了。 如果出现：You don't have permission to access /photo/ on this server. 这个原因我在网上查找资料都说是SELinux导致Apache 403。 
好吧，根据这个设置一下你设置的物理路径的权限了。 执行： 

    
    
    sudo chcon -R -t httpd_user_content_t /data
    
