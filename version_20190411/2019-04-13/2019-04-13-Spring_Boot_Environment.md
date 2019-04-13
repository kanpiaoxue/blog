#Spring Boot Environment
###发表时间：2019-04-13
###分类：Spring,springboot,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2440025" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2440025</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>如何在springboot里面直接读取配置文件里面的内容呢？</p> 
 <p>我们可以使用Environment.</p> 
 <pre name="code" class="java">import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.core.env.Environment;

@SpringBootApplication
public class Application implements CommandLineRunner {

    @Autowired
    private Environment env;    
    
    @Override
    public void run(String... args) throws Exception {

        System.out.println(env.getProperty("JAVA_HOME"));
        System.out.println(env.getProperty("app.name"));
    }
    
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }    
}</pre> 
 <p>&nbsp;</p> 
</div>