#How can I get a Spring bean in a servlet filter?
###发表时间：2019-03-27
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439429" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439429</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>开发基于spring的web程序的时候可能会需要在servlet的filter中得到spring管理的javabean的情况。该如何得到spring管理的javabean呢？</p> 
 <p>我们应该先得到spring的上下文：ApplicationContext</p> 
 <p>使用&nbsp;WebApplicationContextUtils</p> 
 <p>filter中的代码如下：</p> 
 <pre name="code" class="java">public void init(FilterConfig cfg) { 
    ApplicationContext ctx = WebApplicationContextUtils
      .getRequiredWebApplicationContext(cfg.getServletContext());
    this.bean = ctx.getBean(YourBeanType.class);
}</pre> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;<a href="https://stackoverflow.com/questions/7882042/how-can-i-get-a-spring-bean-in-a-servlet-filter">https://stackoverflow.com/questions/7882042/how-can-i-get-a-spring-bean-in-a-servlet-filter</a></p> 
 <p>&nbsp;</p> 
</div>