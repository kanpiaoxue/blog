#eclipse的java-templates.xml
###发表时间：2020-06-22
###分类：eclipse,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2515059" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2515059</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：</p> 
 <p>1、<a href="https://github.com/vogellacompany/saneclipse/blob/master/com.vogella.saneclipse.templates/templates/java-templates.xml">https://github.com/vogellacompany/saneclipse/blob/master/com.vogella.saneclipse.templates/templates/java-templates.xml</a></p> 
 <p>2、<a href="https://howtodoinjava.com/eclipse/create-eclipse-templates-for-faster-java-coding/">https://howtodoinjava.com/eclipse/create-eclipse-templates-for-faster-java-coding/</a></p> 
 <p>3、<a href="https://dzone.com/articles/adding-custom-templates-in-eclipse-for-faster-java">https://dzone.com/articles/adding-custom-templates-in-eclipse-for-faster-java</a></p> 
 <p>&nbsp;</p> 
 <p>模板名称：xpchecknotnull</p> 
 <p>模板内容：</p> 
 <p>${imp:import(java.util.Objects)}</p> 
 <p>Objects.requireNonNull(${name:var}, "${name:var} is null");</p> 
 <p>&nbsp;</p> 
 <p>模板名称：xpisnull</p> 
 <p>模板内容：</p> 
 <p>${imp:import(java.util.Objects)}</p> 
 <p>if (Objects.isNull(${name:var})) {</p> 
 <p>&nbsp; &nbsp; ${cursor}</p> 
 <p>}</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>模板名称：xpnotnull</p> 
 <p>模板内容：</p> 
 <p>${imp:import(java.util.Objects)}</p> 
 <p>if (Objects.nonNull(${name:var})) {</p> 
 <p>&nbsp; &nbsp; ${cursor}</p> 
 <p>}</p> 
 <p>&nbsp;</p> 
 <p>模板名称：xpsysout</p> 
 <p>模板内容：</p> 
 <p>System.out.println(String.format("%s",${name:var}));</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>模板名称：xpcheckstring</p> 
 <p>模板内容：</p> 
 <p>${imp:import(com.google.common.base.Preconditions,com.google.common.base.Strings)}</p> 
 <p>Preconditions.checkArgument(!Strings.isNullOrEmpty(${name:var}), "${name:var} is null or empty!");</p> 
 <p>${name:var}=${name:var}.trim();</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>模板名称：xplogger</p> 
 <p>模板内容：</p> 
 <p>${imp:import(org.slf4j.Logger,org.slf4j.LoggerFactory)}</p> 
 <p>private static final Logger LOGGER = LoggerFactory.getLogger(${enclosing_type}.class);</p> 
 <p>&nbsp;</p> 
</div>