#springboot的Application常用注解
###发表时间：2018-12-03
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434666" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434666</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@SpringBootApplication
@EnableScheduling // 开启Quartz
@EnableCaching // 开启缓存
@EnableRetry // 开启重试
@EnableTransactionManagement // 开始事务
@MapperScan("org.kanpiaoxue.dao") // 开启MyBatis的DAO扫描
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}</pre> 
 <p>&nbsp;</p> 
</div>