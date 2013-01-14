---
title: 使用maven编译Sonatype Nexus源码
author: wahyd4
comments: true
layout: post
permalink: /2012/07/maven-compile-nexus/
categories:
  - java
tags:
  - github
  - maven
  - Nexus
---
[<img class="alignnone size-full wp-image-2044" title="dsf" src="/images/2012/07/dsf.png" alt="" width="298" height="56" />][1]

首先需要使用git客户端从github下载nexus的最新源码：<https://github.com/sonatype/nexus>

因为nexus本身就是一个非常复杂的maven项目，因为我们只能使用maven来编译。如果我直接编译，nexus就会报各种找不到包的错误。

原因是我们需要把nexus官方的一个仓库加入到maven的settings文件中。代码为：

<pre class="brush: xml; title: ; notranslate" title="">&lt;settings&gt;
  &lt;profiles&gt;
    &lt;profile&gt;
      &lt;id&gt;sonatype-forge&lt;/id&gt;
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
  &lt;activeProfiles&gt;
    &lt;activeProfile&gt;sonatype-forge&lt;/activeProfile&gt;
  &lt;/activeProfiles&gt;
&lt;/settings&gt;
</pre>

然后再次编译，就应该可以构建成功了。由于nexus的仓库在国外，个人感觉速度比maven中央仓库要慢一个等级。在编译过程中，maven会自动执行一些插件和完成相关的单元测试。大概等待1-2个小时左右（由电脑性能和网络决定），就可以编译完成了。

 [1]: /images/2012/07/dsf.png
