#mybatis foreach
###发表时间：2019-03-19
###分类：mybatis,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439065" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439065</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考：&nbsp;</p> 
 <p><a href="http://www.mybatis.org/mybatis-3/zh/dynamic-sql.html">http://www.mybatis.org/mybatis-3/zh/dynamic-sql.html</a></p> 
 <p><a href="https://www.jianshu.com/p/a45908678a52">https://www.jianshu.com/p/a45908678a52</a></p> 
 <p>&nbsp;</p> 
 <p>参考：</p> 
 <pre name="code" class="java">&lt;insert id="batchInsert" useGeneratedKeys="true" keyProperty="id"&gt;
    insert into
    tb_hello(
    id, `type`,name, description, job_config
    ) values
    &lt;foreach item="item" collection="list" separator=","&gt;
        (#{item.id}, #{item.type},#{item.name}, #{item.description})
    &lt;/foreach&gt;
&lt;/insert&gt;</pre> 
 <p>&nbsp;</p> 
</div>