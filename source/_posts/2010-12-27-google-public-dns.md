---
title: 使用Google public DNS加速网站访问
author: wahyd4
comments: true
excerpt: >
  如果你也出现了一下问题：本来一些网站的域名存在，可是你缺被莫名其妙的引导到电信的114页面或者联通的什么页面。或者你访问一些网站时
  他告诉你 网站不能打开，或者显示的不是正常的网页。
layout: post
permalink: /2010/12/google-public-dns/
categories:
  - 我说
tags:
  - DNS
---
如果你也出现了一下问题：本来一些网站的域名存在，可是你缺被莫名其妙的引导到电信的114页面或者联通的什么页面。或者你访问一些网站时 他告诉你 网站不能打开，或者显示的不是正常的网页。

那么这些都可能是DNS 的问题。如果我们自己不做修改的话，你联网的时候是默认使用电信运营商的DNS解析。比如电信，或者联通他们自己的。这些dns 平时可能看不出来有什么问题，也许一到关键时刻就出篓子。

这两天我自己是真正遇到了这些问题。一个学院的网站域名我一直打不开。只有偶尔有时候才可以打开。让我一直觉得是网站服务器的问题，可是经过老师解答之后才发现时DNS解析的问题。

今天就给大家推荐使用google public DNS解析。比起其他的DNS解析来说google更加权威。给你带来更快的网站访问速度。还可以提高安全性。因为众所周知google在全球都有自己服务器。

<a href="http://code.google.com/intl/zh-CN/speed/public-dns/" target="_blank">google public dns</a>

那好下面就让我们在动手设置DNS。因为我的电脑是windows 7环境 所以就设置win 7吧。

首先**打开 网络和共享中心（就在右下角的网络菜单栏）**

**然后选择你现在说很使用的网络。 点击连接后面的。**

<p style="text-align: center;">
  <strong><a href="/images/2010/12/12-27-1.jpg"><img class="size-full wp-image-1131 aligncenter" title="12-27-1" src="/images/2010/12/12-27-1.jpg" alt="" width="595" height="90" /> </a></strong>点击进入之后，你将看到如下界面
</p>

<p style="text-align: center;">
  <a href="/images/2010/12/12-27-2.jpg"><img class="size-full wp-image-1132 aligncenter" title="12-27-2" src="/images/2010/12/12-27-2.jpg" alt="" width="365" height="409" /></a><strong>然后点击属性，进行设置 </strong>
</p>

<p style="text-align: center;">
  <strong><a href="/images/2010/12/12-27-3.jpg"><img class="size-full wp-image-1133 aligncenter" title="12-27-3" src="/images/2010/12/12-27-3.jpg" alt="" width="361" height="325" /></a>找到internet 协议版本4 tcp/IP.然后点击属性进入设置</strong>
</p>

<p style="text-align: center;">
  <strong><a href="/images/2010/12/12-27-4.jpg"><img class="size-full wp-image-1135 aligncenter" title="12-27-4" src="/images/2010/12/12-27-4.jpg" alt="" width="406" height="421" /></a>选择使用下面的DNS服务器地址。</strong>
</p>

<p style="text-align: center;">
  <strong>在DNS 服务器里面按照图片所示填入：  8.8.8.8</strong>
</p>

<p style="text-align: center;">
  <strong>备用里面填入：8.8.4.4</strong>
</p>

<p style="text-align: center;">
  <strong>然后点击确定，就可以啦。</strong>
</p>

<p style="text-align: center;">
  <strong>现在断开网络，重新连接，试试。</strong>
</p>

<p style="text-align: center;">
  <strong>是不是以前不能打开的域名地址，现在可以打开了。（当然这里所指的域名是因为DNS关系不能打开） </strong>
</p>

**[ ][1] **

 [1]: /images/2010/12/12-27-1.jpg
