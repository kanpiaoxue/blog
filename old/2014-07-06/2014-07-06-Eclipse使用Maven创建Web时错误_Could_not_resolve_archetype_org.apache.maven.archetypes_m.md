#Eclipse使用Maven创建Web时错误：Could not resolve archetype org.apache.maven.archetypes:m
###发表时间：2014-07-06
###分类：java,maven,eclipse
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2088818" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2088818</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p><span style="color: #333333; font-family: Arial; line-height: 26px; font-size: 18px;">---- 引用自：&nbsp;</span><a href="http://blog.csdn.net/afgasdg/article/details/12757433"><span style="color: #333333; font-family: Arial; font-size: large;"><span style="line-height: 26px;">http://blog.csdn.net/afgasdg/article/details/12757433</span></span></a></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><span style="font-size: 18px;">问题描述：</span></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><span style="font-size: 18px;">&nbsp; &nbsp; &nbsp; &nbsp;&nbsp;<strong>使用Eclipse自带的Maven插件创建Web项目时报错：</strong></span></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><span style="font-size: 18px;">Could not resolve archetype org.apache.maven.archetypes:maven-archetype-webapp:RELEASE from any of the configured repositories.<br>Could not resolve artifact org.apache.maven.archetypes:maven-archetype-webapp:pom:RELEASE<br>Failed to resolve version for org.apache.maven.archetypes:maven-archetype-webapp:pom:RELEASE: Could not find metadata org.apache.maven.archetypes:maven-archetype-webapp/maven-metadata.xml in local (C:\Users\liujunguang\.m2\repository)<br>Failed to resolve version for org.apache.maven.archetypes:maven-archetype-webapp:pom:RELEASE: Could not find metadata org.apache.maven.archetypes:maven-archetype-webapp/maven-metadata.xml in local (C:\Users\liujunguang\.m2\repository)</span></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><strong><span style="font-size: 24px;">错误如图：</span></strong></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20131015220559328?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWZnYXNkZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20131015220559078?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWZnYXNkZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;">&nbsp;</p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><span style="font-size: 18px;"><strong>解决方案：</strong></span></p> 
 <p style="color: #333333; font-family: Arial; line-height: 26px;"><span style="font-size: 18px;"><strong>在Eclipse Maven配置中添加新的Catalog配置：</strong></span></p> 
 <ul style="color: #333333; font-family: Arial; line-height: 26px; display: inline !important;"> 
  <li style="display: inline !important;"><tt><span style="font-size: 18px;"><a style="color: #336699;" href="http://repo1.maven.org/maven2/archetype-catalog.xml" target="_blank">http://repo1.maven.org/maven2/archetype-catalog.xml</a></span></tt></li> 
 </ul> 
 <div style="color: #333333; font-family: Arial; line-height: 26px;">
  <span style="font-family: monospace; font-size: 18px;">&nbsp;</span>
 </div> 
 <p>&nbsp;</p> 
 <div style="color: #333333; font-family: Arial; line-height: 26px;"> 
  <span style="font-family: monospace; font-size: 18px;">&nbsp; &nbsp; &nbsp;如图：<img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20131015221959062?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWZnYXNkZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""><br></span> 
  <p>&nbsp;</p> 
  <p>&nbsp;</p> 
  <p><span style="font-size: 18px;">接下来在使用刚添加的catalog创建web工程</span></p> 
  <p><span style="font-size: 18px;">&nbsp; &nbsp; &nbsp;&nbsp;<img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20131015222052500?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWZnYXNkZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""></span></p> 
  <p><span style="font-size: 18px;">&nbsp; &nbsp; 这个时候就可以看到Eclipse联网下载了：</span></p> 
  <p><span style="font-size: 18px;">&nbsp; &nbsp; &nbsp;<img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20131015222145812?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWZnYXNkZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""><br>这个时候看一下是不是创建成功了</span></p> 
 </div> 
</div>