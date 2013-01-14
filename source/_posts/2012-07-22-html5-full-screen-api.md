---
title: HTML5 全屏(full screen)API
author: wahyd4
comments: true
layout: post
permalink: /2012/07/html5-full-screen-api/
categories:
  - HTML5
tags:
  - html5
  - javascript
---
full screen (全屏)API,现在已经成为了HTML5的一个官方API，不过目前只是被chrome、firefox、safari浏览器实现了，且他们目前都是用的自行实现的函数，而非W3C官方标准的函数。建议在调用之前都检测一下！

full screen API主要有两个方法：一是执行全屏，另外一个则是退出全屏。他们的调用方法为：

**执行全屏**

<pre class="brush: jscript; title: ; notranslate" title="">var element =  XXX      //这里你需要得到你的一个网页中的对象，可以是整个网页，或者其中一个节点

element.requestFullscreen();     //W3C的方法

element.mozRequestFullScreen();     //firefox实现的方法

element.webkitRequestFullScreen();     //chrome 和safari实现的方法

</pre>

**退出全屏**

<pre class="brush: jscript; title: ; notranslate" title="">element.exitFullScreen();     //W3C

element.mozCancelFullScreen();     //firefox

element.webkitCancelFullScreen();  //chrome和safari

</pre>

例如,我想全屏整个页面,那个就应该使用:

<pre class="brush: jscript; title: ; notranslate" title="">var documentEle = document.documentElement;

documentEle.webkitRequestFullScreen(); //chrome

</pre>

此外我们还可以监听，full screen 事件，在其状态改变时执行相关操作。

<pre class="brush: jscript; title: ; notranslate" title="">document.addEventListener("fullscreenchange", function () {}, false);  //w3c

document.addEventListener("mozfullscreenchange",function(){},false); //firefox

document.addEventListener("webkitfullscreenchange", function () {}, false);  //chrome 和safari

</pre>

如果我们想获取当前某个对象数否处于全屏状态，就可以使用下面这个属性：

<pre class="brush: jscript; title: ; notranslate" title="">document.fullScreen  //w3c

document.mozFullScreen //firefox

document.webkitIsFullScreen // chrome 和safari

</pre>

经过我的测试（chrome 22），应该是HTML 里面所有对象都是可以被全屏的,如：<iframe>,<img>,<p>,网页本身。不过我们是不能一开始网页就让其处于全屏状态。而需要一些行为来触发这个事件。

在css 里面也有一个对应的选择器来修饰full screen：

<pre class="brush: css; title: ; notranslate" title="">html:fullscreen{

font-size:30px;
color:white;
background:blue;

}

html:-moz-full-screen{
 font-size:30px;
 color:white;
 background:blue;
 }
 html:-webkit-full-screen{
 font-size:30px;
 color:white;
 background:blue;
 }

</pre>

目前IE9 也是不支持full screen 全屏 API的，不知道在IE 10里面支持不！微软在这方面做得真的不怎么样啊。

> [点我查看我做的demo吧！][1]包含全屏网页，和全屏图片，不过由于图片原因效果不好。但是功能有了。哈哈！

 [1]: http://toozhao.com/playground/fullscreen.html "full screen demo"
