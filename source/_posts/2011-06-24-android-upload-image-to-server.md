---
title: Android上传图片到服务器Server端servlet源码
author: wahyd4
comments: true
layout: post
permalink: /2011/06/android-upload-image-to-server/
categories:
  - 头条推荐
  - 编程之美
tags:
  - android
  - java
  - servlet
  - 上传文件
---
> <del><span style="color: #ff0000;"><strong>更新：现在提供源码下载了！在文末有地址！</strong></span></p> 
  <p>
>     </del><span style="color: #ff0000;"><strong>由于115关闭了外部下载，还是麻烦大家留言写下地址吧，我会把包发给大家的。</strong></span>
>   </p>
</blockquote> 
> 
> 
  <p>
>     最近看到很多朋友都留言回复很开心，我也很高兴，自己做的这样一个小程序可以帮到你们。上篇文章详细讲了如果实现android端的代码，很多朋友都在问s服务器端servlet源代码，这里就贴出来给大家吧，但是最近很忙，就先暂时不详细解释了。
>   </p>

> 
> 
  <p>
>     这里说明一点，这个程序是使用了Apache Commons 的一个上传文件的开源组件叫做FileUpload,用的包是commons-fileupload-1.2.2.jar。其他的就不多说了，如果你直接粘贴使用下面代码，请你一定要导入这个包。
>   </p>

> 
> 
  <pre class="brush: java; title: ; notranslate" title="">
package info.junv;
import java.io.File;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;
import java.util.Iterator;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileItemFactory;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

@WebServlet("/HandleUpload")
public class HandleUpload extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {

	File temp = new File(request.getSession().getServletContext().getRealPath("/")
				+ "temp");// 临时目录
		System.out.println("临时目录为=" + temp);
		String loadpath = request.getSession().getServletContext()
				.getRealPath("/")
				+ "image"; // 上传文件存放目录

		System.out.println("文件保存目录为=" + loadpath);

		DiskFileItemFactory factory = new DiskFileItemFactory();

		factory.setSizeThreshold(1024*1024);   //设置最大可以存到内存值
		factory.setRepository(temp);  //设置缓存文件夹

		ServletFileUpload fu = new ServletFileUpload(factory);

		fu.setSizeMax(1024 * 1024 * 1024); // 设置允许用户上传文件大小,单位:字节

		System.out.println("开始上传。。。。。。。。。。。。");
		// 开始读取上传信息
		int index = 0;
		List fileItems = null;

		try {
			fileItems = fu.parseRequest(request);

		} catch (Exception e) {
		   System.out.println("获取相关信息。。。。。。。。。。。。失败");
		}

		Iterator iter = fileItems.iterator(); // 依次处理每个上传的文件
		while (iter.hasNext()) {

			FileItem item = (FileItem) iter.next();// 忽略其他不是文件域的所有表单信息
			if (!item.isFormField()) {

				String name = item.getName();
				System.out.println("FileName===="+name);

				File fNew = new File(loadpath, name);

				try {

					item.write(fNew);
					System.out.println("..........Uploaded Successed");
				} catch (Exception e) {
                    System.out.println("An Error occured!");
					e.printStackTrace();
				}

			} else // 取出不是文件域的所有表单信息
			{
				String fieldvalue = item.getString();

			}
		}

	}

}
</pre>

> 
> 
  <p>
>     请看我们的下一篇文章：<a href="http://toozhao.com/2011/06/android-%E6%8B%8D%E7%85%A7%E5%B9%B6%E4%B8%8A%E4%BC%A0%E5%9B%BE%E7%89%87%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%BA%90%E7%A0%81/" target="_blank">Android 拍照并上传图片到服务器源码</a>
>   </p>

> 
> 
  <blockquote>
>     <p>
>       android端源码和web 端源码：http://115.com/file/bevc7e16#uploadsome.rar
>     </p>
>   </blockquote>
