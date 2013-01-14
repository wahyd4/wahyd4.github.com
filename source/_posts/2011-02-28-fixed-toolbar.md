---
title: 在页面底部添加固定信息栏，类似于本博客所示效果
author: wahyd4
comments: true
excerpt: |
  |
    下面就稍微详细给大家说一下如何实现吧，其实原理很简单。将底部这个小长条固定在页面的底部涉及到的核心CSS代码就是
    
    #footer{
    position:fixed;
    bottom:0;
    }
    position:fixed是将小条固定，bottom:0 是小条距离底部是0，就是一直贴在页面底部。
layout: post
permalink: /2011/02/fixed-toolbar/
categories:
  - 我说
  - 编程之美
---
> 以前我也不知道我的博客浏览器页面底部的这个灰色固定的信息条是怎么实现的，今天没事就在网上查了一下，结果发现原来这个东西真的很容易。我本以为会用到javascript或者jquery之类的东西，结果没有想到只要简单的CSS即可。

<p style="text-align: center;">
  <a href="/images/2011/02/550365_164344022_2_conew1.jpg"><img class="aligncenter size-full wp-image-1487" title="550365_164344022_2_conew1" src="/images/2011/02/550365_164344022_2_conew1.jpg" alt="" width="350" height="283" /></a>
</p>

下面就稍微详细给大家说一下如何实现吧，其实原理很简单。将底部这个小长条固定在页面的底部涉及到的核心CSS代码就是

> <div id="_mcePaste">
>   #footer{
> </div>
> 
> <div id="_mcePaste">
>   position:fixed;
> </div>
> 
> <div id="_mcePaste">
>   bottom:0;
> </div>
> 
> <div id="_mcePaste">
>   }
> </div>

<div>
  position:fixed是将小条固定，bottom:0 是小条距离底部是0，就是一直贴在页面底部。
</div>

<div>
  如果你想让这个小条有些透明，就可以加上：
</div>

<div>
  <blockquote>
    <div>
      filter:alpha(opacity=75);
    </div>
    
    <div>
      opacity:0.75;
    </div>
  </blockquote>
  
  <div>
    第一行的是支持IE7这样的浏览器，第二行是支持firefox,chrome这样的浏览器，具体的IE9以前的浏览器是否可以实现透明效果我没有试过，因为我用的是IE9。应该是可以的。
  </div>
  
  <div>
    然后稍微美化一下小条：
  </div>
  
  <div>
    <blockquote>
      <div>
        width:100%; //让小条铺满底部宽度，还必须加上 left:0;
      </div>
      
      <div>
        background:#65676a; //设置小条背景颜色为灰色
      </div>
      
      <div>
        left:0;              //让小条在底部铺满
      </div>
      
      <div>
        color:white; //设置字体为白色，好看些
      </div>
      
      <div>
        height:20px; //设置小条高度
      </div>
    </blockquote>
    
    <div>
      <span style="color: #ff0000;">注意：这里的“//”不是CSS里面的注释，我这样写只是为了方便罢了，请柬上面的所有代码都写到#footer 这个选择器里面。</span>
    </div>
    
    <div>
      好了，大概就写好了，大家请看我写的这个效果吧，很烂，只是实现了这个功能。<span style="color: #ff0000;">如果部分浏览器下不行，请大家说一下哦。</span>
    </div>
    
    <blockquote>
      <div>
        <span style="color: #000000;">示例：<a href="http://junv.info/2-28/" target="_blank">点我</a> 在网页右键选择查看源代码，即可查看网页完整源代码。我用的是HTML 5写的。</span>
      </div>
    </blockquote>
  </div>
</div>
