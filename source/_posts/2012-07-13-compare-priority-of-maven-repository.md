---
title: 深入比较几种maven仓库的优先级
author: wahyd4
comments: true
layout: post
permalink: /2012/07/compare-priority-of-maven-repository/
categories:
  - java
  - MAVEN
tags:
  - java
  - maven
  - 仓库
  - 深入
---
平时在使用maven下载依赖或者maven插件的时候，经常被本地仓库，settings里面profile中设置的仓库，mirror仓库，pom文件中的repository搞疯，因为很可能你就会因为这些你所设置的仓库不能正常编译项目。下面将和大家一起探讨和比较下这几种仓库的优先级别。

这里我们有三个仓库 ：

*   远程222.197.xxx仓库
*   localhost镜像，是我自己在本机搭建的一个仓库
*   nexus仓库，是nexus官方的仓库

首先考虑这样一种情况：maven本地仓库中拥有该包，而中央仓库、mirror仓库、profile仓库、pom中仓库均不含该包。我们可以看到maven直接首先从本地仓库中找到该包，编译成功。

[<img class="aligncenter size-large wp-image-2083" title="1" src="/images/2012/07/1-1024x267.png" alt="" width="1024" height="267" />][1]

由此可以看出，本地仓库拥有最高的优先级。

接下来，我们继续剩下的仓库的优先级，（下面所有情况，都默认本地不拥有我们需要的包）剩下的仓库都是远程仓库，这里我们设定mirror设置的镜像仓库是中央仓库的镜像。那么就可以把mirror当成中央仓库，因为其已经被mirror替换了。

这次的场景为：pom文件中定义的仓库（repository）（即远程：222.197.xxx）拥有该包，而mirror(localhost镜像)和profile（nexus仓库）中的仓库不拥有该包。进行测试：

[<img class="aligncenter size-large wp-image-2087" title="2" src="/images/2012/07/2-1024x267.png" alt="" width="1024" height="267" />][2]

从这个结果可以看出，maven首先调用了profile中的仓库，其次找到了pom文件中设置的仓库。而mirror没有出现。我们这里可以初步推测优先级别为：profile > pom > mirror，为了验证我们的判断，我们需要在进行一次测试来验证这个结果。

场景如下：mirror中拥有该包（222.197），而pom(localhost镜像)和profile（nexus仓库）中均不含有该包。进行测试：

[<img class="aligncenter size-large wp-image-2089" title="3" src="/images/2012/07/3-1024x319.png" alt="" width="1024" height="319" />][3]

实际情况的确验证了我们的猜想。那么我们得出这几种maven仓库的优先级别为：

> 本地仓库 >profile > pom中的repository > mirror

注意：我也验证过这样的情况，将mirror这样设置：

<pre class="brush: xml; title: ; notranslate" title="">&lt;mirror&gt;
&lt;id&gt;huacloud-central&lt;/id&gt;
&lt;mirrorOf&gt;*&lt;/mirrorOf&gt;
&lt;name&gt;name-of-this&lt;/name&gt;
&lt;url&gt;http://222.197.XXXXXX/nexus/content/groups/public/&lt;/url&gt;
 &lt;/mirror&gt;
</pre>

即是表示该仓库地址为所有仓库的镜像，那么这个时候，maven会忽略掉其他设置的各种类型仓库仓库，只在mirror里面找。所以建议不要这样设置，他将导致pom文件中、pforile里面的仓库设置都失效。

> 随便科普一下几种仓库的设置吧：

pom中的repository:

<pre class="brush: xml; title: ; notranslate" title="">&lt;repositories&gt;
&lt;repository&gt;
&lt;id&gt;dsdf&lt;/id&gt;
&lt;releases&gt;
&lt;enabled&gt;true&lt;/enabled&gt;
&lt;/releases&gt;
&lt;url&gt;http://222.197.XXXXXX/nexus/content/groups/public/&lt;/url&gt;
&lt;/repository&gt;
 &lt;/repositories&gt;
</pre>

profile中的仓库是在maven的设置文件（maven安装目录/conf/settings.xml）

<pre class="brush: xml; title: ; notranslate" title="">&lt;profile&gt;
 &lt;id&gt;nexus&lt;/id&gt;
 &lt;repositories&gt;
 &lt;repository&gt;
 &lt;id&gt;sonatype-forge&lt;/id&gt;
 &lt;url&gt;http://repository.sonatype.org/content/groups/forge/&lt;/url&gt;
 &lt;releases&gt;
 &lt;enabled&gt;true&lt;/enabled&gt;
 &lt;/releases&gt;
 &lt;snapshots&gt;
 &lt;enabled&gt;true&lt;/enabled&gt;
 &lt;/snapshots&gt;
 &lt;/repository&gt;
 &lt;/repositories&gt;
 &lt;pluginRepositories&gt;
 &lt;pluginRepository&gt;
 &lt;id&gt;sonatype-forge&lt;/id&gt;
 &lt;url&gt;http://repository.sonatype.org/content/groups/forge/&lt;/url&gt;
 &lt;releases&gt;
 &lt;enabled&gt;true&lt;/enabled&gt;
 &lt;/releases&gt;
 &lt;snapshots&gt;
 &lt;enabled&gt;true&lt;/enabled&gt;
 &lt;/snapshots&gt;
 &lt;/pluginRepository&gt;
 &lt;/pluginRepositories&gt;
 &lt;/profile&gt;
 &lt;/profiles&gt;

&lt;!-- 使用下面代码来激活profile--&gt;

&lt;activeProfiles&gt;
&lt;activeProfile&gt;nexus&lt;/activeProfile&gt;
 &lt;/activeProfiles&gt;
</pre>

mirror设置上文有，这里不再赘述。欢迎留言讨论。

 [1]: /images/2012/07/1.png
 [2]: /images/2012/07/2.png
 [3]: /images/2012/07/3.png
