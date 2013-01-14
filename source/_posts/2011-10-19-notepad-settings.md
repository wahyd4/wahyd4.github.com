---
title: Notepad++ 设置、插件配置
author: wahyd4
comments: true
layout: post
permalink: /2011/10/notepad-settings/
categories:
  - 我们爱分享
tags:
  - notepad++
  - 下载
  - 插件
  - 自动补充
---
<p style="text-align: center;">
  <p>
    虽然平时也一直在使用Notepad++，但是并没有深入地了解它，没有去鼓捣它。今天中午看了一篇博文说另外一个文本编辑器多么多么强大。我下载使用了一下，发现里面比较好的功能就是函数花括号自动完成、可以更换主题、支持分屏、可以安装插件同时查看几个文件，不过有一点不好就是他是收费软件。于是我想，开源的notepad++是不是也有那些功能呢？在我搜索一番之后，于是就发现了notepad的惊天大秘密。
  </p>
  
  <p>
    <strong>主题设置</strong>
  </p>
  
  <p>
    依次点击面板上的settings——style configurator。系统默认提供十几种不同的风格，可供选择。用户还可以为不同的编程语言设置个性化的前、后景色，设置字体大小、种类。我个人使用的主题是Black Board.
  </p>
  
  <p>
    <strong>分屏实现</strong>
  </p>
  
  <p>
    据我发现目前notepad++没有快捷键可以开启分屏，而是用户右键点击某个打开的文档列表的Tab。选择Move to other view 或者 Copy to other view，即可以移动或者复制到分屏。此时屏幕编程两屏界面（好像notepad++目前只支持两屏）
  </p>
  
  <p>
    <strong>字体的放缩</strong>
  </p>
  
  <p>
    当光标在目前程序时，按住Ctrl键同时，滚动鼠标滚轮即可实现字体的大小改变。
  </p>
  
  <p>
    <strong>函数自动补充</strong>
  </p>
  
  <p>
    依次点击Settings—-preferences—Back up/Auto completion。勾选enable auto-completion on each input.下面有function completion 和word completion可供选择。
  </p>
  
  <p>
    同样也可以勾选Function parameter hint on input。这个是函数暗示吧。需要注意的是，我发现在javascript 和html  下提示相对较好，但是都不会补充完全，都是部分补充。笔者在Java下面测试，大致只能提示类一级，不能提示其二级方法。如果你想拥有很好的提示还是使用eclipse吧。
  </p>
  
  <p>
    <strong>插件安装：</strong>
  </p>
  
  <p>
    notepad++支持两种方式安装插件（plugin）：第一种，将插件的.dll文件复制到notepad++安装目录的plugin目录下。第二种方法是通过notepad++自带的插件plugin management 进行安装。点击即可实现自动安装插件。安装完成后重启即可工作。
  </p>
  
  <p>
    这里推荐一些比较好的插件列表：<a href="http://my.oschina.net/hcom/blog/4429">http://my.oschina.net/hcom/blog/4429</a>
  </p>
  
  <p>
    Notepad++官方下载：<a href="http://notepad-plus-plus.org/">http://notepad-plus-plus.org/</a>
  </p>
  
  <p>
    我也是今天才发现notepad的这些功能，希望可以和大家一起交流、讨论。
  </p>
