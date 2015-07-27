---
author: fangrenbin
comments: false
date: 2015-07-27 08:44:00+00:00
layout: post
slug: mac%e9%85%8d%e7%bd%aejavamaven%e7%8e%af%e5%a2%83
title: Mac配置JAVA/MAVEN环境
wordpress_id: 666
categories:
- wordpress
---

配置JAVA_HOME:

用户目录下opne .bash_profile    如果没有这个文件可以自己创建一个

可以了解下mac下的配置文件

    ./etc/profile 文件   全局共有配置，无论哪个用户登录，都会读取此文件
    /etc/bashrc    （一般在这个文件中添加系统级环境变量）全局（公有）配置，bash shell执行时，不管是何种方式，都会读取此文件。
    ~/.bash_profile  （一般在这个文件中添加用户级环境变量）

配置环境：

MAVEN_HOME=/Users/taoyutong/Documents/apache-maven-3.0.5
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_40.jdk/Contents/Home
PATH=$MAVEN_HOME/bin:$PATH
PAHT=$JAVA_HOME/bin:$PAHT

export MAVEN_HOME
export JAVA_HOME
export PATH

 

保存退出即可。

立即生效需要执行：$ source .bash_profile（这是文件名）
