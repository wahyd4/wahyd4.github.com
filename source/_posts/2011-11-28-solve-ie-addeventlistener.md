---
title: 解决IE不兼容addEventListener
author: wahyd4
comments: true
layout: post
permalink: /2011/11/solve-ie-addeventlistener/
categories:
  - 编程之美
tags:
  - addEventListener
  - attachEvent()
  - IE兼容
  - js
---
OH，IE太多不爽了，js有一些不能兼容。addEventLister就是一个。还好现在IE9已经支持addEventListener了。

在IE里面使用的是attachEvent().,比如同样地绑定一个事件。在IE下面和其他非IE内核下面就是这样的：

<pre class="brush: jscript; title: ; notranslate" title="">attachEvent('click',myfunction);   //第一个参数为需要绑定的动作，第二个参数为绑定的事件，这是在IE下面

addEventListener('click',myfunction，false); //前两个参数与attachEvent一样，第三个参数为异步还是同步调用，false为异步。而我们通常选择false.</pre>

 

我们可以采用下面的方法实现兼容IE浏览器。如果某个对象节点支持addEventListener()方法。则使用该方法，如果不支持该方法，说嘛浏览器为IE，则调用attachEvent()方法。

<pre class="brush: jscript; title: ; notranslate" title="">if(tr.addEventListener){
       tr.addEventListener("click", handleCheckboxClick, false);
 }else{
      tr.attachEvent("click",handleCheckboxClick);
  }   //tr为对象节点。
</pre>

<pre>好了，试试吧，看看是不是已经可以了！</pre>
