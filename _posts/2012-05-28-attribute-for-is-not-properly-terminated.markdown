---
author: fangrenbin
comments: true
date: 2012-05-28 03:34:04+00:00
layout: post
slug: attribute-for-is-not-properly-terminated
title: attribute for %>" is not properly terminated
wordpress_id: 341
categories:
- java-web小问题解决
---

报错信息：


2012-5-28 11:14:44 org.apache.catalina.core.ApplicationDispatcher invoke




严重: Servlet.service() for servlet jsp threw exception




org.apache.jasper.JasperException: /phoneNum/statisticsCloudNumberList.jsp(96,33) attribute for %>" is not properly terminated




at org.apache.jasper.compiler.DefaultErrorHandler.jspError(DefaultErrorHandler.java:40)




at org.apache.jasper.compiler.ErrorDispatcher.dispatch(ErrorDispatcher.java:407)




at org.apache.jasper.compiler.ErrorDispatcher.jspError(ErrorDispatcher.java:132)




at org.apache.jasper.compiler.Parser.parseAttributeValue(Parser.java:240)




at org.apache.jasper.compiler.Parser.parseAttribute(Parser.java:205)




at org.apache.jasper.compiler.Parser.parseAttributes(Parser.java:148)




at org.apache.jasper.compiler.Parser.parseCustomTag(Parser.java:1207)




..................................................................................


出错行：


    
    
    <s:url var="url_fir" value="<%=request.getContextPath() %>/phoneNum/statisticsCloudNumberList.do">


解决方法：

加上红色斜杆

    
    
    <s:url var="url_fir" value="/<%=request.getContextPath() %>/phoneNum/statisticsCloudNumberList.do">
