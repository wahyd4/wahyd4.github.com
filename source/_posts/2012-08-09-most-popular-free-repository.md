---
title: 分享多个公网上著名的maven组件仓库
author: wahyd4
comments: true
layout: post
permalink: /2012/08/most-popular-free-repository/
categories:
  - java
  - MAVEN
tags:
  - maven
  - Nexus
  - 仓库
---
我们都知道maven是项目构建的神器，不过用maven从国外下载东西的时候这速度可真就不怎么神器了。而且如果你在公司里面使用maven,而公司里面没有自己建一个maven代理仓库的话，大家一起使用maven下载组件的时候，就费力了。

因此一个公司是完全有必须要搭建一个maven代理仓库的。既可以节省宽带资源、也可以节省其他人编译相同代码说下载组件的时间，而且代理仓库服务器上的组件还可以随时复制、迁移到其他服务器，造福其他程序员。通常情况下，我们使用nexus搭建自己的maven仓库和做公网上那些用得很多的仓库的代理仓库，今天就在这里分享一些我搜集的公网上常用的代理仓库。这些已经能够保证我工作中的maven项目95%以上正常编译了。

> 中央仓库：http://repo1.maven.org/maven2/

这个就是全世界最核心的maven仓库，相信大家都知道，nexus默认就已经提供。

> apache snapshots: http://repository.apache.org/snapshots/

apache 的快照组件仓库

> apache webservices :http://ws.zones.apache.org/repository2/

apache 的web services仓库，通常用得不多。

> codehaus snapshots:  http://nexus.codehaus.org/snapshots/
> 
> and ：http://snapshots.repository.codehaus.org/

另外一个比较著名的开源组织codehaus的快照仓库，貌似其中一个已经有一年多没有更新了。

> jenkins :http://repo.jenkins-ci.org/public/

开源项目jenkins 的仓库

> ops4j:http://repository.ops4j.org/maven2/

开源项目ops4j的maven仓库

> nexus ：https://repository.sonatype.org/content/groups/forge/

这是nexus自己的仓库，本身就包含了很过仓库仓库的代理，不过速度貌似不够快。

> spring external:http://repository.springsource.com/maven/bundles/external/
> 
> spring osgi:http://s3.amazonaws.com/maven.springframework.org/osgi/
> 
> spring release bundle:http://repository.springsource.com/maven/bundles/release/
> 
> spring release libs:http://repo.springsource.org/libs-release/
> 
> spring snapshots libs:http://repo.springsource.org/libs-snapshot/

spring 这个开源组织提供的仓库的确很多，而在我平时的编译中也经常用到，有一点spring 做得特别牛，那就是它吧很多一般的jar包转成了或者重新制作成了bundle。(bundle是osgi技术中需要的jar包，bundle可以当成普通jar包使用，而普通jar包不能当成bundle使用，举个简单的例子，如果你想把jar包放到你的osgi 应用服务器virgo 或者 jboss as 7中使用，你就必须得用bundle才可以。)所以当你找不到某个包的bundle版本的时候，试试去spring的maven仓库，他的所有包都是bundle.

> wso2：http://maven.wso2.org/nexus/content/groups/wso2-public/
> 
> wso2-2:http://dist.wso2.org/maven2/

wso2是一个企业级web services中间件，提供了很多，比较强大的组件。如AS， IS,ESB等。大家有兴趣可以看看。

把这样仓库全部做成你的nexus的代理，就相当于你拥有它们所有仓库的能力了。是不是瞬间战斗力提升了很多。

如果你想尽快使用你添加的这些代理仓库，请在nexus中更新这些仓库的 index(索引)，你就可以马上使用这些仓库了。

 
