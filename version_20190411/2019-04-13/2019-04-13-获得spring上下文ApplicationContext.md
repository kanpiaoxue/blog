#获得spring上下文ApplicationContext
###发表时间：2019-04-13
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2440031" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2440031</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>在项目中实现&nbsp;<span style="background-color: #fafafa; font-family: monospace;">ApplicationContextAware 的接口，并且将实现类注册成为组件&nbsp;</span><span style="font-family: monospace;">@Component ，就能得到spring的上下文ApplicationContext</span><span style="font-family: monospace;">。</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;
import org.springframework.stereotype.Component;

/**
 * @ClassName: ApplicationContextProvider
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/04/12 12:01:39
 * @Description: 
 */
@Component
public class ApplicationContextProvider implements ApplicationContextAware {
    private static ApplicationContext applicationContext;

    public static ApplicationContext getApplicationContext() {
        return applicationContext;
    }

    /*
     * (non-Javadoc)
     * @see
     * org.springframework.context.ApplicationContextAware#setApplicationContext
     * (org.springframework.context.ApplicationContext)
     */
    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        ApplicationContextProvider.applicationContext = applicationContext;

    }

}</pre> 
 <p>&nbsp;</p> 
 <p>使用：</p> 
 <pre name="code" class="java">ApplicationContext applicationContext = ApplicationContextProvider.getApplicationContext();</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>