#springboot的web开发设置filter
###发表时间：2018-12-03
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434670" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434670</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料：&nbsp;</p> 
 <p>1、<a href="https://www.jianshu.com/p/05c8be17c80a">https://www.jianshu.com/p/05c8be17c80a</a></p> 
 <p>2、<a href="https://stackoverflow.com/questions/25957879/filter-order-in-spring-boot">https://stackoverflow.com/questions/25957879/filter-order-in-spring-boot</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Configuration
public class FilterConfiguration {

    @Autowired
    private Environment env;


    @Bean
    @Order(1)
    @Profile({ "test", "prod" })
    public FilterRegistrationBean&lt;SSOFilter&gt; ssoFilter() {

        Map&lt;String, String&gt; params = new HashMap&lt;&gt;();
        params.put("app_name", env.getProperty("sso.app.name"));
        params.put("exclusions", "*/api/*,*/actuator/*");
  
        SSOFilter ssoFilter = new SSOFilter();
        ssoFilter.setInitParams(params);
        FilterRegistrationBean&lt;SSOFilter&gt; registration = new FilterRegistrationBean&lt;&gt;(ssoFilter);
        registration.addUrlPatterns("/*");
        return registration;
    }
   
    @Bean
    @Order(2)
    public FilterRegistrationBean&lt;AuthFilter&gt; authFilter() {

        AuthFilter filter = new AuthFilter();
        String ignoreSuffix = env.getProperty("auth.ignoreSuffix");
        FilterRegistrationBean&lt;AuthFilter&gt; registration = new FilterRegistrationBean&lt;&gt;(filter);
        registration.addUrlPatterns("/*");
        registration.addInitParameter("ignoreSuffix", ignoreSuffix);
        return registration;
    }

    
}    </pre> 
 <p>&nbsp;</p> 
</div>