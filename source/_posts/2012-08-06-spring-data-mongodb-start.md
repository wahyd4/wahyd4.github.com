---
title: Spring Data MongoDB 简单使用
author: wahyd4
comments: true
layout: post
permalink: /2012/08/spring-data-mongodb-start/
categories:
  - java
  - mongodb
tags:
  - java
  - mongo
  - Spring
  - 入门
---
> <img class="alignnone" title="mongo" src="/images/2012/07/logo-mongoDB.png" alt="" width="217" height="90" />

这篇文章，主要是作为一个记录，记录我一个小时之前搞定这个东西的兴奋心情。spring mongodb主要是mongodb-java-driver 进行了一些封装，然后可以配合强大的spring使用。我觉得可以简单把它看成一个mongo的”ORM”框架。通过我从星期五到星期天的捣腾，我发现熟悉spring 框架本身其实是最重要的。好下面直接上吧：

首先我在eclipse里面建了一个maven项目，你需要添加如下依赖信息(这里用到的spring框架是3.0.6.RELEASE版本)：

<pre class="brush: xml; title: ; notranslate" title="">&lt;properties&gt;
 &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
 &lt;spring.version&gt;3.0.6.RELEASE&lt;/spring.version&gt;
 &lt;slf4j.version&gt;1.6.1&lt;/slf4j.version&gt;
 &lt;/properties&gt;

&lt;dependencies&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;junit&lt;/groupId&gt;
 &lt;artifactId&gt;junit&lt;/artifactId&gt;
 &lt;version&gt;4.8.1&lt;/version&gt;
 &lt;scope&gt;test&lt;/scope&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.springframework.data&lt;/groupId&gt;
 &lt;artifactId&gt;spring-data-mongodb&lt;/artifactId&gt;
 &lt;version&gt;1.0.2.RELEASE&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;log4j&lt;/groupId&gt;
 &lt;artifactId&gt;log4j&lt;/artifactId&gt;
 &lt;version&gt;1.2.16&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
 &lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;
 &lt;version&gt;${slf4j.version}&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
 &lt;artifactId&gt;jcl-over-slf4j&lt;/artifactId&gt;
 &lt;version&gt;${slf4j.version}&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
 &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
 &lt;version&gt;${slf4j.version}&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;!-- Spring dependencies --&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.springframework&lt;/groupId&gt;
 &lt;artifactId&gt;spring-core&lt;/artifactId&gt;
 &lt;version&gt;${spring.version}&lt;/version&gt;
 &lt;exclusions&gt;
 &lt;exclusion&gt;
 &lt;groupId&gt;commons-logging&lt;/groupId&gt;
 &lt;artifactId&gt;commons-logging&lt;/artifactId&gt;
 &lt;/exclusion&gt;
 &lt;/exclusions&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.springframework&lt;/groupId&gt;
 &lt;artifactId&gt;spring-test&lt;/artifactId&gt;
 &lt;version&gt;${spring.version}&lt;/version&gt;
 &lt;scope&gt;test&lt;/scope&gt;
 &lt;exclusions&gt;
 &lt;exclusion&gt;
 &lt;groupId&gt;commons-logging&lt;/groupId&gt;
 &lt;artifactId&gt;commons-logging&lt;/artifactId&gt;
 &lt;/exclusion&gt;
 &lt;/exclusions&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.springframework&lt;/groupId&gt;
 &lt;artifactId&gt;spring-context&lt;/artifactId&gt;
 &lt;version&gt;${spring.version}&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.springframework&lt;/groupId&gt;
 &lt;artifactId&gt;spring-aop&lt;/artifactId&gt;
 &lt;version&gt;${spring.version}&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;cglib&lt;/groupId&gt;
 &lt;artifactId&gt;cglib&lt;/artifactId&gt;
 &lt;version&gt;2.2&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.mongodb&lt;/groupId&gt;
 &lt;artifactId&gt;mongo-java-driver&lt;/artifactId&gt;
 &lt;version&gt;2.8.0&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;dependency&gt;
 &lt;groupId&gt;org.springframework.data&lt;/groupId&gt;
 &lt;artifactId&gt;spring-data-commons-core&lt;/artifactId&gt;
 &lt;version&gt;1.2.1.RELEASE&lt;/version&gt;
 &lt;/dependency&gt;
 &lt;/dependencies&gt;

</pre>

由于这里面的某些依赖可能maven中央仓库没有，所以请在pom里添加下面两个spring的仓库:

<pre class="brush: xml; title: ; notranslate" title="">&lt;repository&gt;
 &lt;id&gt;spring-maven-release&lt;/id&gt;
 &lt;name&gt;Spring Maven Release Repository&lt;/name&gt;
 &lt;url&gt;http://maven.springframework.org/release&lt;/url&gt;
 &lt;/repository&gt;
 &lt;repository&gt;
 &lt;id&gt;spring-maven-milestone&lt;/id&gt;
 &lt;name&gt;Spring Maven Milestone Repository&lt;/name&gt;
 &lt;url&gt;http://maven.springframework.org/milestone&lt;/url&gt;
 &lt;/repository&gt;

</pre>

下面进行我们的代码编写,首先我们需要一个简单的java POJO类:person.java用于存储人的信息，其有三个属性：id(和mongodb中的ObjectId对应)，name-姓名，age-年龄。

<pre class="brush: java; title: ; notranslate" title="">package com.toozhao.mongo.bean;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

/**
 *
 * @author Junv
 *
 */
@Document
public class Person {

@Id
 private String id;
 private String name;
 private int age;

public Person() {

}

public Person(String name, int age) {
 this.name = name;
 this.age = age;
 }

public String getId() {
 return id;
 }

public String getName() {
 return name;
 }

public void setId(String id) {
 this.id = id;
 }

public void setName(String name) {
 this.name = name;
 }

public void setAge(int age) {
 this.age = age;
 }

public int getAge() {
 return age;
 }

@Override
 public String toString() {
 return "Person [id=" + id + ", name=" + name + ", age=" + age + "]";
 }

}

</pre>

然后我们定义一个执行操作的接口，和其实现类，这里可以看做是一个dao模式。在接口中我们只定义了保存对象和查询一条记录两个方法。

<pre class="brush: java; title: ; notranslate" title="">package com.toozhao.mongo.repository;

import com.toozhao.mongo.bean.Person;
/**
 *
 * @author Junv
 *
 */
public interface MongoAction {

 public void saveObject(Person objToSave);

 public Person findObject(String id);

}

</pre>

实现类：

<pre class="brush: java; highlight: [11,14]; title: ; notranslate" title="">package com.toozhao.mongo.repository;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoOperations;
import org.springframework.data.mongodb.core.query.Criteria;
import org.springframework.data.mongodb.core.query.Query;
import org.springframework.stereotype.Repository;

import com.toozhao.mongo.bean.Person;

@Repository
public class PersonActionImp implements MongoAction {

@Autowired
 MongoOperations operation;

public void saveObject(Person objToSave) {
 operation.insert(objToSave);

}

public Person findObject(String id) {
 return operation.findOne(new Query(Criteria.where("_id").is(id)),
 Person.class);

}

}

</pre>

@repository,和@autowired是spring框架中的，主要功能是起到类似反射的作用吧，具体我还没弄得很清楚。

写一个有main方法的java类，对功能进行简单测试：

<pre class="brush: java; highlight: [20,21,23]; title: ; notranslate" title="">package com.toozhao.mongo;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.toozhao.mongo.bean.Person;
import com.toozhao.mongo.repository.MongoAction;

public class MainTest {

private static final Log log = LogFactory.getLog(MainTest.class);

public static void main(String[] args) {

log.info("initial -----------------");
 ConfigurableApplicationContext context = null;
 //实例化appliaction Context对象
 context = new ClassPathXmlApplicationContext(
 "META-INF/spring/applicationContext.xml");
 //获取一个MongoAction Bean，以便后面执行相关操作
 MongoAction action = context.getBean(MongoAction.class);
 Person person = new Person("Tom", 11);

 action.saveObject(person);
 log.info("结果为：" + action.findObject(person.getId()));

}

}

</pre>

最后，贴出applicationContext文档，里面主要对mongodb进行了简单的配置，和设置了repository的扫描目录（和@repository对应）。

<pre class="brush: xml; highlight: [46]; title: ; notranslate" title="">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xmlns:context="http://www.springframework.org/schema/context"
 xmlns:mongo="http://www.springframework.org/schema/data/mongo"
 xsi:schemaLocation=
 "http://www.springframework.org/schema/context

http://www.springframework.org/schema/context/spring-context-3.0.xsd


http://www.springframework.org/schema/data/mongo


http://www.springframework.org/schema/data/mongo/spring-mongo-1.0.xsd


http://www.springframework.org/schema/beans


http://www.springframework.org/schema/beans/spring-beans-3.0.xsd"&gt;

 &lt;context:annotation-config/&gt;

&lt;context:component-scan base-package="com.toozhao.mongo.repository"&gt;
 &lt;context:exclude-filter type="annotation" expression="org.springframework.context.annotation.Configuration"/&gt;
 &lt;/context:component-scan&gt;

 &lt;!-- Default bean name is 'mongo' --&gt;
 &lt;mongo:mongo host="localhost" port="27017"&gt;
 &lt;mongo:options connections-per-host="8"
 threads-allowed-to-block-for-connection-multiplier="4"
 connect-timeout="1000"
 max-wait-time="1500"
 auto-connect-retry="true"
 socket-keep-alive="true"
 socket-timeout="1500"
 slave-ok="true"
 write-number="1"
 write-timeout="0"
 write-fsync="true"/&gt;
 &lt;/mongo:mongo&gt;
 &lt;!-- xml 配置mongoTemplate--&gt;
 &lt;bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate"&gt;
 &lt;constructor-arg ref="mongo"/&gt;
 &lt;constructor-arg name="databaseName" value="junv"/&gt;
 &lt;/bean&gt;

 &lt;!-- Use this post processor to translate any MongoExceptions thrown in @Repository annotated classes --&gt;
 &lt;bean class="org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor"/&gt;

&lt;/beans&gt;

</pre>

当然你还需要做的就是运行这个项目，我们需要在pom.xml里面添加如下代码,<mainClass>为你需要运行的类：

<pre class="brush: xml; highlight: [7]; title: ; notranslate" title="">&lt;plugin&gt;
 &lt;groupId&gt;org.codehaus.mojo&lt;/groupId&gt;
 &lt;artifactId&gt;exec-maven-plugin&lt;/artifactId&gt;
 &lt;version&gt;1.1.1&lt;/version&gt;
 &lt;!-- 你需要执行的类， --&gt;
 &lt;configuration&gt;
 &lt;mainClass&gt;com.toozhao.mongo.MainTest&lt;/mainClass&gt;
 &lt;/configuration&gt;
 &lt;/plugin&gt;

</pre>

最后，使用 mvn exec:java 就可以运行代码了，当然你在有main方法那个类，右键以java程序的方式也可以运行。结果就是你应该可以看到程序像数据库junv.person中插入了一条数据。
