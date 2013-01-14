---
title: 快将你的windows 7升级到SP1吧
author: wahyd4
comments: true
excerpt: '     作为一个还是比较爱折腾的童鞋，笔者曾在windows 7 RTM版本刚在网上泄露的时候就下载了，系统进行安装，先尝试了一番。最近windows 7 sp1 的最终版本又在网上泄露了，笔者前天晚上已经等不及下载下来进行安装了，经过一天多的使用，确认没有任何和我的windows 7旗舰版 不兼容或者bug,现在和大家分享一下。'
layout: post
permalink: /2011/01/update-windows7-to-sp1/
categories:
  - 我们爱分享
tags:
  - sp1
  - windows
  - 下载
  - 升级
---
> 作为一个还是比较爱折腾的童鞋，笔者曾在windows 7 RTM版本刚在网上泄露的时候就下载了，系统进行安装，先尝试了一番。最近windows 7 sp1 的最终版本又在网上泄露了，笔者前天晚上已经等不及下载下来进行安装了，经过一天多的使用，确认没有任何和我的windows 7旗舰版 不兼容或者bug,现在和大家分享一下。

[<img class="aligncenter size-full wp-image-1342" title="1-20-1_conew1" src="/images/2011/01/1-20-1_conew1.jpg" alt="" width="500" height="311" />][1]

既然是微软的官方系统升级，当然在升级之前确认的是你的系统是完整的不是网上那些经过修改的系统而且还得是正版的系统（当然通过非正常方式激活为正版的系统也算正版。其他系统笔者没有尝试过可行性。）

<span style="color: #ff0000;">注</span>:如何查看你的电脑系统是否为正版：在桌面右键选中计算机点击属性选项，如果在页面下方看到windows 已激活和正版授权的图标即可。

然后则是下载升级文件，此次升级分32位（X86）和64位（X64）两种版本，请分别选中适合自己的版本下载升级文件。文件大小为500多M，保内已经包含所有版本的语言文件。

> **<span style="color: #ff0000;"><a href="http://u.115.com/file/f195a71b2f" target="_blank">32位 </a> <a href="http://u.115.com/file/f1a9f0b123" target="_blank"> 64位</a> 下载</span>**

下载好之后就是安装了，因为升级sp1还需要下载官方的一个更新程序（KB976902）才能升级，所以你升级的时候不能断开网络，你需要做的就是点击运行下载好的升级程序就好了，其他的事系统会自动完成，大概一个小时候升级就完成了。如果你看到以下图片说明你的升级已经完成了。

[<img class="aligncenter size-full wp-image-1340" title="1-18-1_conew1" src="/images/2011/01/1-18-1_conew1.jpg" alt="" width="500" height="397" />][2]现在我们再次右键选中计算机点击属性，将看到如下信息：

[<img class="aligncenter size-full wp-image-1341" title="1-20-2_conew1" src="/images/2011/01/1-20-2_conew1.jpg" alt="" width="594" height="192" />][3]没错，你的windows 7已经升级到sp1正式版本了。

下面是在百度贴吧看到微软的工程人员说的关于sp1具体更新内容：

> *   新的远程桌面服务：该功能需要借助Server 2008 R2相关改进（RemoteFX）；
> *   更好地支持第三方联合服务高效通信：通过这次更新，Windows 7将支持WS-Federation被动配置协议；
> *   改进HDMI音频设备性能：Windows 7 PC在系统重启后，经常会出现与HDMI音频设备间的连接消失的问题。Windows 7 SP1对此做出了改进，确保二者的连接不再中断；
> *   纠正打印混合方向XPS文档时的行为：部分用户反映，使用XPS Viewer打印同时包含横向、竖向的XPS文档时存在困难，导致整个页面变成了要么全部横向、要么全部竖向的单一模式。SP1已经解决了这一问题。
> *   热修复和其他漏洞修复：Windows 7 SP1还包括了此前发布的和新的修复补丁。

<span style="color: #ff0000;">提示：</span>安装sp1后：可在“命令提示符”中键入：”dism /online /cleanup-image /spsuperseded”(不含双引号)，即可删除安装SP1期间创建的备份文件。

 [1]: /images/2011/01/1-20-1_conew1.jpg
 [2]: /images/2011/01/1-18-1_conew1.jpg
 [3]: /images/2011/01/1-20-2_conew1.jpg
