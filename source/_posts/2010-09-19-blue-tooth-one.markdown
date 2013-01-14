---
title: 蓝牙手机控制电脑——不是梦！(1)
author: wahyd4
comments: true
layout: post
permalink: /2010/09/blue-tooth-one/
categories:
  - 头条推荐
  - 我们爱分享
tags:
  - java
  - Salling Clickr
  - 手机
  - 控制电脑
  - 蓝牙
---
作者：Junv

开始之前你需要：智能手机一部（理论上支持Java的手机都行，作者是在Nokia 6120C 下试验成功），支持蓝牙的电脑一台（不支持蓝牙的可以外接蓝牙接收器！淘宝上很便宜。），Salling Clickr 软件（这个是核心）。

作者设备:Nokia 6120c ,Lenovo y450.

下面开始

下面开始实现蓝牙控制电脑，

首先下载<a title="Salling Clickr" href="http://www.salling.com/Clicker/windows/" target="_blank">Salling Clickr</a> 软件，并安装。该软件支持windows 和 Mac两种系统！（这一步没什么特别，相信大家都可以做到！）

安装完成之后运行电脑端Salling Clickr 软件将看到如下页面。

<p style="text-align: center;">
  <a href="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_20-59-02.png"><img class="size-full wp-image-133 aligncenter" title="搜狗截图_2010-09-19_20-59-02" src="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_20-59-02.png" alt="" width="487" height="473" /></a>
</p>

可以看到如界面显示的，用这个软件可以实现控制iTunes ，PowerPoint,windows Mediaplayer,还可以实现操作鼠标！从而达到实现操作电脑几乎所有软件的一半应用。

另外一个选项phone events，大家可以根据自己需要更改，这里不再多讲。

而在底部菜单setting里面，大家可以看到

<p style="text-align: center;">
  <a href="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_21-06-17.png"><img class="size-full wp-image-134 aligncenter" title="搜狗截图_2010-09-19_21-06-17" src="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_21-06-17.png" alt="" width="363" height="370" /></a>
</p>

勾选 automatically run Salling Clickr when logging on,即表示在随电脑启动的时候就自启动该软件。

Disconnect idle 里面则表示多少时间手机不操作则断开手机与电脑的链接。这个可以根据自己需要选择。

其他的设置就不在这里演示了。

现在开始比较关键的设置手机型号，软件会根据相应的型号，然后给你提供相应的软件，支持  Symbian s60,s40(java)，windows moblie ，理论上支持Java的软件都可以支持！这个情大家试试吧。

点主界面的set up device.

<p style="text-align: center;">
  <a href="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_21-18-30.png"><img class="size-full wp-image-135 aligncenter" title="搜狗截图_2010-09-19_21-18-30" src="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_21-18-30.png" alt="" width="433" height="396" /></a>
</p>

先选brand 商标，然后选择型号 model .里面包含了很多手机的型号，出了iphone。android 最新的型号，但是可能android 用Java版本可以使用！

选好之后

<p style="text-align: center;">
  <a href="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_21-21-14.png"><img class="size-full wp-image-136 aligncenter" title="搜狗截图_2010-09-19_21-21-14" src="http://www.junv.info/wp-content/uploads/2010/09/搜狗截图_2010-09-19_21-21-14.png" alt="" width="412" height="223" /></a>
</p>

点copy to desktop，软件就将你手机所需要的软件复制到桌面。再点 continue .然后就是安装手机端软件啦。

<p style="text-align: center;">
  在Nokia 6120c 下面安装好之后，出现如下图标。<a href="http://www.junv.info/wp-content/uploads/2010/09/SuperScreenshot0002.jpg"><img class="size-full wp-image-137 aligncenter" title="SuperScreenshot0002" src="http://www.junv.info/wp-content/uploads/2010/09/SuperScreenshot0002.jpg" alt="" width="240" height="320" /></a>
</p>

我这里有两个一个是sis格式的，另外一个是java 版

本的。

接下来你需要继续阅读：

## [蓝牙手机控制电脑——不是梦！(2)][1]

 [1]: http://www.junv.info/2010/09/19/%e8%93%9d%e7%89%99%e6%89%8b%e6%9c%ba%e6%8e%a7%e5%88%b6%e7%94%b5%e8%84%91%e2%80%94%e2%80%94%e4%b8%8d%e6%98%af%e6%a2%a6%ef%bc%812/
