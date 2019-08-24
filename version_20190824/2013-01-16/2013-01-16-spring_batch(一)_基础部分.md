#spring batch(一)：基础部分
###发表时间：2013-01-16
###分类：Spring,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1768887" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1768887</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;">spring batch</p> 
 <p style="font-size: 14px;">官网：</p> 
 <p style="font-size: 14px;"><a title="http://www.springsource.org/spring-batch" href="http://www.springsource.org/spring-batch" target="_blank">http://www.springsource.org/spring-batch</a></p> 
 <p style="font-size: 14px;">下载页面：</p> 
 <p style="font-size: 14px;"><a class="quote_div" title="http://static.springsource.org/spring-batch/downloads.html" href="http://static.springsource.org/spring-batch/downloads.html" target="_blank">http://static.springsource.org/spring-batch/downloads.html</a></p> 
 <p style="font-size: 14px;">文档：</p> 
 <p style="font-size: 14px;"><a class="quote_div" title="http://static.springsource.org/spring-batch/reference/index.html" href="http://static.springsource.org/spring-batch/reference/index.html" target="_blank">http://static.springsource.org/spring-batch/reference/index.html</a></p> 
 <p style="font-size: 14px;">数据库表格创建连接：DDL</p> 
 <p style="font-size: 14px;"><a class="quote_div" title="http://static.springsource.org/spring-batch/reference/html/metaDataSchema.html#exampleDDLScripts" href="http://static.springsource.org/spring-batch/reference/html/metaDataSchema.html#exampleDDLScripts" target="_blank">http://static.springsource.org/spring-batch/reference/html/metaDataSchema.html#exampleDDLScripts</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><strong>chapter 1、</strong><strong>Introducing Spring Batch</strong></p> 
 <p style="font-size: 14px;">spring batch需要依赖关系型数据库才能运行，在它的官方文档中的附录中，有创建它依赖的数据库表结构。</p> 
 <p style="font-size: 14px;">spring batch设计的目标：</p> 
 <p style="font-size: 14px;">1、大数据处理</p> 
 <p style="font-size: 14px;">2、自动化的</p> 
 <p style="font-size: 14px;">3、健壮的</p> 
 <p style="font-size: 14px;">4、可信赖的</p> 
 <p style="font-size: 14px;">5、高性能的</p> 
 <p style="font-size: 14px;">配置文件中&nbsp;chunk &nbsp;里面的 commit-interval="100"的大小，就是chunk块的大小。它们是一回事。</p> 
 <p style="font-size: 14px;">chunk 里面有 ItemReader ItemProcessor ItemWriter , ItemReader一次读取一条记录，ItemProcessor一次处理一条记录，ItemWriter一次输入commit-interval="100"指定事物大小的记录数（也就是chunk块的大小）。</p> 
 <p style="font-size: 14px;">推荐的commit-interval的大小是 10 至 200。 如果这个数值太大，如果是输出数据到数据库，会造成数据库的事物数据太大，影响数据库的性能，数据库会记录很多回滚数据的事物内容，造成性能低下。这个值太小，又会造成很多事务的产生，造成spring batch运行缓慢。</p> 
 <p style="font-size: 14px;">可以用SpEL动态配置程序运行的参数，例如：</p> 
 <p style="font-size: 14px;">&lt;property name="resource"value="file:#{jobParameters['inputResource']}" /&gt;</p> 
 <p style="font-size: 14px;">这里需要注意一点，bean的scope必须为 “step”。在spring 3.×中支持 SPEL表达式。</p> 
 <p style="font-size: 14px;">&lt;bean id="reader" class="org.springframework.batch.item.file.FlatFileItemReader" scope="step"&gt;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">下面是spring batch的元数据表，oracle数据库的DDL</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="sql">CREATE TABLE BATCH_JOB_INSTANCE  (
	JOB_INSTANCE_ID NUMBER(19,0)  NOT NULL PRIMARY KEY ,  
	VERSION NUMBER(19,0) ,  
	JOB_NAME VARCHAR2(100) NOT NULL, 
	JOB_KEY VARCHAR2(32) NOT NULL,
	constraint JOB_INST_UN unique (JOB_NAME, JOB_KEY)
) ;

CREATE TABLE BATCH_JOB_EXECUTION  (
	JOB_EXECUTION_ID NUMBER(19,0)  NOT NULL PRIMARY KEY ,
	VERSION NUMBER(19,0)  ,  
	JOB_INSTANCE_ID NUMBER(19,0) NOT NULL,
	CREATE_TIME TIMESTAMP NOT NULL,
	START_TIME TIMESTAMP DEFAULT NULL , 
	END_TIME TIMESTAMP DEFAULT NULL ,
	STATUS VARCHAR2(10) ,
	EXIT_CODE VARCHAR2(100) ,
	EXIT_MESSAGE VARCHAR2(2500) ,
	LAST_UPDATED TIMESTAMP,
	constraint JOB_INST_EXEC_FK foreign key (JOB_INSTANCE_ID)
	references BATCH_JOB_INSTANCE(JOB_INSTANCE_ID)
) ;
	
CREATE TABLE BATCH_JOB_PARAMS  (
	JOB_INSTANCE_ID NUMBER(19,0) NOT NULL ,
	TYPE_CD VARCHAR2(6) NOT NULL ,
	KEY_NAME VARCHAR2(100) NOT NULL , 
	STRING_VAL VARCHAR2(250) , 
	DATE_VAL TIMESTAMP DEFAULT NULL ,
	LONG_VAL NUMBER(19,0) ,
	DOUBLE_VAL NUMBER ,
	constraint JOB_INST_PARAMS_FK foreign key (JOB_INSTANCE_ID)
	references BATCH_JOB_INSTANCE(JOB_INSTANCE_ID)
) ;
	
CREATE TABLE BATCH_STEP_EXECUTION  (
	STEP_EXECUTION_ID NUMBER(19,0)  NOT NULL PRIMARY KEY ,
	VERSION NUMBER(19,0) NOT NULL,  
	STEP_NAME VARCHAR2(100) NOT NULL,
	JOB_EXECUTION_ID NUMBER(19,0) NOT NULL,
	START_TIME TIMESTAMP NOT NULL , 
	END_TIME TIMESTAMP DEFAULT NULL ,  
	STATUS VARCHAR2(10) ,
	COMMIT_COUNT NUMBER(19,0) , 
	READ_COUNT NUMBER(19,0) ,
	FILTER_COUNT NUMBER(19,0) ,
	WRITE_COUNT NUMBER(19,0) ,
	READ_SKIP_COUNT NUMBER(19,0) ,
	WRITE_SKIP_COUNT NUMBER(19,0) ,
	PROCESS_SKIP_COUNT NUMBER(19,0) ,
	ROLLBACK_COUNT NUMBER(19,0) , 
	EXIT_CODE VARCHAR2(100) ,
	EXIT_MESSAGE VARCHAR2(2500) ,
	LAST_UPDATED TIMESTAMP,
	constraint JOB_EXEC_STEP_FK foreign key (JOB_EXECUTION_ID)
	references BATCH_JOB_EXECUTION(JOB_EXECUTION_ID)
) ;

CREATE TABLE BATCH_STEP_EXECUTION_CONTEXT  (
	STEP_EXECUTION_ID NUMBER(19,0) NOT NULL PRIMARY KEY,
	SHORT_CONTEXT VARCHAR2(2500) NOT NULL,
	SERIALIZED_CONTEXT CLOB , 
	constraint STEP_EXEC_CTX_FK foreign key (STEP_EXECUTION_ID)
	references BATCH_STEP_EXECUTION(STEP_EXECUTION_ID)
) ;

CREATE TABLE BATCH_JOB_EXECUTION_CONTEXT  (
	JOB_EXECUTION_ID NUMBER(19,0) NOT NULL PRIMARY KEY,
	SHORT_CONTEXT VARCHAR2(2500) NOT NULL,
	SERIALIZED_CONTEXT CLOB , 
	constraint JOB_EXEC_CTX_FK foreign key (JOB_EXECUTION_ID)
	references BATCH_JOB_EXECUTION(JOB_EXECUTION_ID)
) ;

CREATE SEQUENCE BATCH_STEP_EXECUTION_SEQ START WITH 0 MINVALUE 0 MAXVALUE 9223372036854775807 NOCYCLE;
CREATE SEQUENCE BATCH_JOB_EXECUTION_SEQ START WITH 0 MINVALUE 0 MAXVALUE 9223372036854775807 NOCYCLE;
CREATE SEQUENCE BATCH_JOB_SEQ START WITH 0 MINVALUE 0 MAXVALUE 9223372036854775807 NOCYCLE;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">[备注]&nbsp; SQL 脚本在spring batch的核心jar包中有提供。例如：&nbsp;spring-batch-core-2.1.9.RELEASE.jar的核心包org.springframework.batch.core中，schema-drop-[database].sql 的形式提供了各种主流关系型数据库的sql脚本。</p> 
 <p style="font-size: 14px;">spring batch支持的数据库有：Derby, H2, HSQLDB,MySQL, Oracle, PostgreSQL, SQLServer, and Sybase.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><strong>chapter 2、</strong><strong>Spring Batch concepts</strong></p> 
 <p style="font-size: 14px;">1、spring batch 的主要组件：</p> 
 <p style="font-size: 14px;">Job Repository持久化job执行元数据的基础组件</p> 
 <p style="font-size: 14px;">Job launcher引导job执行的基础组件</p> 
 <p style="font-size: 14px;">Jobbatch处理的应用组件</p> 
 <p style="font-size: 14px;">Stepjob内部的一个词语，一个job由一系列的step组成<br>Tasklet在step里面应用事务的，可重复执行的处理步骤</p> 
 <p style="font-size: 14px;">Item从数据源输入或者输出的一条记录</p> 
 <p style="font-size: 14px;">Chunk指定大小的item的列表。</p> 
 <p style="font-size: 14px;">Item reader负责从数据源读取item记录的组件</p> 
 <p style="font-size: 14px;">Item Processor负责处理(转换、验证、过滤等动作)item记录的组件</p> 
 <p style="font-size: 14px;">Item writer负责向数据源输出一个chunk的items，即：向数据源输出指定大小的item的列表的组件</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">2、spring batch如何和外部交互的</p> 
 <p style="font-size: 14px;">外部的cron，quartz等调度，或者web等，可以调用launch，触发spring batch的运行。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">3、spring batch的基础组件包括：job launch和job repository。 它们不需要开发人员进行开发，只需要在配置文件中进行配置。</p> 
 <p style="font-size: 14px;">spring batch 的job是一系列在spring batch XML中的step组成。</p> 
 <p style="font-size: 14px;">4、Tasklet的使用</p> 
 <p style="font-size: 14px;"><strong>创建一个步骤(step)，包括写一个tasklet执行或使用一个Spring Batch提供的tasklet。</strong></p> 
 <p style="font-size: 14px;">当需要解压文件、调用存储过程、或者删除文件、调用sh脚本的时候，需要自己创建Tasklet的实现。</p> 
 <p style="font-size: 14px;">当实现tasklet的时候，这些需求可以划分为batch的read-process-write模式，那么就应该使用chunk元素配置tasklet，作为chunk processing处理步骤。chunk元素使得你的程序更加有效地读取，处理和写入数据。</p> 
 <p style="font-size: 14px;">小结：工作（job）是一系列的步骤（step），这些内容你可以轻易的在spring batch的xml里面进行定义。而步骤（step）由tasklet组成。tasklet可以由“面向模块”编程的chunk组成，或者tasklet完全来由开发者进行定制。</p> 
 <p style="font-size: 14px;">5、Job的相关概念</p> 
 <p style="font-size: 14px;">a、Job工作</p> 
 <p style="font-size: 14px;">b、Job instance工作实例</p> 
 <p style="font-size: 14px;">c、Job execution执行工作</p> 
 <p style="font-size: 14px;">一个工作（job）可以拥有很多工作实例(job instance)，每个工作实例(job instance)可以拥有很多工作执行(job execution)。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">在Spring Batch中，工作实例（job instance）包括工作（job）和工作参数（job parameter）。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">jobLauncher.run(job, new JobParametersBuilder()
.addString("date", "2010-06-27")
.toJobParameters()
);</pre> 
 <p style="font-size: 14px;">工作实例等式：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">JobInstance = Job + Job-Parameters.</p> 
 <p style="font-size: 14px;">Job instance和Job execution的生命周期的一些规则：</p> 
 <p style="font-size: 14px;">a、当你第一次运行job的时候，spring batch创建job instance和第一个job execution。</p> 
 <p style="font-size: 14px;">b、当前面的同一个job instance被成功的执行完成之后，你不能再次运行这个job instance。</p> 
 <p style="font-size: 14px;">c、你不能同时执行多个相同的实例。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;================ 基础部分结束 ============================</p> 
 <p style="font-size: 14px;"><strong>&nbsp;</strong></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>