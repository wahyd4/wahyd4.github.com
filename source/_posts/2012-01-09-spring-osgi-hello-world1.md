---
title: Spring OSGI入门(1) Hello World
author: wahyd4
layout: post
comments: true
permalink: /2012/01/spring-osgi-hello-world1/
categories:
  - java
  - OSGI
tags:
  - eclipse
  - osgi
  - Spring
  - 下载
---
什么是OSGI，他是一个动态组件、服务模型，简单得说就是在运行程序的时候，你可以动态安装、卸载、开始、停止服务。达到动态配置管理的功能，大大增加程序的灵活性。在Eclipse中就用到了OSGI，eclipse自带了一个osgi容器Equinox用来运行和管理OSGI相关的功能。

Spring osgi是springsource基于spring framework开发的OSGI框架，继承了spring的特性，当然使用spring osgi的时候也需要导入spring framwork,现在spring osgi 已经变成了Eclipse 的[gemini blueprint][1]项目。由于本人也在学习之中，具体的细节我也不太清楚，希望与各位分享讨论。

这个实例文章，我们将运行一个简单的Spring osgi示例。首先我们需要建立一个项目用来提供Spring osgi运行相关的类库，我们采用maven来获取类库，maven的操作就不多讲了。这里只是涉及简单操作。

> 这个程序我所用到的所有资源：
> 
> Eclipse 3.7
> 
> Java SDK 1.6
> 
> Maven 3.0、m2e插件
> 
> Spring framework 3.0 、spring source tool 插件
> 
> Spring osgi 1.2.1

下面我们就开始一步一步的操作：

依次点击File–>New–>Project–>选中General下面的Project(建立常规项目)

[<img class="aligncenter size-medium wp-image-1855" title="2" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/2-300x285.png" alt="" width="300" height="285" />][2]弹出新建项目对话框里面，在项目名称里面填入SpringDMTarget,点击Finish结束。

在项目根目录下创建一个target目录，并创建一个pom.xml文件，创建成功后，项目目录如下：

[<img class="aligncenter size-full wp-image-1856" title="3" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/3.png" alt="" width="158" height="59" />][3]由于pom文件里面的依赖关系很多，这里就不一一列出了。下面贴出源文件：

[pom][4] （点击下载）

你需要做的就是改变其中一行，把它改成你的电脑的SpringDMTarget项目target的绝对路径：

> <taget-platform.root>D:javaSpring-DM-Targettarget</taget-platform.root>

然后选中pom.xml右键点击run as –>Maven install 即可开始运行maven，如果本地没有需要的包，maven会自动下载。等待一段时间后（时间长短由网速快慢而定）。只要看到控制台显示** BUILD SUCCESS** 则表明maven 已经成功下载并将包复制到目标目录了。选中项目，右键点击refresh即可看到target目录下已经下载好了相关的包。

[<img class="aligncenter size-medium wp-image-1859" title="4" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/4-300x142.jpg" alt="" width="300" height="142" />][5]接下来我们就需要配置运行环境了。依次点击Windows–>Preferences–>Plug in Development–>Target Platform 出现如下界面

[<img class="aligncenter size-medium wp-image-1860" title="5" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/5-261x300.png" alt="" width="261" height="300" />][6]点击Add按钮，新建一个目标运行环境。选择Nothing:Start with an empty tarfget defination.点击Next,在这个对话框中Name属性行填入对运行环境的命名：我们就填Spring DM,点击右边的Add按钮，弹出Add Content对话框,

[<img class="aligncenter size-medium wp-image-1861" title="6" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/6-300x247.png" alt="" width="300" height="247" />][7]选择Directory点击Next，在下页对话框点击Browse 从电脑中找到SpringDMTagret项目的target目录。完成后将看到，目录中的包已经全部导入了，点击Finish。选中我们新建的运行环境。

[<img class="aligncenter size-medium wp-image-1862" title="7" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/7-300x143.png" alt="" width="300" height="143" />][8]点击OK保存修改。

然后配置我们的项目运行选项，我们需要以Osgi Framework形式运行。选中项目，邮件点击Run As–>Run configurations,进入页面

[<img class="aligncenter size-medium wp-image-1863" title="8" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/8-300x187.png" alt="" width="300" height="187" />][9]选中 OSGI Framework,右键选择New ,我们可以看到系统已经默认将target platform中所有的包已经选中了。点击RUN，即可运行了。如果出现如下界面即说明运行成功了。

[<img class="aligncenter size-medium wp-image-1864" title="9" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/9-300x25.png" alt="" width="300" height="25" />][10]你可以在eclipse 命名行中输入ss查看所有服务运行状态。

[<img class="aligncenter size-medium wp-image-1865" title="10" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/10-300x151.png" alt="" width="300" height="151" />][11]大家也注意到了，上面的那两行红色的字，

> <pre>log4j:WARN No appenders could be found for logger (org.springframework.osgi.extender.internal.activator.ContextLoaderListener).
log4j:WARN Please initialize the log4j system properly.</pre>

他提示我们Log4j没有正确配置，下面我们将修复这个“Bug”，各位请看第二讲吧。

<a href="http://junv.sinaapp.com/?p=1869" target="_blank">Spring OSGI入门 Hello World(2) 处理Log4j “WARN No appenders could be found for logger”</a>

 [1]: http://www.eclipse.org/gemini/blueprint/
 [2]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/2.png
 [3]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/3.png
 [4]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/pom.txt
 [5]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/4.jpg
 [6]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/5.png
 [7]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/6.png
 [8]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/7.png
 [9]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/8.png
 [10]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/9.png
 [11]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/10.png
