#spring-retry的xml配置用法
###发表时间：2019-02-01
###分类：Spring,springboot,java,spring-retry
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2437327" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2437327</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>spring-retry的很多例子都是基于springboot来使用的。都是在springboot的Application类上面添加&nbsp;<span style="background-color: transparent; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; white-space: pre; color: #24292e;">@EnableRetry 注释开启retry的功能。但是原有的基于xml的spring的项目如何使用spring-retry 呢？</span></p> 
 <p><span style="background-color: transparent; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; white-space: pre; color: #24292e;">如下，在 xml 的配置中添加：</span></p> 
 <pre name="code" class="java">&lt;bean class="org.springframework.retry.annotation.RetryConfiguration" /&gt;</pre> 
 <p><span style="background-color: transparent; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; white-space: pre; color: #24292e;">&nbsp;完整例子如下：</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:cache="http://www.springframework.org/schema/cache"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:jdbc="http://www.springframework.org/schema/jdbc"
	xmlns:jee="http://www.springframework.org/schema/jee"
	xmlns:jms="http://www.springframework.org/schema/jms"
	xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:oxm="http://www.springframework.org/schema/oxm"
	xmlns:p="http://www.springframework.org/schema/p"
	xmlns:sec="http://www.springframework.org/schema/security"
	xmlns:task="http://www.springframework.org/schema/task"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:util="http://www.springframework.org/schema/util"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd         http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.0.xsd         http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd         http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-4.0.xsd         http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-4.0.xsd         http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-4.0.xsd         http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-4.0.xsd         http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd         http://www.springframework.org/schema/oxm http://www.springframework.org/schema/oxm/spring-oxm-4.0.xsd         http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security-4.0.xsd         http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-4.0.xsd         http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd         http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-4.0.xsd         http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd"&gt;
	&lt;context:annotation-config /&gt;
	&lt;aop:aspectj-autoproxy /&gt;

	&lt;bean id="propertyConfigurer"
		class="org.springframework.beans.factory.config.PropertiesFactoryBean"&gt;
		&lt;property name="locations"&gt;
			&lt;list&gt;
				&lt;value&gt;classpath:retry/config.properties&lt;/value&gt;
			&lt;/list&gt;
		&lt;/property&gt;
	&lt;/bean&gt;

	&lt;context:component-scan
		base-package="org.kanpiaoxue"&gt;
		&lt;context:exclude-filter type="annotation"
			expression="org.springframework.stereotype.Controller" /&gt;
		&lt;context:exclude-filter type="annotation"
			expression="org.springframework.web.bind.annotation.ControllerAdvice" /&gt;
	&lt;/context:component-scan&gt;
	&lt;!-- 开启spring-retry --&gt;
	&lt;bean class="org.springframework.retry.annotation.RetryConfiguration" /&gt;

&lt;/beans&gt;</pre> 
 <p><span style="background-color: transparent; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; white-space: pre; color: #24292e;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
</div>