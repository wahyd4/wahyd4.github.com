---
title: javascript获取引用js文件所携带的参数
author: wahyd4
comments: true
layout: post
permalink: /2012/08/js-getparameters-from-scriptsfile/
categories:
  - javascript
tags:
  - javascript
  - 对比
  - 效率
  - 正则表达式
---
通常情况下我们在HTML中引用js没有在文件名后面附加任何参数，即：

<pre class="brush: jscript; title: ; notranslate" title="">&lt;script type="text/javascript" src="test.js"&gt;&lt;/script&gt;

</pre>

其实我们在其后面加上一些附加参数，我们现在使用的浏览器也是可以识别，同样找到我们需要的js的。（IE6没有测试，不清楚是否支持），即如下：

<pre class="brush: jscript; title: ; notranslate" title="">&lt;script type="text/javascript" src="test.js?div=mydiv&name=tome&age=3"&gt;&lt;/script&gt;

</pre>

我们现在需要做的就是如何取出这其中的参数。如：div=mydiv;name=tom;age=3。首先附上我自己写的一个js方法，就是使用了常用的函数，如indexOf,substring,split等方法：

<pre class="brush: jscript; title: ; notranslate" title="">//你需要获取值的js文件名
var fileName = "test.js";
//获取到所有&lt;script&gt;对象
 var scripts = document.getElementsByTagName("script");
 for(var i =0; i&lt; scripts.length;i++){
     var src = scripts[i].src;
     //取得你想要的js文件名
     if(src.indexOf(fileName)!==-1){
     //获取js文件名后面的所有参数
        src = src.substring(src.lastIndexOf(fileName+"?")+(fileName.length+1));
        var array = src.split("&");
        //将参数一个一个遍历出来
        for(var j=0;j&lt;array.length;j++){
            var finalObj = array[j].split("=");
        console.log("参数："+finalObj[0]+"值："+finalObj[1]);
     }
   }
 }

</pre>

我在网上又看到另外一个前辈主要使用了RegExp和match函数，以正则表达式的方式完成了同样的操作，代码如下：

<pre class="brush: jscript; title: ; notranslate" title="">var jsFileName = "testParam.js";
var rName = new RegExp(jsFileName+"(\\?(.*))?$")
var jss=document.getElementsByTagName('script');
for (var i = 0;i &lt; jss.length; i++){
    var j = jss[i];
    if (j.src&&j.src.match(rName)){
        var oo = j.src.match(rName)[2];
        if (oo&&(t = oo.match(/([^&=]+)=([^=&]+)/g))){
            for (var l = 0; l &lt; t.length; l++){
                r = t[l];
                var tt = r.match(/([^&=]+)=([^=&]+)/);
                if (tt)
                document.write('参数：' + tt[1] + '，参数值：' + tt[2] + '&lt;br /&gt;');
            }
        }
   }
}

</pre>

在测试确定这两个函数都真实可用的情况下，我突然冒出另外一个想法，想测试一下这两种方法到底效率怎么样，比较他们执行的时间的长短：

测试条件：

*   将两个方法的输出都换成一致console.log();
*   分别在代码执行前和执行后获取当前时间，相减获取这种方法的执行时间。
*   所有测试都在同一台笔记本电脑下，我将测试chrome  21,firefox 14,IE9。每个浏览器分别执行5次

我用的测试方法代码：

<pre class="brush: jscript; title: ; notranslate" title="">var original = new Date().getTime(); //在执行方法前

//在执行方法后

console.log(new Date().getTime()-original);

</pre>

测试5次的结果为：

[<img class="aligncenter size-full wp-image-2182" title="执行结果统计" src="/images/2012/08/saa.png" alt="" width="360" height="132" />][1]

结果有点出乎我的意料：在chrome和firefox中普通方式的时间都要好于使用正则表达式这种方式，而更神奇的是在IE中这两种时间都是0毫秒，只有在我快速刷新的时候才偶尔出现时间，一般只有1或者2ms。

确实很难理解为什么IE时间为0毫秒，只有希望高人可以解答一下了。

不过不管怎样，至少解决了获取参数这个问题。也不错！

**更新**：根据 [@老赵][2]的建议我将测试次数变到反复执行该方法1000次再比较结果，出现如下的数据：（注意较上图正则和普通的位置对调了一下）

[<img class="aligncenter size-full wp-image-2191" title="执行1000次的结果" src="/images/2012/08/1111111111.png" alt="" width="362" height="169" />][3]

欢迎大家讨论。

参考正则方式的代码地址：<http://www.cnblogs.com/nrq/archive/2006/08/30/490347.html>

 [1]: /images/2012/08/saa.png
 [2]: http://weibo.com/jeffz
 [3]: /images/2012/08/1111111111.png
