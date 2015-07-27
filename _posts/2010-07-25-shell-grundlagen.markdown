---
author: fangrenbin
comments: true
date: 2010-07-25 03:48:45+00:00
layout: post
slug: shell-grundlagen
title: shell基础知识
wordpress_id: 65
categories:
- shell
---

昨天学习了SHELL的基础知识。

    
    
    #!/bin/bash
    #name=tom
    #echo $name
    #echo ${name}test
    #echo test$name</p>
    #~~~~~shell的输入~~~~~
    #echo "input your name and age:"
    #read name age
    #echo "name is :" $name
    #echo "age is :" $age
    
    #~~~~~shell数组~~~~~
    #name=(tom jim jane test)
    #echo "name[0] is:" ${name[0]}
    #echo "name[1] is:" ${name[1]}
    #echo "name[2] is:" ${name[2]}
    #echo "name[3] is:" ${name[3]}
    #数组通配符"*","@"
    
    #echo "name set is:" ${name[@]}
    #echo "name set is:" ${name[*]}
    
    #数组的修改操作unset与set
    #name[0]=myself
    #echo ${name[@]}
    #unset name[0]
    #echo ${name[@]}
    #unset name[@]
    #echo ${name[@]}
    #name[0]=myself
    #name[1]=tom
    #echo ${name[*]}
    
    #~~~~~SHELL环境变量~~~~~
    #echo "SHELL:" $SHELL
    #echo "TERM:" $TERM
    #echo "USER:" $USER
    # http://cmpp.linuxforum.netecho "USERNAME:" $USERNAME
    #echo "PWD:" $PWD
    #echo "HOME:" $HOME
    #echo "LOGNAME:" $LOGNAME
    
    #~~~~~SHELL控制语句~~~~~
    #if语句
    
    #1)字符串测试符
    #echo "please input name"
    #read name
    #if test -n $name
    #then
    #    echo "name is:" $name
    #else
    #    echo "name is null"
    #fi
    
    #2)数值测试运算符
    #3)逻辑运算符
    #4)文件运算符
    
    #~~~~~CASE语句~~~~~
    #多重判断语句
    #eg:
    #echo please input your name:
    #read name
    #case $name in
    #tom)
    #    echo your name is tome
    #    ;;
    #jim)
    #    echo your name is jim
    #    ;;
    #*)
    #    echo "sorry we don't know your name"
    #    ;;
    #esac
    
