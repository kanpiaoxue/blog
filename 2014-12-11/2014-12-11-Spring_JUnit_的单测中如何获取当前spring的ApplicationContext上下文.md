#Spring JUnit 的单测中如何获取当前spring的ApplicationContext上下文
###发表时间：2014-12-11
###分类：java,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2165172" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2165172</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我在写单测的时候（spring环境下的单元测试）想获得当前spring的ApplicationContext上下文。我是这样实现的：</p> 
 <pre name="code" class="java">import org.junit.Assert;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

/**
 * &lt;pre&gt;
 * TestGetApplicationContext.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年12月11日 下午2:44:36&lt;br&gt;
 * Description : Spring JUnit 的单测中如何获取当前spring的ApplicationContext上下文
 * &lt;/pre&gt;
 */
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath:spring-ctx-sf-application.xml")
public class TestGetApplicationContext implements ApplicationContextAware {

    private ApplicationContext applicationContext;

    /*
     * (non-Javadoc)
     * @see
     * org.springframework.context.ApplicationContextAware#setApplicationContext
     * (org.springframework.context.ApplicationContext)
     */
    @Override
    public void setApplicationContext(ApplicationContext arg0)
            throws BeansException {
        this.applicationContext = arg0;
    }

    @Test
    public void testGetApplicationContext() {
        System.out.println(applicationContext);
        Assert.assertNotNull(applicationContext);
    }
}</pre> 
 <p>&nbsp;</p> 
</div>