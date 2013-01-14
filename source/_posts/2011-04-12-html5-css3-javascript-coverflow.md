---
title: Html5+CSS 3实现Cover Flow 动画特效(支持chrome、safari浏览器)
author: wahyd4
layout: post
comments: true
permalink: /2011/04/html5-css3-javascript-coverflow/
categories:
  - 编程之美
tags:
  - cover flow
  - css3
  - html5
  - 动画
---
> **<span style="color: #ff6600;">更新：已经加入了javascript，现支持图片之间进行动态切换，大家enjoy吧！</span>**
> 
> 下面将要给大家演示的这个东西，算是这几天的一个小小的成果吧，不过目前仅仅是静态的实现，还没有对其加上javascript 等控制。但是这个动画相比传统动画有一个很大的优点就是，动画的内容组成是可以是DIV，因此里面包含的内容可以是canvas 或者图片，甚至可能视频，等等，目前我还没有测试。理论上可以放进DIV 的东西都可以放到动画里面去。

[<img class="size-full wp-image-2069 aligncenter" title="s_conew1" src="/images/2011/04/s_conew1.jpg" alt="" width="499" height="260" />][1]

这个动画其实最关键的部分就是使用了一个最新的CSS  3 属性 animation，目前仅有webkit核心的浏览器支持这个特效。

而在本动画中涉及的有：（动画的声明）

> <div id="_mcePaste">
>   -webkit-animation-name:junv;                    //动画名称
> </div>
> 
> <div id="_mcePaste">
>   -webkit-animation-duration:4s;                 //动画循环时间，单位为秒
> </div>
> 
> <div id="_mcePaste">
>   -webkit-animation-iteration-count:infinite;              //动画播放次数，infinite 表示 无线循环   也可以饿确定的数字
> </div>

<div>
  <span style="color: #ff0000;">注意：这里的” // ” 并不是CSS 的注释，这里这样写，只是为了方便。下面一样，不再重复说明。</span>
</div>

<div>
</div>

> <div>
>   <span style="color: #000000;">@-webkit-keyframes’junv’{</span>
> </div>
> 
> <div>
>   from{
> </div>
> 
> <div>
>   }
> </div>
> 
> <div>
>
> </div>
> 
> <div>
>   to{
> </div>
> 
> <div>
>   }
> </div>
> 
> <div>
>   <span style="color: #000000;">}</span>
> </div>

<div>
  上面的是动画的默认形式，
</div>

<div>
  <blockquote>
    <div>
      @-webkit-keyframes’junv’{
    </div>
    
    <div>
      from{           //设置动画起始状态的CSS
    </div>
    
    <div>
    </div>
    
    <div>
      top:15px;
    </div>
    
    <div>
      left:-160px;
    </div>
    
    <div>
      -webkit-transform:   rotate(7deg) scale(0.4,0.75) skew(12deg,8deg);
    </div>
    
    <div>
    </div>
    
    <div>
    </div>
    
    <div>
    </div>
    
    <div>
      }
    </div>
    
    <div>
      40%{
    </div>
    
    <div>
      //这是动画过程中 CSS ，  百分之多少，大家可以可以根据自己需要任意设置，数量也不限，设置得越多，对动画的人为控制也越多。
    </div>
    
    <div>
      top:62px;
    </div>
    
    <div>
      left:230px;
    </div>
    
    <div>
      -webkit-transform:  rotate(0deg) scale(1,1) skew(0deg,0deg);         //设置设置对象的形态， rotate 是旋转，跟的 单位度数，可为负数
    </div>
    
    <div>
      //scale 是放缩，分别对 x,y方向放缩倍数
    </div>
    
    <div>
      //skew 是旋转，即x轴方向旋转多少，y轴旋转多少 ，单位为度
    </div>
    
    <div>
      }
    </div>
    
    <div>
      70%{
    </div>
    
    <div>
      top:62px;
    </div>
    
    <div>
      left:230px;
    </div>
    
    <div>
      -webkit-transform:  rotate(0deg) scale(1,1) skew(0deg,0deg);
    </div>
    
    <div>
      }
    </div>
    
    <div>
      100%{
    </div>
    
    <div>
      top:12px;
    </div>
    
    <div>
      left:580px;
    </div>
    
    <div>
      -webkit-transform:  rotate(-7deg) scale(0.4,0.75) skew(-12deg,-8deg);
    </div>
    
    <div>
      }
    </div>
    
    <div>
      }
    </div>
  </blockquote>
  
  <div>
    这是具体在这个页面里面的代码。
  </div>
  
  <div>
  </div>
  
  <div>
    下面稍微解释一下，我之所以设置40%，和70%状态一样，为为了，让整个动画，可以在中间位置停留更长的时间。
  </div>
  
  <div>
    其他的东西先不多说了，我要回寝室睡觉了，大家有什么不懂的，或者想讨论的留言吧。！
  </div>
  
  <blockquote>
    <h2>
      示例（demo）：<a title="cover flow" href="http://toozhao.com/coverflow/" target="_blank">点我进入</a>
    </h2>
  </blockquote>
</div>

 [1]: /images/2011/04/s_conew1.jpg
