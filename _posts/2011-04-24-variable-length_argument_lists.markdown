---
author: fangrenbin
comments: true
date: 2011-04-24 06:24:12+00:00
layout: post
slug: variable-length_argument_lists
title: 变长参数表(转)
wordpress_id: 289
categories:
- c-programming
---

     有些函数的形参表中有"..."，它代表变长参数表，即"..."可用若干个实参取代。适用于有“维数不定的数组”的函数。如果是二维数组
参数中要包括两维的长度，有两个整型量；如果是三维数组，参数中包括三维的长度，有三个整型量。随着维数不同，参数的个数也同，
这就必须使用变长参数表个数不定的问题。变长参数表的操作在C的库函数中有一套完整的实现数据类型和函数，包含在头文件stdarg.h中
变长参数表类型标识符va_list，函数有：va_start(),va_arg(),va_end()
 1. va_start(va_list ap,elemtype ***)，此函数的形参表中ap为变长参数表类型，***为引用该变长参数的函数形参表中变长参前
边的参变量；该函数的功能：将ap指向变长参数表。
 2.va_arg(ap,elemtype)此函数为一个有返回值的某一类型的函数，其返回类型为变长参数表中参数的类型，此函数的形参表中ap变
长参数表类型，elemtype为变长参数表中参数的类型；函数的功能：返回ap指向变长形参表中的实参量。(ap在函数内部充当指针的作用，含有ap++的功能，在循环中可以移动)。
3.va_end(ap)此函数与va_start(va_list ap,int num)配对使用，函数的功能：结束对变长参数表的读取，ap不再指向变长参数表，和//free()功能相似。

    
    
    #include <stdio.h>
    #include <stdarg.h>
    #include <process.h>
    typedef int ElemType;
    ElemType Max(int num,...)
    {
    va_list ap;
         int i;
         ElemType m,n;
         if(num<1)
               exit(0);
         va_start(ap,num);
         m=va_arg(ap,ElemType);
         for(i=1;i<num;++i)
               {
                     n=va_arg(ap,ElemType);
                     if(m<n)
                           m=n;
               }
         va_end(ap);
         return m;
    }
    main()
    {
         printf("1.输出7，9，5，8中的最大数：\n%4d\n",Max(4,7,9,5,8));
         printf("2.输出17，36，15，28，47，39中的最大数：\n%4d\n",Max(6,17,36,15,28,47,39));
    }
    



“C语言的从右到左入栈的特性使其可以实现如printf之类的变长参数函数”
这是个命题，而且是个真命题。晚上查阅了一些资料，先总结如下:
（1）变长参数列表和固定参数的区别:
      我们写的大部分函数都是固定参数函数（至少我没有写过变长参数函数）,编译之后，形参的地址是固定的，而且被调用函数也知道形参的地址，所以可以正确取值。比如int func(int a,int b)。
（2）printf() 变长参数如何取值的？
     printf函数原型中，第一个参数是不变的，一定是一个格式字符串，后面参数的个数和内容取决于第一个参数的内容，所以又称为变长参数。在printf的实现中，不难看出，被调用函数只有在取到第一个参数后，才能确定后面参数类型和个数，所以编译器务必要把第一参数房子一个固定的位置，这个位置就是%ebp+8。

