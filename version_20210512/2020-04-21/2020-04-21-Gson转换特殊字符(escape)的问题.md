#Gson转换特殊字符（escape）的问题
###发表时间：2020-04-21
###分类：gson,java,经验,json
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2513762" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2513762</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考文章：&nbsp;<a href="https://stackoverflow.com/questions/17092044/gson-failure-to-conver-symbols">https://stackoverflow.com/questions/17092044/gson-failure-to-conver-symbols</a></p> 
 <p>&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">You should&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; line-height: inherit; font-family: inherit; vertical-align: baseline;">disable HTML escaping</strong>, here is a sample that illustrates it:</p> 
 <pre name="code" class="java">Gson gson1 = new Gson();

String s1 = gson1.toJson("&lt;&gt;");

Gson gson2 = new GsonBuilder().disableHtmlEscaping().create();

String s2 = gson2.toJson("&lt;&gt;");</pre> 
 <pre class="default prettyprint prettyprinted">&nbsp;</pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">s1: "\u003c\u003e"</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">s2: "&lt;&gt;"</p> 
</div>