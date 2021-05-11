#springboot的json的时间格式：时间戳
###发表时间：2020-07-07
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2515520" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2515520</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>springboot项目中javabean的字段是Date类型，需要通过Controller提供的HTTP API 返给客户端时间戳的形式。</p> 
 <p>可以指定配置如下：</p> 
 <pre name="code" class="java">spring.jackson.serialization.write-dates-as-timestamps: true</pre> 
 <p>&nbsp;这样Date类型的字段都会被序列化为时间戳timestamp的格式：</p> 
 <pre name="code" class="java">"createTime": 1592897548000</pre> 
 <p>&nbsp;</p> 
 <p>参考资料：</p> 
 <p><a href="https://stackoverflow.com/questions/27516499/json-date-format-in-spring-boot">https://stackoverflow.com/questions/27516499/json-date-format-in-spring-boot</a></p> 
 <p>&nbsp;</p> 
</div>