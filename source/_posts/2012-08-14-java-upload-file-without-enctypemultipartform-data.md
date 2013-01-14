---
title: 'java 服务器端实现HTTP无enctype=&#8221;multipart/form-data&#8221;文件上传'
author: wahyd4
comments: true
layout: post
permalink: /2012/08/java-upload-file-without-enctypemultipartform-data/
categories:
  - java
tags:
  - java
  - 上传
---
在java web中我们一般都是使用commons-fileupload 和cos 进行服务器端上传文件的处理，而这种情况通常是我们通过在网页中的form标签中设置enctype=”multipart/form-data”这样的信息，才可以。否则commons-fileupload和cos都不能获取到文件。HTML网页设置格式如下图所示：

<pre class="brush: xml; title: ; notranslate" title="">&lt;html&gt;
&lt;body&gt;
&lt;h2&gt;Hello upload-file&lt;/h2&gt;
&lt;form method="POST" action="upload" enctype="multipart/form-data"&gt;
file upload:&lt;br&gt;
&lt;input type="file" name="file" /&gt;
&lt;input type="submit" value="submit"&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;

</pre>

这只是一个简单例子，但如果我们遇到这样的情况：我们有一个java本地的客户端，使用HTTP协议来上传文件，不过这里没有表单。commons-fileupload的服务器端就会报错

其实解决的办法也很简单，面对没有设置”multipart/form-data”属性的客户端，我们可以通过request.getInputStream() 获取输入流，从中读取文件内容。

下面是我写的一断简单代码，把输入流信息，写入到C盘的一个文件：

<pre class="brush: java; title: ; notranslate" title="">protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

 InputStream input= request.getInputStream(); //获取流
 OutputStream out = new FileOutputStream(new File("c://test.txt"));
 byte[] buffer = new byte[1024];
 int count;
 while ((count = input.read(buffer)) != -1) {
 out.write(buffer, 0, count);  //写文件
 }
 out.flush();
 out.close();
 input.close();
 }

</pre>

不过这种方式是不能直接解析上面那种form表单的文件上传方式，他会在文件的前后各加上一段信息,下面是一个form表单上传，输入流中的信息：

<pre class="brush: xml; title: ; notranslate" title="">------WebKitFormBoundaryOPczhvGNCBlneBER
Content-Disposition: form-data; name="file"; filename="??????.txt"
Content-Type: text/plain
#下面是我写入的文件内容
df03c9cf37c5fbc5a7894e04297127d7
3a9bb0371ea5789666ab438b3b7e05c2
#到此为止
------WebKitFormBoundaryOPczhvGNCBlneBER--

</pre>

如果form中没有加上enctype=”multipart/form-data”属性信息，输入流中得到的只有在<input value=”">中设置的value值，因此，通过流来获取上传的文件，应该只适合于从客户端直接向服务器写文件。
