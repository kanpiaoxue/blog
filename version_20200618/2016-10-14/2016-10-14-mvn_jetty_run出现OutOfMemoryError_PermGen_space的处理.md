#mvn jetty:run出现OutOfMemoryError: PermGen space的处理
###发表时间：2016-10-14
###分类：java,maven,jetty
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2330551" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2330551</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>今天在使用maven运行jetty插件启动web程序的时候报错如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  java.lang.OutOfMemoryError: PermGen space
  <br> at java.lang.ClassLoader.defineClass1(Native Method)
  <br> at java.lang.ClassLoader.defineClassCond(ClassLoader.java:631)
  <br> at java.lang.ClassLoader.defineClass(ClassLoader.java:615)
  <br> at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:141)
  <br> at java.net.URLClassLoader.defineClass(URLClassLoader.java:283)
  <br> at java.net.URLClassLoader.access$000(URLClassLoader.java:58)
  <br> at java.net.URLClassLoader$1.run(URLClassLoader.java:197)
  <br> at java.security.AccessController.doPrivileged(Native Method)
  <br> at java.net.URLClassLoader.findClass(URLClassLoader.java:190)
  <br> at org.mortbay.jetty.webapp.WebAppClassLoader.loadClass(WebAppClassLoader.java:392)
  <br> at org.mortbay.jetty.webapp.WebAppClassLoader.loadClass(WebAppClassLoader.java:363)
 </div> 
 <p>&nbsp;</p> 
 <p>其实就是JVM的内存溢出了，不够用。</p> 
 <p>怎么办？处理的办法有好多种。</p> 
 <p>比如在启动 mvn 的命令里面添加jvm的参数。比如在 mvn.bat 或者 mvn.sh 里面添加jvm参数，扩大内存即可。</p> 
 <p>如过使用eclipse的maven插件启动jetty，可以调整jvm参数。</p> 
 <p>&nbsp;</p> 
 <p>我使用命令行启动的，也不想修改原来的mvn启动命令，怎么办？</p> 
 <p>如下：设置一下环境变量即可，关闭命令行之后，该环境变量也就失效了。</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">set MAVEN_OPTS=-XX:MaxPermSize=128M
mvn jetty:run</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>