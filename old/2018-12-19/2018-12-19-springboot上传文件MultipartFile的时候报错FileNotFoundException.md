#springboot上传文件MultipartFile的时候报错FileNotFoundException
###发表时间：2018-12-19
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2435411" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2435411</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>springboot上传文件，然后将该文件MultipartFile交给其他线程进行异步处理，发生异常。问题描述如下:</p> 
 <p>报错位置</p> 
 <pre name="code" class="java">InputStream is = multipartFile.getInputStream();</pre> 
 <p>&nbsp;报错内容：</p> 
 <div class="quote_div">
  java.io.FileNotFoundException: /tmp/var/folders/w6/tomcat.5030557797053639217.9981/work/Tomcat/localhost/ROOT/upload_d5323221_777b_40a1_8850_258388c80621_00000001.tmp (No such file or directory)
 </div> 
 <p>&nbsp;结论：</p> 
 <p>&nbsp; &nbsp; springboot上传文件之后形成MultipartFile的实例，会在临时文件夹生成临时文件。将MultipartFile的实例交给异步线程处理，该临时文件会被springboot清理掉，就会引起上面的异常。</p> 
 <p>&nbsp;</p> 
 <p>解决方案：</p> 
 <p>&nbsp; &nbsp; 上传文件形成MultipartFile的实例之后立即将该文件保存在服务器，然后将生成之后的文件交给异步线程处理，处理完该文件删除即可。这样就规避掉了上面的问题。</p> 
 <p>&nbsp;</p> 
 <p>参考资料：</p> 
 <p>1、《FileNotFoundException while uploading multi part file - Spring boot》</p> 
 <p><a href="https://stackoverflow.com/questions/30738574/filenotfoundexception-while-uploading-multi-part-file-spring-boot">https://stackoverflow.com/questions/30738574/filenotfoundexception-while-uploading-multi-part-file-spring-boot</a></p> 
 <p>2、《关于springboot以MultipartFile格式上传文件报错临时文件不存在的问题的探究》</p> 
 <p><a href="http://blog.chemcyber.com/2018/03/14/%E5%85%B3%E4%BA%8Espringboot%E4%BB%A5multipartfile%E6%A0%BC%E5%BC%8F%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E6%8A%A5%E9%94%99%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E4%B8%8D%E5%AD%98%E5%9C%A8%E7%9A%84/">http://blog.chemcyber.com/2018/03/14/%E5%85%B3%E4%BA%8Espringboot%E4%BB%A5multipartfile%E6%A0%BC%E5%BC%8F%E4%B8%8A%E4%BC%A0%E6%96%87%E4%BB%B6%E6%8A%A5%E9%94%99%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E4%B8%8D%E5%AD%98%E5%9C%A8%E7%9A%84/</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>