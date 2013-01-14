---
title: linux安装配置postgresql
author: wahyd4
layout: post
comments: true
permalink: /2012/11/install-postgresql-with-linux/
categories:
  - linux
tags:
  - linux
  - postgresql
  - rails
---
这周在公司中的一个任务是，安装postgresql 数据库，并要成功连接rails 程序，执行rake 命令。走了很多弯路吧。主要有：

*   在postgresql 中创建一个与database.yml中用户名一致的用户。
*   创建一致的用户，并赋予superuser身份。
*   在postgres中创建一个用户与当前linux用户名一致。不设置/设置密码
*   修改/etc/postgresql/9.1/main/pg_hba.conf,修改里面的验证方法。

<div>
  主要出现的错误有：no password supplied.等错误。
</div>

最后，在各种操作后终于成功执行了 rake 命令，昨天晚上我自己在自己的电脑上又试了一下，现在将我们应该做的正确操作描述如下。

首先是在linux/ubuntu上安装postgres.

> sudo apt-get install postgresql-9.1
> 
> sudo apt-get install postgresql-server-dev-9.1

postgresql 数据库在安装的时候会默认创建postgres用户，它的身份可以简单理解成为mysql 中的root用户。并且我们现在可以这样登录postgresql

> sudo -u postgres psql (注意这里是小写的u，和后面的有区别)

接下俩我们需要在postgresql 中创建一个与当前你使用的linux用户名一致，并赋予superuser.（当然这个操作需要在连接到数据库的基础上）

``` sql  Create SuperUser
create user junv with superuser (当前我的linux用户名为junv)  
```



完成数据库操作后，使用 \q退出数据库命令行

然后，我们需要修改/etc/postgresql/9.1/main/pg_hba.conf（这里的9.1，是因为我安装的数据库版本是9.1）

> sudo gedit  /etc/postgresql/9.1/main/pg_hba.conf

将里面相似的内容修改为类似如下所示：

> \# Database administrative login by Unix domain socket  
> local all postgres trust
> 
> \# TYPE DATABASE USER ADDRESS METHOD  
> \# “local” is for Unix domain socket connections only  
> local all all trust  
> \# IPv4 local connections:  
> host all all 127.0.0.1/32 trust  
> \# IPv6 local connections:  
> host all all ::1/128 trust

最周这个method,改成trust,表示信任所有来地本地(localhost)的连接。这样我们就可以脸上数据库了

和mysql 我们修改了配置文件之后还需要做的是 重启 数据库，让配置生效。

> sudo service postgresql restart

到现在为止。我们对数据库进行的操作就差不多了。现在你应该已经可以成功脸上数据库了。

但是经过我的实验，我发现，我可以把database.yml中设置的用户名改成任意值，即使是一个在postgresql中根本不存在的用户名，也依然可以成功。所以我猜测，postgresql可能是用的我当前linux 系统的这个用户名吧。具体有待验证。

由于我们配置文件中，配置为对本地的所有连接都是信任的，这应该也是原因之一吧。

这一周在公司的生活很充实，由于使用ubuntu,代理，结对编程的缘故，基本上都没什么时间关注QQ，和浏览新闻了。。。。。。。。

开始适应在thoughtworks的生活。

 
