---
title: 'Spring OSGI入门(2) 处理Log4j &#8220;WARN No appenders could be found for logger&#8221;'
author: wahyd4
comments: true
layout: post
permalink: >
  /2012/01/spring-osgi-hello-world2-log4j-warn-no-appenders-could-be-found-for-logger/
categories:
  - java
  - OSGI
tags:
  - log4j
  - osgi
  - Spring
---
上一篇文章，我们讲到了Spring OSGI运行所需要的目标环境已经建好了，不过Log4j出现一个问题，提示我们：

> log4j:WARN No appenders could be found for logger (org.springframework.osgi.extender.internal.activator.ContextLoaderListener).  
> log4j:WARN Please initialize the log4j system properly.

原因就是我们没有配置Log4j，导致log4j不能正常使用。下面我们就来处理这个问题。

打开Eclipse 依次点击File–>Project–>在对话框中选中Fragment Project 点击Next.在对话框中按如下进行配置：

[<img class="aligncenter size-medium wp-image-1870" title="11" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/11-245x300.png" alt="" width="245" height="300" />][1]项目名称为：info.junv.osgi.log4j,在target platform中选中 an OSGI framework选中 equinox,点击Next:

在plug-in ID中选择**com.springsource.org.apache.log4j**，点击Finish,完成。

在项目src根目录下建立log4j.properties文件。项目结构层次如下：

[<img class="aligncenter size-full wp-image-1871" title="13" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/13.png" alt="" width="221" height="125" />][2]打开log4j.properties，粘贴入一下内容

<pre class="brush: xml; title: ; notranslate" title="">log4j.rootLogger = INFO,FirstAppender
log4j.appender.FirstAppender = org.apache.log4j.ConsoleAppender
log4j.appender.FirstAppender.Threshold = INFO
log4j.appender.FirstAppender.ImmediateFlush = true
log4j.appender.FirstAppender.Target = System.out
log4j.appender.FirstAppender.layout = org.apache.log4j.PatternLayout
log4j.appender.FirstAppender.layout.ConversionPattern = [%x]-%p-%d{yyyy-MM-dd HH:mm:ss}-%m[%c]%n
</pre>

添加点击点击当前项目或者，前面我们写的SpringDMTarget项目，右键选择Run As–>Run Configurations–>OSGI framework（去掉其余所有多于的项目，保证只剩下我们之前导入的包已经当前这个log4j项目。）  
同时需要注意的是，为了让程序顺利运行，需要优先启动…osgi.web.extender，这里我们需要将其的start level设置成4以上（因为默认启动等级为4，为了使其优先启动，所以优先级应大于4，笔者在自己电脑上将优先级设成5依然不行，因为建议如果不行，可以将优先级设得大一些，这里我设置为10，运行成功），

[<img class="aligncenter size-medium wp-image-1873" title="15" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/15-300x187.png" alt="" width="300" height="187" />][3]

点击RUN。即可以运行。

[<img class="aligncenter size-medium wp-image-1872" title="14" src="http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/14-300x93.png" alt="" width="300" height="93" />][4]如果…osgi.web.webextender的优先级不够，将会出现如下错误：

No Catalina Service found, bailing out[org.springframework.osgi.web.deployer.tomcat.TomcatWarDeployer

…….

出现这个错误你需要做的是，将osgi.web.webextender组件的启动优先级别再调高一些。即可。

 [1]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/11.png
 [2]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/13.png
 [3]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/15.png
 [4]: http://junv-wordpress.stor.sinaapp.com/uploads/2012/01/14.png
