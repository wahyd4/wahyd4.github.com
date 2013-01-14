---
title: Virtual Box 虚拟机
author: wahyd4
comments: true
excerpt: >
  今天要给大家介绍的是virtual box,如果你以前用过Vmware station
  的话，那好说virtual box和Vmware 是一样的软件，只是virtual box
  是免费的，vmware 是商业软件。
layout: post
permalink: /2010/11/virtual-box/
categories:
  - 头条推荐
  - 我们爱分享
---
今天要给大家介绍的是virtual box,如果你以前用过Vmware station 的话，那好说virtual box和Vmware 是一样的软件，只是virtual box 是免费的，vmware 是商业软件。如果你以前没用过的话，就这样说吧，virtual box 可以让你在你的电脑上（一般指在windows 上，当然在linux ，mac 也可以运行虚拟机）同时运行多个系统，比如同时使用windows和linux .而不用你真正在硬盘上装几个系统，就目前来讲，虚拟机一般是我们学习linux的好帮手。

[<img class="aligncenter size-full wp-image-979" title="11-28-1_conew1" src="/images/2010/11/11-28-1_conew1.jpg" alt="" width="140" height="180" />][1]

就我上面所说，目前目前出名的虚拟机就是virtual box 和Vmware station，今天我们将着重介绍virtual box,如果你只是想安装虚拟机学习linux 系统，而不是专业人员，哪么virtual box 已经强大到绝对够你使用了。

好，我们下面从下载安装开始说起。

首先登陆这个网站：<a href="http://www.virtualbox.org/" target="_blank">virtual box</a>下载virtual box 软件。下载好之后安装，（提示：如果你用的是windows系统的电脑请下载windows版本，绝大多数都应该选择这个版本。）这之间应该都不会有问题，因为安装过程非常简单和其他软件一样。

安装好之后你将看到如下界面：

[<img class="aligncenter size-full wp-image-980" title="11-28-2_conew1" src="/images/2010/11/11-28-2_conew1.jpg" alt="" width="599" height="450" />][2]你看到左边的是我已经安装好的虚拟机，如果你是刚安装好软件，你的这片区域会是空白的。右边的是关于你安装的缪戈虚拟机的相关配置情况。

安装好软件之后，我们需要新建虚拟机，这时我们要将你想要安装的系统镜像光碟放入光驱中读取，或者，用虚拟光驱加载你的镜像文件。我这里选择的是虚拟光驱加载镜像。

我这里新建一个名叫WWW的系统，是linux ubuntu 的版本，所以我要在系统里面选择 linux 然后是选择ubuntu，之后再到选择内存和硬盘，cpu分配等等，按照软件的提示就可以了不用改了。（建议新手都按照软件提示操作，不用改相关参数）

建好之后你将在上图左侧看到一个www图标。

[<img class="aligncenter size-full wp-image-981" title="11-28-3_conew1" src="/images/2010/11/11-28-3_conew1.jpg" alt="" width="259" height="279" />][3]然后点击开始进行进一步的相关配置，这时刚才装载的系统镜像就发挥作用了，

<p style="text-align: center;">
  <a href="/images/2010/11/11-28-4_conew1.jpg"><img class="aligncenter size-full wp-image-982" title="11-28-4_conew1" src="/images/2010/11/11-28-4_conew1.jpg" alt="" width="474" height="305" /></a>选择你加载的系统的盘，然后点击下一步即可进入系统安装了。
</p>

系统安装这一步我就不再详细说明了，和你在真实环境下载安装时一样的。（PS：这一点和Vmware不一样，Vmware有专门针对ubuntu的优化，如果你选择的是ubuntux系统，那么Vmware可以直接帮你安装好系统，你需要做的就仅仅是输入用户名和密码即可。但是这样也少了很多自定义的配置。对于这一点是仁者见仁智者见智吧。）

安装好之后你就可以享受你的虚拟机生涯啦。

下面再讲一些我个人的感悟吧。对于专业人员来说肯定Vmware更加强大，这一点从文件大小就可以看出来，vMware安装好以后有1G多，个人感觉Vmwar会添加很多服务到你的电脑，如果你的电脑禁止了这些服务，很可能你的虚拟机不能正常运行，比如不能正常联网。然后virtual box 则没有，没有强制加入开机自启动的服务，而且运行时的进程也只有两个。

对于虚拟机联网的问题，联网请输入NAT，这样你就可以在虚拟机里面使用网络了。

综合网上前辈说的，貌似的确virtual box 占用的内存不很多，可是cpu占用则要大一些，相比较于vmware

请大家有什么不懂的在文章后面留言吧，我会尽量帮你们解决的。

virtual box 下载地址：<a href="http://www.virtualbox.org/wiki/Downloads" target="_blank">点我官网下载</a>

 [1]: /images/2010/11/11-28-1_conew1.jpg
 [2]: /images/2010/11/11-28-2_conew1.jpg
 [3]: /images/2010/11/11-28-3_conew1.jpg
