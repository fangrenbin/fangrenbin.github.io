---
author: fangrenbin
comments: true
date: 2010-08-09 09:38:05+00:00
layout: post
slug: file_buffer_html
title: 把文件或buffer彩色输出成html
wordpress_id: 147
categories:
- emacs
---

今天使用AHEI的DEA，终于把这个功能实现了一下。
;; 把文件或buffer彩色输出成html

    
    
    (require 'htmlize)


M-x htmlize-region-view 
然后就提示要输入的是文件还是BUFFER。
输出的效果和emacs里面是一样一样的！
