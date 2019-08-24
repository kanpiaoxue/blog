#spring配置ThreadPoolExecutor
###发表时间：2018-08-01
###分类：Spring,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2427917" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2427917</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;我想使用JDK自带的线程池，如何使用spring配置呢？</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.example.utils;
import java.util.concurrent.ThreadFactory;
import org.apache.commons.lang3.StringUtils;
import org.apache.commons.lang3.concurrent.BasicThreadFactory;

public class ThreadPool {
    /**
     *
     * @param pattern
     *            线程池的名字模式，格式如：threadName-%d
     * @return 线程工厂
     * @author kanpiaoxue
     * @CreateTime: 2018/08/01 20:30:10
     * @Description: 创建带有线程池的名字模式的线程工厂
     */
    public static ThreadFactory newThreadFactory(String pattern) {
        BasicThreadFactory factory = new BasicThreadFactory.Builder()
                .namingPattern(StringUtils.isNotBlank(pattern) ? pattern : "thread-pool-%d").build();
        return factory;
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>spring xml</p> 
 <pre name="code" class="xml">&lt;!-- 配置threadFactory，用来为线程池命名 --&gt;
&lt;bean id="threadFactory" class="org.kanpiaoxue.example.utils.ThreadPool"
    factory-method="newThreadFactory"&gt;
    &lt;!-- 注意 constructor-arg 的用法（javadoc原文）：Note: A single generic argument value will just be used once, 
    rather than potentially matched multiple times (as of Spring 1.1). constructor-arg elements are also used in 
    conjunction with the factory-method element to construct beans using static or instance factory methods.
    不仅仅可以为javabean的构造函数使用，同样可以传递参数给类的静态工厂方法作为参数
     --&gt;
    &lt;constructor-arg index="0" type="java.lang.String" value="messageConsumer-%d"/&gt;
&lt;/bean&gt;

&lt;!-- 配置java.util.concurrent.ThreadPoolExecutor的线程池 --&gt;
&lt;bean id="mqDictMessageConsumerThreadPoolExector" class="java.util.concurrent.ThreadPoolExecutor"
    lazy-init="true" scope="singleton"&gt;
    &lt;constructor-arg index="0" type="int"
        value="$(threadPoolExecutor.corePoolSize:5)" /&gt;
    &lt;constructor-arg index="1" type="int"
        value="$(threadPoolExecutor.maximumPoolSize:10)" /&gt;
    &lt;constructor-arg index="2" type="long"
        value="$(threadPoolExecutor.keepAliveTime:60)" /&gt;
    &lt;constructor-arg index="3" type="java.util.concurrent.TimeUnit"
        value="java.util.concurrent.TimeUnit.SECONDS" /&gt;
    &lt;constructor-arg index="4"
        type="java.util.concurrent.BlockingQueue" value="java.util.concurrent.LinkedBlockingQueue" /&gt;
    &lt;constructor-arg index="5"
        type="java.util.concurrent.ThreadFactory" ref="threadFactory" /&gt;
&lt;/bean&gt;</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>setting.properties 配置文件</p> 
 <pre name="code" class="java">threadPoolExecutor.corePoolSize=10
threadPoolExecutor.maximumPoolSize=20
threadPoolExecutor.keepAliveTime=60</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>