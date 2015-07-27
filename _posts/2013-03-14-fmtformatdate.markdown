---
author: fangrenbin
comments: true
date: 2013-03-14 10:21:36+00:00
layout: post
slug: fmtformatdate
title: fmt:formatDate的输出格式
wordpress_id: 428
categories:
- jsp
---

转自：[http://271788203.iteye.com/blog/585828](http://271788203.iteye.com/blog/585828)

<fmt:formatDate value="${isoDate}" type="both"/>
2004-5-31 23:59:59

<fmt:formatDate value="${date}" type="date"/>
2004-4-1

<fmt:formatDate value="${isoDate}" type="time"/>
23:59:59

<fmt:formatDate value="${isoDate}" type="date" dateStyle="default"/>
2004-5-31

<fmt:formatDate value="${isoDate}" type="date" dateStyle="short"/>
04-5-31

<fmt:formatDate value="${isoDate}" type="date" dateStyle="medium"/>
2004-5-31

<fmt:formatDate value="${isoDate}" type="date" dateStyle="long"/>
2004年5月31日

<fmt:formatDate value="${isoDate}" type="date" dateStyle="full"/>
2004年5月31日 星期一

<fmt:formatDate value="${isoDate}" type="time" timeStyle="default"/>
23:59:59

<fmt:formatDate value="${isoDate}" type="time" timeStyle="short"/>
下午11:59

<fmt:formatDate value="${isoDate}" type="time" timeStyle="medium"/>
23:59:59

<fmt:formatDate value="${isoDate}" type="time" timeStyle="long"/>
下午11时59分59秒

<fmt:formatDate value="${isoDate}" type="time" timeStyle="full"/>
下午11时59分59秒 CDT

<fmt:formatDate value="${date}" type="both" pattern="EEEE, MMMM d, yyyy HH:mm:ss Z"/>
星期四, 四月 1, 2004 13:30:00 -0600

<fmt:formatDate value="${isoDate}" type="both" pattern="d MMM yy, h:m:s a zzzz/>
31 五月 04, 11:59:59 下午 中央夏令时

格式模式：
d   月中的某一天。一位数的日期没有前导零。
dd   月中的某一天。一位数的日期有一个前导零。
ddd   周中某天的缩写名称，在   AbbreviatedDayNames   中定义。
dddd   周中某天的完整名称，在   DayNames   中定义。
M   月份数字。一位数的月份没有前导零。
MM   月份数字。一位数的月份有一个前导零。
MMM   月份的缩写名称，在   AbbreviatedMonthNames   中定义。
MMMM   月份的完整名称，在   MonthNames   中定义。
y   不包含纪元的年份。如果不包含纪元的年份小于   10，则显示不具有前导零的年份。
yy   不包含纪元的年份。如果不包含纪元的年份小于   10，则显示具有前导零的年份。
yyyy   包括纪元的四位数的年份。
gg   时期或纪元。如果要设置格式的日期不具有关联的时期或纪元字符串，则忽略该模式。
h   12   小时制的小时。一位数的小时数没有前导零。
hh   12   小时制的小时。一位数的小时数有前导零。
H   24   小时制的小时。一位数的小时数没有前导零。
HH   24   小时制的小时。一位数的小时数有前导零。
m   分钟。一位数的分钟数没有前导零。
mm   分钟。一位数的分钟数有一个前导零。
s   秒。一位数的秒数没有前导零。
ss   秒。一位数的秒数有一个前导零。

<fmt:formatDate value="${xx}" pattern="dd/MM/yyyy HH:mm aa"/>和

<fmt:formatDate value="${xx}" pattern="dd/MM/yyyy hh:mm aa"/>  对于0点显示的结果不一样
	
* h：小时，从1到12，分上下午 范围：01：00 AM~12:59AM

	
* H：小时，从0到23                 范围：00：00 AM~23:59AM
