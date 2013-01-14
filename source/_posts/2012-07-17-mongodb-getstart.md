---
title: Mongodb 入门
author: wahyd4
comments: true
layout: post
permalink: /2012/07/mongodb-getstart/
categories:
  - mongodb
  - 未分类
tags:
  - mongodb
  - 入门
---
[<img class="aligncenter size-full wp-image-2123" title="logo-mongoDB" src="/images/2012/07/logo-mongoDB.png" alt="" width="217" height="90" />][1]

Mongodb是一个非关系型数据库软件(NoSql),以类似json的形式bson存储数据,bson有二进制的json的意思,官方说bson的效率更高,很适合存储类似于对象的数据,这里权当把自己学习的过程记录下来.

首先是下载安装mongodb,请到[这里][2]下载适合你操作系统的相应版本,这里我们以windows作为介绍.

将下载的压缩包解压到一个文件夹,我这里为 f:\mongodb

在mongodb文件夹下创建一个data文件夹,用于存储你的数据库文件.

下面就可以开始安装运行mongodb了,mongodb不需要进行安装,直接运行即可,进入命令行:

> cd f:\mongodb\bin
> 
> mongod.exe –dbpath=f:\mongodb\data

–dbpath 为配置你的数据库文件路径,注意在等号附近不要空格哦,否则不能正常运行

[<img class="aligncenter size-full wp-image-2120" title="1_conew1" src="/images/2012/07/1_conew1.jpg" alt="" width="500" height="185" />][3]

这样mongodb的服务器端就已经成功运行起来了.下面运行客户端即可.mongodb默认是没有设置登录的用户名和密码,所以我们打开客户端,就可以直接连接上服务器.

> f:\mongodb\bin\mongo.exe

如果连接成功, 你会看到会默认连上test数据库.(connectting to :test)

下面我们就可以进行一些简单的操作了.

> help    // 查看帮助信息
> 
> db.help()  //在当前数据库内的帮助信息
> 
> show dbs   //查看所有的数据库列表
> 
> use dbname    //dbname为你的数据库,如果你想创建一个新的数据库,将dbname写成一个不存在的数据库名称即可,mongodb会自动帮你创建数据库,同时起到切换数据库的作用

在mongodb中没有我们通常说的”表”的概念,与表相对应的是”collection”,我们通常做到增删查改都是都与一个数据库中的collection而言的,在mongodb中不需要特意创建collection,如果我们使用的是一个没有的collection,系统便会自动创建

比如我们想插入一条数据:

<pre class="brush: sql; title: ; notranslate" title="">db.mycollection.save({"name":"junv"});

</pre>

系统便会自动生成名为mycollection的collection,并将数据存入其中.

我们也可以使用下面的话来达到同样的效果:

<pre class="brush: sql; title: ; notranslate" title="">var tom = {"name": "junv"};

db.mycollection.save(tom);

</pre>

我们可以使用 show collections 在查看当前数据库中所拥有的所有collection列表.

我们需要使用db.mycollection.find() 来查询其中的数据,如果我想查询”name” 为mary 的数据,就需要使用:

<pre class="brush: sql; title: ; notranslate" title="">db.mycollection.find({"name":"mary"});

</pre>

在一个collection 中,我们可以插入不同的数据,比如在mycollection中,我们还可以插入:

<pre class="brush: sql; title: ; notranslate" title="">db.mycollection.insert({"city":"chegndu","nation":"china"});

</pre>

这正是mongodb带来的优势.

如果我们查查询若干条数据,或者查询从n到m条数据,就需要使用:

<pre class="brush: sql; title: ; notranslate" title="">db.mycollection.find().limit(n);

db.mycollection.find().limit(n,m)

</pre>

当查询的数据过多而显示不完是,我们就需要使用 it 命令,来显示剩余部分.

更新数据，比如我们将“name”为mary的改为lily

<pre class="brush: sql; title: ; notranslate" title="">var temp = db.mycollection.find({"name":"mary"});

temp.name = "lily";     //改变名字

db.mycollection.update({"name":"mary"},temp);  //保存

</pre>

删除数据,将lily这条数据删除：

<pre class="brush: sql; title: ; notranslate" title="">db.mycollection.remove({"name":"lily"});

</pre>

删除所有数据:

<pre class="brush: sql; title: ; notranslate" title="">db.mycollection.remove({})

</pre>

 [1]: /images/2012/07/logo-mongoDB.png
 [2]: http://www.mongodb.org/downloads
 [3]: /images/2012/07/1_conew1.jpg
