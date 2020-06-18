#Configuration can't be altered once the class has been compiled or used
###发表时间：2014-11-05
###分类：java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2152770" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2152770</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用Spring org.springframework.jdbc.core.simple.SimpleJdbcInsert获得table的元数据的时候，报错：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">org.springframework.dao.InvalidDataAccessApiUsageException: Configuration can't be altered once the class has been compiled or used
</pre> 
 <p>找了资料，是这么说的：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  compiled means you have instantiated a simpleJdbcInsert instance and set up data source and table name already. Once an simpleJdbcInsert instance is compiled, you should not re-config it again; for instance, set another table name. Create a new simpleJdbcInsert instace if you need to do so.
 </div> 
 <p>&nbsp;也就意味着，不能再spring里面像使用JdbcTemplate一样在一个spring上下文中使用一个单例。要想多次重复使用<span style="line-height: 1.5;">SimpleJdbcInsert，就需要每次都创建一个</span><span style="line-height: 1.5;">SimpleJdbcInsert的实例。也就是为一个数据源下面的一张表要单独创建一个</span><span style="line-height: 1.5;">SimpleJdbcInsert。</span></p> 
 <p><span style="line-height: 1.5;">我将代码修改了，每次调用方法的时候，如下：</span></p> 
 <pre name="code" class="java">SimpleJdbcInsert simpleJdbcInsert = new SimpleJdbcInsert(jdbcTemplate);</pre> 
 <p><span style="line-height: 1.5;">&nbsp;就可以解决这个问题。</span></p> 
 <p>&nbsp;</p> 
 <p>参考：<a href="http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant">http://stackoverflow.com/questions/15606588/org-springframework-dao-invaliddataaccessapiusageexception-configuration-cant</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>