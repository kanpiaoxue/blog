#eclipse 中使用maven的jetty插件进行debug出现Source not found的问题解决方案
###发表时间：2016-05-25
###分类：eclipse,maven,jetty
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2300847" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2300847</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>当在eclipse中使用maven的jetty插件进行debug的时候，会出现“Source not found”的问题。你把java项目的文件夹加入到它的搜索路径中，点击确定之后，发现它根本不生效。你多次尝试，依然会有这个问题。</p> 
 <p>怎么解决呢？停掉jetty服务，然后再次启动jetty服务，问题就解决了。可以进行debug了。</p> 
 <p>参考了国外的网站，下面有链接和原文。</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">    &lt;build&gt;
    	&lt;defaultGoal&gt;package&lt;/defaultGoal&gt;
    	&lt;finalName&gt;dmeta2-api-server&lt;/finalName&gt;
    	
        &lt;plugins&gt;
            &lt;!-- web server for jetty begin --&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.mortbay.jetty&lt;/groupId&gt;
                &lt;artifactId&gt;maven-jetty-plugin&lt;/artifactId&gt;
                &lt;version&gt;6.1.24&lt;/version&gt;
                &lt;configuration&gt;
                    &lt;scanIntervalSeconds&gt;5&lt;/scanIntervalSeconds&gt;
                    &lt;contextPath&gt;/dmeta2-api-server&lt;/contextPath&gt;
                    &lt;reload&gt;automatic&lt;/reload&gt;
                    &lt;connectors&gt;
                        &lt;connector implementation="org.mortbay.jetty.nio.SelectChannelConnector"&gt;
                            &lt;port&gt;8090&lt;/port&gt;
                            &lt;headerBufferSize&gt;80000&lt;/headerBufferSize&gt;
                        &lt;/connector&gt;
                    &lt;/connectors&gt;
                &lt;/configuration&gt;
            &lt;/plugin&gt;
            &lt;!-- web server for jetty end --&gt;
        &lt;/plugins&gt;
    &lt;/build&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>----------------------</p> 
 <p>地址：<a href="http://www.javavids.com/video/how-to-solve-source-not-found-error-during-debug-in-eclipse.html">http://www.javavids.com/video/how-to-solve-source-not-found-error-during-debug-in-eclipse.html</a></p> 
 <h1 style="font-size: 36px; margin-top: 20px; margin-bottom: 10px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 500; line-height: 1.1; color: #333333;">How to solve Source not found error during debug in Eclipse</h1> 
 <p style="margin-bottom: 10px; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 20px;">If you run your web application using embedded Java EE server in Maven (like Tomcat or Jetty) and try to run it in debug mode, once you hit some breakpoint, you will encounter this error: "Source not found".</p> 
 <p><span style="color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 20px;">If you run your web application using embedded Java EE server and try to run it in debug mode, once you hit some breakpoint, you will encounter this error: "Source not found". Just simply press "Edit Source Lookup Path ...", add your project and restart your web application. And now it works.</span></p> 
</div>