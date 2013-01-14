---
layout: post
title: "使用jetty-maven-plugin快速调试webapp"
date: 2013-01-05 17:24
comments: true
categories: ['maven','java']
tags: ['maven','java']
---
在我们使用maven这个工具来进行web应用开发的使用，我们在Eclipse或者Intellij中几乎没有一种好的方式来快速调试我们的webapp。通常我们可能采取的做法是利用maven将应用打包成war文件，然后再放到tomcat或者jetty、Jboss等应用服务器中运行。但是这个速度的确有点慢，或者我们也可以使用maven-tomcat-plugin来使用maven将war部署到tomcat中运行，但是这种方案需要我们配置tomcat和手动运行tomcat。  
现在我们其实可以使用jetty-maven-plugin来将一个内嵌的jetty和maven紧密结合。我们直接使用`mvn jetty:run`即可快速运行应用，而且还支持即改即用。  
我们只需要在我们的pom.xml文件中的plugins节点中加入下面的代码即可：  
```xml
<plugin>
  <groupId>org.mortbay.jetty</groupId>
  <artifactId>jetty-maven-plugin</artifactId>
	 <version>8.1.8.v20121106</version>
  <configuration>
    <scanIntervalSeconds>10</scanIntervalSeconds>
    <webApp>
      <contextPath>/test</contextPath>
    </webApp>
  </configuration>
</plugin>
```  
其中的参数contextPath，就是该应用的路径，你可以随便取一个即可。  
然后你运行`mvn jetty:run` 你就可以在[http://localhost:8080/test](http://localhost:8080/test) 看到你的项目了。  
需要注意的是该插件的6.x版本是不支持servlet3.0的，如果你的应用中有用到annotation来声明Servlet路径的话，就得选用7以后的版本。插件的版本大致和jetty server的版本是对应的。  
当然这个插件还有更多详细的参数配置，你可以在[插件网站][1]找到。

[1]: http://wiki.eclipse.org/Jetty/Feature/Jetty_Maven_Plugin  

			链接：  		
			Jetty Maven Plugin : http://wiki.eclipse.org/Jetty/Feature/Jetty_Maven_Plugin
