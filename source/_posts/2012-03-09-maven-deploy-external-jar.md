---
title: Maven 直接部署第三方jar，bundle,war包到仓库
author: wahyd4
comments: true
layout: post
permalink: /2012/03/maven-deploy-external-jar/
categories:
  - MAVEN
---
上一个月，很忙碌。到后面还没退加班到9点，所以就很久很久没有打理自己的博客了。今天说一些如何使用maven部署一个只有编译后的jar的第三方包到我们的nexus仓库服务器。通常我们说的部署都是部署一个maven项目，有pom.xml，里面写有部署管理  ** <distributionManagement> **元素。我们直接使用maven deploy即可以部署成功。今天我们所有的只有一个编译好的jar文件，下面开始部署

我们将使用 mvn deploy:deploy-file 命令执行部署。在命令行中输入下面命令：

<pre class="brush: xml; title: ; notranslate" title="">mvn deploy:deploy-file

-Dfile=&lt;你的文件路径&gt;

-DgroupId=&lt;你想要命名这个jar的groupId&gt;

-DartifactId = &lt;你想要的artifactId,通常为jar的名字即可，如：mysql-jdbc-driver,建议不要有大写&gt;

-Dversion= &lt;版本&gt;

-Dpackaging =&lt;打包类型，一般有jar,war,ear,bundle，根据自己文件的类型决定&gt;

-Drep[ositoryId =&lt;这里是全局配置settings.xml里面用于验证的server Id，要与仓库路径对应&gt;

-Durl = &lt;仓库的url地址，会使用上面的server Id里面的用户名和密码进行验证&gt;

</pre>

回车即可执行了，需要注意的是，版本里面定义的snapshots 和release 要和后面部署的仓库地址对应哦，即是：snaposhot版本只能部署到snapshot仓库。这个很重要。

如果你确保所有信息都输入正确，仍然不能部署成功，请尝试 mvn -e deploy:deploy-file
