#Cookie长度超长的异常问题 net::ERR_EMPTY_RESPONSE
###发表时间：2016-09-28
###分类：web,经验,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2327649" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2327649</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>最近3个月发现一个问题。我设计的系统，我无法访问，其他人都可以。今天彻底的找了一下原因。</p> 
 <p>原因如下：我是系统管理员，还是系统中每个团队的管理员。这些信息都被写到了cookie中，引起浏览器和服务器处理异常。</p> 
 <p>错误信息如下：net::ERR_EMPTY_RESPONSE</p> 
 <p>处理方案：将我从各个团队管理员里面删除，cookie变小，问题解决。</p> 
 <p>&nbsp;</p> 
</div>