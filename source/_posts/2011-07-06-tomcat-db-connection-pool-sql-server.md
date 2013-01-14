---
title: tomcat 7配置数据库连接池，使用SQL Server2005实现
author: wahyd4
comments: true
excerpt: >
  昨天看了一些网上的tomcat数据库连接池配置的东西，但是一直没配好，主要原因是网上的文章几乎没有争对tomcat
  7进行配置的，而且针对SQL
  SERVER的也不多，今天上午看了官方的文档，花了一上午时间终于配置好了数据库连接池，这里发给大家看看，如果有什么疑问就留言吧。
layout: post
permalink: /2011/07/tomcat-db-connection-pool-sql-server/
categories:
  - java
  - 编程之美
tags:
  - java
  - servlet
  - 连接池
---
> 昨天看了一些网上的tomcat数据库连接池配置的东西，但是一直没配好，主要原因是网上的文章几乎没有争对tomcat 7进行配置的，而且针对SQL SERVER的也不多，今天上午看了官方的文档，花了一上午时间终于配置好了数据库连接池，这里发给大家看看，如果有什么疑问就留言吧。

首先我们需要向项目中导入tomcat-dbcp.jar 、servlet-ap.jar和sql server的驱动sqljdbc4.jar 包到 web-inf 文件夹下的lib目录 。

然后增加context.xml

这里有两种方法，第一种是在tomcat程序目录下面的conf/context.xml里面修改，这里修改之后所有的程序都将都将覆盖数据库连接池，但是这种方法不够灵活。这里我们选择第二种方法 在项目的Web-content/meta-inf 目录下创建一个context.xml文件，在里面添加如下内容：

<pre class="brush: xml; title: ; notranslate" title="">&lt;Context path="/SYSDEMO" docBase="SYSDEMO" 
reloadable="true" crossContext="true"&gt; 
&lt;Resource name="jdbc/SYSDEMO" auth="Container" type="javax.sql.DataSource" 
maxActive="100" maxIdle="30" maxWait="10000" 
username="lenovo" password="lenovo" driverClassName="com.microsoft.sqlserver.jdbc.SQLServerDriver" 
url="jdbc:sqlserver://202.115.90.241:1433;DatabaseName=SYSDEMO"/&gt; 
&lt;/Context&gt; 
</pre>

这里需要修改的是 将所有的SYSDEMO改为你自己的使用的数据库的名称

将driverClassName改为你所使用数据库的驱动，这里是SQL SERVER的驱动。

将url改为jdbc链接该数据库的地址,这里是SQL SERVER的地址，

将username 、password改为你自己数据库用户名和密码

maxActive=”100″ maxIdle=”30″ maxWait=”10000″ 

可以将这三个参数进行修改，

第一个是最大活动的连接数

第二个是最大的未连接数

第三个是最长的等待时间，单位是毫秒

然后再修改项目的webContent/web-inf/web.xml文件

添加如下内容:

<pre class="brush: xml; title: ; notranslate" title="">&lt;description&gt;MySQL Test App&lt;/description&gt;
&lt;resource-ref&gt; 
   &lt;description&gt;DB Connection&lt;/description&gt; 
   &lt;res-ref-name&gt;jdbc/blog&lt;/res-ref-name&gt; 
   &lt;res-type&gt;javax.sql.DataSource&lt;/res-type&gt; 
   &lt;res-auth&gt;Container&lt;/res-auth&gt; 
&lt;/resource-ref&gt; 
</pre>

这里必须要改的是: <res-ref-name>jdbc/SYSDEMO</res-ref-name> 

改为 jdbc/你自己的数据库

好了然后就可以使用了。

如下是我测试的servlet文件

<pre class="brush: java; title: ; notranslate" title="">import java.io.IOException;
import java.sql.Connection;
import java.sql.SQLException;
import javax.naming.Context;
import javax.naming.InitialContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.sql.DataSource;
@WebServlet("/TestPool")
public class TestPool extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
     try{
          Context initContext = new InitialContext();
          Context envContext  = (Context)initContext.lookup("java:/comp/env");
          DataSource ds = (DataSource)envContext.lookup("jdbc/SYSDEMO");
          Connection conn = ds.getConnection();
          System.out.println("成功了。。。。。。。。。。");
      }catch(Exception e){
           System.out.println("出错了。。。。。。。。。。。。。。。。。。");
          e.printStackTrace();
      }
    }
}

</pre>

将 DataSource ds = (DataSource)envContext.lookup(“jdbc/SYSDEMO”);

“jdbc/SYSDEMO” 的sysdemo改为你前面使用的数据库的名称即可。

好了。大功告成。
