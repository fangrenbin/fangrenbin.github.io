---
author: fangrenbin
comments: true
date: 2013-04-10 15:15:53+00:00
layout: post
slug: i2c-contected-1602lcd
title: I2C连接1602LCD
wordpress_id: 442
categories:
- arduino
tag:
- '1602'
- 1602lcd
- arduino
- i2c
---

1602LCD与arduino连接有4位接法和8位接法，具体接法[参考资料](http://www.geek-workshop.com/forum.php?mod=viewthread&tid=78)。要占用很多PIN口，而uno的Pin口非常的有限，如果Uno还需要连接其它模块的话，就没有Pin口可以连接了。

通过朋友知道可以使用I2C来帮忙节省PIN口，使用I2C模块，只需要用两个PIN口就可以驱动1602LCD。

I2C模块：

[![i2c](http://frb.name/wp-content/uploads/2013/04/i2c_thumb.jpg)](http://frb.name/wp-content/uploads/2013/04/i2c.jpg)

第一步：i2c与arduino连线方法：
<table cellpadding="2" cellspacing="0" border="1" width="400" >
<tbody >
<tr >

<td width="200" valign="top" >i2c
</td>

<td width="200" valign="top" >arduino
</td>
</tr>
<tr >

<td width="200" valign="top" >SCL
</td>

<td width="200" valign="top" >A5
</td>
</tr>
<tr >

<td width="200" valign="top" >SDA
</td>

<td width="200" valign="top" >A4
</td>
</tr>
<tr >

<td width="200" valign="top" >GND
</td>

<td width="200" valign="top" >GND
</td>
</tr>
<tr >

<td width="200" valign="top" >VCC
</td>

<td width="200" valign="top" >5V
</td>
</tr>
</tbody>
</table>
第二步：导入库文件

由于这个不是官方库文件，所以需要下载。

下载地址：[http://arduino-info.wikispaces.com/file/detail/LiquidCrystal_I2C1602V1.zip/341635514](http://arduino-info.wikispaces.com/file/detail/LiquidCrystal_I2C1602V1.zip/341635514)

下载好库文件以后，将它放入arduiono安装文件的“libraries”目录下面。

第三步：上传程序。

这个库文件中带有例子。

注：示例程序中LiquidCrystal_I2C lcd(0x27,16,2); 0x27是i2c地址，根据自己的板子来改，有的是0x20，也有些是0x27。我买的是0x20，如果没有弄对的话，就显示不出来文字。

最后来个Hello world！


[![i2c_hello_world](http://frb.name/wp-content/uploads/2013/04/i2c_hello_world_thumb.jpg)](http://frb.name/wp-content/uploads/2013/04/i2c_hello_world.jpg)
