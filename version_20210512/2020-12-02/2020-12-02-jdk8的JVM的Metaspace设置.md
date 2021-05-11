#jdk8的JVM的Metaspace设置
###发表时间：2020-12-02
###分类：java,JVM
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2517904" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2517904</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>从JDK8开始，PermSize的配置被废弃，改为Metaspace，如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">-XX:MetaspaceSize=200m -XX:MaxMetaspaceSize=200m</pre> 
 <p>&nbsp;</p> 
</div>