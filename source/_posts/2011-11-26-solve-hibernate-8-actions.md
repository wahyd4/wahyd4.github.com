---
title: 解决Hibernate只执行8次数据库操作
author: wahyd4
comments: true
layout: post
permalink: /2011/11/solve-hibernate-8-actions/
categories:
  - 我说
tags:
  - Hibernate
  - java
  - mysql
---
嗯，原因是这样的，今天下午在写一个获取某个类别下文章数量的时候，需要为每个目录都执行查询，但是我发现一个问题，Hibernate只会执行8次操作，之后就停在那里了，也不会返回数据。

噢，真是恼火，最终在百度上找到了解决办法，原因是这样了，因为我每次执行操作的数据库查询的时候没有关闭Session，因此导致出现了问题。

同志你只要加上这样这样一句话：

<pre class="brush: java; title: ; notranslate" title="">session.close()；</pre>

好了，再试试，已经搞定了!
