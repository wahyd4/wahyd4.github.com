---
title: Node.js操作Mongodb(1)
author: wahyd4
comments: true
layout: post
permalink: /2012/10/nodejs-mongo-one/
categories:
  - javascript
  - mongodb
  - node.js
tags:
  - javascript
  - mongodb
  - Node.js
---
今天想要分享是使用node.js来连接并操作mongodb数据库实现基本的增删查改操作。

首先我们需要在node.js下安装mongodb争对node的驱动。

npm install mongodb

下面就可以开始写代码了。首先当然是在node代码引用mongodb:

<pre class="brush: jscript; title: ; notranslate" title="">var mongodb = require("mongodb");

</pre>

其次就是连接到mongodb数据库server:

<pre class="brush: jscript; title: ; notranslate" title="">var server = new mongodb.Server('localhost',27017,{auto_reconnect:true});

</pre>

其中第一、二分参数分别是IP地址和端口，由于我们这里没有设计到验证，因此便不需要验证参数。最后的参数是一个对象，我们设置了一个属性auto_reconnect为true，就表示如果当程序与mongodb失去连接便回自动重连。

<pre class="brush: jscript; title: ; notranslate" title="">var server = new mongodb.Server('localhost',27017,{auto_reconnect:true},10);

</pre>

通常情况下我们可以不管最后一个参数，这个参数是线程池的数量，系统默认的设置是5，也就是说可以同时支持打开5个数据库连接，并进行操作。当然我们可以根据自己需要设置希望的值。

然后就是获取或者创建一个DB实例。

<pre class="brush: jscript; title: ; notranslate" title="">var db = new mongodb.Db("mydb2",server);

</pre>

第一个参数需要传入被数据库的名称，如果数据库不存在系统会创建该数据库，当时不是现在，而是当我们试图打开数据库的时候。

<pre class="brush: jscript; title: ; notranslate" title="">db.open(function(err,db){
if(err){
console.log(err);
}
if(!err){
console.log("we are connected!");
}
});
</pre>

我们想要对数据库进行的相关操作都是在db.open()的回调函数内完成的。即是说我们对数据库的操作需要在数据库被打开的情况下完成。  
在mongodb中collection可以看做是我们平时所用的关系型数据库中的table(表)，我们可以通过显式或者隐式的方式来创建collection：  
**显式**即是使用db.createCollection()创建。

<pre class="brush: jscript; title: ; notranslate" title="">db.createCollection('test',{safe:true},function(err,collection){
if(err){
console.log(err);
}else{
console.log("created successful!");
}
 });
</pre>

safe:true如果我们使用了这个参数即表示，如果当我们想要创建的collection已经存在时，则会报错，如果去掉则不会。  
隐式则是我们在使用某个collection的时候，系统发现没有该collection，则会自动创建。

<pre class="brush: jscript; title: ; notranslate" title="">db.collection('fuck',function(err,collection){
});
</pre>

这个时候如果我们使用safe:true，当程序发现我们希望使用的collection不存在则会报错。通过这段代码，我们可以在该回调函数中执行所有我们对该collection的操作。

插入数据：

<pre class="brush: jscript; title: ; notranslate" title="">//插入单条数据
collection.insert({'name':'tom'},function(err,result){});
//插入数组
var array = [{'name':'mary'},{'name':'lily','age':20}];
collection.insert(array,{safe:true},function(err,result){
     if(err) throw err;
});
</pre>

当我们一次插入或者在以后的删除、更新多条数据时，我们都应该使用safe:true，以保证数据的完整性和一致性，如果在插入数组的过程中某些数据未能成功插入，即会报错。  
更新数据：

<pre class="brush: jscript; title: ; notranslate" title="">collection.update({'name':'tom'},{$set:{'name':'lily','age':100}},function(err,result){
if(err) throw err;
if(!err){
console.log("update successful");
}
 });
</pre>

第一个参数为我们定位目标的属性，这里即是我们更新所有名字为tom的数据，$set的意思则是我们将其更换其他的数据。  
删除数据：

<pre class="brush: jscript; title: ; notranslate" title="">//删除用户名为tom的数据
collection.remove({'name':'tom'},{safe:true},function(err,result){
if(err) console.log(err);

});

//删除集合内的所有数据

collection.remove();
</pre>

查找数据：

<pre class="brush: jscript; title: ; notranslate" title="">//查找一条符合的数据
collection.findOne({'name':'tom'},function(err,result){
if (err) throw err;
console.log(result);
 });

//查找多条数据，将结果集转换成数组。

collection.find().toArray(function(err,items){
if(err) throw err;

//遍历数据

for(item in array){
 console.log(array[item]);
 }
 });

//另外一种查找多条数据的方式是使用流式来处理。

var stream = collection.find().streamRecords();

//监听获取数据
 stream.on("data",function(item){
 console.log(item);
 });

//当数据读取完毕时，执行的方法。
 stream.on("end",function(){
 console.log("stream is end");
 });
</pre>

当然我们这里使用的查找数据的方式很简单，没有涉及到高级的查询语句，比如限制返回数据的条数limit()，这些都是可以使用的。大家可以从下面的文档中获取到更多的信息。

完整代码下载：

<https://github.com/wahyd4/node.js-mongodb-demo>  
参考文档：  
<http://mongodb.github.com/node-mongodb-native/api-articles/nodekoarticle1.html>  
<http://www.mongodb.org/display/DOCS/Advanced+Queries>

请阅读下一篇：

<a href="http://toozhao.com/2012/10/nodejs-mongodb-gridfs/" target="_blank">Node.js操作mongodb（2）——gridfs操作文件</a>
