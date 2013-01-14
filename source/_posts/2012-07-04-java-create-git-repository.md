---
title: JAVA创建git仓库
author: wahyd4
comments: true
layout: post
permalink: /2012/07/java-create-git-repository/
categories:
  - java
tags:
  - git
  - java
  - jgit
  - 入门
---
[<img class="size-full wp-image-2051 aligncenter" title="logo" src="/images/2012/07/logo.png" alt="" width="110" height="46" />][1]

我们通常使用git都是使用的git的客户端，比如linux下的脚本。其实windows下也是间接使用linux脚本来进行操作。不过在现在有完全使用java语言实现的git：<a title="jgit" href="http://www.eclipse.org/jgit/" target="_blank">JGIT</a>。我们可以通过jgit来完成我们所有的git操作。

下面我将简单些一个例子来说明，使用java来创建一个git仓库，并且为仓库添加一个远端仓库地址。如果通过git脚本来执行，那么语句就是：

<pre class="brush: xml; title: ; notranslate" title="">git init

git remote add git://XXXXXX

</pre>

首先我们需要下载[org.eclipse.jgit.jar][2] 包，并将其加入eclipse 的classpath中（当然这里使用eclipse来完成操作）。示例代码为：

<pre class="brush: java; title: ; notranslate" title="">package com.toozhao.git;

import java.io.File;
import java.io.IOException;
import java.net.URISyntaxException;

import org.eclipse.jgit.api.Git;
import org.eclipse.jgit.api.InitCommand;
import org.eclipse.jgit.api.errors.GitAPIException;
import org.eclipse.jgit.lib.Repository;
import org.eclipse.jgit.lib.StoredConfig;
import org.eclipse.jgit.transport.RefSpec;
import org.eclipse.jgit.transport.RemoteConfig;
import org.eclipse.jgit.transport.URIish;

public class TestJGit {
 public static void main(String[] args) {
 Repository repo = null;

String path = "d:/testjgit"; // 设置git仓库的路径
 InitCommand init = new InitCommand();
 // 设置路径
 init.setBare(false).setDirectory(new File(path));
 // 执行git init ，创建仓库
 Git git;
 try {
 git = init.call(); // 创建仓库
 repo = git.getRepository();
 System.out.println("create repo success");
 } catch (GitAPIException e) {

e.printStackTrace();
 }
 // 执行 git remote add 命令
 // 实例化一个RemoteConfig 对象，用户配置远端仓库
 StoredConfig config = repo.getConfig();
 try {
 RemoteConfig remoteConfig = new RemoteConfig(config, "origin");
 // 设置你的远端地址
 URIish uri = new URIish("git://github.com/wahyd4/testjgit");
 // 设置哪个分支
 RefSpec refSpec = new RefSpec("+refs/head/*:refs/remotes/origin/*");
 // 更新配置
 remoteConfig.addFetchRefSpec(refSpec);
 remoteConfig.addPushRefSpec(refSpec);
 remoteConfig.addURI(uri);
 remoteConfig.addPushURI(uri);
 // 更新配置
 remoteConfig.update(config);
 // 保存到本地文件中
 config.save();
 System.out.println("git remote add success.");
 } catch (URISyntaxException e) {

e.printStackTrace();
 } catch (IOException e) {
 e.printStackTrace();
 }

}

}

</pre>

执行完本代码后，打开d:/testjgit/可以看到一个.git的隐藏文件夹（如果看不到，请设置去除隐藏文件夹）。表明它已经是一个git仓库了。如果你的eclipse安装有aptana 插件，将仓库导入eclipse,eclipse还可以自动识别出git仓库。而在Egit 1.x插件中版本中都不能识别出。

如果你打开.git/CONFIG文件。你还可以看到：

<pre class="brush: xml; title: ; notranslate" title="">[core]
 repositoryformatversion = 0
 filemode = false
 logallrefupdates = true
[remote "origin"]
 url = git://github.com/wahyd4/testjgit
 pushurl = git://github.com/wahyd4/testjgit
 fetch = +refs/head/*:refs/remotes/origin/*
 push = +refs/head/*:refs/remotes/origin/*

</pre>

这些既是我们对仓库进行的配置，全都由这个文件定义。使用aptana，你可以直接将仓库push 到你设置的远端地址。

 [1]: /images/2012/07/logo.png
 [2]: http://download.eclipse.org/jgit/maven/org/eclipse/jgit/org.eclipse.jgit/2.0.0.201206130900-r/org.eclipse.jgit-2.0.0.201206130900-r.jar
