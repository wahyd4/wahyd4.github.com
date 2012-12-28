---
title: maven 远程部署项目到jboss as 7（maven remote deploy to jboss as 7）
author: wahyd4
layout: post
permalink: /2012/02/maven-remote-deploy-to-jboss-as-7/
categories:
  - java
  - jboss
  - MAVEN
tags:
  - java
  - jboss
  - jboss as
  - maven
---
在Jboss as 7中，我们需要通过JMX进行远程部署项目，并进行权限验证。而jboss as 7默认是将jmx 远程关闭了的。

甚至我们尚且不能通过远程主机的真实IP进行访问。默认情况下我们只能通过localhost或者127.0.0.1 进行访问。

下面我们进行通过jboss-as-maven-plugin 远程部署项目到jboss as 7上面。这里只讨论standalone模式。

第一步，首先我们需要允许用户通过外网IP访问服务器。打开${JBOSS_HOME}/standalone/configuration/standalone.xml .

搜索文件中的127.0.0.1 我们大致可以搜索到下面几条信息：

<pre class="brush: xml; title: ; notranslate" title="">${jboss.bind.address:127.0.0.1}

&lt;interfaces&gt;

    &lt;interface name="management"&gt;

         &lt;inet-address value="${jboss.bind.address.management:127.0.0.1}"/&gt;

    &lt;/interface&gt;

    &lt;interface name="public"&gt;

        &lt;inet-address value="${jboss.bind.address:127.0.0.1}"/&gt;

    &lt;/interface&gt;

&lt;/interfaces&gt;

</pre>

通过上面这些信息，我们可以看到jboss已经把其web服务器以及web console(web控制台)以及 comman line（命令行）的地址都绑定到127.0.0.1上面了。也就是用户只能通过本地对服务器对其访问与管理。在网上看到有人解释说，这是因为jboss处于安全的考虑。这个姑且不管，我们现在需要实现通过真实IP访问。

因为将文件中的127.0.0.1全部替换为0.0.0.0,保存文件后，重启。

现在输入服务器的外网IP就已经能够访问了，不管是8080，9990,还是9999端口。

下面添加远程JMX的配置

同样是该文件。我们通过搜索定位到：

<pre class="brush: xml; title: ; notranslate" title="">&lt;subsystem xmlns="urn:jboss:domain:jmx:1.0"&gt;

</pre>

在其节点中，添加下面的信息：

<pre class="brush: xml; title: ; notranslate" title="">    &lt;!-- Delete the following line to disable remote access --&gt;
    &lt;jmx-connector registry-binding="jmx-connector-registry" server-binding="jmx-connector-server" /&gt;
</pre>

该信息即是让jboss as 7 支持远程访问的关键。如果想取消远程访问，则请删除该行后重启服务器即可。

下面是对项目中的pom.xml进行配置，添加jboss-as-maven-plugin

<pre class="brush: xml; title: ; notranslate" title="">&lt;plugin&gt;

    &lt;groupId&gt;org.jboss.as.plugins&lt;/groupId&gt;

    &lt;artifactId&gt;jboss-as-maven-plugin&lt;/artifactId&gt;

    &lt;version&gt;7.1.0.CR1b&lt;/version&gt;

   &lt;executions&gt;

       &lt;execution&gt;

           &lt;!--  下面部分是让执行 mvn install 时 自动执行jboss-as:deploy

           &lt;phase&gt;install&lt;/phase&gt;

          &lt;goals&gt;

             &lt;goal&gt;deploy&lt;/goal&gt;

          &lt;/goals&gt;

          &lt;!—这里是远程服务器的相关配置,如果为本地服务器我们完全可以删除configuration 节点及里面的配置信息，本地部署不需要realm 权限认证 –&gt;

          &lt;configuration&gt;

              &lt;hostname&gt;192.168.1.106&lt;/hostname&gt;

               &lt;port&gt;9999&lt;/port&gt;

               &lt;!--  用户名和密码为jboss as 中添加的用户名和密码，如果没有 请通过运行 /bin/adduser..bat 添加 --

               &lt;username&gt;admin&lt;/username&gt;

               &lt;password&gt;wahyd4&lt;/password&gt;

           &lt;/configuration&gt;

      &lt;/execution&gt;

    &lt;/executions&gt;

&lt;/plugin&gt;

</pre>

现在配置好了，执行mvn install时候 ，maven就会自动部署项目到jboss as 7中了。

这个东西，一直在网上都没有找到答案。。

格式 没有缩减，请谅解。。有问题，请留言一起讨论。