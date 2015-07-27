---
author: fangrenbin
comments: true
date: 2012-06-13 07:05:17+00:00
layout: post
slug: org-hibernate-hql-ast-querysyntaxexception-organization-is-not-mapped
title: 'org.hibernate.hql.ast.QuerySyntaxException: organization is not mapped'
wordpress_id: 364
categories:
- hibernate
---

org.hibernate.hql.ast.QuerySyntaxException: Organizations is not mapped
今天在完成项目的时候遇到这样的问题，由于昨天的把Organizaitons改成Organization，所以导致了这个小问题。
在网上找到了这个参考：http://blog.csdn.net/zxq1406spys/article/details/2881258
参考了这个文章之后，得知。Hibernate是按类查找的organization是数据库的表，原来对应的类是Organizations，现在只要在Hibernate的配置文件里面改成Organization就可以了。


