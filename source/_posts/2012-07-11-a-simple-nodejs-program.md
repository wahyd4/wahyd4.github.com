---
title: 一个Nodejs写的简易订饭程序
author: wahyd4
comments: true
layout: post
permalink: /2012/07/a-simple-nodejs-program/
categories:
  - node.js
tags:
  - expressjs
  - mysql
  - nodejs
---
因为公司最近开始不统一订饭了，但是我那么点工资到下面食堂去吃，既贵也吃不好，其他那些没工资的实训的同学就更伤不起了。为了脱离机械式的让每个人在纸上写上自己的名字。我用nodejs写了一个简单的程序来完成在网上订饭的功能。用户只需要进入网址。即可以完成订饭。这个程序是用nodejs+mysql完成的。使用了nodejs的 express和mysql包

使用下面的命令即可安装：

<pre class="brush: xml; title: ; notranslate" title="">npm install express

npm install mysql

</pre>

下面就附上代码吧，只有50多行，当然功能也很简单，只有订饭和查询所有已订饭的功能：

<pre class="brush: jscript; title: ; notranslate" title="">&lt;p style="padding-left: 30px;"&gt;var express = require('express'),
 mysql = require('mysql');
var app = express.createServer();&lt;/p&gt;
&lt;p style="padding-left: 30px;"&gt;//create mysql client
var client = mysql.createClient({
 user:'root',
 password :'root'
});
//设置mysql属性
client.host ='127.0.0.1';
client.port = 3306;
client.database = 'orderfood';&lt;/p&gt;
&lt;p style="padding-left: 30px;"&gt;//拦截地址
app.get('/add/:name',function(req,res){
 var name = req.params.name;

 res.charset = 'utf-8';
 //查询数据库中是否已经有该用户的记录
 client.query('select * from orders where name= ?',[name],function(err,results,fields){
 if(err) throw err;
 //阻止用户多次提交
 if(results[0]!==undefined){
 res.send('哈哈，'+results[0].name+'小子！你想重复提交吗？没门！！\n');
 return ;
 }else{
 //将数据存入数据库中
 client.query('insert into orders(name) values(?)',[name],function(err,results,fileds){
 if(err) throw err;
 console.log("你的名字为"+name);
 res.write("恭喜你订餐成功！你的名字为"+name +"\n");
 });
 client.query('select * from orders',function(err,results,fileds){
 if(err) throw err;
 if(results[0]!==undefined){
 var count=0;
 res.write("=================已定名单====================\n");
 for(var i=0;i&lt;results.length;i++){
 res.write("姓名："+results[i].name+"————————————订饭时间："+results[i].time+"\n");
 res.write('\n');
 count++;
 }
 res.write("*****************已订饭人数为："+count+"********************");
 res.end();
 return ;
 }
 res.send("已订名单为空！\n");
 });
 }
 });
 });
//设置404页面
app.get('*', function(req, res){
 res.send('小样 ，出错了！！我来自node.js哦', 404);
});
//监听3000端口
app.listen(80);
console.log("server listen on port 80");&lt;/p&gt;
</pre>

格式可能有点问题哈。
