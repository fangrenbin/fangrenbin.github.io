---
author: fangrenbin
comments: false
date: 2014-07-09 03:04:30+00:00
layout: post
slug: hessian-overload-exception
title: Hessian接口重载抛异常
wordpress_id: 636
categories:
- Java
---

项目有一个使用Hessian的模块，其中有一个接口有重载，结束抛异常。
异常如下：

    
    
    nested exception is com.caucho.hessian.io.HessianProtocolException: '' is an unknown code
    


项目使用的是spring配置文件与来创建hessian factory。
原因是没有在spring声明启用接口模块。现在只需要在bean里面加入overloadEnable的property就好了。
示例代码：

    
    
    <bean id="ServiceName" class="org.springframework.remoting.caucho.HessianProxyFactoryBean">
            <property name="serviceUrl" value="http://hostname/hessian/HelloWorldService"></property>
            <property name="serviceInterface" value="name.frb.service.HelloWorldService"></property>
            <property name="overloadEnabled" value="true"></property>
    </bean>
    


如果使用的不是spring配置文件，直接在方法里面创建工厂类可以直接在对象里面set就可以。
示例代码：

    
    
    HessianProxyFactory factory = new HessianProxyFactory();
    factory.setOverloadEnabled(true);
    
