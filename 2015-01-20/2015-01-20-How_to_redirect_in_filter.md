#How to redirect in filter?
###发表时间：2015-01-20
###分类：Filter
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2177792" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2177792</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">HttpServletResponse httpResponse = (HttpServletResponse) response;
httpResponse.sendRedirect("/login.jsp");</pre> 
 <p>&nbsp;</p> 
</div>