---
author: fangrenbin
comments: false
date: 2015-03-15 06:07:30+00:00
layout: post
slug: get-element-from-generated-html-code
title: jquery异步生成的html代码，获取元素
wordpress_id: 670
categories:
- jquery
- web
---

使用jquery ajax请求到数据以后，然后生成的Html代码中。使用$(selector)无法获取到元素。
查了资料发现是因为异步请求的原因。
原代码：
[![](http://frb.name/wp-content/uploads/2015/03/3DB60E8A-10B2-459D-A628-F4FCA0FD963A-300x208.jpg)](http://frb.name/wp-content/uploads/2015/03/3DB60E8A-10B2-459D-A628-F4FCA0FD963A.jpg)
这样无法获取到button元素。需要在异步请求下来数据时，就为button添加click事件。正确的方法如下：
[![](http://frb.name/wp-content/uploads/2015/03/A2496002-95B4-440E-9720-95A9E566B09C-300x204.jpg)](http://frb.name/wp-content/uploads/2015/03/A2496002-95B4-440E-9720-95A9E566B09C.jpg)
