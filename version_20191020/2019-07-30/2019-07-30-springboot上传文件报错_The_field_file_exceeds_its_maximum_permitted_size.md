#springboot上传文件报错：The field file exceeds its maximum permitted size
###发表时间：2019-07-30
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2443072" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2443072</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：<a href="https://blog.csdn.net/awmw74520/article/details/70230591">https://blog.csdn.net/awmw74520/article/details/70230591</a></p> 
 <div class="quote_title">
  上传文件到springboot，报错如下：&nbsp;
 </div> 
 <div class="quote_div">
  The field file exceeds its maximum permitted size
 </div> 
 <p>&nbsp;</p> 
 <p>解决方案：</p> 
 <p>Spring Boot 2.0之后</p> 
 <p>spring.servlet.multipart.max-file-size=100MB</p> 
 <p>spring.servlet.multipart.max-request-size=1000MB</p> 
 <p>&nbsp;</p> 
</div>