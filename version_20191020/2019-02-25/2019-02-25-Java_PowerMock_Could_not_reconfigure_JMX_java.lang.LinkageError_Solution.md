#Java PowerMock Could not reconfigure JMX java.lang.LinkageError Solution
###发表时间：2019-02-25
###分类：powermockito,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2438075" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2438075</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <div class="quote_title">
  问题如下&nbsp;
 </div> 
 <div class="quote_div">
  If you are using Mockito and PowerMock to build mocks for your Java tests and you run into the following error:
  <br>
  <br>2016-05-05 17:31:20,204 main ERROR Could not reconfigure JMX java.lang.LinkageError: loader constraint violation: loader (instance of org/powermock/core/classloader/MockClassLoader) previously initiated loading for a different type with name "javax/management/MBeanServer"
  <br> at java.lang.ClassLoader.defineClass1(Native Method)
  <br> at java.lang.ClassLoader.defineClass(ClassLoader.java:760)
  <br> at org.powermock.core.classloader.MockClassLoader.loadUnmockedClass(MockClassLoader.java:238)
  <br> at org.powermock.core.classloader.MockClassLoader.loadModifiedClass(MockClassLoader.java:182)
  <br> at org.powermock.core.classloader.DeferSupportingClassLoader.loadClass(DeferSupportingClassLoader.java:70)
  <br> at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
 </div> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  解决方案&nbsp;
 </div> 
 <div class="quote_div">
  Simply add the following as a class level annotation:
  <br>
  <br>@PowerMockIgnore( {"javax.management.*"})
 </div> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;</p> 
 <p><a href="http://www.ryanchapin.com/fv-b-4-816/Java-PowerMock-Could-not-reconfigure-JMX-java-lang-LinkageError-Solution.html">http://www.ryanchapin.com/fv-b-4-816/Java-PowerMock-Could-not-reconfigure-JMX-java-lang-LinkageError-Solution.html</a></p> 
 <p>&nbsp;</p> 
</div>