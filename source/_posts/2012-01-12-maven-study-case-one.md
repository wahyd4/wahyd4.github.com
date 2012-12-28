---
title: Maven 学习入门 1
author: wahyd4
layout: post
permalink: /2012/01/maven-study-case-one/
categories:
  - java
  - MAVEN
  - 各类教程
tags:
  - java
  - maven
  - 入门
  - 教程
---
Maven是一个项目构建工具，它不止可以用于Java，可能大家对Ant更加熟悉，个人感觉Maven相比Ant更加高级，功能也更加丰富，使用比较灵活的构建工具，maven还支持插件，当然也有机遇eclipse的插件m2e。现在还有maven的仓库软件nexus，以及更对可以对maven进行持续集成的服务器Hudson。对于Maven过多的讲解就不再这里提及，希望把这个日志作为一个maven学习的记录。下面我们就来一步一步安装并学习使用Maven：

首先下载并安装maven，进入<http://maven.apache.org/download.html> 下载Maven的已编译好的binary可运行版本。然后将这个压缩文件解压到一个指定目录，比如说D盘。我为了使用方便已经将maven后面的版本号去掉，因为我的文件夹目录为：

<pre class="brush: xml; title: ; notranslate" title="">D:maven</pre>

请下载最新版本3.X版。3.X和2.X的版本有较大差别。

接下来我们需要做的是，配置环境变量：**M2_HOME，**其值为你解压的maven文件夹根目录，比如我的就是D:maven.

添加环境变量 **M2**，其值为%M2_HOME%bin目录。（注：所有配置均在windows下完成）

<pre class="brush: xml; title: ; notranslate" title="">M2_HOME=D:maven;

M2=%M2_HOME%bin;
PATH=$M2:$PATH;
</pre>

保存并退出。然后打开命令行，输入以下命令：**mvn –version**

如果出现类似于下面这些信息，即是安装成功了。

[<img class="alignnone size-medium wp-image-2035" title="111" src="/images/2012/01/111-300x78.png" alt="" width="300" height="78" />][1]

我们也可以通过命令行 **mvn –help**来查看maven 有哪些常用命令。

接下来我们对仓库的相关设置做一个简单设置，windows下默认地maven会自动将**c:usersYOURNAE.m2repository**作为仓库，用来存放下载的类库。个人不太喜欢各种这类东西安装在C盘，这样比较消耗资源。因此请将你的maven文件夹下面的 conf/settings.xml打开，找到：

<pre class="brush: xml; title: ; notranslate" title="">&lt;localRepository&gt;/path/to/local/repo&lt;/localRepository&gt;</pre>

并将其值改成你想要防止仓库的位置，个人建议放在maven程序下的repository目录下，并去掉该语句前后的注释。

紧接着，我们就来创建一个maven项目：

我们选择一步一步来创建项目，使用命令行切换到你需要创建项目的文件夹，在命令行输入：

<pre class="brush: xml; title: ; notranslate" title="">mvn archetype:generate</pre>

然后按照maven的提醒来输入相关信息.

大致解释一下相关属性：

**groupId**：在一个项目或者组织中通常是唯一的标识符，一般以项目或者组织的网址来命名，例：info.junv.test

**artifactId**:类似于给项目取个别名。例：first-app

**version**:项目的版本号。例：1.0-snapshot

**package**:为项目的包名，例：info.junv.test

当程序显示DUILD SUCCESS 时即表示，项目创建成功了，打开创建项目的文件夹就可以看到刚才创建的文件了。

源代码在first-app/src/main下面，first-app/src/test下为测试的相关代码。

并且在first-app代码的根目录下生成了pom.xml，该文件非常重要，里面包含程序的相关包依赖和仓库地址，以及其他项目任务等，这里不多讲。

下面执行有管项目的其他一些操作：（需要在命令行下进入该项目，例：cd fitst-app）

<pre class="brush: xml; title: ; notranslate" title="">mvn package #执行项目打包操作，生成target文件夹，jar文件，以及其他相关文件夹

</pre>

下面是maven官方的一些其他命令，以及解释：

Although hardly a comprehensive list, these are the most common *default* lifecycle phases executed.

*   **validate**: validate the project is correct and all necessary information is available
*   **compile**: compile the source code of the project
*   **test**: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
*   **package**: take the compiled code and package it in its distributable format, such as a JAR.
*   **integration-test**: process and deploy the package if necessary into an environment where integration tests can be run
*   **verify**: run any checks to verify the package is valid and meets quality criteria
*   **install**: install the package into the local repository, for use as a dependency in other projects locally
*   **deploy**: done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects.

There are two other Maven lifecycles of note beyond the *default* list above. They are

*   **clean**: cleans up artifacts created by prior builds

*   **site**: generates site documentation for this project

<span style="line-height: 24px;">   如果需要将源代码编译后并打包：则需要使用package或者install。如果选择install，maven还会将该包存放至本地仓库。<br /> </span>

上面这些都是生成普通的项目结构，其实我们平时使用最多的是eclipse项目。maven也可以生成eclipse项目结构。

<pre class="brush: xml; title: ; notranslate" title="">mvn eclipse:eclipse </pre>

为了删除eclipse的文件结构我们需要使用：

<pre class="brush: xml; title: ; notranslate" title="">mvn eclipse:clean </pre>

这样我们就可以在eclipse中导入maven生成的eclipse项目，最方便的还是在eclipse中安装maven 的eclipse插件m2e。

m2e下载地址：<http://download.eclipse.org/technology/m2e/releases/>

好了，这就是maven的简单应用，希望下一次写pom.xml。

 [1]: /images/2012/01/111.png