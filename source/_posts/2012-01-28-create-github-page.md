---
title: 创建自己的github page
author: wahyd4
comments: true
layout: post
permalink: /2012/01/create-github-page/
categories:
  - 我说
tags:
  - blog
  - github
---
昨天我自己创建github page的时候，怎么也创建不起，不过自己看都是按照官方文档来的啊。

到最后才发现，原来github默认给每个注册用户分配了一个github page，地址就是 你的用户名.github.com，不过默认当然是没有开通的。因此不可以创建其他名称的二级域名作为项目名哦，只能是：

<pre class="brush: xml; title: ; notranslate" title="">你的用户名.github.com</pre>

下面简单说一下步骤：

创建一个仓库名称为 ：你的用户名.github.com，

在本地仓库中添加一个index.html文件，并向其中加入一些内容。然后push到github 的master分支就行了。

如果成功的话，系统会在几分钟内给你发个消息说，成功了。

如果没有消息，也就意味着没有成功哦。

你的域名就是： http://用户名.github.com

比如我的：http://wahyd4.github.com/

目前只是简单的github page 。

我们还可以绑定自己的域名，顶级域名或者二级域名都可以的。

其实最诱人的是我们可以利用github page 做我们的博客空间。当然这些都是免费了哦。

jekyll可以用来生成静态博客。我们可以用disqus做我们的评论系统。这样什么都有了哦，当然这里已经有人帮我把这些东西结合好了，博客还用到了twitter bootstrap 哦，这个东西就叫jekyll-bootstrap 我们只需要把他的仓库clone到本地，然后就可以使用了。

具体的东西请看官方教程吧。简单使用是很简单的。

jekyll: https://github.com/mojombo/**jekyll**

jekyll-bootstrap:<http://jekyllbootstrap.com/>

 
