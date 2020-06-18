#oracle 分页SQL
###发表时间：2013-12-18
###分类：java,oracle
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1991275" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1991275</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">	private String getPageSQL(String sourceSQL, int start, int end){
		StringBuilder builder = new StringBuilder(
				"select * from (select rownum as rowno, getSQLGridDatas.* from (")
				.append(sourceSQL).append(") getSQLGridDatas where rownum &lt;= ")
				.append(end)
				.append(") table_alias where table_alias.rowno &gt;= ")
				.append(start);
		return builder.toString();
	}</pre> 
 <p>&nbsp;</p> 
</div>