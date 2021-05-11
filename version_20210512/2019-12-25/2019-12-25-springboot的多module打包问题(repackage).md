#springboot的多module打包问题(repackage)
###发表时间：2019-12-25
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2511426" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2511426</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>我有个java的项目是maven管理的。maven的module结构如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">hello
    |—— commons
    |—— dao
    |—— service
    |—— hello-web
    |—— hello-api</pre> 
 <p>其中&nbsp;hello-web 是非springboot的程序，普通的war的形式。</p> 
 <p>而&nbsp;hello-api 则是基于springboot创建的。</p> 
 <p>要想使&nbsp;hello-api 被打包成springboot的可执行jar，需要在&nbsp;hello-api 的pom.xml添加如下的内容：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">&lt;build&gt;
		&lt;plugins&gt;
			&lt;plugin&gt;
				&lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
				&lt;artifactId&gt;spring-boot-maven-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.0.7.RELEASE&lt;/version&gt;
				&lt;!-- &lt;configuration&gt;
					&lt;mainClass&gt;com.xx.webapps.api.main.WebappsApiBidMain&lt;/mainClass&gt;
				&lt;/configuration&gt; --&gt;
				&lt;executions&gt;
					&lt;execution&gt;
						&lt;goals&gt;
							&lt;goal&gt;repackage&lt;/goal&gt;
						&lt;/goals&gt;
					&lt;/execution&gt;
				&lt;/executions&gt;
			&lt;/plugin&gt;
		&lt;/plugins&gt;
	&lt;/build&gt;</pre> 
 <p>&nbsp;</p> 
 <p>这样运行 mvn clean package 的时候，hello-api 会被打包成springboot的执行jar，hello-web也不会受到影响，还是war的形式。</p> 
 <p>&nbsp;</p> 
 <p>在springboot的官网里面对于repackage有说明，如下：</p> 
 <p>地址：&nbsp;<a href="https://docs.spring.io/spring-boot/docs/2.0.7.RELEASE/reference/htmlsingle/#build-tool-plugins-repackage-implementation">https://docs.spring.io/spring-boot/docs/2.0.7.RELEASE/reference/htmlsingle/#build-tool-plugins-repackage-implementation</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="titlepage" style="margin: 0px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;"> 
  <div style="margin: 0px;"> 
   <div style="margin: 0px;"> 
    <h2 class="title" style="">11.5&nbsp;Creating an Executable Jar</h2> 
   </div> 
  </div> 
 </div> 
 <p style="margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">We finish our example by creating a completely self-contained executable jar file that we could run in production. Executable jars (sometimes called “fat jars”) are archives containing your compiled classes along with all of the jar dependencies that your code needs to run.</p> 
 <div class="sidebar" style="margin: 0px; line-height: 1.4; padding: 0px 20px; background-color: #f8f8f8; border: 1px solid #cccccc; border-radius: 3px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;"> 
  <div class="titlepage" style="margin: 0px;"> 
   <div style="margin: 0px;"> 
    <div style="margin: 0px;"> 
     <p class="title" style=""><strong>Executable jars and Java</strong></p> 
    </div> 
   </div> 
  </div> 
  <p style="margin-bottom: 15px;">Java does not provide a standard way to load nested jar files (jar files that are themselves contained within a jar). This can be problematic if you are looking to distribute a self-contained application.</p> 
  <p style="margin-top: 15px; margin-bottom: 15px;">To solve this problem, many developers use “uber” jars. An uber jar packages all the classes from all the application’s dependencies into a single archive. The problem with this approach is that it becomes hard to see which libraries are in your application. It can also be problematic if the same filename is used (but with different content) in multiple jars.</p> 
  <p style="margin-top: 15px; margin-bottom: 15px;">Spring Boot takes a&nbsp;<a class="link" style="color: #4183c4;" title="Appendix&nbsp;E.&nbsp;The Executable Jar Format" href="https://docs.spring.io/spring-boot/docs/2.0.7.RELEASE/reference/htmlsingle/#executable-jar">different approach</a>&nbsp;and lets you actually nest jars directly.</p> 
 </div> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">To create an executable jar, we need to add the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">spring-boot-maven-plugin</code>&nbsp;to our&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">pom.xml</code>. To do so, insert the following lines just below the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">dependencies</code>&nbsp;section:</p> 
 <pre class="programlisting"><span class="hl-tag" style="color: #3f7f7f;">&lt;build&gt;</span>
	<span class="hl-tag" style="color: #3f7f7f;">&lt;plugins&gt;</span>
		<span class="hl-tag" style="color: #3f7f7f;">&lt;plugin&gt;</span>
			<span class="hl-tag" style="color: #3f7f7f;">&lt;groupId&gt;</span>org.springframework.boot<span class="hl-tag" style="color: #3f7f7f;">&lt;/groupId&gt;</span>
			<span class="hl-tag" style="color: #3f7f7f;">&lt;artifactId&gt;</span>spring-boot-maven-plugin<span class="hl-tag" style="color: #3f7f7f;">&lt;/artifactId&gt;</span>
		<span class="hl-tag" style="color: #3f7f7f;">&lt;/plugin&gt;</span>
	<span class="hl-tag" style="color: #3f7f7f;">&lt;/plugins&gt;</span>
<span class="hl-tag" style="color: #3f7f7f;">&lt;/build&gt;</span></pre> 
 <div class="note" style="margin: 20px 0.5in; padding-top: 10px; padding-bottom: 10px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;"> 
  <table style="border-spacing: 0px; line-height: 1.6; margin: 0px; border: none !important; border-radius: 4px !important; background: 0px 0px !important;" summary="Note" border="0">
   <tbody style="margin: 0px; border: none !important; background: 0px 0px !important;"> 
    <tr style="border: none !important; margin: 0px; background: 0px 0px !important;"> 
     <td style="padding: 10px 13px 6px; border-top: none !important; border-right: 1px solid #cccccc !important; border-bottom: none !important; border-left: none !important; margin: 0px; background: 0px 0px !important;" rowspan="2" align="center" valign="top" width="25"><img style="margin: 0px; border-style: none !important; background: 0px 0px !important;" src="https://docs.spring.io/spring-boot/docs/2.0.7.RELEASE/reference/htmlsingle/images/note.png" alt="[Note]"></td> 
    </tr> 
    <tr style="border: none !important; margin: 0px; background-position: 0px 0px !important; background-color: #f8f8f8;"> 
     <td style="padding: 6px 13px; border: none !important; margin: 0px; background: 0px 0px !important;" align="left" valign="top"> <p style="color: #6f6f6f; line-height: 1.6; border: none !important; background: 0px 0px !important;">The&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background: 0px 0px #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important; margin: 0px;">spring-boot-starter-parent</code>&nbsp;POM includes&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background: 0px 0px #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important; margin: 0px;">&lt;executions&gt;</code>&nbsp;configuration to bind the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background: 0px 0px #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important; margin: 0px;">repackage</code>&nbsp;goal. If you do not use the parent POM, you need to declare this configuration yourself. See the&nbsp;<a class="link" style="color: #4183c4; margin: 0px; border: none !important; background: 0px 0px !important;" href="https://docs.spring.io/spring-boot/docs/2.0.7.RELEASE/maven-plugin/usage.html" target="_top">plugin documentation</a>&nbsp;for details.</p> </td> 
    </tr> 
   </tbody>
  </table> 
 </div> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">Save your&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">pom.xml</code>&nbsp;and run&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">mvn package</code>&nbsp;from the command line, as follows:</p> 
 <pre class="screen">$ mvn package

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.0.7.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------</pre> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">If you look in the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">target</code>&nbsp;directory, you should see&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">myproject-0.0.1-SNAPSHOT.jar</code>. The file should be around 10 MB in size. If you want to peek inside, you can use&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">jar tvf</code>, as follows:</p> 
 <pre class="screen">$ jar tvf target/myproject-0.0.1-SNAPSHOT.jar</pre> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">You should also see a much smaller file named&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">myproject-0.0.1-SNAPSHOT.jar.original</code>&nbsp;in the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">target</code>&nbsp;directory. This is the original jar file that Maven created before it was repackaged by Spring Boot.</p> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">To run that application, use the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">java -jar</code>&nbsp;command, as follows:</p> 
 <pre class="screen">$ java -jar target/myproject-0.0.1-SNAPSHOT.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.0.7.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.536 seconds (JVM running for 2.864)</pre> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">As before, to exit the application, press&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'liberation mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">ctrl-c</code>.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考资料：</p> 
 <p><a href="https://www.cnblogs.com/thinking-better/p/7827368.html">https://www.cnblogs.com/thinking-better/p/7827368.html</a></p> 
 <p><a href="https://www.baeldung.com/spring-boot-multiple-modules">https://www.baeldung.com/spring-boot-multiple-modules</a></p> 
 <p><a href="https://blog.csdn.net/taiyangdao/article/details/75303181">https://blog.csdn.net/taiyangdao/article/details/75303181</a></p> 
 <p><a href="https://docs.spring.io/spring-boot/docs/current/maven-plugin/repackage-mojo.html">https://docs.spring.io/spring-boot/docs/current/maven-plugin/repackage-mojo.html</a></p> 
 <p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/build-tool-plugins.html#build-tool-plugins-maven-plugin">https://docs.spring.io/spring-boot/docs/current/reference/html/build-tool-plugins.html#build-tool-plugins-maven-plugin</a></p> 
 <p>&nbsp;</p> 
</div>