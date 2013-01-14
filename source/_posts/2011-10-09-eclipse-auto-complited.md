---
title: Eclipse 自动补全、联想设置
author: wahyd4
comments: true
layout: post
permalink: /2011/10/eclipse-auto-complited/
categories:
  - 我说
tags:
  - Content Assist
  - eclipse
  - 联想
  - 自动补全
---
笔者在第一次使用eclispe 3.7即indigo这个版本的时候，便发现一个小小的不快：平时在不知道某个方法怎么写的时候会按下Alt +/去获取eclipse给出的提示。但是在3.7这个版本却不好用，得到的是eclipse自动帮你选择一个他认为最合适的方法或者变量等等，帮你补全，而不是原来的显示所有可供选择的，让你来选择。

纠结了很久，期间尝试过使用网上说的修改Content Assist。将之前默认的 .后面加上ABCD…abcd…所有52个字符。并且 把联想的时间从系统默认的200ms提高到50ms。但是经过修改之后，eclipse变得和visual studio 一样，你每输入一个字符，系统就会进行一次提示。不过我发现这种情况下eclipse占用的CPU、内存资源变多了，在我的笔记本有时候还会变得顿卡。这不是最好的办法。

> 前几天吧，我才发现这个问题的症结所在。原来是eclipse官方的快捷键方式改变了。其实以前Alt+/那个联想一直在，只是在3.7版本里面这个快捷键变成了自动补全（即系统自动选择一个最合适的进行补充）。我们需要做的就是依次打开Windows——preferences——General——Keys。找到**Content Assist**这一项，这一项系统默认的是Alt+Space。这里我们把它改成**Alt+/**

[<img class="aligncenter size-medium wp-image-1701" title="Eclipse_content_assist" src="http://junv-wordpress.stor.sinaapp.com/uploads/2011/10/Eclipse_content_assist-300x108.png" alt="" width="300" height="108" />][1]

 [1]: http://junv-wordpress.stor.sinaapp.com/uploads/2011/10/Eclipse_content_assist.png
