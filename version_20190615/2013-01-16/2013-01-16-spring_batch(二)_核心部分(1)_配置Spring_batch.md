#spring batch(二）：核心部分(1)：配置Spring batch
###发表时间：2013-01-16
###分类：Spring,经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1770683" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1770683</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;"><strong>chapter 3、</strong><strong>Batch configuration</strong></p> 
 <p style="font-size: 14px;">1、spring batch 的命名空间</p> 
 <p style="font-size: 14px;">spring xml中指定batch的前缀作为命名空间。</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:batch="http://www.springframework.org/schema/batch"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
	http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/batch
	http://www.springframework.org/schema/batch/spring-batch.xsd"&gt;
	
	&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;/batch:job&gt;
&lt;/beans&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">当指定batch命名空间之后，bean中的声明都需要加上batch的前缀，例如：&lt;batch:job id="importProductsJob"&gt;</p> 
 <p style="font-size: 14px;">spring的命名空间的前缀可以指定任意的名称，这里采用batch作为前缀，为了方便理解。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">2、spring batch XML的主要标签有：job、step、tasklet、chunk、job-repository</p> 
 <p style="font-size: 14px;">3、Job配置。job元素是整个配置的顶级元素，它的属性有：</p> 
 <p style="font-size: 14px;">a、id</p> 
 <p style="font-size: 14px;">b、restartable</p> 
 <p style="font-size: 14px;">c、incrementer</p> 
 <p style="font-size: 14px;">d、abstract</p> 
 <p style="font-size: 14px;">e、parent</p> 
 <p style="font-size: 14px;">f、job-repository</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">restartable 属性如果是false，则程序不允许重启。如果发生重启，会抛出JobRestartException异常。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">&lt;batch:job id="importProductsJob" restartable="false"&gt;
    (...)
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;job除了这些属性外，还可以配置验证器&lt;batch:validator ref="parameterValidator" /&gt;，用来校验工作参数(job parameters)，可以实现JobParametersValidator接口。</p> 
 <p style="font-size: 14px;">如果无法通过验证，会抛出JobParametersInvalidException异常。spring batch提供了一个默认的实现类DefaultJobParametersValidator，完成绝大部分的工作。如果还是无法满足需求，可以自己编码实现接口。</p> 
 <p style="font-size: 14px;">实例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:validator ref="validator"/&gt;
&lt;/batch:job&gt;
&lt;bean id="validator" class="org.springframework.batch.core.job.DefaultJobParametersValidator"&gt;
	&lt;property name="requiredKeys"&gt;
		&lt;set&gt;
			&lt;value&gt;date&lt;/value&gt;
		&lt;/set&gt;
	&lt;/property&gt;
	&lt;property name="optionalKeys"&gt;
		&lt;set&gt;
			&lt;value&gt;productId&lt;/value&gt;
		&lt;/set&gt;
	&lt;/property&gt;
&lt;/bean&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">4、step步骤的配置。</p> 
 <p style="font-size: 14px;">step的属性：</p> 
 <p style="font-size: 14px;">a、next</p> 
 <p style="font-size: 14px;">b、parent</p> 
 <p style="font-size: 14px;">c、abstract</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">&lt;job id="importProductsJob"&gt;
	&lt;step id="decompress" next="readWrite"&gt;
		(...)
	&lt;/step&gt;
	&lt;step id="readWrite"&gt;
		(...)
	&lt;/step&gt;
&lt;/job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">5、tasklet和chunk的配置。</p> 
 <p style="font-size: 14px;">tasklet和chunk是用来指定处理过程的。</p> 
 <p style="font-size: 14px;">一个tasklet对应于一个事务性的、潜在可重复的过程中发生的一个步骤。</p> 
 <p style="font-size: 14px;">你可以自己实现Tasklet 接口，定义自己的tasklet。这个特性很有用，比如：用于解压文件，执行系统命令，执行存储过程等待。</p> 
 <p style="font-size: 14px;">你也可以使用系统tasklet的属性有：</p> 
 <p style="font-size: 14px;">a、ref指定应用的bean</p> 
 <p style="font-size: 14px;">b、transaction-manager事物管理器</p> 
 <p style="font-size: 14px;">c、start-limittasklet重试retry的次数</p> 
 <p style="font-size: 14px;">d、allow-start-if-complete如果tasklet成功完成之后，是否可以进行重试retry操作。</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:step id="readWriteStep"&gt;
		&lt;batch:tasklet
			transaction-manager="transactionManager"
			start-limit="3"
			allow-start-if-complete="true"&gt;
			(...)
		&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;
&lt;bean id="transactionManager" class="(...)"&gt;
	(...)
&lt;/bean&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">chunk ，ChunkOrientedTasklet 类实现类“块处理(chunk processing)”。</p> 
 <p style="font-size: 14px;">配置tasklet很简单，但是配置“块处理”就会复杂一点，因为它涉及的内容更多。</p> 
 <p style="font-size: 14px;">chunk的属性有：</p> 
 <p style="font-size: 14px;">a、reader</p> 
 <p style="font-size: 14px;">b、processor</p> 
 <p style="font-size: 14px;">c、writer</p> 
 <p style="font-size: 14px;">d、commit-interval事物提交一次处理的items的数量。也是chunk的大小。</p> 
 <p style="font-size: 14px;">e、skip-limit跳跃的次数</p> 
 <p style="font-size: 14px;">f、skip-policy跳跃的策略：要实现SkipPolicy接口</p> 
 <p style="font-size: 14px;">g、retry-policy重试的策略：要实现RetryPolicy接口</p> 
 <p style="font-size: 14px;">h、retry-limit最大的重试次数</p> 
 <p style="font-size: 14px;">i、cache-capacity重试的缓存策略</p> 
 <p style="font-size: 14px;">j、reader-transactional-queue从一个拥有事务的JMS的queue读取item数据</p> 
 <p style="font-size: 14px;">k、processor-transactional处理器是否包含事务处理</p> 
 <p style="font-size: 14px;">l、chunk-completion-policychunk的完成策略</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:step id="readWrite"&gt;
		&lt;batch:tasklet&gt;
			&lt;batch:chunk
				reader="productItemReader"
				processor="productItemProcessor"
				writer="productItemWriter"
				commit-interval="100" 
				skip-limit="20"
				retry-limit="3"
				cache-capacity="100"
				chunk-completion-policy="timeoutCompletionPolicy"/&gt;
		&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;
&lt;bean id="productItemReader" class="(...)"&gt;
(...)
&lt;/bean&gt;
&lt;bean id="productItemProcessor" class="(...)"&gt;
(...)
&lt;/bean&gt;
&lt;bean id="productItemWriter" class="(...)"&gt;
(...)
&lt;/bean&gt;
&lt;bean id="timeoutCompletionPolicy"
	class="org.springframework.batch.repeat.policy.TimeoutTerminationPolicy"&gt;
		&lt;constructor-arg value="60"/&gt;
&lt;/bean&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">chunk还有几个子标签，包括：reader、processor、writer、skip-policy、retry-policy</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:step id="readWrite"&gt;
		&lt;batch:tasklet&gt;
			&lt;batch:chunk commit-interval="100"&gt;
				&lt;batch:reader&gt;
					&lt;bean class="(...)"&gt;
						(...)
					&lt;/bean&gt;
				&lt;/batch:reader&gt;
				&lt;batch:processor&gt;
					&lt;bean class="(...)"&gt;
						(...)
					&lt;/bean&gt;
				&lt;/batch:processor&gt;
				&lt;batch:writer&gt;
					&lt;bean class="(...)"&gt;
						(...)
					&lt;/bean&gt;
				&lt;/batch:writer&gt;
			&lt;/batch:chunk&gt;
		&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">chunk的一些其他额外的子标签：retry-listeners、skippable-exception-classes、retryable-exception-classes、streams</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:step id="readWrite"&gt;
		&lt;batch:tasklet&gt;
			&lt;batch:chunk commit-interval="100"
				skip-limit="10"&gt;
				&lt;skippable-exception-classes&gt;
					&lt;include class="org.springframework.batch.item.file.FlatFileParseException"/&gt;
					&lt;exclude class="java.io.FileNotFoundException"/&gt;
				&lt;/skippable-exception-classes&gt;
			&lt;/batch:chunk&gt;
		&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">在chunk里面配置streams</p> 
 <p style="font-size: 14px;">示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:step id="readWrite"&gt;
			&lt;batch:tasklet&gt;
				&lt;batch:chunk reader="productItemReader" writer="compositeWriter"/&gt;
				&lt;streams&gt;
					&lt;stream ref="productItemWriter1"/&gt;
					&lt;stream ref="productItemWriter2"/&gt;
				&lt;/streams&gt;
			&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;

&lt;bean id="compositeWriter"
	class="org.springframework.batch.item.support.CompositeItemWriter"&gt;
	&lt;property name="delegates"&gt;
		&lt;list&gt;
			&lt;ref bean="productItemWriter1"/&gt;
			&lt;ref bean="productItemWriter2"/&gt;
		&lt;/list&gt;
	&lt;/property&gt;
&lt;/bean&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">使用一个复合的stream形式，如上例的itemWriter，内部是writer1和writer2是stream的，需要在chunk里面的streams元素里面注册。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">6、事务配置。</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; 事务是spring batch的一个重要主题。主要作用于batch处理程序的健壮性，chunk处理的合并来完成它的工作。因为事务调用的对象类型不同，你可以在不同的层次配置事务。</p> 
 <p style="font-size: 14px;">示例:</p> 
 <pre name="code" class="xml">&lt;batch:job id="importProductsJob"&gt;
	(...)
	&lt;batch:step id="readWrite"&gt;
		&lt;batch:tasklet transaction-manager="transactionManager" (...)&gt;
			(...)
		&lt;/batch:tasklet&gt;
	&lt;/batch:step&gt;
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;事务，有几个定义的属性：行为，隔离 isolation，超时 timeout。</p> 
 <p style="font-size: 14px;">spring batch提供transaction-attributes标签来描述这些事务的属性。</p> 
 <p style="font-size: 14px;">&nbsp;示例：</p> 
 <pre name="code" class="xml">&lt;batch:tasklet&gt;
	&lt;batch:chunk reader="productItemReader"
		writer="productItemReader"
		commit-interval="100"/&gt;
		&lt;batch:transaction-attributes isolation="DEFAULT"
		propagation="REQUIRED"
		timeout="30"/&gt;
	&lt;/batch:chunk&gt;
&lt;/batch:tasklet&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;isolation 定义数据库的隔离级别以及对外部事务的可见性。</p> 
 <p style="font-size: 14px;">spring的事务处理是基于java的异常体系的。java里面的异常分为两类：检查型异常(extends Exception)和非检查型异常(extends RuntimeException)</p> 
 <p style="font-size: 14px;">spring对检查型异常进行commit提交处理，对非检查型异常进行rollback回滚处理。</p> 
 <p style="font-size: 14px;">spring batch运行你对不需要触发rollback回滚动作的异常进行定义。你可以在tasklet的no-rollback-exception-class元素中进行指定。</p> 
 <p style="font-size: 14px;">&nbsp;示例：</p> 
 <pre name="code" class="xml">&lt;batch:tasklet&gt;
	(...)
	&lt;batch:no-rollback-exception-classes&gt;
		&lt;batch:include
			class="org.springframework.batch.item.validator.ValidationException"/&gt;
	&lt;/batch:no-rollback-exception-classes&gt;
&lt;/batch:tasklet&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;对于JMS，spring batch提供chunk的reader-transactional-queue 属性，提供事务处理。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">7、配置job仓库</p> 
 <p style="font-size: 14px;">job仓库(job repository)是spring batch底层基础的一个关键特征，它为spring batch的运行提供信息。</p> 
 <p style="font-size: 14px;">job仓库必须实现JobRepository接口，spring batch只提供了一个具体的实现类：SimpleJobRepository。</p> 
 <p style="font-size: 14px;">spring batch为DAO提供了两种实现：</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; a、内存无持久化</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; b、jdbc元数据的持久化</p> 
 <p style="font-size: 14px;">第一种“内存无持久化”的方式可以用来spring batch的测试和开发，但是不能应用于生产环境。因为内存中的东西会丢失。</p> 
 <p style="font-size: 14px;">设定job仓库的参数</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; (1)、配置内存模式的job仓库：Configuring an in-memory job repository</p> 
 <p style="font-size: 14px;">示例：</p> 
 <pre name="code" class="xml">&lt;bean id="jobRepository" class="org.springframework.batch.core.repository.support.MapJobRepositoryFactoryBean"&gt;
	&lt;property name="transactionManager-ref" ref="transactionManager"/&gt;
&lt;/bean&gt;

&lt;bean id="transactionManager"	class="org.springframework.batch.support.transaction.ResourcelessTransactionManager"/&gt;

&lt;batch:job id="importInvoicesJob"	job-repository="jobRepository"&gt;
	(...)
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;由于job仓库是内存模式的，所以事务管理器采用ResourcelessTransactionManager。 这个类是NOOP (NO&nbsp;OPeration)无操作的PlatformTransactionManager接口实现。</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; &nbsp;(2)、持久化的job仓库：Configuring a persistent job repository</p> 
 <p style="font-size: 14px;">关系型数据库的job仓库的属性如下：data-source,transaction-manager,isolation-level-for-create,max-varchar-length,table-prefix,lob-handler</p> 
 <p style="font-size: 14px;">示例：</p> 
 <pre name="code" class="xml">&lt;bean id="dataSource"
	class="org.apache.commons.dbcp.BasicDataSource"
	destroy-method="close"&gt;
	&lt;property name="driverClassName" value="${batch.jdbc.driver}" /&gt;
	&lt;property name="url" value="${batch.jdbc.url}" /&gt;
	&lt;property name="username" value="${batch.jdbc.user}" /&gt;
	&lt;property name="password" value="${batch.jdbc.password}" /&gt;
&lt;/bean&gt;

&lt;bean id="transactionManager" lazy-init="true"
	class="org.springframework.jdbc.datasource.DataSourceTransactionManager"&gt;
	&lt;property name="dataSource" ref="dataSource" /&gt;
&lt;/bean&gt;

&lt;batch:job-repository id="jobRepository"
	data-source="dataSource"
	transaction-manager="transactionManager"
	isolation-level-for-create="SERIALIZABLE"
	table-prefix="BATCH_"
/&gt;

&lt;batch:job id="importInvoicesJob" job-repository="jobRepository"&gt;
	(...)
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;[问题：如果在不同的物理节点上面运行同样的job会发生什么呢？]</p> 
 <p style="font-size: 14px;">前提：使用同一份spring batch的元数据，即采用同一份数据库上面的表结构。</p> 
 <p style="font-size: 14px;">当创建job实例和执行信息的元数据的时候，job仓库扮演了一个集中维护的工作库的角色。当job并发运行的时候，spring batch 的job仓库，可以防止创建相同的工作情况。这个功能依赖于底层数据库的事务能力，完成job的同步任务。我们设置job仓库的属性isolation-level-for-create="SERIALIZABLE"，来避免发生job的并发问题。由于有这种防护措施，你可以把你的spring batch的job分布到各个不同的物理节点，保证你的job实例不会被创建两次。</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; &nbsp;job仓库是spring batch底层结构中的重要部分，它记录了batch处理的信息，并且跟踪job运行的成功与失败。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;8、spring batch配置的高级主题。</p> 
 <p style="font-size: 14px;">(1)、使用step作用域。当使用SpEL的时候，step作用域很有用，来实现属性的晚绑定。</p> 
 <p style="font-size: 14px;">(2)、Spring表达式语言：Spring Expression Language (SpEL)&nbsp;</p> 
 <p style="font-size: 14px;">Spring3.× 开始提供。</p> 
 <p style="font-size: 14px;">&nbsp;step的作用的实例范围包括：jobParameters、jobExecutionContext、stepExecutionContext</p> 
 <p style="font-size: 14px;">&nbsp;示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;bean id="decompressTasklet"
			class="com.manning.sbia.ch01.batch.DecompressTasklet"
			scope="step"&gt;
	&lt;property name="inputResource"
	value="#{jobParameters['inputResource']}" /&gt;
	&lt;property name="targetDirectory"
	value="#{jobParameters['targetDirectory']}" /&gt;
	&lt;property name="targetFile"
	value="#{jobParameters['targetFile']}" /&gt;
&lt;/bean&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;SpEL由&nbsp;#{ 和 } 组成</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;在jobExecutionContext 和 stepExecutionContext也可以应用SpEL表达式。</p> 
 <p style="font-size: 14px;">&nbsp;(3)、使用Linteners提供的更多的处理。</p> 
 <p style="font-size: 14px;">Spring batch在job和step级别上面提供listener。</p> 
 <p style="font-size: 14px;">Spring batch提供的listener的类型：</p> 
 <p style="font-size: 14px;">a、Job listener：在job级别监听处理过程</p> 
 <p style="font-size: 14px;">b、Step listeners：在step级别监听处理过程</p> 
 <p style="font-size: 14px;">c、Item listeners：监听item的retry重试和repeat重做动作</p> 
 <p style="font-size: 14px;">一、Job listener 可以监听job的运行，在job运行前和后添加动作。可以利用 listener标签，在job标签下面作为子元素进行添加。</p> 
 <p style="font-size: 14px;">示例1：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;batch:job id="importProductsJob"&gt;
	&lt;batch:listeners&gt;
	&lt;batch:listener ref="importProductsJobListener"/&gt;
	&lt;/batch:listeners&gt;
&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;importProductsJobListener不管job运行成功还是失败，它都会在job运行的开始和结束的时候，接收job的通知，进行监听。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">还可以通过普通的POJO的java对象来做监听器，只需要进行简单的配置即可。</p> 
 <p style="font-size: 14px;">示例2：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="xml">&lt;batch:listeners&gt;
    &lt;batch:listener ref="importProductsJobListener" after-job-method="afterJob" before-job-method="beforeJob"/&gt;
&lt;/batch:listeners&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;可以在listener里面的ref指定引用的POJO的bean，通过after-job-method="afterJob" before-job-method="beforeJob" 来指定job之前和之后的执行方法。不过，被指定的这两个方法的参数都需要是：JobExecution jobExecution。 这个2个方法的返回值都是void</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">还有一种方法是利用“注释”来配置listener，spring batch会自己发现并运行该类。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">二、Step listener</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; Step有一系列的listener来跟踪step的处理过程。这里所有的listener接口都继承了StepListener接口。</p> 
 <p style="font-size: 14px;">Spring batch提供的Step的listener有：</p> 
 <p style="font-size: 14px;">a、ChunkListener：在chunk执行的之前和之后调用。</p> 
 <p style="font-size: 14px;">b、ItemProcessListener：在&nbsp;ItemProcessor得到一个item之前和之后调用，在ItemProcessor抛出一个异常的时候调用。</p> 
 <p style="font-size: 14px;">c、ItemReadListener：在读取item之前和读取item之后调用，或者在读取item的过程中触发异常的时候调用。</p> 
 <p style="font-size: 14px;">d、ItemWriteListener：在一个item输出之前和之后调用，或者在item输出的过程中调用。</p> 
 <p style="font-size: 14px;">e、SkipListener：当读取、处理和输出的过程中产生了skip跳跃一个item的时候调用。</p> 
 <p style="font-size: 14px;">f、StepExecutionListener：在step运行之前和之后调用。</p> 
 <p style="font-size: 14px;">&nbsp;接口代码：</p> 
 <pre name="code" class="java">public interface StepExecutionListener extends StepListener {
	void beforeStep(StepExecution stepExecution);
	ExitStatus afterStep(StepExecution stepExecution);
}

public interface ChunkListener extends StepListener {
	void beforeChunk();
	void afterChunk();
}


public interface ItemProcessListener&lt;T, S&gt; extends StepListener {
	void beforeProcess(T item);
	void afterProcess(T item, S result);
	void onProcessError(T item, Exception e);
}

public interface ItemReadListener&lt;T&gt; extends StepListener {
	void beforeRead();
	void afterRead(T item);
	void onReadError(Exception ex);
}

public interface ItemWriteListener&lt;S&gt; extends StepListener {
	void beforeWrite(List&lt;? extends S&gt; items);
	void afterWrite(List&lt;? extends S&gt; items);
	void onWriteError(Exception exception, List&lt;? extends S&gt; items);
}

public interface SkipListener&lt;T,S&gt; extends StepListener {
	void onSkipInRead(Throwable t);
	void onSkipInProcess(T item, Throwable t);
	void onSkipInWrite(S item, Throwable t);
}</pre> 
 <p style="font-size: 14px;">&nbsp;Step listener 作为tasklet标签的一个子标签进行配置。</p> 
 <p style="font-size: 14px;">&nbsp;上面这些所有的Step listener都可以作为tasklet标签的子标签以相同的方式和等级进行配置。</p> 
 <p style="font-size: 14px;">示例：</p> 
 <pre name="code" class="xml">	&lt;bean id="importProductsJobListener"
		class="test.case01.java.batch.listener.job.ImportProductsJobListener" /&gt;
		
	&lt;bean id="productStepExecutionListener"
		class="test.case01.java.batch.listener.step.ProductStepExecutionListener" /&gt;

	&lt;bean id="productChunkListener"
		class="test.case01.java.batch.listener.step.chunk.ProductChunkListener" /&gt;
		
	&lt;bean id="productItemProcessListener"
		class="test.case01.java.batch.listener.step.chunk.item.ProductItemProcessListener" /&gt;
		
	&lt;batch:job id="importProducts" restartable="false"&gt;
		&lt;batch:step id="readWriteProducts"&gt;
			&lt;batch:tasklet&gt;
				&lt;batch:chunk reader="reader" writer="writer" processor="processor"
					commit-interval="100" skip-limit="5"&gt;
					&lt;batch:skippable-exception-classes&gt;
						&lt;batch:include
							class="org.springframework.batch.item.file.FlatFileParseException" /&gt;
					&lt;/batch:skippable-exception-classes&gt;
				&lt;/batch:chunk&gt;
				&lt;batch:listeners&gt;
					&lt;!-- here configure three kinds listeners for StepExecutionListener ,  ChunkListener , ItemProcessListener  for example.--&gt;
					&lt;batch:listener ref="productStepExecutionListener" /&gt;
					&lt;batch:listener ref="productChunkListener" /&gt;
					&lt;batch:listener ref="productItemProcessListener" /&gt;
				&lt;/batch:listeners&gt;
			&lt;/batch:tasklet&gt;
		&lt;/batch:step&gt;
		&lt;batch:validator ref="parameterValidator" /&gt;
		&lt;batch:listeners&gt;
			&lt;batch:listener ref="importProductsJobListener" /&gt;
		&lt;/batch:listeners&gt;
	&lt;/batch:job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;三、retry重试和repeat重做的listener</p> 
 <p style="font-size: 14px;">repeat listener拥有的方法名称：before、after、close(在一个item最后一次repeat重做之后调用，不管repeat成功与否)、onError、open</p> 
 <p style="font-size: 14px;">retry listener拥有的方法名称：close(在一个item上面最后一次尝试retry之后调用，不管retry成功与否)、onError、open</p> 
 <p style="font-size: 14px;">接口代码：</p> 
 <pre name="code" class="java">public interface RepeatListener {
	void before(RepeatContext context);
	void after(RepeatContext context, RepeatStatus result);
	void open(RepeatContext context);
	void onError(RepeatContext context, Throwable e);
	void close(RepeatContext context);
}

public interface RetryListener {
	&lt;T&gt; void open(RetryContext context, RetryCallback&lt;T&gt; callback);
	&lt;T&gt; void onError(RetryContext context,
	RetryCallback&lt;T&gt; callback, Throwable e);
	&lt;T&gt; void close(RetryContext context,
	RetryCallback&lt;T&gt; callback, Throwable e);
}</pre> 
 <p style="font-size: 14px;">&nbsp;这2个接口，和上面的step listener的配置位置和方式一致，都是tasklet标签的子标签位置</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">四、配置继承关系</p> 
 <p style="font-size: 14px;">spring的XML提供配置的继承。使用abstract和parent两个属性。从一个parent的bean继承，表示该bean可以利用parent bean中的所有的属性，并且可以覆盖这些属性。</p> 
 <p style="font-size: 14px;">示例：</p> 
 <pre name="code" class="xml">&lt;bean id="parentBean" abstract="true"&gt;
	&lt;property name="propertyOne" value="(...)"/&gt;
&lt;/bean&gt;

&lt;bean id="childBean" parent="parentBean"&gt;
	&lt;property name="propertyOne" value="(...)"/&gt;
	&lt;property name="propertyTwo" value="(...)"/&gt;
&lt;/bean&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;这种继承关系是由spring提供的，在spring batch里面也可以使用。</p> 
 <p style="font-size: 14px;">listeners标签，提供merge属性，可以用来合并parent和自身的listener</p> 
 <p style="font-size: 14px;">&nbsp;示例：</p> 
 <pre name="code" class="xml">&lt;job id="parentJob" abstract="true"&gt;
	&lt;listeners&gt;
		&lt;listener ref="globalListener"/&gt;
	&lt;listeners&gt;
&lt;/job&gt;

&lt;job id="importProductsJob" parent="parentJob"&gt;
	(...)
	&lt;listeners merge="true"&gt;
		&lt;listener ref="specificListener"/&gt;
	&lt;listeners&gt;
&lt;/job&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;spring XML的这种继承关系，使得spring batch的XML配置更简单。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>