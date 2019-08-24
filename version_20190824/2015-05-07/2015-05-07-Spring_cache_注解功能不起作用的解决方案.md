#Spring cache 注解功能不起作用的解决方案
###发表时间：2015-05-07
###分类：ehcache,java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2209257" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2209257</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>最近使用spring的cache模块来加速程序，写了很多注解，如：&nbsp;@Cacheable/@CachePut/@CacheEvict/@Caching</p> 
 <p>发现这些注解根本不起作用啊。赶紧跑去看了看spring的文档，发现缺失了下面内容：</p> 
 <p>&lt;cache:annotation-driven/&gt;&nbsp;</p> 
 <p>之后我的配置文件如下：</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">	
&lt;!-- cache start --&gt;
	&lt;cache:annotation-driven cache-manager="cacheManager"/&gt; 
	&lt;bean id="cacheManager" class="org.springframework.cache.ehcache.EhCacheCacheManager"
		p:cache-manager-ref="ehcache" /&gt;

	&lt;!-- EhCache spring library setup --&gt;
	&lt;bean id="ehcache"
		class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean"
		p:configLocation="classpath:${dmap.console.cache.file}" p:shared="true" /&gt;

	&lt;!-- cache end --&gt;</pre> 
 <p>&nbsp;</p> 
 <p>参考下面xml添加上cache的schema</p> 
 <pre name="code" class="xml">&lt;beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:cache="http://www.springframework.org/schema/cache"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd"&gt;

        &lt;cache:annotation-driven /&gt;

&lt;/beans&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;经过添加&nbsp;<span style="font-family: monospace; line-height: 1.5; background-color: #fafafa;">&lt;cache:annotation-driven cache-manager="cacheManager"/&gt; 之后我的cache注解能用了。&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p>spring的原文如下：</p> 
 <div class="titlepage" style="margin: 0pt; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium; line-height: 25.6000003814697px;"> 
  <div style="margin: 0pt;"> 
   <div style="margin: 0pt;"> 
    <h3 class="title" style="">30.3.6&nbsp;Enable caching annotations</h3> 
   </div> 
  </div> 
 </div> 
 <p style="margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium; line-height: 25.6000003814697px;">It is important to note that even though declaring the cache annotations does not automatically trigger their actions - like many things in Spring, the feature has to be declaratively enabled (which means if you ever suspect caching is to blame, you can disable it by removing only one configuration line rather than all the annotations in your code).</p> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium; line-height: 25.6000003814697px;">To enable caching annotations add the annotation&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap; background-color: #f2f2f2;">@EnableCaching</code>&nbsp;to one of your&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap; background-color: #f2f2f2;">@Configuration</code>&nbsp;classes:</p> 
 <pre class="programlisting"><em><span class="hl-annotation" style="color: gray;">@Configuration</span></em>
<em><span class="hl-annotation" style="color: gray;">@EnableCaching</span></em>
<span class="hl-keyword" style="color: #7f0055; font-weight: bold;">public</span> <span class="hl-keyword" style="color: #7f0055; font-weight: bold;">class</span> AppConfig {
}</pre> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium; line-height: 25.6000003814697px;">Alternatively for XML configuration use the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap; background-color: #f2f2f2;">cache:annotation-driven</code>&nbsp;element:</p> 
 <pre class="programlisting"><span class="hl-tag" style="color: #3f7f7f;">&lt;beans</span> <span class="hl-attribute" style="color: #7f007f;">xmlns</span>=<span class="hl-value" style="color: #2a00ff;">"http://www.springframework.org/schema/beans"</span>
    <span class="hl-attribute" style="color: #7f007f;">xmlns:xsi</span>=<span class="hl-value" style="color: #2a00ff;">"http://www.w3.org/2001/XMLSchema-instance"</span>
    <span class="hl-attribute" style="color: #7f007f;">xmlns:cache</span>=<span class="hl-value" style="color: #2a00ff;">"http://www.springframework.org/schema/cache"</span>
    <span class="hl-attribute" style="color: #7f007f;">xsi:schemaLocation</span>=<span class="hl-value" style="color: #2a00ff;">"
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/cache http://www.springframework.org/schema/cache/spring-cache.xsd"</span><span class="hl-tag" style="color: #3f7f7f;">&gt;</span>

        <span class="hl-tag" style="color: #3f7f7f;">&lt;cache:annotation-driven /&gt;</span>

<span class="hl-tag" style="color: #3f7f7f;">&lt;/beans&gt;</span></pre> 
 <p>&nbsp;</p> 
</div>