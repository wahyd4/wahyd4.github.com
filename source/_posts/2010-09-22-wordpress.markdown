---
title: 一款很棒的wordpress 首页动画展示插件
author: wahyd4
layout: post
comments: true
permalink: /2010/09/wordpress/
categories:
  - 头条推荐
  - 酷玩软件
tags:
  - wordpress
  - 幻灯片
  - 插件
  - 首页
---
笔者为了找这样一款在首页显示的插件费了很多功夫，本来国产的有一款类似的差距叫helloFlash做的还不错，但是有一点不好的就是，这个插件会截取你发辫文章里面的每一张图片，而不是只是一张。这样就不好了。

经过苦苦寻找，终于让我找到了这样一款插件，做得比较好。叫做Featured Content Valley ，是一款英文的插件，设置相比helloflash那样的傻瓜配置是要复杂一些，不过还好。下面我就介绍一下这款插件的配置。[<img class="aligncenter size-large wp-image-300" title="8-15" src="http://www.junv.info/wp-content/uploads/2010/09/8-15-1024x513.png" alt="" width="1024" height="513" />][1]

这里面可以设置你要截取图片的类别，就是 Category name ，我这里选择的是头条推荐。下面一个是显示数量。说一下比较重要的事，你可以自定义幻灯片的宽度和高度。你完全可以按照你自己的需要设置就好了，下面一个选项是在图片下方留多高的区域来显示文字。这篇区域的颜色由幻灯片的背景颜色控制，这个颜色也是可以设置的。即是Gallery Background color。然后你还可以设置幻灯片的边框的颜色，你可以设置成与你的主题相协调的颜色。即是Gallery Border color. 你还可以在Gallery Text color 里面设置显示的字体的颜色。这些事基本设置，下面还有一些设置。

[<img class="aligncenter size-large wp-image-301" title="8-15-2" src="http://www.junv.info/wp-content/uploads/2010/09/8-15-2-1024x450.png" alt="" width="1024" height="450" />][2]

下面两行的设置，你可以不用修改，如果你不需要高级属性的话，因为插件本身已经有默认值了。这里我就不再介绍了，如果大家想自己设置这些，就花点功夫自己研究研究吧。

Slide Transition Type 这是动画效果的选择，你可以根据你自己的需要来设置什么效果。

下面就是有一个Advanced Custom Fields ，一些高级选项。 如果你不勾选高级选项的话，系统就会采用默认选项。 即你只需要在自定义栏目里面属于  类似于键值对这样的东西。键是“ artucleimg”不要引号。然后再值里面跟上图片的地址，说选择的图片还是尽量满足你设置的大小比较好。

最后你要做的很简单就是   代码放到你想显示这个动画的任何地方。他就可以显示啦，不信你试试。很简单的。

<span style="color: #ff0000;"><?php include (ABSPATH . ‘/wp-content/plugins/featured-content-gallery/gallery.php’); ?></span>

下面附上最新版本3.2.0下载地址吧：[点我下载][3]（wordpress 官方网站下载）!

 [1]: http://www.junv.info/wp-content/uploads/2010/09/8-15.png
 [2]: http://www.junv.info/wp-content/uploads/2010/09/8-15-2.png
 [3]: http://downloads.wordpress.org/plugin/featured-content-gallery.3.2.0.zip
