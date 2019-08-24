#Eclipse 部署(Publish)报错：java.lang.ClassNotFoundException: ContextLoaderListener
###发表时间：2017-11-17
###分类：eclipse,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2400086" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2400086</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用eclipse部署tomcat的jee应用，报错如下：</p> 
 <pre name="code" class="java">严重: Error configuring application listener of class [org.springframework.web.context.ContextLoaderListener]
java.lang.ClassNotFoundException: org.springframework.web.context.ContextLoaderListener
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1285)
	at org.apache.catalina.loader.WebappClassLoaderBase.loadClass(WebappClassLoaderBase.java:1119)
	at org.apache.catalina.core.DefaultInstanceManager.loadClass(DefaultInstanceManager.java:512)
	at org.apache.catalina.core.DefaultInstanceManager.loadClassMaybePrivileged(DefaultInstanceManager.java:493)
	at org.apache.catalina.core.DefaultInstanceManager.newInstance(DefaultInstanceManager.java:119)
	at org.apache.catalina.core.StandardContext.listenerStart(StandardContext.java:4667)
	at org.apache.catalina.core.StandardContext.startInternal(StandardContext.java:5207)
	at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:150)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1419)
	at org.apache.catalina.core.ContainerBase$StartChild.call(ContainerBase.java:1409)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
	at java.lang.Thread.run(Thread.java:748)</pre> 
 <p>&nbsp;检查了maven的pom.xml的jar的引入，以及各个引入的jar的依赖关系是否存在冲突，发现都没有问题。</p> 
 <p>最后检查eclipse的自身设置，找到了问题。</p> 
 <p>解决方法如下：</p> 
 <p>选中jee的项目，点击鼠标的右键，选中“Properties”，弹出的窗口中左侧菜单找到选项“Deployment Assembly”。在右侧点击按钮“Add...”，弹出的窗口中选中“Java Build Path Entities”，选中“Maven Dependencies”，确认。</p> 
 <p>这样就可以解决该问题了。</p> 
 <p>参考如下：</p> 
 <p><strong>解决方案：</strong></p> 
 <p>1.右键点击项目--选择Properties</p> 
 <p>选择Deployment Assembly,在右边点击Add按钮，在弹出的窗口中选择Java Build Path Entries。如下图所示：</p> 
 <p><img src="http://dl.iteye.com/upload/picture/pic/124397/103f5758-dcd0-3a15-89b1-a39b804ea732.jpg" alt="" width="625" height="577"></p> 
 <p>2.点击Next，选择Maven Dependencies</p> 
 <p><img src="http://dl.iteye.com/upload/picture/pic/124399/94770734-7a9c-3836-b34b-040ccdd4b28c.jpg" alt="" width="625" height="574"></p> 
 <p>3.点击Finish，然后可以看到已经把Maven Dependencies添加到Web应用结构中了</p> 
 <p><img src="http://dl.iteye.com/upload/picture/pic/124401/0c075b66-5833-3d05-910f-9af4cae256b9.jpg" alt="" width="624" height="323"></p> 
 <p>&nbsp;</p> 
 <p>操作完后，重新部署工程，不再报错了。然后我们再到.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\目录下，发现工程WEB-INF目录下自动生成了lib目录，并且所有的依赖jar包也都已经部署进来。问题因此解决。</p> 
 <p>参考地址：&nbsp;<a href="http://chenzhou123520.iteye.com/blog/1836987">http://chenzhou123520.iteye.com/blog/1836987</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>