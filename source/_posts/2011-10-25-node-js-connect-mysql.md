---
title: 使用node.js连接mysql数据库
author: wahyd4
comments: true
layout: post
permalink: /2011/10/node-js-connect-mysql/
categories:
  - node.js
tags:
  - mysql
  - node
  - query
  - 错误
---
<p style="text-align: center;">
  <a href="http://junv-wordpress.stor.sinaapp.com/uploads/2011/10/1036320.png"><img class="aligncenter size-medium wp-image-1778" title="1036320" src="http://junv-wordpress.stor.sinaapp.com/uploads/2011/10/1036320-296x300.png" alt="" width="190" height="192" /></a>
</p>

Javascript连接数据库可能很多同学之前都没有想到吧，不过现在使用node.js我们可以很容易地连接各种数据库。比如传统关系型数据库Mysql以及现在正火的非关系型数据库。这里讲一下如何连接mysql数据库其实官方的文档以及很详细了。

首先我们需要连接mysql所需的Module

<pre class="brush: jscript; title: ; notranslate" title="">npm install mysql</pre>

接下来就可以开始编程，连接数据库了。

<pre class="brush: jscript; title: ; notranslate" title="">var mysql = require('mysql');//导入mysql Module
var client = mysql.createClient({
	user:'root',
	password :'root'
});
/*
设置数据库的地址，这里请不要使用localhost，
至少我在windows这里出错,如果不写系统默认为localhost
*/
client.host ='127.0.0.1';
client.port = 3306;       //设置数据库端口，如果不写默认为3306
client.database = 'node';
	//create a database
	client.query('create database test_db',function(err){
	if (err &amp;&amp; err.number != mysql.ERROR_DB_CREATE_EXISTS) {
             throw err;   //添加异常处理
	}
	});
</pre>

这里我们使用的是client.query();执行sql语句，官方的API中client.query(sql,[params,cb])方法中还可以添加回调函数。

执行其他SQL语句也是使用client.query()函数。这里说一下插入语句

<pre class="brush: jscript; title: ; notranslate" title="">client.query('insert into node_t  values(?,?)',[1000,'Junv']  );</pre>

推荐这种参数化插入，而不是将值直接写在里面，可以防止sql注入。

注意：今天下午我最初尝试连接数据库的时候，它一直报错“Domain name not found”,只要我们加上

<pre class="brush: jscript; title: ; notranslate" title="">client.host ='127.0.0.1';</pre>

将系统默认的host=localhost改成127.0.0.1即可。具体原因不明。

是不是很简单呢？接下来我会写关于express 和jade的博客了。一边学习一边写博客。哈哈。
