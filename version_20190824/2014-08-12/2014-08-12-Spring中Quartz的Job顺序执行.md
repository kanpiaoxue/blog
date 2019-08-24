#Spring中Quartz的Job顺序执行
###发表时间：2014-08-12
###分类：Spring,java,quartz
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2103210" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2103210</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p><span style="line-height: 25.200000762939453px; font-size: 12px;">使用Quartz做计划任务时，默认情况下，当前任务总会执行，无论前一个任务是否结束。</span></p> 
 <p><span style="font-size: 12px;"><span style="line-height: 25.200000762939453px;">使用Spring配置Quartz的Job的时候，也是默认</span><span style="line-height: 25.200000762939453px;">当前任务总会执行，无论前一个任务是否结束。</span></span></p> 
 <p><span style="line-height: 25.200000762939453px; font-size: 12px;">因此，如果采用默认条件，需要考虑并发执行的逻辑问题，否则需要设置为顺序执行。</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">我写了一个Spring配置Quartz的Demo。里面Spring的xml中</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">代码如下：</span></p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:jee="http://www.springframework.org/schema/jee"
	xmlns:jms="http://www.springframework.org/schema/jms" xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:oxm="http://www.springframework.org/schema/oxm"
	xmlns:p="http://www.springframework.org/schema/p" xmlns:sec="http://www.springframework.org/schema/security"
	xmlns:task="http://www.springframework.org/schema/task" xmlns:tx="http://www.springframework.org/schema/tx"

	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-4.0.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-4.0.xsd
		http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-4.0.xsd
		http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-4.0.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
		http://www.springframework.org/schema/oxm http://www.springframework.org/schema/oxm/spring-oxm-4.0.xsd
		http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security-4.0.xsd
		http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-4.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd"&gt;



	&lt;bean id="testJob"
		class="org.kanpiaoxue.learn.quartz.disallowConcurrentExecution.TestJob" /&gt;

	&lt;bean id="testJobDetail"
		class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean"&gt;
		&lt;property name="targetObject" ref="testJob" /&gt;
		&lt;property name="targetMethod" value="execute" /&gt;
		&lt;!-- 使用Quartz做计划任务时，默认情况下，当前任务总会执行，无论前一个任务是否结束。
			设置 &lt;property name="concurrent" value="false" /&gt; 可以让Job顺序执行。
			设置 &lt;property name="concurrent" value="true" /&gt; 可以让Job并行执行，而不用管上一个Job是否结束。
		 --&gt;
		&lt;property name="concurrent" value="false" /&gt;
	&lt;/bean&gt;
	&lt;bean id="testJobCronTrigger"
		class="org.springframework.scheduling.quartz.CronTriggerFactoryBean"&gt;
		&lt;property name="jobDetail" ref="testJobDetail" /&gt;
		&lt;!-- 间隔1秒钟执行一次 --&gt;
		&lt;property name="cronExpression" value="0/1 * * * * ? *" /&gt;
	&lt;/bean&gt;

	&lt;bean id="taskExecutor"
		class="org.kanpiaoxue.learn.quartz.disallowConcurrentExecution.ThreadPoolExecutorImpl"&gt;
		&lt;constructor-arg name="nThreads" value="30" /&gt;
	&lt;/bean&gt;

	&lt;bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean"&gt;
		&lt;property name="taskExecutor" ref="taskExecutor" /&gt;
		&lt;property name="triggers"&gt;
			&lt;list&gt;
				&lt;ref bean="testJobCronTrigger" /&gt;
			&lt;/list&gt;
		&lt;/property&gt;
	&lt;/bean&gt;
	&lt;!-- job end --&gt;
&lt;/beans&gt;</pre> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">&nbsp;</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">Main函数的入口类如下：</span></p> 
 <pre name="code" class="java">import org.springframework.context.support.FileSystemXmlApplicationContext;

/**
 * &lt;pre&gt;
 * Test.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月12日 下午6:45:06&lt;br&gt;
 * Description : main函数入口
 * &lt;/pre&gt;
 */
public class Test {

    /**
     * &lt;pre&gt;
     * @param args
     * &lt;/pre&gt;
     */
    @SuppressWarnings("resource")
    public static void main(String[] args) {
        new FileSystemXmlApplicationContext(
                "D:/org/kanpiaoxue/learn/quartz/disallowConcurrentExecution/spring-ctx-application.xml");

    }

}</pre> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">&nbsp;</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">Job的测试类如下：</span></p> 
 <pre name="code" class="java">import org.joda.time.DateTime;
import java.util.concurrent.TimeUnit;

/**
 * &lt;pre&gt;
 * TestJob.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月12日 下午6:45:48&lt;br&gt;
 * Description : Job测试类
 * &lt;/pre&gt;
 */
public class TestJob {
    public TestJob() {
    }

    public void execute() throws InterruptedException {

        System.out.println(String.format("[%s] %s start to work", getNow(),
                Thread.currentThread().getName()));

        /**
         * 让Job沉睡20秒，模拟当前Job一直在执行任务的情形。
         */
        TimeUnit.SECONDS.sleep(20L);

        System.out.println(String.format("[%s] %s wake up.", getNow(), Thread
                .currentThread().getName()));
    }

    private String getNow() {
        return DateTime.now().toString("yyyy-MM-dd HH:mm:ss");
    }
}</pre> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">&nbsp;</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">如果不设置Spring的Quartz执行的线程大小，默认是：10个</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">我们也可以指定线程池的大小，代码如下：</span></p> 
 <pre name="code" class="java">import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

/**
 * &lt;pre&gt;
 * ThreadPoolExecutorImpl.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月12日 下午7:04:44&lt;br&gt;
 * Description : 线程池类
 * &lt;/pre&gt;
 */
public class ThreadPoolExecutorImpl extends ThreadPoolExecutor {

    /**
     * &lt;pre&gt;
     * @param nThreads 线程池的大小
     * &lt;/pre&gt;
     */
    public ThreadPoolExecutorImpl(int nThreads) {
        super(nThreads, nThreads, 0L, TimeUnit.MILLISECONDS,
                new LinkedBlockingQueue&lt;Runnable&gt;());
    }

}</pre> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">&nbsp;</span></p> 
 <p><span style="font-size: 12px; line-height: 25.200000762939453px;">通过在Spring的XML中配置&nbsp;</span><span style="font-size: 12px; line-height: 25.200000762939453px;">org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean 的&nbsp;</span><span style="font-family: monospace;"><span style="font-size: 12px; line-height: 25.200000762939453px;">concurrent 的属性，可以决定Quartz的Job是否顺序执行，还是不考虑顺序的并行执行。</span></span></p> 
 <p><span style="font-family: monospace;"><span style="font-size: 12px; line-height: 25.200000762939453px;">查看&nbsp;MethodInvokingJobDetailFactoryBean 关于&nbsp;</span></span><span style="font-family: monospace; font-size: 12px; line-height: 25.200000762939453px;">concurrent 属性</span><span style="font-size: 12px; line-height: 25.200000762939453px; font-family: monospace;">的原码，可以发现默认是“并行”的。</span></p> 
 <p>&nbsp;<span style="font-family: monospace; font-size: 12px; line-height: 25.200000762939453px;">MethodInvokingJobDetailFactoryBean&nbsp;的部分原码：</span></p> 
 <pre name="code" class="java">public class MethodInvokingJobDetailFactoryBean extends ArgumentConvertingMethodInvoker
		implements FactoryBean&lt;JobDetail&gt;, BeanNameAware, BeanClassLoaderAware, BeanFactoryAware, InitializingBean {

	private static Class&lt;?&gt; jobDetailImplClass;

	private static Method setResultMethod;

	static {
		try {
			jobDetailImplClass = Class.forName("org.quartz.impl.JobDetailImpl");
		}
		catch (ClassNotFoundException ex) {
			jobDetailImplClass = null;
		}
		try {
			Class&lt;?&gt; jobExecutionContextClass =
					QuartzJobBean.class.getClassLoader().loadClass("org.quartz.JobExecutionContext");
			setResultMethod = jobExecutionContextClass.getMethod("setResult", Object.class);
		}
		catch (Exception ex) {
			throw new IllegalStateException("Incompatible Quartz API: " + ex);
		}
	}


	private String name;

	private String group = Scheduler.DEFAULT_GROUP;

	private boolean concurrent = true;</pre> 
 <p>&nbsp;关于Quartz原生的Job的顺序执行，请参考文章：&nbsp;<a href="http://feuyeux.iteye.com/blog/1842966">http://feuyeux.iteye.com/blog/1842966</a></p> 
</div>