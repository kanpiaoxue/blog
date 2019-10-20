#nginx的header带有下划线的问题
###发表时间：2019-06-13
###分类：nginx,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2441836" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2441836</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>默认nginx的header都是不带有下划线( _ )的，如果带有下划线的header会被nginx忽略。该如何解决该问题呢？</p> 
 <div class="quote_title">
  &nbsp;
 </div> 
 <div class="quote_div">
  Syntax: underscores_in_headers on | off;
  <br>Default: underscores_in_headers off;
  <br>Context: http, server
 </div> 
 <p>&nbsp;Enables or disables the use of underscores in client request header fields. When the use of underscores is disabled, request header fields whose names contain underscores are marked as invalid and become subject to the ignore_invalid_headers directive.</p> 
 <p>&nbsp;</p> 
 <p>If the directive is specified on the server level, its value is only used if a server is a default one. The value specified also applies to all virtual servers listening on the same address and port.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考文档：&nbsp;</p> 
 <p>1）<a href="https://stackoverflow.com/questions/26938604/get-headers-with-an-underscore-on-nginx">https://stackoverflow.com/questions/26938604/get-headers-with-an-underscore-on-nginx</a></p> 
 <p>2）<a href="http://nginx.org/en/docs/http/ngx_http_core_module.html#underscores_in_headers">http://nginx.org/en/docs/http/ngx_http_core_module.html#underscores_in_headers</a></p> 
 <p>&nbsp;</p> 
</div>