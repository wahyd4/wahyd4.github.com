---
title: Node.js web框架express入门（1）
author: wahyd4
comments: true
layout: post
permalink: /2011/10/node-js-web-express/
categories:
  - node.js
tags:
  - express
  - Node.js
  - 入门
  - 教程
---
从我自己现在学校node.js说了解的情况，我觉得node.js至少比Java简单不少。使用node.js的诸多第三方框架更是让node.js简单了不少。其实express 框架几天前我就看了一些。也写了一些例子。虽然没有完全掌握，但是我想在这里和大家一起分享我学到的知识，也算是一种记录。

首先，当然我们也得安装express 的module

<pre class="brush: xml; title: ; notranslate" title="">npm install express</pre>

接下来我们就是可以开始写一个简单的程序了。

<pre class="brush: jscript; title: ; notranslate" title="">var express = require('express'); //导入module
 var app = express.createServer(); //创建并返回一个express的server对象
 app.get('/',function (req,res){ //为跟地址目录设置路由，并且监听get方法。
       res.send("Hello,World"); //向浏览器返回hello world
  });
 app.listen(4000); //设置服务器监听4000端口
</pre>

运行程序，然后再浏览器中输入localhost:4000试试，是不是出现了hello world了。当然这只是一个最简单的程序。下面我们可以再多做一些。

这里需要说明一下。默认的，系统将在您的请求处理中，在此例里面即在app.get();里面为你添加下面两句话

<pre class="brush: jscript; title: ; notranslate" title="">res.charset='utf-8';         //系统默认的res.send()和res.render（）都默认采用utf-8编码
	res.contentType('Text/html');      //系统提供默认为Text/Html的Content-Type
</pre>

接下来，我们将通过链接中的地址获取请求内容

在程序中加入一段代码如下

<pre class="brush: jscript; title: ; notranslate" title="">app.get('/hello/:name',function (req,res){
       //如果你在地址栏中输入如下/hello/Junv.那么你将在页面中看到name=======Junv
      //'/hello/:name'中的name相当于定义一个变量name，并且把我们输入的名字赋值给他。
       res.send('name======'+req.params.name);
});
</pre>

试试看看吧。成功了吧！

对不起，写着写着觉得很别扭。今天就写到这里吧。下次在继续吧。
