#spring batch(二）：核心部分(2)Spring batch的启动
###发表时间：2013-01-16
###分类：java,Spring,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1771208" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1771208</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;<strong style="font-size: 12px; font-family: Verdana, Arial, Helvetica, sans-serif; line-height: 1.5;">chapter 4、</strong><strong>Running batch jobs</strong></p> 
 <p>&nbsp;1、Spring Launch API：它的核心就是 JobLauncher 接口。</p> 
 <p>JobLauncher 的接口：</p> 
 <pre name="code" class="java">public interface JobLauncher {
	public JobExecution run(Job job, JobParameters jobParameters) throws (…);
}</pre> 
 <p>&nbsp;JobLauncher 需要2个参数：Job , JobParameters。</p> 
 <p>示例：</p> 
 <pre name="code" class="java">ApplicationContext context = (...)
JobLauncher jobLauncher = context.getBean(JobLauncher.class);
Job job = context.getBean(Job.class);
jobLauncher.run(
	job,
	new JobParametersBuilder()
	.addString("inputFile", "file:./products.txt")
	.addDate("date", new Date())
	.toJobParameters()
);</pre> 
 <p>&nbsp;job的参数是key-value的键值对的形式。Spring batch提供4种类型的job参数：string,long,double,date</p> 
 <p>[注意：一个job的参数定义了一个job的实例。而一个job实例有一个或更多个的执行上下文内容。这种执行的上下文，你可以把它看作是“一次尝试执行处理过程”]</p> 
 <p>一个JobLauncher必须依赖一个Job仓库（jobRepository）</p> 
 <p>示例：</p> 
 <pre name="code" class="xml">&lt;batch:job-repository id="jobRepository" /&gt;

&lt;bean id="jobLauncher" class="org.springframework.batch.core.launch.support.SimpleJobLauncher"&gt;
	&lt;property name="jobRepository" ref="jobRepository" /&gt;
&lt;/bean&gt;</pre> 
 <p>&nbsp;JobExecution 接口的示例，提供job的“运行、结束、失败”等状态的查询。</p> 
 <p>由于Job运行可能消耗非常长的时间，Spring batch同步和异步两种launcher。</p> 
 <p>异步的情况，用于类似于http请求启动job的情况。如果不是异步的启动job，会耗尽http的线程资源。</p> 
 <p>指定一个launcher是异步的，只需要给launcher的配置添加一个taskExecutor属性。</p> 
 <p>示例：</p> 
 <pre name="code" class="xml">&lt;task:executor id="executor" pool-size="10" /&gt;

&lt;bean id="jobLauncher" class="org.springframework.batch.core.launch.support.SimpleJobLauncher"&gt;
	&lt;property name="jobRepository" ref="jobRepository" /&gt;
	&lt;property name="taskExecutor" ref="executor" /&gt;
&lt;/bean&gt;</pre> 
 <p>&nbsp;</p> 
 <p>一、从命令行启动job</p> 
 <p>Triggering system ---&gt; Creates JVM process ---&gt; Spring Batch job</p> 
 <p>CommandLineJobRunner 是Spring batch的启动类。里面包含main函数。</p> 
 <p>运行CommandLineJobRunner的必要配置有：Spring的XML配置文件，Job，Job参数，程序退出编码。</p> 
 <p>可以把整个spring batch的项目打包成jar文件，用来运行程序。也可以指定classpath，指定CommandLineJobRunner的包中的路径来运行。</p> 
 <p>[注意：]CommandLineJobRunner是利用spring的ClassPathXmlApplicationContext来使用启动spring的，需要把spring的XML配置文件放在classpath目录内</p> 
 <pre name="code" class="c">java -classpath "./lib/*" org.springframework.batch.core.launch.support.CommandLineJobRunner import-products-job.xml importProductsJob inputFile=file:./products.txt date(date)=2010/12/08</pre> 
 <p>&nbsp;CommandLineJobRunner 指定参数，是name=value的键值对的形式，即名字后面跟随指定的值。在指定参数的时候，可以指定参数的类型（spring batch的参数类型有：string、long、double、date)，形式如下：name(type)=value &nbsp;如上面的date(date)=2010/12/08 。注意date的格式是yyyy/MM/dd</p> 
 <p><strong>Type &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Java Type &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Example</strong></p> 
 <p>String &nbsp; &nbsp; &nbsp;java.lang.String &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;inputFile(string)=products.txt</p> 
 <p>Date &nbsp; &nbsp; &nbsp; java.util.Date &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; date(date)=2010/12/08</p> 
 <p>Long &nbsp; &nbsp; &nbsp; Long &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; timeout(long)=1000</p> 
 <p>Double &nbsp; &nbsp;Double &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; delta(double)=20.1</p> 
 <p>参数的默认类型是string，上面的 inputFile=file:./products.txt 也可以写成 inputFile(string)=file:./products.txt</p> 
 <p>&nbsp;</p> 
 <p>CommandLineJobRunner是拥有运行返回值的。这个返回值默认的是：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">0 --&gt; The job completed successfully (COMPLETED).
1 --&gt; The job failed (FAILED).
2 --&gt; Used for errors from the command-line job runner—for example,the runner couldn’t find the job in the Spring application context.</pre> 
 <p>&nbsp;当然spring batch也允许你定制这个返回值来满足不同的需求，只要实现&nbsp;ExitCodeMapper 接口即可。</p> 
 <p>示例：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.batch.core.ExitStatus;
import org.springframework.batch.core.launch.support.ExitCodeMapper;

public class SkippedAwareExitCodeMapper implements ExitCodeMapper {
	@Override
	public int intValue(String exitCode) {
		if(ExitStatus.COMPLETED.getExitCode().equals(exitCode)) {
			return 0;
		} else if(ExitStatus.FAILED.getExitCode().equals(exitCode)) {
			return 1;
		} else if("COMPLETED WITH SKIPS".equals(exitCode)) {
			return 3;
		} else {
			return 2;
		}
	}
}</pre> 
 <p>&nbsp;这个SkippedAwareExitCodeMapper类，该如何使用呢？把它生命在spring的XML里面靠近job就可以了，CommandLineJobRunner 会自己感知到它并且使用的。</p> 
 <p>示例：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;bean class="com.manning.sbia.ch04.SkippedAwareExitCodeMapper" /&gt;

&lt;job id="importProductsJob" xmlns="http://www.springframework.org/schema/batch"&gt;
	(...)
&lt;/job&gt;</pre> 
 <p>&nbsp;</p> 
 <p>二、Job调度</p> 
 <p>&nbsp;(1)、UNIX-like的cron命令</p> 
 <p>示例：</p> 
 <pre name="code" class="c">0 4 * * ? acogoluegnes java -classpath "/usr/local/bin/sb/lib/*" org.springframework.batch.core.launch.support.CommandLineJobRunner import-products-job.xml importProductsJob inputFile=file:/home/sb/import/products.txt date=2010/12/08</pre> 
 <p>&nbsp;操作系统的cron命令的缺点也很明显，它会为每一个job启动一个java的进程。如果是频繁的启动job，会启动大量的java进程，消耗资源；另外，如果想在一个JVM里面启动多个job，这样job之间就可以进行内部的交互，显然这是cron做不到的。</p> 
 <p>&nbsp;(2)、基于java的scheduler</p> 
 <p>&nbsp;这里可以使用Quartz框架，还可以使用spring提供的task scheduler。</p> 
 <p>task scheduler的使用请参考spring reference，里面有详细的介绍。这里给出简单的例子。</p> 
 <p>java类：</p> 
 <pre name="code" class="java">public class SpringSchedulingLauncher {
	private Job job;
	private JobLauncher jobLauncher;
	
	public void launch() throws Exception {
		JobParameters jobParams = createJobParameters();
		jobLauncher.run(job, jobParams);
	}
	
	private JobParameters createJobParameters() {
		(...)
	}
	// --- setter / getter
}</pre> 
 <p>&nbsp;这里的setter/getter一定要书写，保证spring的XML能够注入属性。</p> 
 <p>使用spring的task配置调度：</p> 
 <pre name="code" class="xml">&lt;bean id="springSchedulingLauncher"
	class="com.manning.sbia.ch04.SpringSchedulingLauncher"&gt;
		&lt;property name="job" ref="job" /&gt;
		&lt;property name="jobLauncher" ref="jobLauncher" /&gt;
&lt;/bean&gt;

&lt;task:scheduler id="scheduler" /&gt;

&lt;task:scheduled-tasks scheduler="scheduler"&gt;
	&lt;task:scheduled ref="springSchedulingLauncher" method="launch" fixed-rate="1000" /&gt;
&lt;/task:scheduled-tasks&gt;
</pre> 
 <p>&nbsp;</p> 
 <p>三、从web触发job</p> 
 <p>可以在使用spring的web环境配置job。通过取得http request传递过来的参数，构建JobParameter，通过JobLauncher，为每一个http request请求启动一个job。可以使用Servlet，spring MVC，structs2等框架，进行触发。</p> 
 <p>还可以在spring的web环境中配置quartz的调度，来是web拥有job的能力，不过这种方法不会响应用户http request的请求。</p> 
 <p>&nbsp;</p> 
 <p>四、优雅地停止job的运行</p> 
 <p>&nbsp;谁需要停止job呢？从两个角度来考虑：使用者和开发者。</p> 
 <p>(1)、使用者可能由于某些原因，需要停止job的运行，比如发现job出现数据错误，或者接到领导的命令，需要停止job的工作。</p> 
 <p>(2)、开发者。在开发程序的过程中，开发者明确的知道一些业务逻辑需要停止job。比如，一个job运行的时间不能超过早上8点，如果超过这个时间需要停止job的运行，等等的情况。</p> 
 <p>使用者，如何停止job呢？</p> 
 <p>&nbsp; &nbsp; 调用JMX或者使用spring batch administration的管理web程序，停止job</p> 
 <p>在程序中调用JMX或者使用spring batch的JobOperator接口。</p> 
 <p>也可以在spring batch里面配置简单的JobOperator，</p> 
 <p>示例：</p> 
 <pre name="code" class="xml">&lt;bean id="jobOperator" class="org.springframework.batch.core.launch.support.SimpleJobOperator"&gt;
	&lt;property name="jobRepository" ref="jobRepository"/&gt;
	&lt;property name="jobLauncher" ref="jobLauncher" /&gt;
	&lt;property name="jobRegistry" ref="jobRegistry" /&gt;
	&lt;property name="jobExplorer" ref="jobExplorer" /&gt;
&lt;/bean&gt;

&lt;batch:job-repository id="jobRepository" data-source="dataSource" /&gt;

&lt;bean id="jobLauncher" class="org.springframework.batch.core.launch.support.SimpleJobLauncher"&gt;
	&lt;property name="jobRepository" ref="jobRepository" /&gt;
&lt;/bean&gt;

&lt;bean class="org.springframework.batch.core.configuration.support.JobRegistryBeanPostProcessor"&gt;
	&lt;property name="jobRegistry" ref="jobRegistry" /&gt;
&lt;/bean&gt;

&lt;bean id="jobRegistry"class="org.springframework.batch.core.configuration.support.MapJobRegistry" /&gt;

&lt;bean id="jobExplorer" class="org.springframework.batch.core.explore.support.JobExplorerFactoryBean"&gt;
	&lt;property name="dataSource" ref="dataSource" /&gt;
&lt;/bean&gt;

&lt;bean class="org.springframework.jmx.export.MBeanExporter"&gt;
	&lt;property name="beans"&gt;
		&lt;map&gt;
			&lt;entry key="com.manning.sbia:name=jobOperator" value-ref="jobOperator" /&gt;
		&lt;/map&gt;
	&lt;/property&gt;
&lt;/bean&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;job停止的过程的可能情况：</p> 
 <p>a、代码中的job运行的之后，检查Thread.currentThread().isInterrupted()的状态，则job会马上停止。</p> 
 <p>b、job中的程序在运行逻辑代码，只有当这些业务完成之后，程序的管理权交回到spring batch的时候，才会被终止。如果中间的业务运行需要很长的时间，则job不会马上停止。</p> 
 <p>&nbsp;</p> 
 <p>开发者，如何停止job呢？</p> 
 <p>(1)、运行的过程中抛出一个exception，造成job的停止。</p> 
 <p>(2)、利用StepExecution来设置一个标识，停止job的运行。</p> 
 <p>最好的办法是，利用StepExecution来设置一个标识，停止job的运行。</p> 
 <p>代码：StepExecution.setTerminateOnly()</p> 
 <p>如何获得StepExecution 呢？</p> 
 <p>a、在Tasklet接口的方法中有StepExecution参数，可以进行调用。</p> 
 <p>示例：</p> 
 <pre name="code" class="java">public class ProcessItemsTasklet implements Tasklet {
	@Override
	public RepeatStatus execute(StepContribution contribution,
			ChunkContext chunkContext) throws Exception {
		if(shouldStop()) {
			chunkContext.getStepContext().getStepExecution().setTerminateOnly();
		}
		processItem();
		if(moreItemsToProcess()) {
			return RepeatStatus.CONTINUABLE;
		} else {
			return RepeatStatus.FINISHED;
		}
		}
		(...)
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;b、面向“块”的step中，ItemReader, ItemProcessor, 和 ItemWriter 这3个接口中，你会惊奇的发现它们中间没有&nbsp;StepExecution。那么你该如何在“块”Chunk中获得StepExecution 而停止程序呢？在Listener中，可以找到StepExecution。</p> 
 <p>示例：</p> 
 <pre name="code" class="java">public class StopListener {
	private StepExecution stepExecution;
	@BeforeStep
	public void beforeStep(StepExecution stepExecution) {
		this.stepExecution = stepExecution;
	}
	
	@AfterRead
	public void afterRead() {
		if(stopConditionsMet()) {
			stepExecution.setTerminateOnly();
		}
	}
	(...)
}</pre> 
 <p>&nbsp;</p> 
 <p>spring batch 的listener的配置文件：</p> 
 <pre name="code" class="xml">&lt;bean id="stopListener" class="com.manning.sbia.ch04.stop.StopListener" /&gt;

&lt;batch:job id="importProductsJob"&gt;
	&lt;batch:step id="importProductsStep"&gt;
		&lt;batch:tasklet&gt;
			&lt;batch:chunk reader="reader" writer="writer" commit-interval="100"/&gt;
			&lt;batch:listeners&gt;
				&lt;batch:listener ref="stopListener" /&gt;
			&lt;/batch:listeners&gt;
		&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;[备注：] 可以把schedule调度和停止job结合起来。可以定时调用一个程序，来停止job的运行。可以把这个定时停止job的任务和spring batch放在一个spring的上下文中，在一个java进程中运行。</p> 
 <p>&nbsp;从业务逻辑的需要出发，停止job的最佳的方式，还是设置stepExecution.setTerminateOnly();这个job停止标识，来让job停止运行。</p> 
 <p>&nbsp;</p> 
</div>