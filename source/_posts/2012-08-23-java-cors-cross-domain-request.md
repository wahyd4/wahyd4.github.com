---
title: Java CORS实现Ajax跨域请求
author: wahyd4
comments: true
layout: post
permalink: /2012/08/java-cors-cross-domain-request/
categories:
  - HTML5
  - java
  - javascript
tags:
  - ajax
  - http
  - java
  - 跨域
---
跨域问题在我们开发web应用的时候经常遇到，但一直没有很好的解决方案。目前可能大家认为相对比较好使的就是——JSONP技术。不过这样前台通常需要告诉后台需要返回的函数名称，而后台需要向前台前台返回的则是一个可以执行的代码段。这样在后台处理的时候就相对麻烦一些。

其实在新的W3C标准中，我们只需要在服务器后端添加一句话即可以比较好的解决跨域问题。如java servlet中：

<pre class="brush: java; title: ; notranslate" title="">response.setHeader("Access-Control-Allow-Origin","http://toozhao.com");

</pre>

这段代码的意思就是，允许来自toozhao.com的跨域HTTP请求，当然我们也可以使用通配符 “*”,这样任意的请求都可以访问这个地址了，而不会出现跨域的问题。

不过据其他文档中介绍，这样做是不安全的。因为这样服务器不能访问document.cookie 对象。不知道请求者的相关信息，而微软的介绍文档中说到：

> **安全警报**  为了保护用户数据，跨域请求是匿名的，这意味着服务器无法轻松找出正在请求数据的用户。 因此，只应请求和响应不属于敏感信息或个人身份识别信息的跨域数据。

因此为了安全，我们只应该向我们能保证其安全的站点提供Access-Control-Allow-Origin，即（CORS）。或者对可以公开的数据采用该种方式。

我个人认为在下面的情景中，比较适合采用这种跨域处理技术：

[<img class="aligncenter size-full wp-image-2179" title="aa" src="/images/2012/08/aa1.png" alt="" width="622" height="432" />][1]

此外，CORS还有一些其他属性可以设置：

<pre class="brush: xml; title: ; notranslate" title="">Access-Control-Allow-Origin: http://www.toozhao.com   //设置允许跨域的地址
Access-Control-Allow-Methods: POST, GET   //设置跨域允许的方法
Access-Control-Allow-Headers: NCZ      //设置跨域允许的头部信息
Access-Control-Max-Age: 1728000   //设置跨域允许的最大时间

</pre>

好了有了上面的这些参数，只要我们在java 中可以获取到HttpServletResponse 对象，即可以设置属性。被允许的前台就可以使用一般的ajax调用了。如jquery：

<pre class="brush: jscript; title: ; notranslate" title="">$.ajax({

url: 'http://toozhao.com/test/xxx',

method: 'GET'，

success: function(msg){

console.log(msg);

}

});

</pre>

参考文档：  
<http://huaidan.org/archives/2729.html>  
<http://msdn.microsoft.com/zh-cn/library/dd573303(v=vs.85).aspx>

注：已修正图片中B系统URL错误。

 [1]: /images/2012/08/aa1.png
