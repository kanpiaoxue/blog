#SpringBoot项目的The temporary upload location ***is not valid 问题
###发表时间：2019-02-21
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2437903" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2437903</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在linux上面使用springboot的上传文件的功能的时候，引起下面的异常:</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  org.springframework.web.multipart.MultipartException: Failed to parse multipart servlet request; nested exception is java.io.IOException: The temporary upload location [/tmp/tomcat.6561926259726375802.9096/work/Tomcat/localhost/ROOT] is not valid
 </div> 
 <p>原因是：springboot启动之后会在 /tmp 目录创建文件夹等内容，上传文件夹在那里是不存在的 。</p> 
 <p>解决方案：在配置文件中添加上传文件的临时目录：</p> 
 <div class="quote_div">
  spring:
  <br>&nbsp; servlet:
  <br>&nbsp; &nbsp; multipart:
  <br>&nbsp; &nbsp; &nbsp; enabled: true
  <br>&nbsp; &nbsp; &nbsp; location: /hello/tempuploadfiles
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;或者在启动参数上面添加JVM的参数指定临时文件夹：</p> 
 <div class="quote_div">
  -Djava.io.tmpdir=temp
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考资料：</p> 
 <p>1、<a href="https://stackoverflow.com/questions/29923682/how-does-one-specify-a-temp-directory-for-file-uploads-in-spring-boot">https://stackoverflow.com/questions/29923682/how-does-one-specify-a-temp-directory-for-file-uploads-in-spring-boot</a></p> 
 <p>2、<a href="https://blog.csdn.net/llibin1024530411/article/details/79474953">https://blog.csdn.net/llibin1024530411/article/details/79474953</a></p> 
</div>