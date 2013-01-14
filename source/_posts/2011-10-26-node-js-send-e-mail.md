---
title: 使用Node.js发送电子邮件（E-mail）
author: wahyd4
comments: true
layout: post
permalink: /2011/10/node-js-send-e-mail/
categories:
  - node.js
tags:
  - email
  - Node.js
  - 发送
---
 

<span style="color: #ff0000;">10月27日更新，可以发送附件</span>

今天晚上花了点时间试了一下使用node.js发送电子邮件，也挺简单的，<del>不过有个问题一直没有解决，就是发送附件,</del>我弄明白的时候，会补充资料的。

首先我们还是得安装node的第三方用户发送email的module 。

    npm install nodemailer

安装好之后，还有一个问题需要注意，我们应该确保用来发送邮件的邮箱地址是打开只是IMAP 、SMTP功能的，这样才可以发送邮件成功。

接下来我们就开始写代码，其实很简单，官方网站也都已经说得很清楚了。

<pre class="brush: jscript; title: ; notranslate" title="">var mail = require('nodemailer');  //包含发送邮件所需module
mail.SMTP = {
	use_authentication: true, //如果我们使用QQ等邮箱，这个必须写且为true
	host: 'smtp.qq.com',   //定义用来发送邮件的邮箱服务器，一般是QQ这些的
	port:25,    //定义服务器端口，一般是25	,如果是使用SSL端口一般为465,或者587
	ssl:false,     //默认不适用SSL，可以省略不写
	user: 'wahyd4@qq.com',   //邮箱用户名
	pass:'*****'   //输入邮箱密码
}
mail.send_mail(
{
	sender:'wahyd4@qq.com',   //发送邮件的地址
	to:'wahyd4@gmail.com',     //发给谁
	subject:'随便把',               //主题
	body:'Hello,这个邮件来自node.js'
},
//回调函数，用户判断发送是否成功，如果失败，输出失败原因。
function(error,success){
	if(!error){
		console.log('message success');
		}else{
		console.log('failed'+error);
	}
}
);</pre>

这里我没有使用SSL进行发送，而且发送的是纯文本，也可以发送html,如果发送html则在send_mail函数里面加上：

    html: '<p> 你好。。邮件来自node.js</p>',

如果使用SSL进行发送我们则需要将mail.SMTP改为：

<pre class="brush: jscript; title: ; notranslate" title="">mail.SMTP = {
	use_authentication: true,  //如果我们使用QQ等邮箱，这个必须写且为true
	host: 'smtp.qq.com',   //定义用来发送邮件的邮箱服务器，一般是QQ这些的
	port:465,    //定义服务器端口，一般是25	,如果是使用SSL端口一般为465
	ssl:true,     //默认不适用SSL，可以省略不写
	user: 'wahyd4@qq.com',   //邮箱用户名
	pass:'*****'   //输入邮箱密码
}
</pre>

好了。现在你运行程序试试,是不是成功了。

我今天晚上遇到一个错误 :**503 ERROR,need EHLO and AUTH first**。就是因为没有添加use_authentication = true的缘故。加上之后，搞定。

———————————————————分割线———————-

发送附件的话。首先我们得使用

<pre class="brush: jscript; title: ; notranslate" title="">var fs = require('fs');    //导入文件系统相关的包</pre>

饭后我们将文件读入内存，并将其发送。

<pre class="brush: jscript; title: ; notranslate" title="">//读入文件
var img = fs.readFileSync(__dirname+"/cat.jpg");

var attachment = [{
    'filename': "cat.jpg",   //这里只是给附件取名称，而不是导入文件内容
    'contents': img         //导入文件
}]    //定义我们需要发送的附件
</pre>

接下来我们需要在send_mail函数中加入发送附件即可

<pre class="brush: jscript; title: ; notranslate" title="">mail.send_mail(
{
	sender:'wahyd4@qq.com',   //发送邮件的地址
	to:'wahyd4@gmail.com',     //发给谁
	subject:'测试发送文件',       //主题
	attachments: attachment, //添加附件
	body:'Hello,这个邮件来自node.js，包含附件哦，亲！'

},
</pre>

附上Nodemailer的网址：http://www.nodemailer.org/

enjoy it!

最后还是感谢 [andris9][1] 大叔很快帮我解决了问题！

 [1]: https://github.com/andris9
