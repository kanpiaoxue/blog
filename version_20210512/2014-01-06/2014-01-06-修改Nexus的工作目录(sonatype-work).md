#修改Nexus的工作目录(sonatype-work)
###发表时间：2014-01-06
###分类：java,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2000048" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2000048</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p><span style="line-height: 25.1875px;">一、如果下载的是WAR包版，请修改：</span></p> 
 <p><span style="line-height: 25.1875px;">nexus-2.7.0-06\WEB-INF\plexus.properties</span></p> 
 <pre name="code" class="java">nexus-work=${user.home}/sonatype-work/nexus</pre> 
 <p><span style="line-height: 25.1875px;">&nbsp;修改这个目录为你想设置的目录。</span></p> 
 <p><span style="line-height: 25.1875px;">nexus-2.7.0-06.war 文件可以用zip的解压缩程序打开，将修改好的</span><span style="line-height: 25.1875px;">nexus-2.7.0-06\WEB-INF\plexus.properties 的文件覆盖掉。放在WEB server（如：tomcat）的web发布目录，启动web程序，就可以了。</span></p> 
 <p>&nbsp;</p> 
 <p><span style="line-height: 25.1875px;">二、修改环境变量，添加：&nbsp;</span><span style="line-height: 25.1875px;">PLEXUS_NEXUS_WORK &nbsp;</span><span style="color: #ff0000; line-height: 25.1875px;">/sonatype-work/nexus</span></p> 
 <p>&nbsp;</p> 
 <p><span style="color: #ff0000; line-height: 25.1875px;">参考：&nbsp;</span><a style="line-height: 1.5;" href="http://chenfeicqq.iteye.com/blog/1595516">http://chenfeicqq.iteye.com/blog/1595516</a></p> 
</div>