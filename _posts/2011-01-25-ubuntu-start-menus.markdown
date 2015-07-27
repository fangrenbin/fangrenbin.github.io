---
author: fangrenbin
comments: true
date: 2011-01-25 05:06:15+00:00
layout: post
slug: ubuntu-start-menus
title: ubuntu系统启动菜单变多
wordpress_id: 269
categories:
- ubuntu
tag:
- ubuntu
- 启动
- 菜单
---

原帖地址：[http://forum.ubuntu.org.cn/viewtopic.php?f=48&t=315186&p=2196457#p2196457](http://forum.ubuntu.org.cn/viewtopic.php?f=48&t=315186&p=2196457#p2196457)

ubuntu10.04我用了大概有半年多了吧，使用的时间长了，系统启动菜单选项变的越来越多，原来是内核一次一次更新，添加到菜单了，一般都选的最新内核进入系统，所以那么多菜单看着就那么没有必要了。

[![](http://frb.name/wp-content/uploads/2011/01/kernels-300x225.jpg)](http://frb.name/wp-content/uploads/2011/01/kernels.jpg)

有朋友推荐使用ubuntu tweak，很不幸我的系统不能用，好像因为Tweak好久没有更新了。下面又朋友说使用：

sudo aptitude purge ~ilinux-image-2.*(! `uname -r`)

下面关于这个命令的一些内容。关于aptitude命令linuxtoy有介绍：

[http://linuxtoy.org/archives/aptitude_quick_reference.html](http://linuxtoy.org/archives/aptitude_quick_reference.html)

aptitude purge pkgname 删除包及其配置文件。

用于删除内核镜像包吧。　具体我只能看懂这么多了。得再去问问。
