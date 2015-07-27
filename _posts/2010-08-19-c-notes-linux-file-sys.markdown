---
author: fangrenbin
comments: true
date: 2010-08-19 17:43:25+00:00
layout: post
slug: c-notes-linux-file-sys
title: Ｃ语言编程笔记：LINUX文件系统
wordpress_id: 207
categories:
- c-programming
---

## **LINUX文件系统**




## 标准文件操作




### 一、底层文件操作


Ｃ语言访问底层文件的操作函数包括 open() 、close() 、read() 、write() 、ioctl()等。


#### １、open()函数


头文件#include <unistd.h>

函数原型：int open(const char *pathname, int flags);


int open(const char *pathname, int flags, mode_t mode);


函数说明：open()函数以 flags|mode 方式打开以参数 pathname 指向字符串为路径的文件，如果成功则返回一个整形的文件描述符，read() 和 write()函数就可以对文件进行读写操作。文件舞蹈术符是唯一的，不会与其他当前正在运行的进程共享。如果两个进程同时打开同一个文件，则会得到两个不同的文件描述符。

返回值：若打开文件成功，则返回唯一的文件描述符；若文件打开失败，则返回值为-1，失败原因记录在全局erron中。


#### ２、close()函数


头文件#include <unistd.h>

函数原型：int close(int fd);

函数说明：close()的作用是关闭文件描述符 fd 指定的文件，将数据写回磁盘，并释放该文件所占内存资源。

返回值：若文件成功关闭返回0；否则返回-1。

错误代码：EBADF，表示参数 fd 不是有效的文件描述符，或者该文件已经关闭。

<!-- more -->


#### ３、read()函数


头文件：#include <unistd.h>

函数原型：size_t read(int fd, void *buf, size_t count);

函数说明：read()函数的作用是从文件描述符 fd 指向的文件读取 count 个字节的数据，存入 buf 指针指向的内存单元。

返回值：若读取成功，函数返回实际读取的字节数；若返回0，表示已到达文件尾或没有可读的数据；若返回值小于 count ，不代表发生错误，而可能是达到文件尾，从管道或终端读取数据，或者读取数据，或都读取操作被中断等原因。


#### ４、write()函数


头文件：#include <unistd.h>

函数原型：size_t write(int fd, const void*buf, size_t count);

函数说明：write()函数将buf所在内存中的 count　个字节的数据写入 fd 指向的文件中。

返回值：若写入成功，则返回写入的字节数（返回值为０表示没有写入数据）；若写入失败，则返回－１，失败原因记录在全局变量 errno。


#### ５、ioctl()函数


头文件：#include <unistd.h>

函数原型：int ioctl (int fd, int request);

函数说明：ioctl()函数提供了一个用于控制设备及其描述符和配置底层服务的接口。对文件描述符 fd 指定的对象执行参数 request 中给出的操作。

返回值：惹成功则返回０；若失败，则返回－１，并将错误记录在全局变量 errno中。
