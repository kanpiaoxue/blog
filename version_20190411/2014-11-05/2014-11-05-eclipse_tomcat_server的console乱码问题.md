#eclipse tomcat server的console乱码问题
###发表时间：2014-11-05
###分类：eclipse,tomcat
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2152712" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2152712</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在eclipse启动tomcat的是否，我发现log4j打印出来的汉字是乱码。我的workspace的编码确实是UTF-8，我的文件编码，JSP编码都是UTF-8，为何启动eclipse启动tomcat依然乱码呢。</p> 
 <p>我找到了解决办法。</p> 
 <p>解决问题之前，如图：</p> 
 <p><img src="http://dl2.iteye.com/upload/attachment/0102/8611/78d9ab38-eeb6-3996-a0f9-6d1de336ebac.jpg" alt="" width="639" height="193"></p> 
 <p>&nbsp;</p> 
 <p>解决的办法：进入eclipse配置tomcat的地方，给JVM添加参数 -Dfile.encoding=UTF-8</p> 
 <p>（myeclipse的截图）</p> 
 <p>&nbsp;</p> 
 <p><img src="http://dl2.iteye.com/upload/attachment/0102/8615/4f62f929-ea14-3c74-9219-a4117379f6da.jpg" alt="" width="685" height="422"></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>这样之后，console就不乱码了。如图：</p> 
 <p><img src="http://dl2.iteye.com/upload/attachment/0102/8617/6e3c2bf6-5bdb-312d-af8f-86bbc132825e.jpg" alt="" width="619" height="166"></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>