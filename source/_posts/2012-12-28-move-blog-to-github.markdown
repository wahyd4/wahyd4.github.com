---
layout: post
title: "把博客移到Github"
date: 2012-12-28 14:39
comments: true
author: Junv
categories:   
     - github
     - blog
tags:
   - github
---
  做这个决定还是反反复复用了很久的时间，我纠结的原因主要有两个：  
1. wordpress 的博客使用起来的确更加简单，不用像Octopress这样相对复杂一点。  
2. 主要还是之前觉得不太好把wordpress中的文章转移到Octopress上来。  
   现在这个两个问题都已经解决了。而且我还换了相对比较漂亮的主题，现在算是安心了，当然对我来说Github 有个最大的好处就是不需要为空间付钱。也省得经常备份这些麻烦事。  
   昨天到今天大概花了一天的时间来将我以前的博客迁移到Octopress上来，下面就分享一下吧：  
Github Page支持的博客主要有两种 Octopress 和 Jekyll BootStrap ，大概比较了一下，最后选择了Octopress，其实我之前也折腾过这些东西，只是后来觉得麻烦就没有继续使用。Octopress的优点在于，它里面包含的插件和相关配置更多。用起来也相对更加方便一点。  

迁移博客数据主要包括文章数据和评论数据,首先迁移文章，我使用的是 [wordpress-to-jekyll-exporter][1]插件来做,下载其zip文件，然后安装到你的wordpress博客中。在工具菜单中选择导出**Export to Jekyll** 即可导出你的日志数据为 *.md的文件，需要注意的是如果你的wordpress文章的固定链接名中含有中文，将无法正确导入到octopress中。  
接下来将这些*.md 文件放入到Octopress博客的 source/_post目录中，然后执行**rake generate**，如果不出意外，你就成功将你的博客文件导入到你的Octopress中了。使用这个插件，默认没有在文章中开启Disqus评论，因此你需要向你的每篇日志文件中手动添加：  
		comments: true   

然后再执行**rake generate** 即可了。  
评论的话，我们需要先去Disqus申请你的网站的一个评论实例（如果你的wordpress之前就是用Disqus，现在可以忽略这一步，只需要在**_config.yml**配置即可使用了。），然后在你的Wordpress中安装Disuqs插件，并导出评论到Disqus中，这样主要你在Octopress博客中配置好你的Disqus实例短名称，就可以自动同步使用这些评论了。  
可能你还会发现你的Octopress博客中的图片全都破了，因为这个图片的连接是使用的Wordpress生成的绝对路径，我们需要做的是：  
		1. 将wordpress uploads文件夹下的图片文件夹拷贝到Octopress中的**source/images** 目录中        		  
		2. 在linux下运行如下命令： 
		> find -name '*.md' | xargs perl -pi -e 's|http://yourdomain/web-contnet/uploads|/images|g'      

这样就可以把图片的坏链接修改过来了。  
大概整个迁移过程就是这样，另外插一句，我的博客是使用的 [Phase][2],大家可自行到链接处去安装使用该主题。  


[1]: https://github.com/benbalter/wordpress-to-jekyll-exporter
[2]: http://zespia.tw/blog/2012/05/02/new-theme-phase/
