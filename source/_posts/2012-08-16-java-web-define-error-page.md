---
title: java web.xml定义配置错误页面及使用
author: wahyd4
comments: true
layout: post
permalink: /2012/08/java-web-define-error-page/
categories:
  - java
  - 未分类
tags:
  - java
  - web
  - web.xml
---
我们在开发java web 的程序时候，经常会需要给用户提示信息，或者页面。最常见的，比如用户输入了一个不存在的网址，默认情况下Tomcat会给用户返回一个默认的页面。如下所示：

[<img class="aligncenter size-full wp-image-2165" title="22" src="/images/2012/08/22.jpg" alt="" width="529" height="182" />][1]

这个页面千篇一律。我们完全可以给用户展示一个自定义的页面。

其实java web程序中web.xml 本身就支持自定义错误页面，我们只需要在web.xml添加如下信息：

<pre class="brush: xml; title: ; notranslate" title="">&lt;error-page&gt;
 &lt;error-code&gt;404&lt;/error-code&gt;
 &lt;location&gt;/errorpage/404.html&lt;/location&gt;
 &lt;/error-page&gt;
 &lt;error-page&gt;
 &lt;error-code&gt;401&lt;/error-code&gt;
 &lt;location&gt;/errorpage/401.html&lt;/location&gt;
 &lt;/error-page&gt;
 &lt;error-page&gt;
 &lt;error-code&gt;500&lt;/error-code&gt;
 &lt;location&gt;/errorpage/500.html&lt;/location&gt;
 &lt;/error-page&gt;

</pre>

当然“error-code”，可以自己选择在程序中出现得最多的错误码。我个人认为通常我们拦截：

401：未授权

404：没有找到页面

500：服务器内部错误

这三个即可。在“location”中配置你自己的html,当然页面样式，内容这些这些都可以自己定义。这个就看你自己啦。

如果我们不做其他操作，当系统出现这些错误情况时，服务器就会自动调用我们配置的网页。当然我们可以自行在恰当的时候使用它。

在servlet或者其他可能访问到HttpServletResponse对象的地方，使用：

<pre class="brush: java; title: ; notranslate" title="">response.sendError(404); //404为你需要的错误代码

//也可以向前台网页传输错误语句，不过前台网页需要相应支持。这里没有实现

response.sendError(404,"这里写想要输出到前台的提示信息");

</pre>

在java中还可以使用：

<pre class="brush: java; title: ; notranslate" title="">response.setStatus(404);  //设置状态码

</pre>

设置状态码来实现，不过这并不能调用配置的自定义页面。只是在前台显示错误，并无输出。

 [1]: /images/2012/08/22.jpg
