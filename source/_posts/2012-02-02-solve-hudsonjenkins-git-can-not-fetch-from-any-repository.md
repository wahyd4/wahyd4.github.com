---
title: 解决 hudson/Jenkins git can not fetch from any repository错误
author: wahyd4
comments: true
layout: post
permalink: /2012/02/solve-hudsonjenkins-git-can-not-fetch-from-any-repository/
categories:
  - hudson
  - java
tags:
  - git
  - hudson
  - maven
  - 持续集成
  - 错误
---
hudson是一个很强大的持续集成服务器，支持maven、git等强大工具,通常情况下我们我们使用期来持续集成如git 仓库中的代码，编译后打包发送到maven包仓库如nexus中。

今天在执行Hudson编译git仓库中代码的时候发现如下错误：

<pre class="brush: xml; title: ; notranslate" title="">ERROR: Problem fetching from origin / origin - could be unavailable. Continuing anyway
ERROR: Could not fetch from any repository
FATAL: Could not fetch from any repository
hudson.plugins.git.GitException: Could not fetch from any repository
</pre>

在网上看到一些资料，这里有一篇Jenkins对git plugin 的描述比较详细：<https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin> 。

发现。出现这种问题的大多是windows 系统上的git。不能fetch数据，也就是将服务器上最新的代码下载下来与本地同步。大致原因就是因为git找不到读取git 仓库中代码所需要的密钥。

我们所需要做的是将系统中集成的path to git executable 路径换成msysgitcmdgit.cmd，而不是我们通常设置成的msysgitbingit.exe.

这样git就可以成功工作了。当然也就可以fetch repository 了。

现在应该就可以正常工作了吧。
