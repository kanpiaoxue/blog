#Javascript 正则表达式获取分组数据
###发表时间：2014-05-05
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2061826" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2061826</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">var url = 'http://localhost:8080/datamarket/tableList?search=%E6%8F%90%E4%BE%9B%E6%95%B0%E6%8D%AE%E8%A1%A8%E5%8F%8A%E5%AD%97%E6%AE%B5%E7%9A%84%E6%9F%A5%E8%AF%A2';
re = /^(.+?)#$/;

var r = re.exec(url) ;
alert(r.constructor)
if(r) {
    alert(r[1]);
}</pre> 
 <p>&nbsp;</p> 
</div>