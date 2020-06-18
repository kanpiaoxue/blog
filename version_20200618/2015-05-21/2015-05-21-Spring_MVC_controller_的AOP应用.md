#Spring MVC controller 的AOP应用
###发表时间：2015-05-21
###分类：java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2213108" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2213108</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在使用Spring MVC的时候，一般会有至少2个Spring的XML。一个用来配置一般的Spring的Bean（如：spring-ctx-application.xml），一个用来声明Spring Controller对于的view的内容（如：spring-mvc-servlet.xml）。</p> 
 <p>很多人发现在<span style="line-height: 1.5;">spring-ctx-application.xml里面声明AOP对Controller不起作用，这是为什么呢？因为Spring MVC里面的一般性配置</span><span style="line-height: 1.5;">spring-ctx-application.xml是一个上下文，而管理Spring MVC的</span><span style="line-height: 1.5;">spring-mvc-servlet.xml又是一个上下文。对Controller的配置都在</span><span style="line-height: 1.5;">spring-mvc-servlet.xml这个里面。也就是说存在2个不同的Spring上下文。你配置在</span><span style="line-height: 1.5;">spring-ctx-application.xml的堆Controller的AOP当然不起作用了。如何修改呢？在</span><span style="line-height: 1.5;">spring-mvc-servlet.xml里面再添加一份AOP的配置即可。同样的道理，在Controller里面配置@Value，也需要在</span><span style="line-height: 1.5;">spring-mvc-servlet.xml里面指定.properties的配置文件，才能正确的读取内容。</span></p> 
 <p><span style="line-height: 1.5;">spring-mvc-servlet.xml</span><span style="line-height: 1.5;">如下：</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:jee="http://www.springframework.org/schema/jee"
	xmlns:jms="http://www.springframework.org/schema/jms" xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:oxm="http://www.springframework.org/schema/oxm"
	xmlns:p="http://www.springframework.org/schema/p" xmlns:sec="http://www.springframework.org/schema/security"
	xmlns:task="http://www.springframework.org/schema/task" xmlns:tx="http://www.springframework.org/schema/tx"

	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-4.0.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-4.0.xsd
		http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-4.0.xsd
		http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-4.0.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
		http://www.springframework.org/schema/oxm http://www.springframework.org/schema/oxm/spring-oxm-4.0.xsd
		http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security-4.0.xsd
		http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-4.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd"&gt;
	&lt;bean
		class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer"&gt;
		&lt;property name="locations"&gt;
			&lt;list&gt;
				&lt;value&gt;classpath:console-configure.properties&lt;/value&gt;
			&lt;/list&gt;
		&lt;/property&gt;
	&lt;/bean&gt;

	&lt;mvc:annotation-driven /&gt;

	&lt;context:component-scan base-package="com.kanpiaoxue.rigel.dmap.console.controller" /&gt;
	
	
	&lt;aop:aspectj-autoproxy /&gt;
		&lt;bean id="performanceCalculate" class="com.kanpiaoxue.rigel.dmap.console.utils.PerformanceCalculateController"&gt;
		&lt;property name="order" value="100" /&gt;
	&lt;/bean&gt;
	
	&lt;bean class="com.kanpiaoxue.rigel.dmap.console.utils.DmapExceptionResolver" /&gt;
    
    &lt;bean class="org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter" &gt;
        &lt;property name="messageConverters"&gt;
            &lt;list&gt;  
                &lt;ref bean="mappingJacksonHttpMessageConverter"/&gt;  
            &lt;/list&gt;  
        &lt;/property&gt;
    &lt;/bean&gt;
    
    &lt;bean id="mappingJacksonHttpMessageConverter" 
        class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"&gt;  
        &lt;property name="supportedMediaTypes"&gt;  
            &lt;list&gt;
                &lt;value&gt;text/html;charset=UTF-8&lt;/value&gt;
                &lt;value&gt;text/javascript;charset=UTF-8&lt;/value&gt;
            &lt;/list&gt;
        &lt;/property&gt;  
    &lt;/bean&gt;
    
	&lt;bean
		class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver"&gt;
		&lt;property name="mediaTypes"&gt;
			&lt;map&gt;
				&lt;entry key="html" value="text/html" /&gt;
				&lt;entry key="json" value="application/json" /&gt;
				&lt;entry key="xml" value="application/xml" /&gt;
			&lt;/map&gt;
		&lt;/property&gt;
		&lt;property name="viewResolvers"&gt;
			&lt;list&gt;
				&lt;bean
					class="org.springframework.web.servlet.view.InternalResourceViewResolver"&gt;
					&lt;property name="viewClass"
						value="org.springframework.web.servlet.view.JstlView" /&gt;
					&lt;property name="prefix" value="/WEB-INF/views/" /&gt;
					&lt;property name="suffix" value=".jsp" /&gt;
				&lt;/bean&gt;
			&lt;/list&gt;
		&lt;/property&gt;
&lt;!-- 		&lt;property name="defaultViews"&gt;
			&lt;list&gt;
				&lt;bean
					class="org.springframework.web.servlet.view.json.MappingJacksonJsonView" /&gt;
			&lt;/list&gt;
		&lt;/property&gt; --&gt;
	&lt;/bean&gt;


	&lt;bean id="multipartResolver"
		class="org.springframework.web.multipart.commons.CommonsMultipartResolver"
		p:defaultEncoding="UTF-8"&gt;
		&lt;property name="resolveLazily" value="true" /&gt;
		&lt;property name="maxUploadSize" value="${file.upload.max.size}" /&gt;
		&lt;property name="maxInMemorySize" value="${file.upload.max.in.memory.size}" /&gt;
	&lt;/bean&gt;

	&lt;!-- cache start --&gt;
	&lt;!-- &lt;bean id="cacheManager" class="org.springframework.cache.ehcache.EhCacheCacheManager"
		p:cache-manager-ref="ehcache" /&gt;

	EhCache library setup
	&lt;bean id="ehcache"
		class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean"&gt;
		&lt;property name="configLocation" value="classpath:${dmap.console.cache.file}" /&gt;
	&lt;/bean&gt; --&gt;
	&lt;!-- cache end --&gt;
	
&lt;/beans&gt;
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><span style="line-height: 1.5;">AOP范例类如下：</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package com.kanpiaoxue.rigel.dmap.console.utils;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.core.Ordered;

import com.google.common.base.Stopwatch;

/**
 * &lt;pre&gt;
 * <span style="line-height: 1.5;">PerformanceCalculateController </span><span style="font-size: 1em; line-height: 1.5;">.java</span></pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java"> * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月29日 下午3:47:10&lt;br&gt;
 * Description : AOP性能切面类
 * &lt;/pre&gt;
 */
@Aspect
public class PerformanceCalculateController implements Ordered {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(PerformanceCalculate.class);

    private int order = 1;

    /**
     * &lt;pre&gt;
     * 统计指定切面的方法的耗时，单位：毫秒
     *  @param point
     *  @return
     *  @throws Throwable
     * &lt;/pre&gt;
     */
    @Around("execution(* com.kanpiaoxue.rigel.dmap.console.controller.*.*(..))")
    public Object calculateConsume(ProceedingJoinPoint point) throws Throwable {

        Object[] args = point.getArgs();
        Stopwatch watch = Stopwatch.createStarted();
        Object rs = null;
        if (null != args) {
            rs = point.proceed(args);
        } else {
            rs = point.proceed();
        }
        String className = point.getTarget().getClass().getName();
        String methodName = point.getSignature().getName();
        if (LOGGER.isDebugEnabled()) {
            LOGGER.debug(String.format("%s.%s consumes %s.", className,
                    methodName, watch.toString()));
        }
        return rs;
    }

    @Override
    public int getOrder() {
        return this.order;
    }

    public void setOrder(int order) {
        this.order = order;
    }

}
</pre> 
 <p><span style="line-height: 1.5;">&nbsp;</span></p> 
</div>