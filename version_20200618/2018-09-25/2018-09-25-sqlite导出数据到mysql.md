#sqlite导出数据到mysql
###发表时间：2018-09-25
###分类：mysql,经验,sqlite,数据库
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431321" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431321</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  命令行
 </div> 
 <div class="quote_div">
  $sqlite3 hello.db .dump |grep "INSERT INTO \"user\""&nbsp; &nbsp;#导出user表的内容
  <br>$sqlite3 hello.db .dump |grep "INSERT INTO \"group\""&nbsp; &nbsp;#导出group表的内容
 </div> 
 <p>&nbsp;</p> 
</div>