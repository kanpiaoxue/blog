#html标签“<textarea>”文字对齐
###发表时间：2015-01-15
###分类：html
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2176331" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2176331</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>写了一段html的textarea，发现里面的文字总是不在左上角对齐，而是会换行，会有空格。很是奇怪！代码如下：</p> 
 <pre name="code" class="html">	&lt;textarea rows="5"&gt;
	hello
	&lt;/textarea&gt;</pre> 
 <p>&nbsp;后来想了一下并进行了测试，代码如下：</p> 
 <pre name="code" class="html">&lt;textarea rows="5"&gt;hello&lt;/textarea&gt;</pre> 
 <p>&nbsp;这样一来，上面的问题就解决了。很是奇怪。难道&lt;textarea&gt;这样做是为了保证原有文字的格式？</p> 
</div>