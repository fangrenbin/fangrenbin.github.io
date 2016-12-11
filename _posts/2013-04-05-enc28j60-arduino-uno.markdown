---
#author: fangrenbin
comments: true
date: 2013-04-05 06:37:38+00:00
layout: post
slug: enc28j60-arduino-uno
title: enc28j60学习笔记
wordpress_id: 434
categories:
- arduino
tag:
- arduino
- enc28j60
- mega2560
---

使arduiono与互联网连接，用ethernet shield显然更方便些，但使用enc28j60更便宜些，ethernet shield直接插在uno上面就可以使用，有官方支持，也不需要下载第三方库。enc28j60价格只是ethernet shield的四分之一，需要下载第三方库。两个板子的优缺点，衡量一下，我还是使用enc28j60。

本次实验使用的材料：
1、enc28j60
2、arduono uno
3、杜邦线（一头公一头母）
4、网线一根
5、下载enc28j60使用的第三方库：

[https://github.com/jcw/ethercard](https://github.com/jcw/ethercard)
连接方法：
[![ENC-table](http://frb.name/wp-content/uploads/2013/04/ENC-table_thumb.jpg)](http://frb.name/wp-content/uploads/2013/04/ENC-table.jpg)

连接的口在这张表上都有标注，直接连上可以了。
注：spi有一个口是自己指定的，是CS口，所以自己需要查看自己下载的库中CS指定的是哪个口，我下载的库中指定的是D8口，所以，所以我的就连8了，不连10了。
连接mega2560也是同样的。

[https://github.com/jcw/ethercard/blob/master/EtherCard.h](https://github.com/jcw/ethercard/blob/master/EtherCard.h)

这个文件里定义了PIN连接口。
将第三方库加入arduino:
1、将原来官方的库备份
2、解压下载的第三方库放入libraries文件夹里（注：文件夹的名称起成英文的）
这样就可以使用了，连接网上和USB线，开始烧录程序了。


测试：
未例程序中有个backSonn，可以直接烧录这个程序来测试你的板子是否连接好。
程序中myip(enc28j60的ip)和gwip(网关ip)，根据自己的情况来设定。
如果程序正确运行打开你的IP地址就可以看到下图：
[![enc28j60](http://frb.name/wp-content/uploads/2013/04/enc28j60_thumb.png)](http://frb.name/wp-content/uploads/2013/04/enc28j60.png)


连接实物图：


[![](http://frb.name/wp-content/uploads/2013/04/QQ图片20130405144451-224x300.jpg)](http://frb.name/wp-content/uploads/2013/04/QQ图片20130405144451.jpg)
