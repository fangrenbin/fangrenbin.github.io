---
author: fangrenbin
comments: true
date: 2013-08-18 09:06:48+00:00
layout: post
slug: jenkins%e5%ae%89%e8%a3%85%e6%ad%a5%e9%aa%a4
title: ' jenkins安装步骤'
wordpress_id: 521
categories:
- jenkins
tag:
- jenkins
- maven
---

安装环境:CentOS release 5.9 (Final) 

一、安装java 
下载jdk-6u30-linux-x64-rpm.bin 

    
    
    chmod +x jdk-6u30-linux-x64-rpm.bin
    ./jdk-6u30-linux-x64-rpm.bin
    


二、安装maven 

    
    
    tar -zxvf apache-maven-3.0.4
    sudo mkdir /opt/maven
    sudo mv ~/software/apache-maven-3.0.4 /opt/maven
    sudo vim /etc/profile
    //在末尾加
    MAVEN_HOME=/opt/maven/apache-maven-3.0.4
    export MAVEN_HOME
    export PATH=${PATH}:${MAVEN_HOME}/bin
    //保存 :wq!
    source /etc/profile
    


查看mvn版本信息 

    
    
    mvn -v
    


三、安装jenkins 

    
    
    sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
    sudo rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
    sudo yum install jenkins
    #更改权限
    sudo chown -R admin /var/log/jenkins
    sudo chgrp -R admin /var/log/jenkins
    
    sudo chown -R admin /var/lib/jenkins
    sudo chgrp -R admin /var/lib/jenkins
    
    sudo chown -R admin /var/cache/jenkins
    sudo chgrp -R admin /var/cache/jenkins
    


jenkins配置文件

    
    
    /etc/sysconfig/jenkins
    


随机系统

    
    
    sudo chkconfig jenkins on  
    


jenkins系统设置中的maven设置： 
[![](http://frb.name/wp-content/uploads/2013/09/6029f3e1-7500-39aa-96d3-148c7e3737cf-300x65.png)](http://frb.name/wp-content/uploads/2013/09/6029f3e1-7500-39aa-96d3-148c7e3737cf.png)

jenkins邮件通知设置，先需要设置系统管理员邮件地址：
系统管理->系统设置->
[![](http://frb.name/wp-content/uploads/2013/08/QQ图片20140703130800-300x160.jpg)](http://frb.name/wp-content/uploads/2013/08/QQ20140703130800.jpg)
然后再进行电子邮件服务器的设置，在系统设置页面最底下，有一个邮件通知。
[![](http://frb.name/wp-content/uploads/2013/08/QQ20140703131113-300x160.jpg)](http://frb.name/wp-content/uploads/2013/08/QQ20140703131113.jpg)
