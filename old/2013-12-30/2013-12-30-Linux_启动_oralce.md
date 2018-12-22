#Linux 启动 oralce
###发表时间：2013-12-30
###分类：Linux
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1997474" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1997474</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">启动oracle
$su - oracle
$sqlplus /nolog
SQL&gt;conn /as sysdba
SQL&gt;startup
SQL&gt;exit
$lsnrctl start</pre> 
 <p>&nbsp;</p> 
</div>