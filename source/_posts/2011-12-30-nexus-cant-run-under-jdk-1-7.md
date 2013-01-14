---
title: Nexus 1.9 在JDK 1.7下不能安装运行
author: wahyd4
layout: post
comments: true
permalink: /2011/12/nexus-cant-run-under-jdk-1-7/
categories:
  - java
tags:
  - java
  - JDK
  - maven
  - Nexus
  - Tomcat
---
Nexus 是一个Maven仓库管理软件，或者叫做Maven包管理软件。一般用于企业内部当做自己的maven仓库，同时也可以对他做一些配置用来优化内部仓库和外部仓库中间的访问等等。如果需要详细了解Nexus和MAVEN相关信息，这里有一篇文章写得比较好 <a href="http://blog.csdn.net/cuker919/article/details/5922007" target="_blank">MAVEN仓库管理（穿越吧）</a>。

笔者昨天安装Nexus的时候，一直没有成功，不论是通过Nexus自带Jetty服务器，还是通过Tomcat 安装WAR程序都不行。经查看日志文件，发现如下错误：

> jvm 1 | 2011-12-29 22:59:40 WARN [er\_start\_runner] -  
> org.sonatype.security.configuration.source.FileSecurityConfigurationSource -  
> No configuration file in place, copying the default one and continuing with it.

后面我反编译异常里面的class文件。发现原来由于Nexus 没有按照要求生成nexus.xml配置文件，于是他就停止工作了。我尝试将class里面的xml文件拷到相关目录，并命名为nexus.xml，不行。后面检查tmp目录，发现有nexus.xxxxxxx.xml。更加使我确信了。是配置文件的错误。

哎。后面所做的工作，就不必多讲了，总之我弄到凌晨1点也没有解决。

今天来在同学电脑上安装测试，可行，在老师电脑电脑上安装测试也可行。他们的电脑都使用的是JDK 1.6，我把JAVA\_HOME改成1.6在Tomcat下测试也可行，但是使用Jetty还是不行。这个不难解释，Tomcat调用的是JAVA\_HOME的JDK而程序自带的Jetty调用的是JRE，而我的JRE是1.7。

<span style="color: #ff00ff;">现在真相大白了，是程序不支持Java JDK 1.7.</span>

 

需要值得提一下的是我在JDK 1.7下面测试过1.9 和1.9.2.4 两个版本都是不行的。

刚才也向他们官网提交了这个bug,第一次提交bug哦！

[<img class="aligncenter size-medium wp-image-1847" title="psb" src="http://junv-wordpress.stor.sinaapp.com/uploads/2011/12/psb-300x140.png" alt="" width="300" height="140" />][1]安装Nexus 成功之后，你应该是可以看到这样的画面：

[<img class="aligncenter size-medium wp-image-1848" title="sasd" src="http://junv-wordpress.stor.sinaapp.com/uploads/2011/12/sasd-300x131.png" alt="" width="300" height="131" />][2]期待下一篇文章将OSGI或者MAVEN！！！！加油

 [1]: http://junv-wordpress.stor.sinaapp.com/uploads/2011/12/psb.png
 [2]: http://junv-wordpress.stor.sinaapp.com/uploads/2011/12/sasd.png
