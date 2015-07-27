---
author: fangrenbin
comments: true
date: 2013-03-11 08:44:28+00:00
layout: post
slug: centos-svn-store
title: Centos搭建SVN代码仓库
wordpress_id: 423
categories:
- linux
- svn
tag:
- centos
- maven模块
- svn
---

参考文档：







http://wenku.baidu.com/view/01bb3f26a5e9856a56126080.html




http://wenku.baidu.com/view/7bc8dcc65fbfc77da269b122.html




http://wenku.baidu.com/view/29b7c5a5284ac850ad024270.html




http://wenku.baidu.com/view/5f5c758002d276a200292e75.html





我的环境：

LSB Version:    :core-4.0-ia32:core-4.0-noarch:graphics-4.0-ia32:graphics-4.0-noarch:printing-4.0-ia32:printing-4.0-noarch

Distributor ID: CentOS
Description:    CentOS release 5.6 (Final)
Release:        5.6
Codename:       Final





Centos搭建SVN仓库




1、安装SVN软件：




#yum install subversion




//yum install httpd 这个好像不需要安装




2、把SVN相关命令路径添加到环境变量




#echo "export PATH=$PATH:/usr/local/svn/bin/" >> /etc/profile




#source /etc/profile




3、建立仓库




（1）建立SNV根目录：#mkdir -p /opt/svn/




（2）建立一个测试仓库：#mkdir -p /opt/svn/svntest/




#svnadmin create /opt/svn/svntest/




4、修改配置文件




在cd /opt/svn/svntest/conf/目录下有三个文件：




svnserve.conf 是svn的配置文件




authz 是设置用户权限的配置文件（可自定义文件名，在svnserve.conf的authz-db = authz中指定）




passwd 是设置用户名和密码的配置文件（可自定义文件名，在svnserve.conf的password-db = passwd中指定）




#vi svnserve.conf




修改如下：




[general]




anon-access = none




auth-access = write




password-db = passwd




authz-db = authz




realm = /opt/svn/svntest




设置用户权限




vi authz




修改如下




[svntest:/]




#设置上面这样竟然不行，我的配置为[/]




#这里有疑问以后再说




frb.name = rw




#给svntest仓库添加一个名称为frb.name的用户，权限为可写。




添加用户




vi /opt/svn/svntest/conf/passwd




frb.name=123123 #加在最后 设置用户名为frb.name密码为123132




启动SVN服务,并指定SVN的根目录（可以换其它端口来启动：svnserve -d -r /opt/svn/ --listen-port 3391）：




svnserve -d -r /opt/svn/




2、检查服务是否已经正常起来




netstat -tunlp | grep svn




结果如下，则表示正常监听3690端口




tcp 000.0.0.0:36900.0.0.0:*                   LISTEN 8646/svnserve




使用Eclipse SVN




添加资源库地址：svn://ip:prot




share project 端口后面添加你仓库的地址。




解决一些小麻烦：




之前因为安装SVN的时候一个项目已经与SVN连过了，现在我要把这个项目重新传到另一个仓库，他有默认的配置，不能重新改仓库地址




解决：进入这个项目目录下面删除.svn的文件夹，就断开了与以前SVN了，也就是删除了以前的配置文件。




maven模块更新到SVN




1、先更新子模块到SVN




2、再更新父模块




更新子模块的时候注意把目录写好。




以mail项目为例，一个父模块，两个子模块。




父模块名称：mail-all




子模块1（View模块）名称：mail




子模块2（Control模块）名称：mail-manager




1、子模块1点Team-->Share Project-->SVN 地址写为：svn://198.100.100.18:3391/mail/dev/mail-all/mail，点Finish，在列表中把资源文件添加至SVN:ignore，然后提交。




2、子模块2点Team-->Share Project-->SVN 地址写为：svn://198.100.100.18:3391/mail/dev/mail-all/mail-manager，点Finish，在列表中把资源文件添加至SVN:ignore，然后提交。




3、父模块点Team-->Share Project-->SVN 地址写为：svn://198.100.100.18:3391/mail/dev/mail-all，点击Finish，把.setting文件添加至SVN:ignore，然后提交。这次提交主要是为了提




交MAVEN父模块的pom.xml文件。




如图这样







[![](http://frb.name/wp-content/uploads/2013/03/svn-218x300.jpg)](http://frb.name/wp-content/uploads/2013/03/svn.jpg)
