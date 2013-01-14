---
title: Node.js操作mongodb（2）——gridfs操作文件
author: wahyd4
layout: post
comments: true
permalink: /2012/10/nodejs-mongodb-gridfs/
categories:
  - javascript
  - mongodb
  - node.js
tags:
  - javascript
  - mongodb
  - Node.js
---
昨天文章主要分享了node.js对mongodb数据的增删查改，由于mongodb本身操作脚本也是使用javascript写的，所有其实很多node.js中的很多操作方法和其脚本是差不多的，应该说相对比较简单入手吧，今天我要分享的是node.js使用mongodb中的gridfs操作文件的一些方法。

[<img class="aligncenter size-full wp-image-2261" title="Documents-icon" src="/images/2012/10/Documents-icon.png" alt="" width="128" height="128" />][1]

今天我们会主要用到两个模块：mongodb和node.js本身提供的fs模块，fs模块主要是node.js对文件处理的一些方法。首先当然是使用require。

``` ruby  
var mongo = require('mongodb');
var fs = require('fs');  
```
在mongodb提供的node.js API中主要有两种用于操作gridfs文件模块的对象：

``` ruby  
var gridFs = new mongo.Grid(db, 'fs');
var gridStore = new mongo.GridStore(db, new mongo.ObjectID(), 'w', {root: 'fs'});
```

简单说一下两种方式的区别：  
Grid()在读写文件的时候需要将文件的所有内容读取到内存中，因此在存储大文件的时候可能会导致内存溢出。但API相对简单主要有get(),put(),和delete()方法。  
GridStore()应该说是mongodb中GridFs的标准实现吧。可以防止内存溢出（后面说明）。API相对更加复杂，当然功能也更加强大。  
**那我们首先使用Grid进行文件的读写操作，**当然在操作之前我们需要新建Server、DB对象，并打开db：

``` ruby  
var server = new mongo.Server('localhost', 27017, {
	auto_reconnect: true
});
var db = new mongo.Db('mydb', server);

db.open(function(err, db) {
	if(err) throw err;
        //do some actions.
});
```

这部分由于前面一篇文章已经说过这里便不再赘述。下面直接操作文件。新建一个Grid对象。

``` ruby  
//第一个参数为被打开的db，第二个参数为我们希望使用的存储文件的collection名称
var gridFs = new mongo.Grid(db, 'fs');
```

Grid在使用put方法向mongodb数据库写入文件的时候，传入的参数为node.js中的Buffer（）（这也正是可能会导致内存溢出的原因），因此我们需要使用fs.readFileSync()读取文件存入buffer.注意这里读取文件必须使用同步操作，否则将不能读取到文件内容。

``` ruby  
var buffer = fs.readFileSync('c://a.iso');
	//该种方式存文件需要读取所有文件信息，如果文件过大可能会导致内存溢出
	gridFs.put(buffer, {}, function(err, fileInfo) {
		if(!err) {
			console.log('write file success!');
		}
		//通过ID获取文件
		gridFs.get(fileInfo._id, function(err, data) {
			if(err) throw err;
			//使用nodejs 原生fs api写入文件到硬盘
			fs.writeFile('c:\\my.iso', data, 'utf-8', function(err) {
				if(!err) {
					console.log('write file to local file system succeed!');
				}
			});
		})
	});
```

put()方法的第一个参数为buffer，第二个参数为文件的一些属性，将保存到mongodb中，这里我们不写，系统将自动填写相关信息，第三个是回调函数，我们可以从回调函数中获取到我们刚才保存的文件的相关信息。  
get()方法，即是通过mongodb中文件的_id参数去获取文件。并在回调函数中返回文件内容。  
最后我们再使用fs.writeFile()，来讲获取到的数据写入外部文件即可。其中的第三个参数，通常我们可以省略。系统模式会设置为utf-8。

**下面使用GridStore（）的方式来存储文件。**

``` ruby  
var gridStore = new mongo.GridStore(db, new mongo.ObjectID(), 'w', {root: 'fs'});
```  

解释一下这几个参数，第一个为你的DB对象，第二个需要传入一个mongodb的ObjectId对象，因此我们需要自动生成一个，第三个是模式，她有三个选择：

> 1.  r    读模式，文件只能被读取，不能被修改
> 2.  w  写模式，可以读写，已存在的文件会被覆盖。
> 3.  w+ 编辑模式，这个具体我不太清楚，应该是比w更高，也就是说不仅可以去写吧。

这里由于我们是向数据库写入文件，当然至少得w模式。

最后一个参数你要选择用于存储文件的collection，系统默认是fs,因此这个我们也可以不写。

``` ruby  
gridStore.writeFile('c://a.iso', function(err, fileInfo) {
		if(err) throw err;
		console.log(fileInfo);
		//新建一个gridstore用于读取文件
		var readGrid = new mongo.GridStore(db, fileInfo._id, 'r');
		readGrid.open(function(err, gridStore) {
			//读取数据
			readGrid.read(function(err, data) {
				//写入到本地文件系统
				fs.writeFile('c:\\myaaa.iso', data, function(err) {
					if(!err) {
						console.log('write file to local file system succeed!');
					}
				});
				db.close();
			});
		});
	});
```   

这个wrtieFile（)是把外部文件存入到mongodb的数据库 中，和fs.writeFile()是相反的，这个需要注意。其本身使用是比较简单的。  
当然后面我们需要从mongodb数据库中读出文件，于是新建了一个模式为“r”的GridStore。  
open函数，mongodb官方的解释是：  
Opens the file from the database and initialize this object. Also creates a new one if file does not exist.  
这里我们当然是从数据库中打开这个文件，并初始化这个对象。  
然后在使用read读取数据，并使用fs.writeFile（)写入外部函数。

完整代码下载：

<https://github.com/wahyd4/node.js-mongodb-demo>

参考资料：

<http://nodejs.org/api/fs.html>

<http://mongodb.github.com/node-mongodb-native/api-generated/gridstore.html>

<http://mongodb.github.com/node-mongodb-native/api-articles/nodekoarticle2.html>

 [1]: /images/2012/10/Documents-icon.png
