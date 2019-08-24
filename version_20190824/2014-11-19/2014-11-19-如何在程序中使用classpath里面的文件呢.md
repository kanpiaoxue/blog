#如何在程序中使用classpath里面的文件呢？
###发表时间：2014-11-19
###分类：java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2158187" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2158187</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">Resource resource = new ClassPathResource("ehcache-console.xml");</pre> 
 <p>&nbsp;上面的这段代码，使用了classpath里面的一个Ehcache的xml配置文件。为了达到这个目的，我使用了spring提供的&nbsp;org.springframework.core.io.Resource 接口以及它的一个实现类。</p> 
 <p>&nbsp;</p> 
</div>