---
title: 教你一招:清除你电脑中的垃圾文件(很好用)
author: wahyd4
layout: post
comments: true
permalink: /2010/09/remove-trashes/
categories:
  - 我们爱分享
tags:
  - 电脑
  - 维护
---
作者：Lee

<p style="text-align: center;">
  步骤很简单就两步！<br /> 【方法】新建一个记事本，把下面的文字复制进去,点“另存为”，路径选“桌面”，保存类型为“所有文件”，文件名为“清除系统LJ.bat”，就完成了。记住后缀名一定要是.bat，ok！你的垃圾清除器就这样制作成功了！<br /> 双击它就能很快地清理垃圾文件，大约一分钟不到。
</p>

======就是下面的文字(这行不用复制)=============================

@echo off  
echo 正在清除系统垃圾文件，请稍等……  
del /f /s /q %systemdrive%*.tmp  
del /f /s /q %systemdrive%*._mp  
del /f /s /q %systemdrive%*.log  
del /f /s /q %systemdrive%*.gid  
del /f /s /q %systemdrive%*.chk  
del /f /s /q %systemdrive%*.old  
del /f /s /q %systemdrive%recycled\*.\*  
del /f /s /q %windir%*.bak  
del /f /s /q %windir%prefetch\*.\*  
rd /s /q %windir%temp & md %windir%temp  
del /f /q %userprofile%cookies\*.\*  
del /f /q %userprofile%recent\*.\*  
del /f /s /q “%userprofile%Local SettingsTemporary Internet Files\*.\*“  
del /f /s /q “%userprofile%Local SettingsTemp\*.\*“  
del /f /s /q “%userprofile%recent\*.\*“  
echo 清除系统LJ完成！  
echo. & pause

=====到这里为止(这行不用复制)============================================  
以后只要双击运行该文件，当屏幕提示“清除系统LJ完成！就还你一个“苗条”的系统了！！怎么样？是不是很好用？隔一段时间后，都可以使用该文件来处理产生的垃圾文件。  
注：LJ就是垃圾的意思！这招比那些所谓的优化大师好用！最重要的是无论在公司默认的系统环境还是在自己家中的电脑都不会破坏系统文件

<p style="text-align: center;">
  <a href="http://www.junv.info/wp-content/uploads/2010/09/273e6263c0ac12610c33faa5.gif"></a><a href="http://www.junv.info/wp-content/uploads/2010/09/273e6263c0ac12610c33faa51.gif"><img class="aligncenter size-thumbnail wp-image-433" title="creation." src="http://www.junv.info/wp-content/uploads/2010/09/273e6263c0ac12610c33faa51-150x150.gif" alt="" width="150" height="150" /></a>
</p>
