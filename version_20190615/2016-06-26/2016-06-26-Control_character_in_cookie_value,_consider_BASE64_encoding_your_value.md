#Control character in cookie value, consider BASE64 encoding your value
###发表时间：2016-06-26
###分类：cookie
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2307371" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2307371</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>之前一直向项目的cookie里面写英文或者数字，表现一直很好。但是今天项目当中用到cookie保存中文，报如下错误：&nbsp;</p> 
 <p><span style="line-height: 25.2px; color: red;">Control character in cookie value, consider BASE64 encoding your value</span><span style="line-height: 25.2px;">&nbsp;</span></p> 
 <p><span style="line-height: 25.2px;">意思就是向cookie里面写入内容需要采用</span><span style="color: #ff0000; line-height: 25.2px;">BASE64</span><span style="color: #ff0000; line-height: 25.2px;">&nbsp;<span style="color: #000000;">来进行编码。</span></span></p> 
 <p><span style="color: #000000; line-height: 25.2px;">解决方案：将要保存的值使用URLEncoder.encode(value,"utf-8")编码即可。当然web页面要使用它，还需要进行反编码。</span></p> 
 <p><span style="color: #000000; line-height: 25.2px;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>