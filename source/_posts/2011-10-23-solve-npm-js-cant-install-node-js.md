---
title: 解决npm.js不能成功安装Node.js包
author: wahyd4
comments: true
layout: post
permalink: /2011/10/solve-npm-js-cant-install-node-js/
categories:
  - node.js
tags:
  - Node.js
  - npm
  - 失败
  - 安装
  - 成功
  - 问题
---
[<img class="aligncenter size-full wp-image-2110" title="3" src="/images/2011/10/3.jpg" alt="" width="169" height="74" />][1]

学习Node.js当然安装其他开发者开发的各种各样的包一定是必须的，不知道在内地的童鞋发现一个问题没有，我们现在很难从npm.js直接去下载安装包了。笔者在电信和教育网连续试了几天都没有成功。

大概介绍一下npm.js吧。npm.js是node.js的一个包管理工具。通过你可以很方便的安装所有node.js的第三方包、类库，而不需要知道他们的地址、不需要再自己一次一次手动安装。

过程是这样的：（注：笔者只是在windows环境下测试过）

一般地我们会在cygwin里面使用” npm install 你需安装的包名”进行安装。但是我反反复复试过多次，均是很难成功，只有昨天夜里一点左右成功过一次。最初我认为我我们的网速太慢了，于是我在cygwin下面配置代理：

> export http_proxy=http://127.0.0.1:8087 注：我使用的是go agent进行代理（具体安装请google一下）。

通过代理我成功地安装成功了npm 本身，但是当我转而通过  npm install …进行安装的时候就出现错误了，npm提示 Socket hang up。具体原因不明，总之npm 不能使用cygwin里面配置的代理，于是我使用 export -n http_proxy 删除代理设置。

随后我在网上又收到了另外一个解决方法。在npm里面设置打理

> npm  –proxy http://127.0.0.1:8087

不过设置好之后使用 npm install …，发现同样不成成功，npm 根本没有通过代理去发请求。

最后，我找到一个神器npmf。它的大致介绍是说npmf 是npm的一个复制，他可以永久保存那些包的每个版本。并且你通过npmf安装的包在你下次部署软件的时候依然可用。老实说后面一句话，我没有理解明白，到底是本地缓存，还是在网上缓存。

> 各位可以前往npmf网站一看究竟：<http://npmfjs.org/>
> 
> 同时还有一个介绍npmf的网页：<http://nodeknockout.com/teams/preservation-society>

<span style="color: #008080;"><strong>接下来就是见证奇迹的时刻了：</strong></span>

我们可以直接把npm 默认的registry 换成 npmf的：

> npm config set registry http://npmfjs.org:9000
> 
> npm install <span style="color: #ff0000;">你需要安装的包</span>

是不是发现很神奇，一个包可能10秒甚至更少就可以安装成功。如果你想把registry改成npm默认的

> npm config set registry http://registry.npmjs.org

或者你可以临时使用npmf的registry的包，在你每次安装的包的时候都使用一下语句

> npm –registry http://npmfjs.org:9000 install <span style="color: #ff0000;">你需要安装的包</span>

告诉你们个秘密：通过上面的两种方法，可以使用代理哦。速度又提高了不少。哈哈。。。。。

总结：造成npmjs.org的速度很慢的原因我始终不太清楚。我想npmjs.org的网络应该比npmfjs.org好很多才对。怎么会反过来了。以前我在有人抱怨过说内地使用 npm安装包很难。但是我不知道这是个别现象还是大家都是这个样子。难道G\*F\*W故意把 registry.npmjs.org和谐了？哎，不管了，大家使用我这个方法来吧。欢迎各位留言

 [1]: /images/2011/10/3.jpg
