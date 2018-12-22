#springboot读取可运行jar里面的resources内的文件
###发表时间：2018-12-04
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434712" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434712</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用eclipse等IDE开发Springboot的web系统的时候，需要下载位于resources/下面excel文件。在IDE中运行springboot程序，一切正常，但是打包成execute jar 之后就报错，找不到文件。</p> 
 <p>原因：使用File file来现在文件，会去判断文件是否存在。在文件系统中是好用的，但是在打包jar之后就不好用了。那么该如何读取jar里面resources下面的文件呢？</p> 
 <pre name="code" class="java">String data = "";
ClassPathResource cpr = new ClassPathResource("static/file.txt");
try {
    byte[] bdata = FileCopyUtils.copyToByteArray(cpr.getInputStream());
    data = new String(bdata, StandardCharsets.UTF_8);
} catch (IOException e) {
    LOG.warn("IOException", e);
}</pre> 
 <p>代码如上，就可以读取jar里面resources下面的文件。</p> 
 <p>关键：不能使用file来读取file的内容，应该直接使用InputStream来读取。</p> 
 <pre name="code" class="java">public ResponseEntity&lt;byte[]&gt; download(String fileName, String folderPath)
         throws Exception {
     checkStringArgs(fileName, "fileName");
     checkStringArgs(folderPath, "folderPath");
     
     // 下载文件路径
     URL url = Resources.getResource(folderPath + File.separator + fileName);
     LOGGER.debug("url:{}",url);
     //读取流中的内容
     byte[] contents = FileCopyUtils.copyToByteArray(url.openStream());
     HttpHeaders headers = new HttpHeaders();
     // 通知浏览器以attachment（下载方式）
     headers.setContentDispositionFormData("attachment", fileName);
     // application/octet-stream ： 二进制流数据（最常见的文件下载）。
     headers.setContentType(MediaType.APPLICATION_OCTET_STREAM);
     return new ResponseEntity&lt;byte[]&gt;(contents, headers, HttpStatus.CREATED);
}</pre> 
 <p>&nbsp;参考地址：</p> 
 <p>Classpath resource not found when running as jar：<a href="https://stackoverflow.com/questions/25869428/classpath-resource-not-found-when-running-as-jar">https://stackoverflow.com/questions/25869428/classpath-resource-not-found-when-running-as-jar</a></p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  resource.getFile() expects the resource itself to be available on the file system, i.e. it can't be nested inside a jar file. This is why it works when you run your application in STS but doesn't work once you've built your application and run it from the executable jar. Rather than using getFile() to access the resource's contents, I'd recommend using getInputStream() instead. That'll allow you to read the resource's content regardless of where it's located.
 </div> 
 <p>&nbsp;</p> 
</div>