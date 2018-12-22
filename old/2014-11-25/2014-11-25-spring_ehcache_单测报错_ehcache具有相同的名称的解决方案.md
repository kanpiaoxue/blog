#spring ehcache 单测报错：ehcache具有相同的名称的解决方案
###发表时间：2014-11-25
###分类：java,Spring,ehcache
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2159995" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2159995</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <h2 class="date-header" style="margin-bottom: 0px; font-weight: normal; font-size: 14px; line-height: normal; font-family: 'Trebuchet MS', Trebuchet, sans-serif; color: #666666;">地址：<a href="http://www.captaindebug.com/2012/09/spring-31-caching-and-ehcache.html#.VHPs-568eCk">&nbsp;http://www.captaindebug.com/2012/09/spring-31-caching-and-ehcache.html#.VHPs-568eCk</a> </h2> 
 <h2 class="date-header" style="margin-bottom: 0px; font-weight: normal; font-size: 14px; line-height: normal; font-family: 'Trebuchet MS', Trebuchet, sans-serif; color: #666666;">&nbsp;</h2> 
 <h2 class="date-header" style="margin-bottom: 0px; font-weight: normal; font-size: 14px; line-height: normal; font-family: 'Trebuchet MS', Trebuchet, sans-serif; color: #666666;">Tuesday, 25 September 2012</h2> 
 <div class="date-posts" style="color: #757575; font-family: 'Trebuchet MS', Trebuchet, sans-serif; font-size: 13px; line-height: 18.2000007629395px;"> 
  <div class="post-outer"> 
   <div class="post hentry" style=""> 
    <a name="4479616670707995134"></a> 
    <h3 class="post-title entry-title" style="margin-top: 20px; margin-bottom: 0px;">Spring 3.1: Caching and EhCache</h3> 
    <div class="post-header" style="line-height: 1.6; margin-top: 0px; margin-right: 0px; margin-left: 0px;">
     &nbsp;
    </div> 
    <div id="post-body-4479616670707995134" class="post-body entry-content" style="width: 810px; line-height: 1.4;">
     If you look around the web for examples of using Spring 3.1’s built in caching then you’ll usually bump into Spring’s&nbsp;
     <a style="color: #d8970a;" href="http://www.captaindebug.com/2012/09/spring-31-caching-and-config.html" target="new"><tt>SimpleCacheManager</tt></a>, which the Guys at Spring say is “Useful for testing or simple caching declarations”. I actually prefer to think of&nbsp;
     <tt>SimpleCacheManager</tt>&nbsp;as lightweight rather than simple; useful in those situations where you want a small in memory cache on a per JVM basis. If the Guys at Spring were running a supermarket then&nbsp;
     <tt>SimpleCacheManager</tt>would be in their own brand ‘basics’ product range.
     <br>
     <br>If, on the other hand, you need a heavy duty cache, one that’s scalable, persistent and distributed, then Spring also comes with a built in
     <a style="color: #d8970a;" href="http://ehcache.org/" target="new">ehCache</a>&nbsp;wrapper.
     <a name="more"></a>&nbsp;
     <br>
     <br>The good news is that swapping between Spring's caching implementations is easy. In theory it’s all a matter of configuration and, to prove the theory correct, I took the sample code from my&nbsp;
     <a style="color: #d8970a;" href="http://www.captaindebug.com/2012/09/spring-31-caching-and-cacheable.html" target="new">Caching and&nbsp;<tt>@Cacheable</tt></a>&nbsp;blog and ran it using an EhCache implementation.
     <br>
     <br>The configuration steps are similar to those described in my last blog&nbsp;
     <a style="color: #d8970a;" href="http://www.captaindebug.com/2012/09/spring-31-caching-and-config.html" target="new">Caching and Config</a>&nbsp;in that you still need to specify:
     <br>
     <br>
     <pre class="pp_xml">&lt;cache:annotation-driven /&gt;
</pre> 
     <br>...in your Spring config file to switch caching on. You also need to define a bean with an id of&nbsp;
     <tt>cacheManager</tt>, only this time you reference Spring’s&nbsp;
     <tt>EhCacheCacheManager</tt>&nbsp;class instead of&nbsp;
     <tt>SimpleCacheManager</tt>.
     <br>
     <br>
     <pre class="pp_xml">&lt;bean id="cacheManager"
    class="org.springframework.cache.ehcache.EhCacheCacheManager"
    p:cacheManager-ref="ehcache"/&gt;
</pre> 
     <br>The example above demonstrates an&nbsp;
     <tt>EhCacheCacheManager</tt>&nbsp;configuration. Notice that it references a second bean with an id of '
     <tt>ehcache</tt>'. This is configured as follows:
     <br>
     <br>
     <pre class="pp_xml">&lt;bean id="ehcache" class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean"
    p:configLocation="ehcache.xml"
    p:shared="true"/&gt;
</pre> 
     <br>"
     <tt>ehcache</tt>" has two properties:&nbsp;
     <tt>configLocation</tt>&nbsp;and&nbsp;
     <tt>shared</tt>.
     <br>
     <br>'
     <tt>configLocation</tt>' is an optional attribute that’s used to specify the location of an ehcache configuration file. In my test code I used the following example file:
     <br>
     <br>
     <pre class="pp_xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"&gt;
    &lt;defaultCache eternal="true" maxElementsInMemory="100" overflowToDisk="false" /&gt;
    &lt;cache name="employee" maxElementsInMemory="10000" eternal="true" overflowToDisk="false" /&gt;
&lt;/ehcache&gt;
</pre> 
     <br>...which creates two caches: a default cache and one named “employee”.
     <br>
     <br>If this file is missing then the&nbsp;
     <tt>EhCacheManagerFactoryBean</tt>&nbsp;simply picks up a default ehcache config file:&nbsp;
     <tt>ehcache-failsafe.xml</tt>, which is located in ehcache’s&nbsp;
     <tt>ehcache-core</tt>&nbsp;jar file.
     <br>
     <br>The other&nbsp;
     <tt>EhCacheManagerFactoryBean</tt>&nbsp;attribute is '
     <tt>shared</tt>'. This is supposed to be optional as the documentation states that it defines "whether the EHCache CacheManager should be shared (as a singleton at the VM level) or independent (typically local within the application). Default is 'false', creating an independent instance.” However, if this is set to false then you’ll get the following exception:&nbsp;
     <br>
     <br>
     <pre class="pre_text">org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.cache.interceptor.CacheInterceptor#0': Cannot resolve reference to bean 'cacheManager' while setting bean property 'cacheManager'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'cacheManager' defined in class path resource [ehcache-example.xml]: Cannot resolve reference to bean 'ehcache' while setting bean property 'cacheManager'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'ehcache' defined in class path resource [ehcache-example.xml]: Invocation of init method failed; nested exception is net.sf.ehcache.CacheException: Another unnamed CacheManager already exists in the same VM. Please provide unique names for each CacheManager in the config or do one of following:
1. Use one of the CacheManager.create() static factory methods to reuse same CacheManager with same name or create one if necessary
2. Shutdown the earlier cacheManager before creating new one with same name.
The source of the existing CacheManager is: InputStreamConfigurationSource [stream=java.io.BufferedInputStream@424c414]
 at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:328)
 at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveValueIfNecessary(BeanDefinitionValueResolver.java:106)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyPropertyValues(AbstractAutowireCapableBeanFactory.java:1360)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1118)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:517)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:456)
... stack trace shortened for clarity
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:683)
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.run(RemoteTestRunner.java:390)
 at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.main(RemoteTestRunner.java:197)
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'cacheManager' defined in class path resource [ehcache-example.xml]: Cannot resolve reference to bean 'ehcache' while setting bean property 'cacheManager'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'ehcache' defined in class path resource [ehcache-example.xml]: Invocation of init method failed; nested exception is net.sf.ehcache.CacheException: Another unnamed CacheManager already exists in the same VM. Please provide unique names for each CacheManager in the config or do one of following:
1. Use one of the CacheManager.create() static factory methods to reuse same CacheManager with same name or create one if necessary
2. Shutdown the earlier cacheManager before creating new one with same name.
The source of the existing CacheManager is: InputStreamConfigurationSource [stream=java.io.BufferedInputStream@424c414]
 at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:328)
 at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveValueIfNecessary(BeanDefinitionValueResolver.java:106)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyPropertyValues(AbstractAutowireCapableBeanFactory.java:1360)
... stack trace shortened for clarity
 at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:193)
 at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:322)
 ... 38 more
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'ehcache' defined in class path resource [ehcache-example.xml]: Invocation of init method failed; nested exception is net.sf.ehcache.CacheException: Another unnamed CacheManager already exists in the same VM. Please provide unique names for each CacheManager in the config or do one of following:
1. Use one of the CacheManager.create() static factory methods to reuse same CacheManager with same name or create one if necessary
2. Shutdown the earlier cacheManager before creating new one with same name.
The source of the existing CacheManager is: InputStreamConfigurationSource [stream=java.io.BufferedInputStream@424c414]
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1455)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:519)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:456)
 at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:294)
 at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:225)
 at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:291)
 at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:193)
 at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:322)
 ... 48 more
Caused by: net.sf.ehcache.CacheException: Another unnamed CacheManager already exists in the same VM. Please provide unique names for each CacheManager in the config or do one of following:
1. Use one of the CacheManager.create() static factory methods to reuse same CacheManager with same name or create one if necessary
2. Shutdown the earlier cacheManager before creating new one with same name.
The source of the existing CacheManager is: InputStreamConfigurationSource [stream=java.io.BufferedInputStream@424c414]
 at net.sf.ehcache.CacheManager.assertNoCacheManagerExistsWithSameName(CacheManager.java:521)
 at net.sf.ehcache.CacheManager.init(CacheManager.java:371)
 at net.sf.ehcache.CacheManager.(CacheManager.java:339)
 at org.springframework.cache.ehcache.EhCacheManagerFactoryBean.afterPropertiesSet(EhCacheManagerFactoryBean.java:104)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1514)
 at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1452)
 ... 55 more
</pre> 
     <br>...when you try to run a bunch of unit tests.
     <br>
     <br>I think that this comes down to a simple bug Spring’s the ehcache manager factory as it’s trying to create multiple cache instances using
     <tt>new()</tt>&nbsp;rather than using, as the exception states, “one of the CacheManager.create() static factory methods" which allows it to reuse same CacheManager with same name. Hence, my first JUnit test works okay, but all others fail.
     <br>
     <br>
     <div class="separator" style="clear: both; text-align: center;">
      <a style="color: #d8970a; margin-left: 1em; margin-right: 1em;" href="http://3.bp.blogspot.com/-RKSamFir0SU/UGDVAs-SRoI/AAAAAAAAAgo/-mrI7AhzEtQ/s1600/unit%2Btest.png"><img style="border-style: none;" src="http://3.bp.blogspot.com/-RKSamFir0SU/UGDVAs-SRoI/AAAAAAAAAgo/-mrI7AhzEtQ/s320/unit%2Btest.png" alt="" width="320" height="191" border="0"></a>
     </div> 
     <br>The offending line of code is:
     <br>
     <br>
     <pre class="pre_text">this.cacheManager = (this.shared ? CacheManager.create() : new CacheManager());
</pre> 
     <br>My full XML config file is listed below for completeness:
     <br>
     <br>
     <pre class="pp_xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans" 
  xmlns:p="http://www.springframework.org/schema/p"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:cache="http://www.springframework.org/schema/cache" 
  xmlns:context="http://www.springframework.org/schema/context"
   xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
     http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.1.xsd
        http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd"&gt;
 
  &lt;!-- Switch on the Caching --&gt;
   &lt;cache:annotation-driven /&gt;

 &lt;!-- Do the component scan path --&gt;
 &lt;context:component-scan base-package="caching" /&gt;

 &lt;bean id="cacheManager" class="org.springframework.cache.ehcache.EhCacheCacheManager" 
  p:cacheManager-ref="ehcache"/&gt;
 
 &lt;bean id="ehcache" class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean" 
     p:configLocation="ehcache.xml"  
     p:shared="true"/&gt; 
&lt;/beans&gt;
</pre> 
     <br>In using ehcache, the only other configuration details to consider are the Maven dependencies. These are pretty straight forward as the Guys at Ehcache have combined all the various ehcache jars into one Maven&nbsp;
     <em>POM</em>&nbsp;module. This POM module can be added to your project's POM file using the XML below:
     <br>
     <br>
     <pre class="pp_xml">&lt;dependency&gt;
        &lt;groupId&gt;net.sf.ehcache&lt;/groupId&gt;
        &lt;artifactId&gt;ehcache&lt;/artifactId&gt;
        &lt;version&gt;2.6.0&lt;/version&gt;
    &lt;/dependency&gt;
</pre> 
     <br>Finally, the ehcache Jar files are available from both the Maven Central and Sourceforge repositories:
     <br>
     <br>
     <pre class="pp_xml">&lt;repositories&gt;
        &lt;repository&gt;
            &lt;id&gt;sourceforge&lt;/id&gt;
            &lt;url&gt;http://oss.sonatype.org/content/groups/sourceforge/&lt;/url&gt;
            &lt;releases&gt;
                &lt;enabled&gt;true&lt;/enabled&gt;
            &lt;/releases&gt;
            &lt;snapshots&gt;
                &lt;enabled&gt;true&lt;/enabled&gt;
            &lt;/snapshots&gt;
        &lt;/repository&gt;
    &lt;/repositories&gt;
</pre> 
     <p>&nbsp;</p> 
    </div> 
   </div> 
  </div> 
 </div> 
</div>