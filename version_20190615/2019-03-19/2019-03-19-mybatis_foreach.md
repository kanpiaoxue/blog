#mybatis foreach
###发表时间：2019-03-19
###分类：mybatis,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439065" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439065</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">参考：&nbsp;</p> 
 <p style="font-size: 14px;"><a href="http://www.mybatis.org/mybatis-3/zh/dynamic-sql.html">http://www.mybatis.org/mybatis-3/zh/dynamic-sql.html</a></p> 
 <p style="font-size: 14px;"><a href="https://www.jianshu.com/p/a45908678a52">https://www.jianshu.com/p/a45908678a52</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;select id="selectPostIn" resultType="domain.blog.Post"&gt;
  SELECT *
  FROM POST P
  &lt;if test="list != null and list.size != 0"&gt;
      WHERE ID in
      &lt;foreach item="item" index="index" collection="list" open="(" separator="," close=")"&gt;
            #{item}
      &lt;/foreach&gt;
    &lt;/if&gt;
&lt;/select&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;insert id="batchInsert" useGeneratedKeys="true" keyProperty="id"&gt;  
    insert into  
    tb_hello(  
    id, `type`,name, description, job_config  
    ) values  
    &lt;foreach item="item" collection="list" separator=","&gt;  
        (#{item.id}, #{item.type},#{item.name}, #{item.description})  
    &lt;/foreach&gt;  
&lt;/insert&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>