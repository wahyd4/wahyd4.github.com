---
title: '解决Spring 管理Hibernate执行数据库操作出现“too  many connection&#8221;的错误'
author: wahyd4
comments: true
layout: post
permalink: /2011/11/spring-hibernate-db-too-many-connection/
categories:
  - java
tags:
  - Hibernate
  - java
  - SessionFactory
  - Spring
  - 错误
---
随着代码的不断深入，出现了一些意想不到的错误.如上面所写。

mysql数据库报出了can’t open connection , …….. too many connection 等等错误。

但是我使用的是Spring  管理Hibernate执行相关操作。我们都知道Spring 在执行Hibernate相关操作完成时会自动关闭连接。 比如执行这样的操作：this.getHibernateTemplate().update(msg);

我也知道如果我们这样执行：

<pre class="brush: java; title: ; notranslate" title="">Session mySession = getSession();
		 Query query = mySession.createQuery(hql);
        query.setFirstResult(start);
        query.setMaxResults(count);
		@SuppressWarnings("unchecked")
		List&lt;Message&gt; msgs = query.list();
		 mySession.close();
</pre>

需要自己关闭Session.我关闭了Session之后，Hibnerate一次可以执行超过8次的链接。但是，一旦频繁请求时依然会出现文首的错误。  
这是为什么呢？  
大致是这样的，Session 上面还有一个SessionFactory，而SessionFactory是负责管理Session的。我们虽然调用了   session.close()  
但是没有真正关闭该Session，为了彻底关闭该Session交出使用权，我们需要使用

<pre class="brush: java; title: ; notranslate" title="">this.getSessionFactory().close()；//关闭sessionFactory
</pre>

这样就彻底关闭该Session了。  
好了，现在程序性能提升不少了，我在自己电脑上至少是已经不能刷爆程序了。  
如果说得哪里不对，请指正，因为本人也在学习之中！
