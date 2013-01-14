---
title: Java实现单一账号某时刻单一登录
author: wahyd4
layout: post
comments: true
permalink: /2011/12/java-single-sign-on/
categories:
  - java
tags:
  - Application
  - java
  - JAVA EE
  - Session
---
原谅我使用如此晦涩的词语来表达我的意思，其实我想表达的意思的用java实现类似于当其他人登录你的QQ时，你会收到“你的账号已在其他地方登录，请重新登录。”这样的东西，简单的说就是同一时刻一账号只允许一个人登录在线状态。也许就是保证时间、空间上的唯一性。但是我想强调的是这种效果绝不是单点登录，真正的单点登录是类似于Google中，使用多个产品只需要登录一次，其实QQ也有这样的功能。好了，废话少说下面说正经的。

我们最常用的用来验证用户使用登录的东西是Session，但是session并不能达到我们想要的效果，因为每个客户端访问网站的时候都会获得一个session，因此虽然是同一个账号登录系统，只要用户使用的浏览器，服务器都会产生两个session。但是每个客户端访问服务器的服务器的时候都会产生一个SessionId,而这个ID这是唯一的，我们会在后面用到。这里我们使用使用Application 域，在Java EE里面是ServletContext。这个东西是一个全局变量，当Web 程序运行的时候便会一直存在。而且整个程序只有一个Application.

于是我们可以这样。我们将数据存入Application中。而存入的内容则是：键（key）为当前用户使用用户名或者其他一个可以识别用户身份信息的ID，而值（value）则是用户得到的sessionID。这样便保证了一个账号同时至于一个用户对应。在用户登录的时候想Application中写入 key:value信息，在以后用户每次请求数据的时候，进行验证。看Application中的SessionID与用户本身的SessionID是否一致，不一致则说明多人登录。

下面是代码了：（我感觉说了好多废话）

首先获取Application:

<pre class="brush: java; title: ; notranslate" title="">HttpSession session = request.getSession(); //request为HttpServletRequest对象
	ServletContext  application = session.getServletContext();</pre>

向其中存入我们的验证数据，这里键为用户ID，值为该用户实例获得的sessionID

<pre class="brush: java; title: ; notranslate" title="">application.setAttribute(userId, session.getId());//userID为用户ID，</pre>

在每次验证的时候，在java里面我们可以采用至少两种方法，一种是Filter(Servlet 过滤器)、另外一种则是Spring AOC 面向切面编程，这里由于我对Spring AOC还不太熟悉，所以就用Filter，Filter具体设置，编写都不说了，只说一些怎么处理。拿到一个客户端来的请求，就进行sessionID比较，如果相同就让请求继续，如果不相同，就将该请求所对于的session清空（如果采用session验证用户是否登录，就可以达到让该用户退出登录）,并给出提示信息，跳转到登录页面。

<pre class="brush: java; title: ; notranslate" title="">//获取application对象
      ServletContext  application = session.getServletContext();
      String sessionId = (String) application.getAttribute(userid);
	String trueSessionId = session.getId();
	System.out.println("sessionID====="+sessionId+"现在的sessionID"+trueSessionId);
	if(sessionId.equals(trueSessionId)){
		//do nothing		
	}else{
		//说明有多个用户登录,去掉其session
		session.removeAttribute(sessionKey);
		//response.sendRedirect(request.getContextPath() + redirectURL);
		response.setContentType("text/html;charset=utf-8");
	         PrintWriter out = response.getWriter();
	        out.println(MyTools.getAlertMessage(request.getContextPath(), "您的账户已在别处登录，请重新登录", 3));
		return;
		}
</pre>

这里可以使用sendRedirect,将用户直接跳转到某个页面，但是这样不太友好，因为没有提示信息，我选择另外一个使用response给用户一些提示信息，然后设置一段时间后跳转到另外的页面。这就是我写的一个静态方法 getAlertMessage,下面贴出具体代码吧。

<pre class="brush: java; title: ; notranslate" title="">/**
	 * 生成用户返回的警告页面信息
	 * 
	 * @param path
	 *            系统根目录
	 * @param content
	 *            需要显示的内容
	 * @param second
	 *            需要停留消息的秒数
	 * @return String
	 */
	public static String getAlertMessage(String path, String content, int second) {
		StringBuilder sb = new StringBuilder();
		sb.append("&lt;html&gt;");
		sb.append("&lt;head&gt;");
		sb.append("&lt;meta http-equiv='refresh' content='3;url=" + path
				+ "/login.html'&gt;");
		sb.append("&lt;link rel='stylesheet' type='text/css' href='" + path
				+ "/css/login.css'&gt;");
		sb.append("&lt;/head&gt;");
		sb.append("&lt;body&gt;&lt;form id='login'&gt;&lt;fieldset id='inputs' style='font-size:18px;'&gt;"
				+ content
				+ ","
				+ second
				+ "秒后你将跳转到登录页面&lt;/form&gt;&lt;/fieldset&gt;&lt;/body&gt;");
		sb.append("&lt;/html&gt;");

		return sb.toString();

	}</pre>

好了，现在差不多实现这个功能的主要代码都有了。原谅我的表达能力不够好，如果各位有什么问题，留言吧。我们可以讨论一下。
