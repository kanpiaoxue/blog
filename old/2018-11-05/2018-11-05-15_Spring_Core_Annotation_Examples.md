#15 Spring Core Annotation Examples
###发表时间：2018-11-05
###分类：Spring,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2433220" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2433220</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">原文地址：&nbsp;<a href="https://dzone.com/articles/15-spring-core-annotations-with-examples?edition=416199&amp;utm_source=Daily%20Digest&amp;utm_medium=email&amp;utm_campaign=Daily%20Digest%202018-11-04">https://dzone.com/articles/15-spring-core-annotations-with-examples?edition=416199&amp;utm_source=Daily%20Digest&amp;utm_medium=email&amp;utm_campaign=Daily%20Digest%202018-11-04</a></p> 
 <p style="font-size: 14px;">【备注】附件中是该文章的PDF压缩文件。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">============ 精简版</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@Autowired</strong></p> 
 <p>We can use the @Autowired annotation to mark the dependency that Spring is going to resolve and inject. We can use this annotation with a constructor, setter, or field injection.</p> 
 <p>Constructor Injection:</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@RestController
public class CustomerController {
    private CustomerService customerService;
    @Autowired
    public CustomerController(CustomerService customerService) {
        this.customerService = customerService;
    }
}</pre> &nbsp;Setter Injection: 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class CustomerController {
    private CustomerService customerService;
    @Autowired
    public void setCustomerService(CustomerService customerService) {
        this.customerService = customerService;
    }
}</pre> &nbsp;Field Injection: 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class CustomerController {
    @Autowired
    private CustomerService customerService;
}</pre> &nbsp; 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><strong>@Bean</strong></p> 
 <ul> 
  <li>&nbsp;@Bean is a method-level annotation and a direct analog of the XML element. The annotation supports some of the attributes offered by, such as the init-method, destroy-method, auto-wiring, and name.</li> 
  <li>You can use the&nbsp; @Bean annotation in a&nbsp; @Configuration-annotated or @Component-annotated class.</li> 
 </ul> 
 <p>The following is a simple example of an @Bean method declaration:</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import com.companyname.projectname.customer.CustomerService;
import com.companyname.projectname.order.OrderService;
@Configuration
public class Application {
    @Bean
    public CustomerService customerService() {
        return new CustomerService();
    }
    @Bean
    public OrderService orderService() {
        return new OrderService();
    }
}
</pre> &nbsp;The preceding configuration is equivalent to the following Spring XML: 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;beans&gt;
        &lt;bean id="customerService" class="com.companyname.projectname.CustomerService"/&gt;
        &lt;bean id="orderService" class="com.companyname.projectname.OrderService"/&gt;
&lt;/beans&gt;
</pre> &nbsp; 
 <p>&nbsp;</p> 
 <p><strong>@Qualifier</strong></p> 
 <p>This annotation helps fine-tune annotation-based auto-wiring. There may be scenarios when we create more than one bean of the same type and want to wire only one of them with a property. This can be controlled using the @Qualifier annotation along with the&nbsp; @Autowired annotation.</p> 
 <p>Example: Consider the EmailService and SMSService classes to implement the single&nbsp; MessageService interface.</p> 
 <p>Create the MessageService interface for multiple message service implementations.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public interface MessageService {
    public void sendMsg(String message);
}</pre> &nbsp;Next, create implementations:&nbsp; EmailService and SMSService. 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public class EmailService implements MessageService{
    public void sendMsg(String message) {
         System.out.println(message);
    }
}


public class SMSService implements MessageService{
    public void sendMsg(String message) {
         System.out.println(message);
    }
}</pre> &nbsp;It's time to see the usage of the @Qualifier annotation. 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public interface MessageProcessor {
    public void processMsg(String message);
}
public class MessageProcessorImpl implements MessageProcessor {
    private MessageService messageService;
    // setter based DI
    @Autowired
    @Qualifier("emailService")
    public void setMessageService(MessageService messageService) {
        this.messageService = messageService;
    }
    // constructor based DI
    @Autowired
    public MessageProcessorImpl(@Qualifier("emailService") MessageService messageService) {
        this.messageService = messageService;
    }
    public void processMsg(String message) {
        messageService.sendMsg(message);
    }
}</pre> &nbsp; 
 <p>&nbsp;</p> 
 <p><strong>@Required</strong></p> 
 <p>The @Required annotation is a method-level annotation and applied to the setter method of a bean.</p> 
 <p>This annotation simply indicates that the setter method must be configured to be dependency-injected with a value at configuration time.</p> 
 <p>For example, @Required on setter methods marks dependencies that we want to populate through XML:</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Required
void setColor(String color) {
    this.color = color;
}</pre> &nbsp; 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;bean class="com.javaguides.spring.Car"&gt;
    &lt;property name="color" value="green" /&gt;
&lt;/bean&gt;</pre> &nbsp;Otherwise, the&nbsp; BeanInitializationException will be thrown. 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@Value</strong></p> 
 <p>The Spring @Value annotation is used to assign default values to variables and method arguments. We can read Spring environment variables as well as system variables using the @Value annotation.</p> 
 <p>The Spring @Value annotation also supports SpEL. Let’s look at some of the examples of using the @Value annotation.</p> 
 <p>Examples: We can assign a default value to a class property using the @Value annotation.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Value("Default DBConfiguration")
private String defaultName;</pre> &nbsp;The @Value annotation argument can be a string only, but Spring tries to convert it to the specified type. The following code will work fine and assign the boolean and integer values to the variable. 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Value("true")
private boolean defaultBoolean;
@Value("10")
private int defaultInt;</pre> &nbsp;This demonstrates the Spring&nbsp; @Value — Spring Environment Property 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Value("${APP_NAME_NOT_FOUND}")
private String defaultAppName;</pre> &nbsp;Next, assign system variables using the @Value annotation. 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Value("${java.home}")
private String javaHome;
@Value("${HOME}")
private String homeDir;</pre> &nbsp;Spring @Value&nbsp; – SpEL 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Value("#{systemProperties['java.home']}")
private String javaHome;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@DependsOn</strong></p> 
 <p>The@DependsOn annotation can force Spring IoC containers to initialize one or more beans before the bean, which is annotated by the&nbsp; @DependsOn annotation.</p> 
 <p>The @DependsOn annotation may be used on any class directly or indirectly annotated with the&nbsp; @Component or on methods annotated with the @Bean.</p> 
 <p>Example: Let's create&nbsp; FirstBean and&nbsp; SecondBean classes. In this example, the&nbsp; SecondBean is initialized before bean&nbsp; FirstBean.</p> 
 <pre name="code" class="java">public class FirstBean {
    @Autowired
    private SecondBean secondBean;
}
public class SecondBean {
    public SecondBean() {
        System.out.println("SecondBean Initialized via Constuctor");
    }
}</pre> 
 <p>&nbsp;Declare the above beans in Java based on the configuration class.</p> 
 <pre name="code" class="java">@Configuration
public class AppConfig {
    @Bean("firstBean")
    @DependsOn(value = {
        "secondBean"
    })
    public FirstBean firstBean() {
        return new FirstBean();
    }
    @Bean("secondBean")
    public SecondBean secondBean() {
        return new SecondBean();
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@Lazy</strong></p> 
 <p>By default, the Spring IoC container creates and initializes all singleton beans at the time of application startup. We can prevent this pre-initialization of a singleton bean by using the @Lazy annotation.</p> 
 <p>The&nbsp; @Lazy annotation may be used on any class, directly or indirectly annotated with the&nbsp; @Component or on methods annotated with the @Bean.</p> 
 <p>Example: Consider we have below two beans — FirstBean and&nbsp; SecondBean. In this example, we will explicitly load&nbsp; FirstBean using the&nbsp; @Lazyannotation.</p> 
 <pre name="code" class="java">public class FirstBean {
    public void test() {
        System.out.println("Method of FirstBean Class");
    }
}


public class SecondBean {
    public void test() {
        System.out.println("Method of SecondBean Class");
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;Declare the above beans in Java based on the configuration class.</p> 
 <pre name="code" class="java">@Configuration
public class AppConfig {
    @Lazy(value = true)
    @Bean
    public FirstBean firstBean() {
        return new FirstBean();
    }
    @Bean
    public SecondBean secondBean() {
        return new SecondBean();
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;As we can see, bean secondBean is initialized by the Spring container, while the bean firstBean is initialized explicitly.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@Lookup</strong></p> 
 <p>A method annotated with&nbsp; @Lookup tells Spring to return an instance of the method’s return type when we invoke it.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><strong>@Primary</strong></p> 
 <p>We use the&nbsp; @Primary to give higher preference to a bean when there are multiple beans of the same type.</p> 
 <pre name="code" class="java">@Component
@Primary
class Car implements Vehicle {}
@Component
class Bike implements Vehicle {}
@Component
class Driver {
    @Autowired
    Vehicle vehicle;
}
@Component
class Biker {
    @Autowired
    @Qualifier("bike")
    Vehicle vehicle;
}</pre> 
 <p>&nbsp;</p> 
 <p><strong>@Scope</strong></p> 
 <p>We use the@Scope annotation to define the scope of a&nbsp; @Component class or the @Bean definition. It can be either singleton, prototype, request, session, globalSession, or some custom scope.</p> 
 <p>For example:</p> 
 <pre name="code" class="java">@Component
@Scope(value = ConfigurableBeanFactory.SCOPE_SINGLETON)
public class TwitterMessageService implements MessageService {
}
@Component
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class TwitterMessageService implements MessageService {
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@Profile</strong></p> 
 <p>If we want Spring to use the @Component class or the @Bean method only when a specific profile is active, we can mark it with&nbsp; @Profile. We can configure the name of the profile with the value argument of the annotation:</p> 
 <pre name="code" class="java">@Component
@Profile("sportDay")
class Bike implements Vehicle {}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@Import</strong></p> 
 <p>The&nbsp; @Import annotation indicates one or more @Configuration classes to import.</p> 
 <p>For example: in a Java-based configuration, Spring provides the @Import&nbsp; annotation, which allows the loading @Bean definitions from another configuration class.</p> 
 <pre name="code" class="java">@Configuration
public class ConfigA {
    @Bean
    public A a() {
        return new A();
    }
}
@Configuration
@Import(ConfigA.class)
public class ConfigB {
    @Bean
    public B b() {
        return new B();
    }
}
</pre> 
 <p style="font-size: 14px;">&nbsp;Now, rather than needing to specify both the ConfigA class and ConfigB class when instantiating the context, only ConfigB needs to be supplied explicitly.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@ImportResource</strong></p> 
 <p>Spring provides an @ImportResource annotation used to load beans from an applicationContext.xml file into an ApplicationContext. For example: consider that we have applicationContext.xml Spring bean configuration XML file on the classpath.</p> 
 <pre name="code" class="java">@Configuration
@ImportResource({"classpath*:applicationContext.xml"})
public class XmlConfiguration {
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><strong>@PropertySource</strong></p> 
 <p>The&nbsp; @PropertySource annotation provides a convenient and declarative mechanism for adding a PropertySource to Spring’s Eenvironment to be used in conjunction with the @Configuration classes.</p> 
 <p>For example, we are reading database configuration from the file config.propertiesfile and setting these property values to the DataSourceConfig class using the Environment.</p> 
 <pre name="code" class="java">import org.springframework.beans.factory.InitializingBean;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;
import org.springframework.core.env.Environment;
@Configuration
@PropertySource("classpath:config.properties")
public class ProperySourceDemo implements InitializingBean {
    @Autowired
    Environment env;
    @Override
    public void afterPropertiesSet() throws Exception {
        setDatabaseConfig();
    }
    private void setDatabaseConfig() {
        DataSourceConfig config = new DataSourceConfig();
        config.setDriver(env.getProperty("jdbc.driver"));
        config.setUrl(env.getProperty("jdbc.url"));
        config.setUsername(env.getProperty("jdbc.username"));
        config.setPassword(env.getProperty("jdbc.password"));
        System.out.println(config.toString());
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p><strong>@PropertySources</strong></p> 
 <p>We can use this annotation to specify multiple&nbsp; @PropertySource&nbsp; configurations:</p> 
 <pre name="code" class="java"> @PropertySources({
  @PropertySource("classpath:config.properties"),
  @PropertySource("classpath:db.properties")
 })
 public class AppConfig {
  //...
 }</pre> 
 <p>&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">============ 原文</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As we know,&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/06/guide-to-dependency-injection-in-spring.html" rel="nofollow" target="_blank">Spring DI</a>&nbsp;and&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-ioc-container-overview.html" rel="nofollow" target="_blank">Spring IOC</a>&nbsp;are core concepts of the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/p/spring-framework.html" rel="nofollow" target="_blank">Spring Framework</a>. Let's explore some Spring core annotations from the&nbsp;<em>org.springframework.beans.factory.annotation</em>&nbsp;and&nbsp;<em>org.springframework.context.annotation</em>&nbsp;packages.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We often call these “Spring core annotations,” and we’ll review them in this article.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Here's a list of all known Spring core annotations.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" src="https://dzone.com/storage/temp/10586750-spring-core-annotations.png" alt="Image title" width="620"></p> 
 <h2 style="font-size: 14px;">@Autowired</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We can use the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Autowired</code>&nbsp;annotation&nbsp;to mark the dependency that Spring is going to resolve and inject. We can use this annotation with a constructor, setter, or field injection.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><strong>Constructor Injection:</strong></p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@RestController</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class CustomerController {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    private CustomerService customerService;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public CustomerController(CustomerService customerService) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        this.customerService = customerService;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 170px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><strong>Setter Injection:</strong></p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.beans.factory.annotation.Autowired;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.web.bind.annotation.RestController;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@RestController</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class CustomerController {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    private CustomerService customerService;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void setCustomerService(CustomerService customerService) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        this.customerService = customerService;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 224px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><strong>Field Injection:</strong></p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.beans.factory.annotation.Autowired;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.web.bind.annotation.RestController;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@RestController</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class CustomerController {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    private CustomerService customerService;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 152px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  For more details, visit our articles about&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-autowired-annotation-with-example.html" rel="nofollow" target="_blank">@Autowired</a>&nbsp;and&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/06/guide-to-dependency-injection-in-spring.html" rel="nofollow" target="_blank">Guide to Dependency Injection in Spring</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Bean</h2> 
 <ul style="margin-bottom: 10px; color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <li style="padding-bottom: 8px;">&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Bean</code>&nbsp;is a method-level annotation and a direct analog of the XML element. The annotation supports some of the attributes offered by, such as the init-method, destroy-method, auto-wiring, and name.</li> 
  <li style="padding-bottom: 8px;">You can use the &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Bean</code>&nbsp;annotation in a &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Configuration</code>-annotated or&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Component</code>-annotated class.</li> 
 </ul> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The following is a simple example of an&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">@Bean</a>&nbsp;method declaration:</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.context.annotation.Bean;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.context.annotation.Configuration;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import com.companyname.projectname.customer.CustomerService;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import com.companyname.projectname.order.OrderService;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class Application {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public CustomerService customerService() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new CustomerService();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public OrderService orderService() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new OrderService();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 350px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The preceding configuration is equivalent to the following Spring XML:</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>&lt;beans&gt;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        &lt;bean id="customerService" class="com.companyname.projectname.CustomerService"/&gt;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        &lt;bean id="orderService" class="com.companyname.projectname.OrderService"/&gt;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>&lt;/beans&gt;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 80px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about the&nbsp;&nbsp;
  <code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Bean</code>&nbsp;annotation in this article&nbsp;&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">Spring @Bean Annotation with Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Qualifier</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This annotation helps fine-tune annotation-based auto-wiring. There may be scenarios when we create more than one bean of the same type and want to wire only one of them with a property. This can be controlled using the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Qualifier</code>&nbsp;annotation along with the &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Autowired</code>&nbsp;annotation.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Example: Consider the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">EmailService</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">SMSService</code>&nbsp;classes to implement the single &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">MessageService</code>&nbsp;interface.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Create the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">MessageService</code>&nbsp;interface for multiple message service implementations.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public interface MessageService {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void sendMsg(String message);</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 62px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Next, create implementations:&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">EmailService</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">SMSService</code>.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class EmailService implements MessageService{</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void sendMsg(String message) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>         System.out.println(message);</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 116px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class SMSService implements MessageService{</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void sendMsg(String message) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>         System.out.println(message);</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 116px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">It's time to see the usage of the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Qualifier</code>&nbsp;annotation.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public interface MessageProcessor {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void processMsg(String message);</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class MessageProcessorImpl implements MessageProcessor {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    private MessageService messageService;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    // setter based DI</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Qualifier("emailService")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void setMessageService(MessageService messageService) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        this.messageService = messageService;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    // constructor based DI</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public MessageProcessorImpl(@Qualifier("emailService") MessageService messageService) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        this.messageService = messageService;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void processMsg(String message) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        messageService.sendMsg(message);</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 458px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about this annotation in this article:&nbsp;&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/06/spring-qualifier-annotation-example.html" rel="nofollow" target="_blank">Spring @Qualifier Annotation Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Required</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Required</code>&nbsp;annotation is a method-level annotation and applied to the setter method of a bean.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This annotation simply indicates that the setter method must be configured to be dependency-injected with a value at configuration time.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For example,&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Required</code>&nbsp;on setter methods marks dependencies that we want to populate through XML:</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Required</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>void setColor(String color) {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    this.color = color;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 80px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>&lt;bean class="com.javaguides.spring.Car"&gt;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    &lt;property name="color" value="green" /&gt;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>&lt;/bean&gt;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 62px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Otherwise, the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">BeanInitializationException</code>&nbsp;will be thrown.</p> 
 <h2 style="font-size: 14px;">@Value</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The Spring&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation is used to assign default values to variables and method arguments. We can read Spring environment variables as well as system variables using the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The Spring&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation also supports SpEL. Let’s look at some of the examples of using the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><strong>Examples:</strong>&nbsp;We can assign a default value to a class property using the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("Default DBConfiguration")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private String defaultName;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 44px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation argument can be a string only, but Spring tries to convert it to the specified type. The following code will work fine and assign the boolean and integer values to the variable.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("true")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private boolean defaultBoolean;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("10")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private int defaultInt;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 98px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This demonstrates the Spring &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;—&nbsp;Spring Environment Property</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("${APP_NAME_NOT_FOUND}")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private String defaultAppName;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 44px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Next, assign system variables using the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;annotation.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("${java.home}")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private String javaHome;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("${HOME}")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private String homeDir;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 98px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Spring&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Value</code>&nbsp;&nbsp;– SpEL</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Value("#{systemProperties['java.home']}")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>private String javaHome;</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 44px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <h2 style="font-size: 14px;">@DependsOn</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@DependsOn</code>&nbsp;annotation can force Spring IoC containers to initialize one or more beans before the bean, which is annotated by the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@DependsOn</code>&nbsp;annotation.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@DependsOn</code>&nbsp;annotation may be used on any class directly or indirectly annotated with the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Component</code>&nbsp;or on methods annotated with the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">@Bean</a>.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Example: Let's create &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">FirstBean</code>&nbsp;and &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">SecondBean</code>&nbsp;classes. In this example, the &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">SecondBean</code>&nbsp;is initialized before bean &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">FirstBean</code>.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class FirstBean {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    private SecondBean secondBean;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class SecondBean {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public SecondBean() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        System.out.println("SecondBean Initialized via Constuctor");</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 206px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Declare the above beans in Java based&nbsp;on the configuration class.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class AppConfig {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean("firstBean")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @DependsOn(value = {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        "secondBean"</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    })</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public FirstBean firstBean() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new FirstBean();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean("secondBean")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public SecondBean secondBean() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new SecondBean();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 296px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about @DependsOn annotation on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-dependson-annotation-example.html" rel="nofollow" target="_blank">Spring - @DependsOn Annotation Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Lazy</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">By default, the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-ioc-container-overview.html" rel="nofollow" target="_blank">Spring IoC container</a>&nbsp;creates and initializes all singleton beans at the time of application startup. We can prevent this pre-initialization of a singleton bean by using the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Lazy</code>&nbsp;annotation.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Lazy</code>&nbsp;annotation may be used on any class, directly or indirectly annotated with the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Component</code>&nbsp;or on methods annotated with the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">@Bean</a>.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Example: Consider we have below two beans —&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">FirstBean</code>&nbsp;and &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">SecondBean</code>. In this example, we will explicitly load &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">FirstBean</code>&nbsp;using&nbsp;the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Lazy</code>annotation.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class FirstBean {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void test() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        System.out.println("Method of FirstBean Class");</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 98px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class SecondBean {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void test() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        System.out.println("Method of SecondBean Class");</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 98px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Declare the above beans in Java based on the configuration class.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class AppConfig {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Lazy(value = true)</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public FirstBean firstBean() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new FirstBean();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public SecondBean secondBean() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new SecondBean();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 260px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As we can see, bean&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">secondBean</code>&nbsp;is initialized by the Spring container, while the bean&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">firstBean</code>&nbsp;is initialized explicitly.</p> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about the&nbsp;&nbsp;
  <code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Lazy</code>&nbsp;&nbsp;annotation with a complete example on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-lazy-annotation-example.html" rel="nofollow" target="_blank">Spring - @Lazy Annotation Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Lookup</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">A method annotated with &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Lookup</code>&nbsp;tells Spring to return an instance of the method’s return type when we invoke it.</p> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Detailed information about this annotation can be found on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="https://www.baeldung.com/spring-lookup" rel="nofollow" target="_blank">Spring @LookUp Annotation</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Primary</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We use the&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Primary</code>&nbsp;to give higher preference to a bean when there are multiple beans of the same type.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Primary</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>class Car implements Vehicle {}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>class Bike implements Vehicle {}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>class Driver {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    Vehicle vehicle;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>class Biker {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Qualifier("bike")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    Vehicle vehicle;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 350px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about this annotation on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-primary-annotation-example.html" rel="nofollow" target="_blank">Spring - @Primary Annotation Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Scope</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We use the<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Scope</code>&nbsp;annotation to define the scope of a<em>&nbsp;&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Component</code>&nbsp;</em>class or the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">@Bean</a>&nbsp;definition. It can be either singleton, prototype, request, session, globalSession, or some custom scope.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For example:</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Scope(value = ConfigurableBeanFactory.SCOPE_SINGLETON)</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class TwitterMessageService implements MessageService {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class TwitterMessageService implements MessageService {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 170px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about the @Scope annotations on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-scope-annotation-with-singleton-scope-example.html" rel="nofollow" target="_blank">Spring @Scope annotation with Singleton Scope Example</a>and&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/10/spring-scope-annotation-with-prototype.html" rel="nofollow" target="_blank">Spring @Scope annotation with Prototype Scope Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Profile</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">If we want Spring to use the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Component</code>&nbsp;class or the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">@Bean</a>&nbsp;method only when a specific profile is active, we can mark it with &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Profile</code>. We can configure the name of the profile with the value argument of the annotation:</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Component</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Profile("sportDay")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>class Bike implements Vehicle {}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 62px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  You can read more about profiles in this&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="https://www.baeldung.com/spring-profiles" rel="nofollow" target="_blank">Spring Profiles</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@Import</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Import</code>&nbsp;annotation indicates one or more&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-configuration-annotation-with-example.html" rel="nofollow" target="_blank">@Configuration</a>&nbsp;classes to import.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For example: in a Java-based configuration, Spring provides the&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@Import</code>&nbsp;&nbsp;annotation, which allows the loading&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-bean-annotation-with-example.html" rel="nofollow" target="_blank">@Bean</a>&nbsp;definitions from another configuration class.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class ConfigA {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public A a() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new A();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Import(ConfigA.class)</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class ConfigB {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Bean</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public B b() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        return new B();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 332px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Now, rather than needing to specify both the&nbsp;<strong>ConfigA</strong>&nbsp;class and&nbsp;<strong>ConfigB</strong>&nbsp;class when instantiating the context, only&nbsp;<strong>ConfigB</strong>&nbsp;needs to be supplied explicitly.</p> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about the @Import annotation on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-import-annotation-with-example.html" rel="nofollow" target="_blank">Spring @Import Annotation</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@ImportResource</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Spring provides an&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@ImportResource</code>&nbsp;annotation used to load beans from an&nbsp;<em>applicationContext.xml</em>&nbsp;file into an&nbsp;<strong>ApplicationContext</strong>. For example: consider that we have applicationContext.xml Spring bean configuration XML file on the classpath.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@ImportResource({"classpath*:applicationContext.xml"})</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class XmlConfiguration {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 80px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about this annotation with a complete example on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-importresource-annotation-example.html" rel="nofollow" target="_blank">Spring @ImportResource Annotation</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@PropertySource</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@PropertySource</code>&nbsp;annotation provides a convenient and declarative mechanism for adding a&nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">PropertySource</code>&nbsp;to Spring’s Eenvironment to be used in conjunction with the&nbsp;<a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-configuration-annotation-with-example.html" rel="nofollow" target="_blank">@Configuration</a>&nbsp;classes.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For example, we are reading database configuration from the file&nbsp;<em>config.properties</em>file and setting these property values to the&nbsp;<strong>DataSourceConfig</strong>&nbsp;class using the Environment.</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.beans.factory.InitializingBean;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.beans.factory.annotation.Autowired;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.context.annotation.Configuration;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.context.annotation.PropertySource;</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>import org.springframework.core.env.Environment;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@Configuration</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>@PropertySource("classpath:config.properties")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>public class ProperySourceDemo implements InitializingBean {</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Autowired</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    Environment env;</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    @Override</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    public void afterPropertiesSet() throws Exception {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        setDatabaseConfig();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div>
         &nbsp;
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    private void setDatabaseConfig() {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        DataSourceConfig config = new DataSourceConfig();</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        config.setDriver(env.getProperty("jdbc.driver"));</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        config.setUrl(env.getProperty("jdbc.url"));</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        config.setUsername(env.getProperty("jdbc.username"));</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        config.setPassword(env.getProperty("jdbc.password"));</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>        System.out.println(config.toString());</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>    }</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>}</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 494px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about this annotation on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-propertysource-annotation-with-example.html" rel="nofollow" target="_blank">Spring @PropertySource Annotation with Example</a>.
 </blockquote> 
 <h2 style="font-size: 14px;">@PropertySources</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We can use this annotation to specify multiple &nbsp;<code style="font-family: monospace; font-size: 13px; padding: 2px 4px; color: #000000; background-color: transparent; white-space: normal; border-radius: 4px;">@PropertySource</code>&nbsp;&nbsp;configurations:</p> 
 <div class="CodeMirror cm-s-default" style="border: 1px solid #d9dcdd; font-family: monospace; overflow: hidden; font-size: 13px; clear: both; height: auto !important;"> 
  <div class="CodeMirror-scroll"> 
   <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 29px; margin-bottom: 0px; min-width: 319px; padding-right: 0px; padding-bottom: 0px;"> 
    <div> 
     <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
      <div> 
       <div class="CodeMirror-code"> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre> @PropertySources({</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>  @PropertySource("classpath:config.properties"),</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>  @PropertySource("classpath:db.properties")</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre> })</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre> public class AppConfig {</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre>  //...</pre> 
        </div> 
        <div> 
         <div class="CodeMirror-gutter-wrapper">
          &nbsp;
         </div> 
         <pre> }</pre> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
   </div> 
   <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 134px;">
    &nbsp;
   </div> 
  </div> 
 </div> 
 <blockquote style="padding: 8px 35px 12px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 975.797px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  Read more about this annotation on&nbsp;
  <a style="background: transparent; color: #29a8ff;" href="http://www.javaguides.net/2018/09/spring-propertysource-annotation-with-example.html" rel="nofollow" target="_blank">Spring @PropertySources Annotation</a>.
 </blockquote> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Hope you enjoyed this post on the best Spring annotations for your project! Happy coding!</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>