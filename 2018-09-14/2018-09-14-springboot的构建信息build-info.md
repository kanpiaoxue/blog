#springboot的构建信息build-info
###发表时间：2018-09-14
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2430687" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2430687</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">我们想在springboot的<span style="color: #404040; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">Actuator</span>上面看见构建信息，需要配置springboot的打包插件。如下：</p> 
 <pre name="code" class="xml">	&lt;build&gt;
		&lt;plugins&gt;
			&lt;plugin&gt;
				&lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
				&lt;artifactId&gt;spring-boot-maven-plugin&lt;/artifactId&gt;
				&lt;executions&gt;
					&lt;execution&gt;
						&lt;goals&gt;
							&lt;goal&gt;build-info&lt;/goal&gt;
						&lt;/goals&gt;
					&lt;/execution&gt;
				&lt;/executions&gt;
			&lt;/plugin&gt;
		&lt;/plugins&gt;
	&lt;/build&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;参考地址：</p> 
 <ul> 
  <li><a href="https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/html/howto-build.html">https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/html/howto-build.html</a></li> 
  <li><a href="https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/maven-plugin/build-info-mojo.html">https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/maven-plugin/build-info-mojo.html</a></li> 
 </ul> 
</div>