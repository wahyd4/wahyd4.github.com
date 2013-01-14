---
title: Ubuntu安装 GTK主题 Elementary 3
author: wahyd4
comments: true
layout: post
permalink: /2012/09/ubuntu-install-elementary3-gtk-theme/
categories:
  - linux
  - 我说
tags:
  - gnome
  - linux
---
不知道大家有没有这样的感受，Ubuntu桌面环境虽然已经很不错了，但是与Windows 和OS X 系统相比，我个人觉得还是有不小差距的。今天我要分享的就是在Ubuntu 12.04LTS下安装一款非常漂亮的GTK主题 Elementary 3。我觉得这是我用过的最漂亮的主题。

首先我们需要安装Gnome 3桌面环境，来替换掉Ubuntu 默认的Unity桌面环境。我们使用命令行来完成如下这些操作。

> sudo apt-get install gnome-shell

为了配置gnome3 更加方便和快捷，我们需要安装另外一个小工具gnome-tweak-tool

> sudo apt-get install gnome-tweak-tool

待系统安装好后，重启，在登录界面选择gnome 桌面环境，你就可以看见新的桌面了。现在我们使用还是默认的gnome主题。接下来安装GTK 主题 Elementary 3。

Elementary 3 使用了新的 Unico 引擎。因此我们当然也需要安装。

> sudo apt-get install gtk3-engines-unico

由于Elementary 主题文件，不在ubuntu默认的软件源仓库里面，因为我们需要首先添加软件源仓库，然后在安装：

> sudo add-apt-repository ppa:noobslab/themes
> 
> sudo apt-get update
> 
> sudo apt-get install elementary-theme   elementary-icon-theme

安装好后，打开gnome-tweak-tool(也可以在命令行直接输入改命令即可打开)，在Theme选项中的GTK+ Theme中就可以选择Elementary主题了。

Elementary 还有个黑色版本可以通过下面的方式安装：

> sudo apt-get install elementary-dark-theme

给大家秀秀这个主题：

<p style="text-align: center;">
  <a href="/images/2012/09/aaaaa.jpg"><img class="aligncenter  wp-image-2198" title="aaaaa" src="/images/2012/09/aaaaa-1024x575.jpg" alt="" width="717" height="403" /></a>
</p>

<p style="text-align: left;">
  由于我截图的时候，保存的时候是jpg，因为图片有失真，不过真的是相当惊艳。各位可以安装试试！
</p>

<p style="text-align: left;">
  我安装的时候，并不是严格按照这个路线，如果大家发现这种路线不能正常安装，请留言。
</p>

<p style="text-align: left;">
  资料：官方网站 提供基本Elementary优化的linux下载  ：<a href="http://elementaryos.org/">http://elementaryos.org/</a>
</p>

<p style="text-align: left;">
           gnome主题页面：   <a href="http://gnome-look.org/content/show.php/elementary+GTK+theme?content=149900">http://gnome-look.org/content/show.php/elementary+GTK+theme?content=149900</a>
</p>
