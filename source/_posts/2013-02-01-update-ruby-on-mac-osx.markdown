---
layout: post
title: "更新Mac OSX 中Ruby到最新版本"
date: 2013-02-01 20:19
comments: true
categories: [ruby]
---

大概一个月前，我拿到了公司发的Macbook Pro，但是这一个月中，似乎它有时会出点问题。Anyway, 这些都不重要。重要的是搞不懂苹果的新出的10.8 Mountain Lion 居然内置的Ruby 版本还是1.87。但是要用最近版本的Rails 版本的话，还是需要ruby 1.9以上的。因此我们需要将其更新。此文只是针对小白，和自己的一个记录，其他人可以忽略。  
在Mac OSX 中，我们可以使用 Homebrew 和 rvm 来安装新的版本。homebrew 正如你官网介绍所说，是Mac 下的包安装管理工具。而rvm这是ruby的版本管理工具，这里当然最好选用 rvm.  
首先我们需要需要登录苹果开发者中心，安装 [Command Line Tools][1].  
然后，我们在terminal中输入以下命令安装rvm:  
		\curl -L https://get.rvm.io | bash -s stable --ruby  
如果中途没有出错的话，系统将会安装最新的rvm 和最新的 ruby，如果没有成功安装ruby，你也可以手动使用：  
		rvm install ruby   
来安装最新版本的ruby,系统并会自动切换到最新的ruby。
如果你在更新ruby的时候，也出现这样的错误，可以使用使用一下的命令行：  
		rvm get head  
		rvm requirements run  
安装说需要，依赖的包，然后在使用下面的命令行安装ruby:  
		rvm install 1.9.3 --with-opt-dir=`brew --prefix readline` --without-tcl --without-tk  
应该就成功了。So, enjoy.



[1]:https://developer.apple.com/downloads/index.action