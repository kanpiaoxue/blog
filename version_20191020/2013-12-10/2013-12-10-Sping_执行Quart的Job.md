#Sping 执行Quart的Job
###发表时间：2013-12-10
###分类：java,Spring,quartz
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1987711" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1987711</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>这里给出一个Spring执行Quartz的Job的情况：</p> 
 <p>这个支持 <span style="color: #ff0000; background-color: #c0c0c0;">Quartz1.x 和&nbsp;Quartz2.x</span> 的Quartz的版本。</p> 
 <pre name="code" class="java">public interface Job extends State{
	public void execute();
}

public class InitializeDataSourceMapJob implements Job {
	private static final Logger LOGGER = LoggerFactory
			.getLogger(InitializeDataSourceMapJob.class);
	@Override
	public void execute() {
		if(LOGGER.isInfoEnabled()){
			LOGGER.info(this.getClass().getName() +" start to work.");
		}
	}

}</pre> 
 <p>&nbsp;spring的配置文件：</p> 
 <pre name="code" class="java">	&lt;!-- job start --&gt;
	&lt;!-- 这里我指定 init-method="execute" 主要是希望这个job能在类在加载的过程中就被运行。你可以去掉。--&gt;
	&lt;bean id="initializeDataSourceMapJob" class="test.job.impl.InitializeDataSourceMapJob"
		init-method="execute"/&gt;
	
	&lt;bean id="initializeDataSourceMapJobDetail"
		class="org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean"&gt;
		&lt;property name="targetObject" ref="initializeDataSourceMapJob" /&gt;
		&lt;property name="targetMethod" value="execute" /&gt;
		&lt;property name="concurrent" value="false" /&gt;
	&lt;/bean&gt;
	&lt;bean id="initializeDataSourceMapJobCronTrigger"
		class="org.springframework.scheduling.quartz.CronTriggerFactoryBean"&gt;
		&lt;property name="jobDetail" ref="initializeDataSourceMapJobDetail" /&gt;
		&lt;property name="cronExpression" value="0 0/2 * * * ? *" /&gt;
	&lt;/bean&gt;
	&lt;bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean"&gt;
		&lt;property name="triggers"&gt;
			&lt;list&gt;
				&lt;ref bean="initializeDataSourceMapJobCronTrigger" /&gt;
			&lt;/list&gt;
		&lt;/property&gt;
	&lt;/bean&gt;
	&lt;!-- job end --&gt;</pre> 
 <p>&nbsp;</p> 
</div>