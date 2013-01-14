---
title: 给你的Rails 项目配Travis 持续集成工具
author: wahyd4
layout: post
comments: true
permalink: /2012/12/rails-github-travis-ci/
categories:
  - 'ruby &amp; rails'
tags:
  - rails
  - travis
---
可能很多人都在github的某些开源项目上看到过类似这样的图标吧！

[<img class="alignnone" src="https://secure.travis-ci.org/wahyd4/ocelots.png?branch=master" alt="" width="89" height="13" />][1]

它是Travis-CI,一个免费向开源项目提供持续集成服务的网站，它可以在你每次向仓库提交更新之后，编译你的代码，实时告诉你的项目现在的编译状态。

下面分享一下如何给一个开源的rails 项目配这样一个持续集成服务。首先你需要去 https://travis-ci.org 通过你的github帐号登录，导入你需要编译的项目。

其实这个时候，Travis-CI已经开始工作了。已经可以编译你代码了。

但是你的Rails里面有测试，并且需要使用像 连接数据库的操作，我们就需要Travis-CI在执行编译之前，进行创建数据库的操作。或者指定我们的编译环境。Travis-CI是通过.travis.yml识别的。

因此我们需要在Rails项目的跟目录创建一个.travis.yml 的文件。文件的内容格式大致如下

``` ruby  
rvm:  
  - 1.9.3  
env:  
  - DB=postgresql  
script:  
  - RAILS_ENV=test bundle exec rake ci --trace db:migrate  
before_script:  
  - psql -c 'create database ocelots_test' -U postgres  
```

大致解释一下，这里我们指定了我们使用的编译环境是 ruby 1.9.3,指定了我们使用的数据库，因为我希望travis 可以帮我创建测试数据库。  
script 标签里指定了我们运行测试的命令。  
而before_script 将在我们测试之前，运行，在这里即是帮我创建测试数据库。  
类似的Travis还有after_script，用于指定在测试之后所做的动作。  
更多的使用说明可以通过 <http://about.travis-ci.org/docs/user/build-configuration/> 了解。  
最后我们需要做的当然是把这个.travis.yml文件 push 到github 中，这样travis就可以帮助你编译了。

 [1]: https://secure.travis-ci.org/wahyd4/ocelots.png?branch=master
