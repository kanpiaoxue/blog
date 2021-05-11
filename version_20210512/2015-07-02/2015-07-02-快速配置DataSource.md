#快速配置DataSource
###发表时间：2015-07-02
###分类：Spring,java,DataSource,jdbc
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2223795" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2223795</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">import org.apache.commons.dbcp.BasicDataSource;
import org.springframework.jdbc.core.JdbcTemplate;

        String url = "jdbc:mysql://localhost:3306/cdc_dmap_dev?useUnicode=true&amp;characterEncoding=utf-8&amp;zeroDateTimeBehavior=convertToNull";  
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setDriverClassName("com.mysql.jdbc.Driver");  
        dataSource.setUrl(url);  
        dataSource.setUsername("root");  
        dataSource.setPassword("hao123"); 

JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);</pre> 
 <p>&nbsp;</p> 
</div>