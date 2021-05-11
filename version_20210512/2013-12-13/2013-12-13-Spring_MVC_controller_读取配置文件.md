#Spring MVC controller 读取配置文件
###发表时间：2013-12-13
###分类：java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1989026" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1989026</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>用Spring的MVC做开发有段时间里。天天打交道的就是各种的controller。</p> 
 <p>今天遇到一个问题，需要读取配置文件configure.properties，通过“注释”方式注入给controller。</p> 
 <p>spring的读取配置如下：</p> 
 <pre name="code" class="java">	&lt;bean
		class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer"&gt;
		&lt;property name="locations"&gt;
			&lt;list&gt;
				&lt;value&gt;classpath:config/configure.properties&lt;/value&gt;
			&lt;/list&gt;
		&lt;/property&gt;
	&lt;/bean&gt;</pre> 
 <p>我的spring的XML配置文件如下：</p> 
 <pre name="code" class="java">spring-ctx-application.xml
spring-ctx-repository.xml
spring-mvc-servlet.xml</pre> 
 <p>&nbsp;我把PropertyPlaceholderConfigurer的XML配置放到了spring-ctx-application.xml里面。配置文件和controller的代码如下：</p> 
 <pre name="code" class="java">page.query.rownum=10</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Value("${page.query.rownum}")
	private String pageQueryRownum;
	
	
	public void setPageQueryRownum(String pageQueryRownum) {
		this.pageQueryRownum = pageQueryRownum;
	}</pre> 
 <p>但是发现了一个问题，被注入的&nbsp;pageQueryRownum 并没有打印出我期望的数字 10， 而是打印出来了${page.query.rownum}。让我困惑。</p> 
 <p>后来找到了问题，我把PropertyPlaceholderConfigurer的XML配置放到了spring-mvc-servlet.xml的xml中，问题就解决了。看了老外写的东西，才知道，这是不同的spring context，才造成配置在&nbsp;spring-ctx-application.xml的配置信息无法读取到。而我的springMVC的配置信息都在spring-mvc-servlet.xml中。为了让controller读取到配置文件，需要把PropertyPlaceholderConfigurer的XML配置到同样的context的spring-mvc-servlet.xml中，问题就解决了。</p> 
 <p>参考：</p> 
 <p><a href="http://stackoverflow.com/questions/5275724/spring-3-0-5-doesnt-evaluate-value-annotation-from-properties">http://stackoverflow.com/questions/5275724/spring-3-0-5-doesnt-evaluate-value-annotation-from-properties</a></p> 
 <p><a href="http://stackoverflow.com/questions/11890544/spring-value-annotation-in-controller-class-not-evaluating-to-value-inside-pro">http://stackoverflow.com/questions/11890544/spring-value-annotation-in-controller-class-not-evaluating-to-value-inside-pro</a></p> 
 <p>&nbsp;</p> 
</div>