#Caused by: java.lang.AbstractMethodError: org.apache.xerces.jaxp.DocumentBuilder
###发表时间：2019-05-20
###分类：java,经验,XML
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2441105" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2441105</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>异常信息：Caused by: java.lang.AbstractMethodError: org.apache.xerces.jaxp.DocumentBuilderFactoryImpl.setFeature(Ljava/lang/String;Z)V&nbsp;</p> 
 <p>异常原因：在系统中存在着多个解析器的时候，这时候程序无法选择解析器。需要人工指定解析器。&nbsp;</p> 
 <p>解决方案：System.setProperty("javax.xml.parsers.DocumentBuilderFactory","com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderFactoryImpl");&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>异常信息举例：</p> 
 <pre name="code" class="java">信息: Loading 'hazelcast-default.xml' from the classpath.
Exception in thread "main" java.lang.AbstractMethodError: javax.xml.parsers.DocumentBuilderFactory.setFeature(Ljava/lang/String;Z)V
	at com.hazelcast.config.XmlConfigBuilder.parse(XmlConfigBuilder.java:188)
	at com.hazelcast.config.XmlConfigBuilder.parseAndBuildConfig(XmlConfigBuilder.java:154)
	at com.hazelcast.config.XmlConfigBuilder.build(XmlConfigBuilder.java:146)
	at com.hazelcast.config.XmlConfigBuilder.build(XmlConfigBuilder.java:139)
	at com.hazelcast.instance.HazelcastInstanceFactory.newHazelcastInstance(HazelcastInstanceFactory.java:153)
	at com.hazelcast.core.Hazelcast.newHazelcastInstance(Hazelcast.java:91)
	at Test.test013(Test.java:36)
	at Test.main(Test.java:28)
</pre> 
 <p>&nbsp;</p> 
</div>