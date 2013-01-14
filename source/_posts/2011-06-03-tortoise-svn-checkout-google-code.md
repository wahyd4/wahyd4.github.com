---
title: 解决tortoise svn不能checkout Google code
author: wahyd4
comments: true
excerpt: >
  不知道各位同学使用svn吗？简单说SVN是一个代码版本管理软件，可以让不同的人更新和同步代码，并对代码进行版本管理。现在google
  code 里面这么多开源项目，都是可以去用SVN checkout
  下载下来源代码的，不知道各位有没有尝试呢？
layout: post
permalink: /2011/06/tortoise-svn-checkout-google-code/
categories:
  - 我说
tags:
  - CODE
  - google
  - SVN
---
不知道各位同学使用svn吗？简单说SVN是一个代码版本管理软件，可以让不同的人更新和同步代码，并对代码进行版本管理。现在google code 里面这么多开源项目，都是可以去用SVN checkout 下载下来源代码的，不知道各位有没有尝试呢？

最近在做一个小小的项目的时候用到了SVN，但是当时也发现一个问题，就是tortoise SVN 不能checkout google code 里面的代码。当时用谷歌找了找，可是没发现解决的办法，今天又看到我比较喜欢的google制作的一本电子书——[20thingsilearned][1]，里面包含了很多HTML 5和CSS 3特性，而且他还说一个开源项目，说明我们免费的去下载源代码来研究它里面很酷炫的东西。当然也面对了同样的问题，不能checkout.

<div>
  <blockquote>
    <div>
      <tt># Non-members may check out a read-only working copy anonymously over HTTP.</tt><br /> <tt id="checkoutcmd">svn checkout <strong><em>http</em></strong>://20thingsilearned.googlecode.com/svn/trunk/ 20thingsilearned-read-only</tt>
    </div>
  </blockquote>
</div>

这是谷歌官方的代码，大概的意思是所有的匿名用户都可以使用下面这个地址进行匿名checkout ,即是不用登陆。不过我试着新建一个文件件，右键，选中tortoise SVN的checkout 选项，还是不行，最终在[国外一个网站][2]找到了解决的办法，即是正确的地址是***http***://20thingsilearned.googlecode.com/svn/trunk/ 去掉后面的那些东西，因为那些东西是为CLI 用户使用的（什么是CLI用户我也不太清楚）.总之你使用去掉后面那一块的地址就可以checkout啦。

[<img class="aligncenter size-full wp-image-1633" title="xxx" src="/images/2011/06/xxx.jpg" alt="" width="665" height="304" />][3]

还有如果你是项目发布者checkout不能弹出提示框要求你输入密码的话，请先这样做，请先选中tortoiseSVN里面的import选项，在里面弹出你的SVN地址，比如我的项目的地址是https://moland.googlecode.com/svn/trunk/ moland –username wahyd4。这个回跟上你的项目名称和用户名的。然后就会提示你输入用户名和SVN密码，这个密码是项目里面生成的SNV密码而不是google账户密码哦。然后就会自动import了，然后你就可可以顺利checkout l了、。。

 [1]: http://code.google.com/p/20thingsilearned/
 [2]: http://superuser.com/questions/44409/cant-checkout-source-from-google-code
 [3]: /images/2011/06/xxx.jpg
