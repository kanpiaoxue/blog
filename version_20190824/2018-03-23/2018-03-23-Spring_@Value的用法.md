#Spring @Value的用法
###发表时间：2018-03-23
###分类：java,Spring,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2414374" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2414374</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">参考：</p> 
 <p style="font-size: 14px;">&nbsp;https://blog.csdn.net/hry2015/article/details/72353994</p> 
 <p>https://blog.csdn.net/hry2015/article/details/72453920</p> 
 <p style="font-size: 14px;"><br class="Apple-interchange-newline">为@Value设置默认值。</p> 
 <p style="font-size: 14px;">【注意】不设置默认值的时候，而且配置文件中找不到配置项，spring启动的时候会报错。</p> 
 <p style="font-size: 14px;">设置默认值的方法：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Value("$(person.name:kanpiaoxue)");
private String name;</pre> 
 <p style="font-size: 14px;">&nbsp;如上：这段代码会去classpath中配置文件中找person.name，如果找不到则用默认值kanpiaoxue。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">The&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">@Value</code>&nbsp;annotation can be placed on fields, methods and method/constructor parameters to specify a default value.</p> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">Here is an example to set the default value of a field variable.</p> 
 <pre class="programlisting">public static class FieldValueTestBean

    <em>@Value("#{ systemProperties['user.region'] }")</em>
    private String defaultLocale;

    public void setDefaultLocale(String defaultLocale) {
        this.defaultLocale = defaultLocale;
    }

    public String getDefaultLocale() {
        return this.defaultLocale;
    }

}</pre> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">The equivalent but on a property setter method is shown below.</p> 
 <pre class="programlisting">public static class PropertyValueTestBean

    private String defaultLocale;

    <em>@Value("#{ systemProperties['user.region'] }")</em>
    public void setDefaultLocale(String defaultLocale) {
        this.defaultLocale = defaultLocale;
    }

    public String getDefaultLocale() {
        return this.defaultLocale;
    }

}</pre> 
 <p style="margin-top: 15px; margin-bottom: 15px; color: #333333; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium;">Autowired methods and constructors can also use the&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; background-color: #f2f2f2; border: 1px solid #cccccc; border-radius: 4px; padding: 1px 3px 0px; white-space: nowrap;">@Value</code>&nbsp;annotation.</p> 
 <pre class="programlisting">public class SimpleMovieLister {

    private MovieFinder movieFinder;
    private String defaultLocale;

    <em>@Autowired</em>
    public void configure(MovieFinder movieFinder,
            <em>@Value("#{ systemProperties['user.region'] }")</em> String defaultLocale) {
        this.movieFinder = movieFinder;
        this.defaultLocale = defaultLocale;
    }

    // ...
}</pre> 
 <pre class="programlisting">public class MovieRecommender {

    private String defaultLocale;

    private CustomerPreferenceDao customerPreferenceDao;

    <em>@Autowired</em>
    public MovieRecommender(CustomerPreferenceDao customerPreferenceDao,
            <em>@Value("#{systemProperties['user.country']}")</em> String defaultLocale) {
        this.customerPreferenceDao = customerPreferenceDao;
        this.defaultLocale = defaultLocale;
    }

    // ...
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">为@Value设置默认值</p> 
 <pre class="programlisting">@Value("#{systemProperties['pop3.port'] ?: 25}")</pre> 
 <p style="color: #6f6f6f; line-height: 1.6; font-family: Helvetica, Arial, Freesans, Clean, sans-serif; font-size: medium; border: none !important; background: none !important;">This will inject a system property&nbsp;<code class="literal" style="font-size: 16px; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important; margin: 0px;">pop3.port</code>&nbsp;if it is defined or 25 if not.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">@Autowired</code>,&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">@Inject</code>,&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">@Resource</code>, and&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">@Value</code>&nbsp;annotations are handled by Spring&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">BeanPostProcessor</code>&nbsp;implementations which in turn means that you&nbsp;<em style="margin: 0px; border: none !important; background: none !important;">cannot</em>&nbsp;apply these annotations within your own&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">BeanPostProcessor</code>&nbsp;or&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">BeanFactoryPostProcessor</code>&nbsp;types (if any). These types must be 'wired up' explicitly via XML or using a Spring&nbsp;<code class="literal" style="font-size: medium; font-family: Consolas, 'Liberation Mono', Courier, monospace; color: #6d180b; margin: 0px; background: none #f2f2f2 !important; border: 1px solid #cccccc !important; border-radius: 4px !important; padding: 1px 3px 0px !important; white-space: nowrap !important;">@Bean</code>&nbsp;method.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>