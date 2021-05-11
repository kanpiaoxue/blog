#eclipse中的tomcat和maven的profile协作
###发表时间：2020-08-07
###分类：eclipse,maven,tomcat,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2516165" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2516165</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>在使用eclipse、maven、tomcat开发java应用的时候，可能maven中使用到了maven的profile来切换不同的环境（dev 开发、test 测试、prod 线上）。 如果在eclipse中的tomcat启动该项目的时候，如何让maven的profile生效呢？</p> 
 <p>&nbsp;</p> 
 <p>回答：</p> 
 <p>鼠标右键点击eclipse的project，找到Properties的选项，弹出窗口。在窗口的左侧找到Maven的配置，有一项配置是：Active Maven Profiles（comma separated），在这里填写你指定的maven的profile，然后启动tomcat即可。</p> 
 <p>&nbsp;</p> 
 <p>下面是网上给出的解决方案。</p> 
 <p>==============================================</p> 
 <p>问题：</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">If I have 2 maven profiles for a WAR application like this:</p> 
 <pre class="lang-xml prettyprint prettyprinted"><code style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: transparent; white-space: inherit;">mvn clean install -Pdevelopment
mvn clean install -Pproduction</code></pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">and I import it in Eclipse to run in Tomcat, how to I tell Tomcat to use one profile or the other?</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">回答：</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">Answer:</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">You can activate the maven profile at the Eclipse by using the following step: -</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">Right click at your project and select properties .</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">At the Properties windows select Maven.</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">At the right hand panel you will see Active Maven Profiles text box.</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">Please enter your profile name, e.g. development or production.</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; vertical-align: baseline; clear: both;"><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;">I hope this may help.</span></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">参考资料：<a style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px;" href="https://stackoverflow.com/questions/16280858/maven-profiles-and-tomcat-in-eclipse">https://stackoverflow.com/questions/16280858/maven-profiles-and-tomcat-in-eclipse</a></p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
</div>