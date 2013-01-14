---
title: 使用maven部署项目到tomcat 7
author: wahyd4
comments: true
layout: post
permalink: /2012/01/use-maven-deploy-totomcat-7/
categories:
  - java
  - maven
tags:
  - java
  - maven
  - Tomcat
  - tomcat7
  - 部署项目
---
[<img class="size-full wp-image-1982 aligncenter" title="tomcat" alt="" src="/images/2012/01/tomcat.gif" width="146" height="92" />][1]

上一篇文章，我们讲了maven的简单入门应用，其实最详尽的文档还是应该看官方的document。我想其他人在网上写都是一些细节上的解释和补充。或者干脆就是简单的大致的描述。

今天我想分享的是使用maven插件部署we项目到tomcat 7 中运行。之前如果我们没有使用maven,那么我想很多人都是使用的eclipse自带的run on server中选择tomcat，将web项目部署到tomcat中实现自动部署和运行。我想maven本身强大也在于，我们可以写很多插件（plugin）来扩展maven的功能，实现各种自动化的操作。下面进入正题。

对于使用maven插件部署项目到tomcat 6中，网上已经有很多说明。对tomcat 7由于推出不久，笔者今天弄的时候，也在网上找了很多资料感觉都说得不好，或者不能解决问题，于是今天我们来讲这个。（<span style="color: #ff0000;">下面Tomcat 均指Tomcat 7</span>）

tomcat maven plugin 插件已经从codehaus 转到Tomcat官网了，以前的codehaus只支持tomcat 6.这里我们需要使用最新的<a href="http://tomcat.apache.org/maven-plugin.html" target="_blank">tomcat maven plugin</a>. 该插件的pom为，即是在pom.xml加入：

<pre class="brush: xml; highlight: [12,13,14,15]; title: ; notranslate" title="">&lt;pluginManagement&gt;
      &lt;plugins&gt;
        &lt;plugin&gt;
          &lt;groupId&gt;org.apache.tomcat.maven&lt;/groupId&gt;
          &lt;artifactId&gt;tomcat6-maven-plugin&lt;/artifactId&gt;
          &lt;version&gt;2.0-SNAPSHOT&lt;/version&gt;
        &lt;/plugin&gt;
        &lt;plugin&gt;
          &lt;groupId&gt;org.apache.tomcat.maven&lt;/groupId&gt;
          &lt;artifactId&gt;tomcat7-maven-plugin&lt;/artifactId&gt;
          &lt;version&gt;2.0-SNAPSHOT&lt;/version&gt;
              &lt;configuration&gt;
                 &lt;url&gt;http://localhost:8080/manager/html&lt;/url&gt;
                 &lt;server&gt;tomcat&lt;/server&gt;
             &lt;/configuration&gt;
        &lt;/plugin&gt;
      &lt;/plugins&gt;
    &lt;/pluginManagement&gt;
</pre>

这样写的目的是既支持tomcat 6 也支持tomcat 7.虽说这个插件是2.0-snapshot版本，不太稳定，不过我试的时候没有遇到任何问题，可以放心使用。(红色部分我们将在下面解释)

下面我们需要在插件仓库（plugin repositories）和普通仓库（repositories）中添加以下仓库到pom.xml:

**repository:**

<pre class="brush: xml; title: ; notranslate" title="">&lt;repository&gt;
      &lt;id&gt;people.apache.snapshots&lt;/id&gt;
      &lt;url&gt;http://repository.apache.org/content/groups/snapshots-group/&lt;/url&gt;
      &lt;releases&gt;
        &lt;enabled&gt;false&lt;/enabled&gt;
      &lt;/releases&gt;
      &lt;snapshots&gt;
        &lt;enabled&gt;true&lt;/enabled&gt;
      &lt;/snapshots&gt;
    &lt;/repository&gt;
</pre>

**plugin repository:**

<pre class="brush: xml; title: ; notranslate" title="">&lt;pluginRepository&gt;
      &lt;id&gt;apache.snapshots&lt;/id&gt;
      &lt;name&gt;Apache Snapshots&lt;/name&gt;
      &lt;url&gt;http://repository.apache.org/content/groups/snapshots-group/&lt;/url&gt;
      &lt;releases&gt;
        &lt;enabled&gt;false&lt;/enabled&gt;
      &lt;/releases&gt;
      &lt;snapshots&gt;
        &lt;enabled&gt;true&lt;/enabled&gt;
      &lt;/snapshots&gt;
    &lt;/pluginRepository&gt;
</pre>

这样做的目的是为了保证maven能够下载到maven tomcat plugin。而且是从上述的仓库。

为了成功执行maven 部署 我们需要开启tomcat支持 admin-script，manager-gui的权限。

admin-script:是让tomcat支持以脚本的形式来管理

manager-gui:是让tomcat支持图形化的管理界面。

打开tomcat的安装目录的 conf/tomcat-users.xml

添加以下内容：

<pre class="brush: xml; title: ; notranslate" title="">&lt;role rolename="admin-script"/&gt;
&lt;role rolename="manager-gui"/&gt;
&lt;user username="admin" password="admin" roles="manager-gui,admin-script"/&gt;
</pre>

这里请自行改变用户名和密码。

接下来我们还需要配置一下maven，给他添加一个服务器和相关配置，在maven安装目录下的conf/settings.xml添加如下内容。

<pre class="brush: xml; title: ; notranslate" title="">&lt;!--Tomcat 7 server --&gt;
	 &lt;server&gt;
            &lt;id&gt;tomcat&lt;/id&gt;
            &lt;username&gt;admin&lt;/username&gt;
            &lt;password&gt;admin&lt;/password&gt;
     &lt;/server&gt;
</pre>

注意：这里的id需要和上面用醒目绿色标记的ID一致，用户名和密码需要和tomcat里面设置的用户名和密码相同。

这里在解释一下，上面红色部分的地址的是因为tomcat7中的部署地址变成了

<pre class="brush: plain; title: ; notranslate" title="">http://localhost:8080/manager/html</pre>

好了，配置我们就做好了，在部署之前，当然我们需要打开tomcat服务器。tomcat 7部署请使用命令:

<pre class="brush: xml; title: ; notranslate" title="">mvn tomcat7:deploy
</pre>

在eclipse只需要在goal中填入 **tomcat7：deploy** 即可。  
不出意外，应该就可以部署成功了。  
童鞋们，试试吧。有什么疑问以及文中的缺点，请指出。谢谢。

如果出现以下错误，请按照本文章验证，就可以搞定了。

> Failed to execute goal org.codehaus.mojo:tomcat-maven-plugin:1.0:deploy (default-cli) on project my-webapp: Cannot invoke Tomcat manager: Server returned HTTP response code: 403 for URL:

 [1]: /images/2012/01/tomcat.gif
