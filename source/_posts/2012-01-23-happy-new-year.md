---
title: 嘿，有人在吗？新年快乐
author: wahyd4
comments: true
layout: post
permalink: /2012/01/happy-new-year/
categories:
  - 我说
tags:
  - linux
  - ubuntu
---
人长大了，过年都觉得没什么意思了。今天大年初一就在家了。有点无聊。下午在弄Linux，本来装了centos minial 可是文字界面，网络连接搞不定。然后就转到ubuntu server 了，之所以这样做，是因为本来用linux也是为了做服务器用，而且服务器版开机不起其他进程的话，占用的内存很少。因为不需要桌面。

分享一个经验吧：如果你想在在host 主机商ping virtualbox 里面的linux 虚拟机的话，请把网络连接设成**桥接（Bridge Adapter）**模式.桥接模式，虚拟机将使用和host主机同一类的IP地址。

然后推荐使用putty 通过ssh对linux进行控制。这个在windows下面真的很好用。当然请记得在你的虚拟机上安装

<pre class="brush: xml; title: ; notranslate" title="">sudo apt-get install openssh-server

sudo apt-get install ssh

</pre>

在这里这大家新年快乐，龙年大吉，当然也祝自己今年又好的发展，马上实习了，希望找到好的工作。

 

 
