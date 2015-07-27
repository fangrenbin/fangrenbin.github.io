---
author: fangrenbin
comments: false
date: 2014-11-05 02:19:41+00:00
layout: post
slug: android%e4%b8%a4%e4%b8%aatextview%e5%ae%9e%e7%8e%b0%e8%b7%91%e9%a9%ac%e7%81%af%e6%95%88%e6%9e%9c
title: android两个TextView实现跑马灯效果
wordpress_id: 665
categories:
- android
---

imooc学习笔记：
[http://www.imooc.com/video/4308](http://www.imooc.com/video/4308)
在视频中主要讲述了，如何实现两个TextView的跑马灯效果，如果使用常规的做法，只能够使一个TextView起作用。
现在方法具体如下：
 1.为TextView增加四个属性

    
    
        android:ellipsize="marquee"
        android:focusable="true"
        android:focusableInTouchMode="true"
        android:singleLine="true"
    


2. 实现TextView类，实现三个构造函数并重载 isFocused方法。

    
    
    public class MarqueeText extends TextView {
        public MarqueeText(Context context) {
            super(context);
        }
    
        public MarqueeText(Context context, AttributeSet attrs) {
            super(context, attrs);
        }
    
        public MarqueeText(Context context, AttributeSet attrs, int defStyle) {
            super(context, attrs, defStyle);
        }
    
        @Override
        public boolean isFocused() {
            return true;
        }
    }
    


3. 在main.xml文件中使用自己实现的TextView类。

    
    
    <com.example.marqueetext android:focusableintouchmode="true" android:id="@+id/textView1" android:layout_width="wrap_content" android:singleline="true" android:layout_height="wrap_content" android:ellipsize="marquee" android:text="@string/hello_world" android:focusable="true"></com.example.marqueetext>
    


这样就实现了两个跑马灯的效果了。
这里主要是重写了isFocuse方法，这样默认两个TextView都被Focuse了，所以这两个TextView都可以跑马灯了。
