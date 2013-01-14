---
title: node、express、mysql、jade实现用户登录数据获取及验证
author: wahyd4
comments: true
layout: post
permalink: /2011/11/node-jade-express-mysql-simplelogin/
categories:
  - node.js
tags:
  - express
  - form
  - jade
  - mysql
  - node
  - 登录验证
---
今天要给大家介绍一下如何利用node.js的expressjademysql三个module实现获取form表单的内容以及通过数据库验证登录的正确性。请确保你已经下载好了前面三个module并且你的电脑里面已经安装好mysql。

首先看看运行页面：

[<img class="aligncenter size-full wp-image-2104" title="1" src="/images/2011/11/1.jpg" alt="" width="537" height="395" />][1]

再给大家看看整个小系统的目录结构吧：

[<img class="aligncenter size-full wp-image-2105" title="2" src="/images/2011/11/2.jpg" alt="" width="254" height="280" />][2]

请大家按照图中所示的目录结构建立好所有的文档吧。当然jquery你下载就可以了。

接下来，我们将建立数据库：

<pre class="brush: sql; title: ; notranslate" title="">create database receipts;  #创建数据库

#创建名为user的表
&lt;pre style="padding-left: 30px;"&gt;use receipts;
create table  user (
    userid bigint auto_increment not null primary key,
    username  varchar(20) not null,
    pass  varchar(30) not null
);
</pre>

然后我们来书写我们所需要的login.jade。这里使用jade，我们需要创建一个简单的layout.jade（模板）,在layout模板中我们将定义最基本的网页框架。设定大多数网页相同的部分。这里关于jade的语法我就不多讲了，jade的官网上很详细，直接给出layout的代码：

<pre class="brush: xml; title: ; notranslate" title="">!!! 5
html
      head
         &lt;span style="color: #ff0000;"&gt; title=title&lt;/span&gt;
       &lt;span style="color: #ff0000;"&gt; link(rel='stylesheet',type='text/css',href='/css/style.css')&lt;/span&gt;
      body!=body
</pre>

注意，由于jade会对我们所写的代码进行重新编码，编码成linux的相关格式，这里建议大家使用类似notepad++、ultra editor等软件时将其编码为UTF-8 无DOM格式，并且请不要在文件中同时使用空格和Tab对文件分隔，会导致报错。这里强调一下比如上述 title=title，这里是把网页的标题赋值给一个变量叫做title，之后我们声明并赋值title。link后面不能添加空格。类似的也一样。

下面是我们的登录界面login.jade,代码如下：

<pre class="brush: xml; title: ; notranslate" title="">form(id='login',method='post',action='/login')
    h1 Log In
    p(style='margin-top:20px;')   #{error}
    fieldset(id='inputs')
        input(id='username',name='username',type='text',placeholder='Username',autofocus='',required='')
        input(id='password',name='password',type='password',placeholder='Passowrd',required='')
     fieldset(id='actions')
        input(type='submit',id='submit',value='Log in')
        a(href='') Forgot your password
        a(href='http://google.com') Register
</pre>

大致是定义一个完整的表单。并且定义一个显示提示错误信息的地方。当然还有最重要的css代码。我将在后面提供源码给大家下载。  
home.jade和index.jade这个程序里面我们用不到，因此内容可以不管它。

接下来，我们就开始写代码了。当然是使用express了。首先我们将写两个路由器在app.js中，一个是显示登录的页面并且作为首页，另外一个是验证登录的页面。

//首先添加配置信息

<pre class="brush: jscript; title: ; notranslate" title="">app.set('view engine','jade');   //设置模板引擎
app.set('views',__dirname+'/views');   //配置jade文件夹
app.use(express.static(__dirname+'/public'));  //设置静态文件文件夹,比如css，js,/images
&lt;span style="color: #ff0000;"&gt;app.use(express.bodyParser()); //用户获取form表单数据&lt;/span&gt;
app.use(express.methodOverride());

//设置首页。
app.get('/',function(req,res){
	res.render('index',{title:'欢迎使用收据管理系统',error:''});
});
</pre>

<pre style="padding-left: 30px;">在编写登录验证登录路由之前，我们需要明确这里我们需要处理那些事：</pre>

*   获取表单中数据
*   创建mysql数据库连接
*   从mysql请求数据
*   将数据库中数据与form表单进行比较，并返回结果。

//获取表单中数据  
var user = req.body.username； //这样便可以获取到form表单中 name=”username”值，依赖于express.bodyParser()

创建mysql数据库连接。这里我们将做一个小小的封装。将封装的函数写入 user.js

<pre class="brush: jscript; title: ; notranslate" title="">//连接mysql服务器
function connectServer(){
	//创建mysql连接,设置用户名，密码
	var client = mysql.createClient({
		user:'root',
		password :'root'
	});
	client.host= '127.0.0.1';
	client.port=3306;
	&lt;span style="color: #ff0000;"&gt;client.database='receipts'; //选择需要使用的数据库，创建数据库时不必须，其他时候必须&lt;/span&gt;
	return client;   //返回创建好的数据库连接对象
}
</pre>

//接下来我们将从数据库获取数据，同样我们也做一个封装。因为要执行数据库操作。因此我们需要传入一个数据库连接对象client，并且传入用户名，以便查出该用户对应的密码。再则我们需要创建一个回调函数以便于，在获取到数据库中的值后，做出相关判断。按照常规长发很难获取值。应该闭包可以。（这个回调函数得感谢一个群里的大牛。），代码如下。

<pre class="brush: jscript; title: ; notranslate" title="">//执行mysql查询操作。返回查询获取到的对象
 function  selectFun(client,username,callback){
	//client为一个mysql连接对象
	client.query('select pass from user where username="'+username+'"',function(err,results,fields){
		if(err) throw err;

		callback(results);   //在获取结果之后由回调函数进行相关操作
	});
}
</pre>

<pre style="padding-left: 30px;">我们将关于数据库的两个函数，写在user.js里面。因此这里我们需要导出这两个函数，使用exports关键字，以便在其他地方可以使用。
<pre class="brush: jscript; title: ; notranslate" title="">
exports.connect = connectServer;
exports.selectFun  = selectFun;    //注意没有函数的（）哦。&lt;/pre&gt;
</pre>


<pre style="padding-left: 30px;"></pre>


<pre style="padding-left: 30px;">好了函数写好了。现在我们就该在app.js中使用了。</pre>


<pre style="padding-left: 30px;">导入我们刚创建的user.jsmodule</pre>


<pre style="padding-left: 30px;"><span style="color: #ff0000;">var usr = require('./dao/user');</span></pre>


<pre style="padding-left: 30px;">然后就可以使用了。
<pre class="brush: jscript; title: ; notranslate" title="">
app.post('/login',function(req,res){
	var user = req.body.username,
	pass = req.body.password,
	client = usr.connect(), //创建数据库连接
	result  = null;
	 //这里在回调函数里面进行mysql返回值的验证。很重要
	&lt;span style="color: #ff0000;"&gt;usr.selectFun(client,req.body.username,function(result){&lt;/span&gt;
		console.log('查询结果为'+result);

		if(result[0]===undefined){   //这里需要说明的是，mysql返回结果存在一个数组对象中。
			res.send('没有该用户！');
			}else{
			&lt;span style="color: #ff0000;"&gt;if(result[0].pass==req.body.password){&lt;/span&gt;
				res.send('登录成功');
				}else{
				    res.send('你输入的密码有误');&lt;/pre&gt;
                          });
			}
		}
	});  //执行查询
});
</pre>


<pre style="padding-left: 30px;">大家是不是看得太乱了。对不起。都是我的文字控制能力不好。大家凑合着看看吧。我把源码给大家，当然没有包含mysql创建数据库的源码哦。</pre>


<blockquote>
  <pre style="padding-left: 30px;">大家下载源码吧：http://115.com/file/bh03gw2q#</pre>
  
</blockquote>


<pre style="padding-left: 30px;">有什么问题，我们一起交流一起学习吧。</pre>

 [1]: /images/2011/11/1.jpg
 [2]: /images/2011/11/2.jpg
