---
title: 那些年我用过的开源软件、框架
author: wahyd4
comments: true
layout: post
permalink: /2012/07/good-open-source/
categories:
  - 我说
tags:
  - java
  - 开源
  - 框架
---
作为一个Java程序员，我想我们很多时候都需要和开源（open source software）扯上关系，我不得不说如果我的生活没有开源，肯定会比现在更糟，我们程序员效率一定没有现在这么高。我们通过使用那些著名的开源软件，逐步深入，不断提升了自己的编码水平。也学习了人家的设计功力。

<div>
         到目前为止我没有设计出或者说贡献出什么开源软件，我自知自己的能力真的还不够。不过我希望哪一天可以为开源世界添砖加瓦，也希望其他童鞋能够加入这个行列。让世界变得更美好。
</div>

<div>
         下面是我曾经用过的开源软件，可能有些只是简单了解，并不是很熟悉，但是我觉得它很不错也会记录在下面：
</div>

<div>
  ========================== 开发语言 ===============================
</div>

<div>
  <strong>Java      </strong>      不多说，正是我现在深入学习，使用的。
</div>

<div>
  <strong>PHP  </strong>           适合于快速开发的服务器语言。我只是学习过一些，大概有两三次学习，每次都是学习一点，然后又放弃。最后遗忘。因为我还是喜欢java
</div>

<div>
  <strong>Node.js  </strong>      基于js的服务器后台语言框架。其非阻塞的特点，便于开发高性能的网站。开发快速，现在在国内已经开始流行，而且有很多开源的组件，使得node.js的可以实现的功能越来越多，比如著名的express.js 这是提供快速开发网站的支持，自带restful
</div>

<div>
  <strong>C#, C              ,</strong>曾经学过，现在已经快忘得差不多。
</div>

<div>
  <strong>javascript </strong>    主要是用于浏览器的脚本语言，现在有了node.js当然也可以用在后台服务器，入门较简单。jquery也是必学。学好这个东西很重要。现在HTML5 的世界，javascript可以做到事越来越多了。基于V8虚拟机，也使得javascipt在chrome的性能提升了很多倍。
</div>

<div>
</div>

<div>
  ==================== 工具类 ===================
</div>

<div>
  <strong>Eclipse  </strong>       开源java IDE，当然这个IDE也可以用来开发C/C++ ,PHP,ruby等程序，我认为它是世界上最好的集成开发工具。可以通过插件无限扩展其功能。
</div>

<div>
  <strong>netbeans </strong>    oracle开发的开源java IDE，不过我认为和eclipse还是有一定差距的。不够好用，而且有点卡。
</div>

<div>
  <strong>notepad++ </strong> 开源的文本编辑器，支撑几乎所有语言的高亮显示，还支持安装各种插件扩展其功能哦。很小巧。
</div>

<div>
  <strong>tomcat  </strong>      开源的java servlet容器，轻量级服务器。性能很好。不过很多Java EE的特性程序，是不能在tomcat上运行的。
</div>

<div>
  <strong>Jboss AS </strong>   开源的JAVA 应用服务器，它的功能则强大得多，支持tomcat的所有功能，而且对JAVA EE也提供完整支持，现在最新的jboss AS 7中，加入了OSGI功能，使得它更加强大。
</div>

<div>
  <strong>Jetty    </strong>        开源的java servlet容器，你可以把它简单理解和tomcat 差不多，不过它更加小巧，甚至可以内嵌到应用中，小到只有一个包。也就是你的程序可以本身就单独运行，当然需要在程序中加入jetty相关包。
</div>

<div>
  <strong>Aptana </strong>     开源的eclipse插件，功能强大，提供了很多web开发功能，支持主题、内嵌git 插件等，而且它的javascript 辅助功能也更加强大。其他很多功能我还没有用到，但是它值得你开始使用。
</div>

<div>
  <strong>checkstyle</strong>   用于检查代码语法和结构的eclipse插件，它的要求比eclipse自身更加严格，对开发人员的编程规范要求很高，不过可以让你写出的代码质量更高、更易于他人阅读理解。
</div>

<div>
  <strong>findbugs </strong>     检查代码中潜在bug的eclipse插件。我对它使用还不够熟悉，但是它还是很有用，方便你随时检查下代码是否有常见bug。
</div>

<div>
  <strong>MAVEN  </strong>     类似于ANT的项目打包、构建工具，也是基于组件式的，你可以通过使用多个maven插件来完成很多功能。使用自动化构建程序等任务，比ant强大很多，同时支持调用ant命令。
</div>

<div>
  <strong>git    </strong>            开源的代码版本控制工具。分布式，没有中央服务器照样安全工作。
</div>

<div>
  <strong>chrome</strong>       谷歌浏览器，我通常用它来调试web 应用程序，相当给力啊。
</div>

<div>
  <strong>Nexus  </strong>        开源的maven 仓库管理工具，功能很强大。
</div>

<div>
  <strong>Jenkins  </strong>     开源的项目自动构建、持续集成服务器。基于Hudson 开发。
</div>

<div>
  <strong>run jetty  </strong>    在eclipse 内一键运行jetty的插件，在开发maven项目的使用用起来特别方便。简单，而传统的run on server是做不到这点的。
</div>

<div>
  <strong>M2E  </strong>         开源的maven eclipse 插件，提供图形化支撑。
</div>

<div>
</div>

<div>
</div>

<div>
  =====================java开发框架=======================
</div>

<div>
  <strong>struts  </strong>        很著名的控制层框架，不过我不太喜欢
</div>

<div>
  <strong>spring framework</strong>  全世界最好的框架之一，它的能力之强大，使用范围之广。据说它里面的代码实现相当经典，不过还没有拜读。其衍生出的很多框架也很好。比如spring security
</div>

<div>
  <strong>hibernate </strong>     开源的ORM框架，将所有对数据库的 操作都做成操作对象的形式，不过它的弱点在于不能直接使用sql 语句操作，在处理一些比较复杂的查询功能时没有直接操作sql语句简单。很麻烦。
</div>

<div>
  <strong>jgit    </strong>           git的java实现。很不错哦，在一个eclipse插件里面使用了这个包，这样再也没有狂平台的问题，java帮我解决了一切。
</div>

<div>
  <strong>apache poi </strong>  开源的java api，你可以用它来操作windows 文档：doc，xls，ppt，pdf等等。很方便。以前用它作过导出数据到excel中。
</div>

<div>
  <strong>jersey  </strong>        开源的java restful 服务实现。比较简单吧。用起来也舒服。
</div>

<div>
  <strong>apache CXF </strong> 另一个开源的java web services 实现，当然支持标准的rest服务。通过它还有osgi 版本，很前卫。
</div>

<div>
  <strong>dom4j </strong>        java的操作xml 的开源类库，有了它读或者写xml文档都很简单。
</div>

<div>
  <strong>apache fileupload </strong> java开源的文件上传插件，很实用，也比较简单。
</div>

<div>
  <strong>log4j    </strong>     java 开源的日志框架，可以将软件日志写到控制台、外部文件、数据库中
</div>

<div>
  slf4j          另外一个开源的java日志框架，但是它本身并不提供实现，而是提供了接口。如过你想把日志写入外部文件或者数据库还需要配合log4j等其他框架使用。
</div>

<div>
</div>

<div>
  ================其他开发框架 =========================
</div>

<div>
  <strong>twitter bootstrap </strong>    twitter的开源前端框架，用它开发一个网页界面，超级简单，快速，而且很美哦，兼容性也很好。
</div>

<div>
  <strong>artdialog    </strong>            一个中国人写的开源js弹出层框架，很好用，而且也很绚丽。强烈推荐。
</div>

<div>
  <strong>jquery form     </strong>      一个开源的jquery form 插件，可以用来执行ajax 表单请求。等等。
</div>

<div>
  <strong>xml2json      </strong>        一个用于把xml文档转成json的jquery 插件。js操作json还是更加舒服。
</div>

<div>
  <strong>highcharts  </strong>         开源的js图表插件，功能强大，有多种图表，并支持ajax异步强求。
</div>

<div>
  <strong>jquery      </strong>           这个强大的js 框架，让js变得更加好用。
</div>

<div>
  jquery UI             jquery 的UI控件框架，集成了很多网页UI组件，不过我认为有了twitter bootstrap 此框架少了很多吸引力。
</div>

<div>
  <strong>jquery mobile </strong>    用于移动平台的jquery UI插件，可以把节目做得更像移动平台原生，我感觉目前性能还有待提升。
</div>

<div>
</div>

<div>
  目前只想到这些，文中对开源软件的描述可能有错，欢迎指出，讨论。
</div>

<div>
  不要重复造轮子。
</div>
