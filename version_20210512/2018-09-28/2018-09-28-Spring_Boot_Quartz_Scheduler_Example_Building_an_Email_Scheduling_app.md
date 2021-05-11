#Spring Boot Quartz Scheduler Example: Building an Email Scheduling app
###发表时间：2018-09-28
###分类：Spring,springboot,java,quartz
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431472" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431472</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>引用地址：&nbsp;<a href="https://www.callicoder.com/spring-boot-quartz-scheduler-email-scheduling-example/">https://www.callicoder.com/spring-boot-quartz-scheduler-email-scheduling-example/</a></p> 
 <p>&nbsp;</p> 
 <p>代码地址：<a href="https://github.com/callicoder/spring-boot-quartz-scheduler-email-scheduling">&nbsp;https://github.com/callicoder/spring-boot-quartz-scheduler-email-scheduling</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style=""><a style="background-color: transparent; color: #419be8;" href="http://www.quartz-scheduler.org/">Quartz</a>&nbsp;is an open source Java library for scheduling Jobs. It has a very rich set of features including but not limited to persistent Jobs, transactions, and clustering.</p> 
 <p style="">You can schedule Jobs to be executed at a certain time of day, or periodically at a certain interval, and much more. Quartz provides a fluent API for creating jobs and scheduling them.</p> 
 <p style="">Quartz Jobs can be persisted into a database, or a cache, or in-memory. This is in contrast to&nbsp;<a style="background-color: transparent; color: #419be8;" href="https://www.callicoder.com/spring-boot-task-scheduling-with-scheduled-annotation/">Spring’s built-in task scheduling API</a>&nbsp;that doesn’t support persistent jobs.</p> 
 <blockquote style=""> 
  <p style="margin-bottom: 15px;">In this article, you’ll learn how to schedule Jobs in spring boot using Quartz Scheduler by building a simple&nbsp;<span style="font-weight: 600;">Email Scheduling application</span>. The application will have a Rest API that allows clients to schedule Emails at a later time.</p> 
  <p style="">We’ll use MySQL to persist all the jobs and other job-related data.</p> 
 </blockquote> 
 <p style="">Sounds interesting? Let’s start…</p> 
 <h2 id="creating-the-application" style="">Creating the Application</h2> 
 <p style="">Let’s bootstrap the application using&nbsp;<a style="background-color: transparent; color: #419be8;" href="https://www.callicoder.com/scaffolding-your-spring-boot-application/#spring-boot-cli">Spring Boot CLI</a>. Open your terminal and type the following command -</p> 
 <pre class=" language-bash"><code class=" language-bash" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;">spring init -d<span class="token operator" style="color: #a67f59;">=</span>web,jpa,mysql,quartz,mail -n<span class="token operator" style="color: #a67f59;">=</span>quartz-demo quartz-demo
</code></pre> 
 <p style="">The above command will generate the project with all the specified dependencies in a folder named&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">quartz-demo</code>.</p> 
 <p style="">Note that, you can also use Spring Initializr web tool to bootstrap the project by following the instructions below -</p> 
 <ul style=""> 
  <li style="">Open&nbsp;<a style="background-color: transparent; color: #419be8;" href="http://start.spring.io/">http://start.spring.io</a> </li> 
  <li style="">Enter&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">quartz-demo</code>&nbsp;in the&nbsp;<em style="">Artifact</em>&nbsp;field.</li> 
  <li style="">Add&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">Web</code>,&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">JPA</code>,&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">MySQL</code>,&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">Quartz</code>, and&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">Mail</code>&nbsp;in the dependencies section.</li> 
  <li style="">Click&nbsp;<em style="">Generate Project</em>&nbsp;to generate and download the project.</li> 
 </ul> 
 <p style="">That’s it! You may now import the project into your favorite IDE and start working.</p> 
 <p style=""><span style="font-weight: 600;">Directory Structure</span></p> 
 <p style="">Following is the directory structure of the complete application for your reference. We’ll create all the required folders and classes one-by-one in this article -</p> 
 <p>&lt;source media="(max-width: 520px)" srcset="https://www.callicoder.com/assets/images/post/medium/spring-boot-quartz-scheduler-email-scheduling-project-example.jpg" style="box-sizing: border-box;"&gt;&lt;/source&gt;<img style="border-style: none; max-width: 100%; vertical-align: middle; margin-bottom: 15px;" src="https://www.callicoder.com/assets/images/post/large/spring-boot-quartz-scheduler-email-scheduling-project-example.jpg" alt="Spring Boot Quartz Scheduler Email Scheduling App directory structure" width="600px"></p> 
 <h2 id="configuring-mysql-database-quartz-scheduler-and-mail-sender" style="">Configuring MySQL database, Quartz Scheduler, and Mail Sender</h2> 
 <p style="">Let’s configure Quartz Scheduler, MySQL database, and Spring Mail. MySQL database will be used for storing Quartz Jobs, and Spring Mail will be used to send emails.</p> 
 <p style="">Open&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">src/main/resources/application.properties</code>&nbsp;file and add the following properties -</p> 
 <pre class=" language-properties"><code class=" language-properties" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;"><span class="token comment" style="color: #708090;">## Spring DATASOURCE (DataSourceAutoConfiguration &amp; DataSourceProperties)</span>
<span class="token attr-name" style="color: #669900;">spring.datasource.url</span> <span class="token punctuation" style="color: #999999;">=</span> <span class="token attr-value" style="color: #0077aa;">jdbc:mysql://localhost:3306/quartz_demo?useSSL=false</span>
<span class="token attr-name" style="color: #669900;">spring.datasource.username</span> <span class="token punctuation" style="color: #999999;">=</span> <span class="token attr-value" style="color: #0077aa;">root</span>
<span class="token attr-name" style="color: #669900;">spring.datasource.password</span> <span class="token punctuation" style="color: #999999;">=</span> <span class="token attr-value" style="color: #0077aa;">callicoder</span>

<span class="token comment" style="color: #708090;">## QuartzProperties</span>
<span class="token attr-name" style="color: #669900;">spring.quartz.job-store-type</span> <span class="token punctuation" style="color: #999999;">=</span> <span class="token attr-value" style="color: #0077aa;">jdbc</span>
<span class="token attr-name" style="color: #669900;">spring.quartz.properties.org.quartz.threadPool.threadCount</span> <span class="token punctuation" style="color: #999999;">=</span> <span class="token attr-value" style="color: #0077aa;">5</span>

<span class="token comment" style="color: #708090;">## MailProperties</span>
<span class="token attr-name" style="color: #669900;">spring.mail.host</span><span class="token punctuation" style="color: #999999;">=</span><span class="token attr-value" style="color: #0077aa;">smtp.gmail.com</span>
<span class="token attr-name" style="color: #669900;">spring.mail.port</span><span class="token punctuation" style="color: #999999;">=</span><span class="token attr-value" style="color: #0077aa;">587</span>
<span class="token attr-name" style="color: #669900;">spring.mail.username</span><span class="token punctuation" style="color: #999999;">=</span><span class="token attr-value" style="color: #0077aa;">rajeevc217@gmail.com</span>
<span class="token attr-name" style="color: #669900;">spring.mail.password</span><span class="token punctuation" style="color: #999999;">=</span>

<span class="token attr-name" style="color: #669900;">spring.mail.properties.mail.smtp.auth</span><span class="token punctuation" style="color: #999999;">=</span><span class="token attr-value" style="color: #0077aa;">true</span>
<span class="token attr-name" style="color: #669900;">spring.mail.properties.mail.smtp.starttls.enable</span><span class="token punctuation" style="color: #999999;">=</span><span class="token attr-value" style="color: #0077aa;">true</span>
</code></pre> 
 <p style="">You’ll need to create a MySQL database named&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">quartz_demo</code>. Also, don’t forget to change the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">spring.datasource.username</code>&nbsp;and&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">spring.datasource.password</code>&nbsp;properties as per your MySQL installation.</p> 
 <p style="">We’ll be using Gmail’s SMTP server for sending emails. Please add your password in the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">spring.mail.password</code>&nbsp;property. You may also pass this property at runtime as command line argument or set it in the environment variable.</p> 
 <p style="">Note that, Gmail’s SMTP access is disabled by default. To allow this app to send emails using your Gmail account -</p> 
 <ul style=""> 
  <li style="">Go to&nbsp;<a style="background-color: transparent; color: #419be8;" href="https://myaccount.google.com/security?pli=1#connectedapps">https://myaccount.google.com/security?pli=1#connectedapps</a> </li> 
  <li style="">Set ‘Allow less secure apps’ to YES</li> 
 </ul> 
 <h2 id="creating-quartz-tables" style="">Creating Quartz Tables</h2> 
 <p style="">Since we have configured Quartz to store Jobs in the database, we’ll need to create the tables that Quartz uses to store Jobs and other job-related meta-data.</p> 
 <p style="">Please download the following SQL script and run it in your MySQL database to create all the Quartz specific tables.</p> 
 <ul style=""> 
  <li style=""><span style="font-weight: 600;"><a style="background-color: transparent; color: #419be8;" href="https://github.com/callicoder/spring-boot-quartz-scheduler-email-scheduling/blob/master/src/main/resources/quartz_tables.sql">Quartz Tables SQL script</a></span></li> 
 </ul> 
 <p style="">After downloading the above SQL script, login to MySQL and run the script like this -</p> 
 <pre class=" language-bash"><code class=" language-bash" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;">mysql<span class="token operator" style="color: #a67f59;">&gt;</span> <span class="token function" style="color: #dd4a68;">source</span> <span class="token operator" style="color: #a67f59;">&lt;</span>PATH_TO_QUARTZ_TABLES.sql<span class="token operator" style="color: #a67f59;">&gt;</span> 
</code></pre> 
 <h2 id="overview-of-quartz-scheduler-s-apis-and-terminologies" style="">Overview of Quartz Scheduler’s APIs and Terminologies</h2> 
 <h4 id="1-scheduler" style="">1. Scheduler</h4> 
 <p style="">The Primary API for scheduling, unscheduling, adding, and removing Jobs.</p> 
 <h4 id="2-job" style="">2. Job</h4> 
 <p style="">The interface to be implemented by classes that represent a ‘job’ in Quartz. It has a single method called&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">execute()</code>&nbsp;where you write the work that needs to be performed by the Job.</p> 
 <h4 id="3-jobdetail" style="">3. JobDetail</h4> 
 <p style="">A JobDetail represents an instance of a Job. It also contains additional data in the form of a&nbsp;<span style="font-weight: 600;">JobDataMap</span>&nbsp;that is passed to the Job when it is executed.</p> 
 <p style="">Every JobDetail is identified by a&nbsp;<span style="font-weight: 600;">JobKey</span>&nbsp;that consists of a&nbsp;<em style="">name</em>&nbsp;and a&nbsp;<em style="">group</em>. The name must be unique within a group.</p> 
 <h4 id="4-trigger" style="">4. Trigger</h4> 
 <p style="">A Trigger, as the name suggests, defines the schedule at which a given Job will be executed. A Job can have many Triggers, but a Trigger can only be associated with one Job.</p> 
 <p style="">Every Trigger is identified by a&nbsp;<span style="font-weight: 600;">TriggerKey</span>&nbsp;that comprises of a&nbsp;<em style="">name</em>&nbsp;and a&nbsp;<em style="">group</em>. The name must be unique within a group.</p> 
 <p style="">Just like JobDetails, Triggers can also send parameters/data to the Job.</p> 
 <h4 id="5-jobbuilder" style="">5. JobBuilder</h4> 
 <p style="">JobBuilder is a fluent builder-style API to construct JobDetail instances.</p> 
 <h4 id="6-triggerbuilder" style="">6. TriggerBuilder</h4> 
 <p style="">TriggerBuilder is used to instantiate Triggers.</p> 
 <h2 id="creating-a-rest-api-to-schedule-email-jobs-dynamically-in-quartz" style="">Creating a REST API to schedule Email Jobs dynamically in Quartz</h2> 
 <p style="">All right! Let’s now create a REST API to scheduler email Jobs in Quartz dynamically. All the Jobs will be persisted in the database and executed at the specified schedule.</p> 
 <p style="">Before writing the API, Let’s create the DTO classes that will be used as request and response payloads for the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">scheduleEmail</code>&nbsp;API -</p> 
 <h4 id="scheduleemailrequest" style="">ScheduleEmailRequest</h4> 
 <pre class=" language-java"><code class=" language-java" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;"><span class="token keyword" style="color: #0077aa;">package</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>payload<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> javax<span class="token punctuation" style="color: #999999;">.</span>validation<span class="token punctuation" style="color: #999999;">.</span>constraints<span class="token punctuation" style="color: #999999;">.</span>Email<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> javax<span class="token punctuation" style="color: #999999;">.</span>validation<span class="token punctuation" style="color: #999999;">.</span>constraints<span class="token punctuation" style="color: #999999;">.</span>NotEmpty<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> javax<span class="token punctuation" style="color: #999999;">.</span>validation<span class="token punctuation" style="color: #999999;">.</span>constraints<span class="token punctuation" style="color: #999999;">.</span>NotNull<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>time<span class="token punctuation" style="color: #999999;">.</span>LocalDateTime<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>time<span class="token punctuation" style="color: #999999;">.</span>ZoneId<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">class</span> <span class="token class-name" style="">ScheduleEmailRequest</span> <span class="token punctuation" style="color: #999999;">{</span>
    <span class="token annotation punctuation" style="color: #999999;">@Email</span>
    <span class="token annotation punctuation" style="color: #999999;">@NotEmpty</span>
    <span class="token keyword" style="color: #0077aa;">private</span> String email<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@NotEmpty</span>
    <span class="token keyword" style="color: #0077aa;">private</span> String subject<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@NotEmpty</span>
    <span class="token keyword" style="color: #0077aa;">private</span> String body<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@NotNull</span>
    <span class="token keyword" style="color: #0077aa;">private</span> LocalDateTime dateTime<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@NotNull</span>
    <span class="token keyword" style="color: #0077aa;">private</span> ZoneId timeZone<span class="token punctuation" style="color: #999999;">;</span>
	
	<span class="token comment" style="color: #708090;">// Getters and Setters (Omitted for brevity)</span>
<span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <h4 id="scheduleemailresponse" style="">ScheduleEmailResponse</h4> 
 <pre class=" language-java"><code class=" language-java" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;"><span class="token keyword" style="color: #0077aa;">package</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>payload<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> com<span class="token punctuation" style="color: #999999;">.</span>fasterxml<span class="token punctuation" style="color: #999999;">.</span>jackson<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>JsonInclude<span class="token punctuation" style="color: #999999;">;</span>

<span class="token annotation punctuation" style="color: #999999;">@JsonInclude</span><span class="token punctuation" style="color: #999999;">(</span>JsonInclude<span class="token punctuation" style="color: #999999;">.</span>Include<span class="token punctuation" style="color: #999999;">.</span>NON_NULL<span class="token punctuation" style="color: #999999;">)</span>
<span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">class</span> <span class="token class-name" style="">ScheduleEmailResponse</span> <span class="token punctuation" style="color: #999999;">{</span>
    <span class="token keyword" style="color: #0077aa;">private</span> <span class="token keyword" style="color: #0077aa;">boolean</span> success<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token keyword" style="color: #0077aa;">private</span> String jobId<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token keyword" style="color: #0077aa;">private</span> String jobGroup<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token keyword" style="color: #0077aa;">private</span> String message<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token keyword" style="color: #0077aa;">public</span> <span class="token function" style="color: #dd4a68;">ScheduleEmailResponse</span><span class="token punctuation" style="color: #999999;">(</span><span class="token keyword" style="color: #0077aa;">boolean</span> success<span class="token punctuation" style="color: #999999;">,</span> String message<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        <span class="token keyword" style="color: #0077aa;">this</span><span class="token punctuation" style="color: #999999;">.</span>success <span class="token operator" style="color: #a67f59;">=</span> success<span class="token punctuation" style="color: #999999;">;</span>
        <span class="token keyword" style="color: #0077aa;">this</span><span class="token punctuation" style="color: #999999;">.</span>message <span class="token operator" style="color: #a67f59;">=</span> message<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token keyword" style="color: #0077aa;">public</span> <span class="token function" style="color: #dd4a68;">ScheduleEmailResponse</span><span class="token punctuation" style="color: #999999;">(</span><span class="token keyword" style="color: #0077aa;">boolean</span> success<span class="token punctuation" style="color: #999999;">,</span> String jobId<span class="token punctuation" style="color: #999999;">,</span> String jobGroup<span class="token punctuation" style="color: #999999;">,</span> String message<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        <span class="token keyword" style="color: #0077aa;">this</span><span class="token punctuation" style="color: #999999;">.</span>success <span class="token operator" style="color: #a67f59;">=</span> success<span class="token punctuation" style="color: #999999;">;</span>
        <span class="token keyword" style="color: #0077aa;">this</span><span class="token punctuation" style="color: #999999;">.</span>jobId <span class="token operator" style="color: #a67f59;">=</span> jobId<span class="token punctuation" style="color: #999999;">;</span>
        <span class="token keyword" style="color: #0077aa;">this</span><span class="token punctuation" style="color: #999999;">.</span>jobGroup <span class="token operator" style="color: #a67f59;">=</span> jobGroup<span class="token punctuation" style="color: #999999;">;</span>
        <span class="token keyword" style="color: #0077aa;">this</span><span class="token punctuation" style="color: #999999;">.</span>message <span class="token operator" style="color: #a67f59;">=</span> message<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token comment" style="color: #708090;">// Getters and Setters (Omitted for brevity)</span>
<span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <h3 id="scheduleemail-rest-api" style="">ScheduleEmail Rest API</h3> 
 <p style="">The following controller defines the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">/scheduleEmail</code>&nbsp;REST API that schedules email Jobs in Quartz -</p> 
 <pre class=" language-java"><code class=" language-java" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;"><span class="token keyword" style="color: #0077aa;">package</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>controller<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>job<span class="token punctuation" style="color: #999999;">.</span>EmailJob<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>payload<span class="token punctuation" style="color: #999999;">.</span>ScheduleEmailRequest<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>payload<span class="token punctuation" style="color: #999999;">.</span>ScheduleEmailResponse<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>quartz<span class="token punctuation" style="color: #999999;">.</span>*<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>slf4j<span class="token punctuation" style="color: #999999;">.</span>Logger<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>slf4j<span class="token punctuation" style="color: #999999;">.</span>LoggerFactory<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>beans<span class="token punctuation" style="color: #999999;">.</span>factory<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>Autowired<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>http<span class="token punctuation" style="color: #999999;">.</span>HttpStatus<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>http<span class="token punctuation" style="color: #999999;">.</span>ResponseEntity<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>web<span class="token punctuation" style="color: #999999;">.</span>bind<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>PostMapping<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>web<span class="token punctuation" style="color: #999999;">.</span>bind<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>RequestBody<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>web<span class="token punctuation" style="color: #999999;">.</span>bind<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>RestController<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> javax<span class="token punctuation" style="color: #999999;">.</span>validation<span class="token punctuation" style="color: #999999;">.</span>Valid<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>time<span class="token punctuation" style="color: #999999;">.</span>ZonedDateTime<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>util<span class="token punctuation" style="color: #999999;">.</span>Date<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>util<span class="token punctuation" style="color: #999999;">.</span>UUID<span class="token punctuation" style="color: #999999;">;</span>

<span class="token annotation punctuation" style="color: #999999;">@RestController</span>
<span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">class</span> <span class="token class-name" style="">EmailJobSchedulerController</span> <span class="token punctuation" style="color: #999999;">{</span>
    <span class="token keyword" style="color: #0077aa;">private</span> <span class="token keyword" style="color: #0077aa;">static</span> <span class="token keyword" style="color: #0077aa;">final</span> Logger logger <span class="token operator" style="color: #a67f59;">=</span> LoggerFactory<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getLogger</span><span class="token punctuation" style="color: #999999;">(</span>EmailJobSchedulerController<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@Autowired</span>
    <span class="token keyword" style="color: #0077aa;">private</span> Scheduler scheduler<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@PostMapping</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"/scheduleEmail"</span><span class="token punctuation" style="color: #999999;">)</span>
    <span class="token keyword" style="color: #0077aa;">public</span> ResponseEntity<span class="token operator" style="color: #a67f59;">&lt;</span>ScheduleEmailResponse<span class="token operator" style="color: #a67f59;">&gt;</span> <span class="token function" style="color: #dd4a68;">scheduleEmail</span><span class="token punctuation" style="color: #999999;">(</span><span class="token annotation punctuation" style="color: #999999;">@Valid</span> <span class="token annotation punctuation" style="color: #999999;">@RequestBody</span> ScheduleEmailRequest scheduleEmailRequest<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        <span class="token keyword" style="color: #0077aa;">try</span> <span class="token punctuation" style="color: #999999;">{</span>
            ZonedDateTime dateTime <span class="token operator" style="color: #a67f59;">=</span> ZonedDateTime<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">of</span><span class="token punctuation" style="color: #999999;">(</span>scheduleEmailRequest<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getDateTime</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span> scheduleEmailRequest<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getTimeZone</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            <span class="token keyword" style="color: #0077aa;">if</span><span class="token punctuation" style="color: #999999;">(</span>dateTime<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">isBefore</span><span class="token punctuation" style="color: #999999;">(</span>ZonedDateTime<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">now</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
                ScheduleEmailResponse scheduleEmailResponse <span class="token operator" style="color: #a67f59;">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">ScheduleEmailResponse</span><span class="token punctuation" style="color: #999999;">(</span><span class="token boolean" style="color: #990055;">false</span><span class="token punctuation" style="color: #999999;">,</span>
                        <span class="token string" style="color: #669900;">"dateTime must be after current time"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
                <span class="token keyword" style="color: #0077aa;">return</span> ResponseEntity<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">badRequest</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">body</span><span class="token punctuation" style="color: #999999;">(</span>scheduleEmailResponse<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            <span class="token punctuation" style="color: #999999;">}</span>

            JobDetail jobDetail <span class="token operator" style="color: #a67f59;">=</span> <span class="token function" style="color: #dd4a68;">buildJobDetail</span><span class="token punctuation" style="color: #999999;">(</span>scheduleEmailRequest<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            Trigger trigger <span class="token operator" style="color: #a67f59;">=</span> <span class="token function" style="color: #dd4a68;">buildJobTrigger</span><span class="token punctuation" style="color: #999999;">(</span>jobDetail<span class="token punctuation" style="color: #999999;">,</span> dateTime<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            scheduler<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">scheduleJob</span><span class="token punctuation" style="color: #999999;">(</span>jobDetail<span class="token punctuation" style="color: #999999;">,</span> trigger<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

            ScheduleEmailResponse scheduleEmailResponse <span class="token operator" style="color: #a67f59;">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">ScheduleEmailResponse</span><span class="token punctuation" style="color: #999999;">(</span><span class="token boolean" style="color: #990055;">true</span><span class="token punctuation" style="color: #999999;">,</span>
                    jobDetail<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getKey</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getName</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span> jobDetail<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getKey</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getGroup</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token string" style="color: #669900;">"Email Scheduled Successfully!"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            <span class="token keyword" style="color: #0077aa;">return</span> ResponseEntity<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">ok</span><span class="token punctuation" style="color: #999999;">(</span>scheduleEmailResponse<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        <span class="token punctuation" style="color: #999999;">}</span> <span class="token keyword" style="color: #0077aa;">catch</span> <span class="token punctuation" style="color: #999999;">(</span><span class="token class-name" style="">SchedulerException</span> ex<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
            logger<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">error</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Error scheduling email"</span><span class="token punctuation" style="color: #999999;">,</span> ex<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

            ScheduleEmailResponse scheduleEmailResponse <span class="token operator" style="color: #a67f59;">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">ScheduleEmailResponse</span><span class="token punctuation" style="color: #999999;">(</span><span class="token boolean" style="color: #990055;">false</span><span class="token punctuation" style="color: #999999;">,</span>
                    <span class="token string" style="color: #669900;">"Error scheduling email. Please try later!"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            <span class="token keyword" style="color: #0077aa;">return</span> ResponseEntity<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">status</span><span class="token punctuation" style="color: #999999;">(</span>HttpStatus<span class="token punctuation" style="color: #999999;">.</span>INTERNAL_SERVER_ERROR<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">body</span><span class="token punctuation" style="color: #999999;">(</span>scheduleEmailResponse<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        <span class="token punctuation" style="color: #999999;">}</span>
    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token keyword" style="color: #0077aa;">private</span> JobDetail <span class="token function" style="color: #dd4a68;">buildJobDetail</span><span class="token punctuation" style="color: #999999;">(</span>ScheduleEmailRequest scheduleEmailRequest<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        JobDataMap jobDataMap <span class="token operator" style="color: #a67f59;">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">JobDataMap</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        jobDataMap<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">put</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"email"</span><span class="token punctuation" style="color: #999999;">,</span> scheduleEmailRequest<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getEmail</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        jobDataMap<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">put</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"subject"</span><span class="token punctuation" style="color: #999999;">,</span> scheduleEmailRequest<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getSubject</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        jobDataMap<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">put</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"body"</span><span class="token punctuation" style="color: #999999;">,</span> scheduleEmailRequest<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getBody</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> JobBuilder<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">newJob</span><span class="token punctuation" style="color: #999999;">(</span>EmailJob<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">withIdentity</span><span class="token punctuation" style="color: #999999;">(</span>UUID<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">randomUUID</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token string" style="color: #669900;">"email-jobs"</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">withDescription</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Send Email Job"</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">usingJobData</span><span class="token punctuation" style="color: #999999;">(</span>jobDataMap<span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">storeDurably</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">build</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token keyword" style="color: #0077aa;">private</span> Trigger <span class="token function" style="color: #dd4a68;">buildJobTrigger</span><span class="token punctuation" style="color: #999999;">(</span>JobDetail jobDetail<span class="token punctuation" style="color: #999999;">,</span> ZonedDateTime startAt<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        <span class="token keyword" style="color: #0077aa;">return</span> TriggerBuilder<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">newTrigger</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">forJob</span><span class="token punctuation" style="color: #999999;">(</span>jobDetail<span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">withIdentity</span><span class="token punctuation" style="color: #999999;">(</span>jobDetail<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getKey</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getName</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token string" style="color: #669900;">"email-triggers"</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">withDescription</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Send Email Trigger"</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">startAt</span><span class="token punctuation" style="color: #999999;">(</span>Date<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">from</span><span class="token punctuation" style="color: #999999;">(</span>startAt<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toInstant</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">withSchedule</span><span class="token punctuation" style="color: #999999;">(</span>SimpleScheduleBuilder<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">simpleSchedule</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">withMisfireHandlingInstructionFireNow</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">build</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>
<span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <p style="">Spring Boot has built-in support for Quartz. It automatically creates a Quartz&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">Scheduler</code>&nbsp;bean with the configuration that we supplied in the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">application.properties</code>&nbsp;file. That’s why we could directly inject the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">Scheduler</code>&nbsp;in the controller.</p> 
 <p style="">In the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">/scheduleEmail</code>&nbsp;API,</p> 
 <ul style=""> 
  <li style=""> <p style="margin-bottom: 15px;">We first validate the request body</p> </li> 
  <li style=""> <p style="margin-bottom: 15px;">Then, Build a JobDetail instance with a JobDataMap that contains the recipient email, subject, and body. The&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">JobDetail</code>&nbsp;that we create is of type&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">EmailJob</code>. We’ll define&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">EmailJob</code>&nbsp;in the next section.</p> </li> 
  <li style=""> <p style="margin-bottom: 15px;">Next, we Build a Trigger instance that defines when the Job should be executed.</p> </li> 
  <li style=""> <p style="margin-bottom: 15px;">Finally, we schedule the Job using&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">scheduler.scheduleJob()</code>&nbsp;API.</p> </li> 
 </ul> 
 <h2 id="creating-the-quartz-job-to-sends-emails" style="">Creating the Quartz Job to sends emails</h2> 
 <p style="">Let’s now define the Job that sends the actual emails. Spring Boot provides a wrapper around Quartz Scheduler’s Job interface called&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">QuartzJobBean</code>. This allows you to create Quartz Jobs as Spring beans where you can autowire other beans.</p> 
 <p style="">Let’s create our&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">EmailJob</code>&nbsp;by extending&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">QuartzJobBean</code>&nbsp;-</p> 
 <pre class=" language-java"><code class=" language-java" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;"><span class="token keyword" style="color: #0077aa;">package</span> com<span class="token punctuation" style="color: #999999;">.</span>example<span class="token punctuation" style="color: #999999;">.</span>quartzdemo<span class="token punctuation" style="color: #999999;">.</span>job<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>quartz<span class="token punctuation" style="color: #999999;">.</span>JobDataMap<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>quartz<span class="token punctuation" style="color: #999999;">.</span>JobExecutionContext<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>quartz<span class="token punctuation" style="color: #999999;">.</span>JobExecutionException<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>slf4j<span class="token punctuation" style="color: #999999;">.</span>Logger<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>slf4j<span class="token punctuation" style="color: #999999;">.</span>LoggerFactory<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>beans<span class="token punctuation" style="color: #999999;">.</span>factory<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>Autowired<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>boot<span class="token punctuation" style="color: #999999;">.</span>autoconfigure<span class="token punctuation" style="color: #999999;">.</span>mail<span class="token punctuation" style="color: #999999;">.</span>MailProperties<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>mail<span class="token punctuation" style="color: #999999;">.</span>javamail<span class="token punctuation" style="color: #999999;">.</span>JavaMailSender<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>mail<span class="token punctuation" style="color: #999999;">.</span>javamail<span class="token punctuation" style="color: #999999;">.</span>MimeMessageHelper<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>scheduling<span class="token punctuation" style="color: #999999;">.</span>quartz<span class="token punctuation" style="color: #999999;">.</span>QuartzJobBean<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>stereotype<span class="token punctuation" style="color: #999999;">.</span>Component<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> javax<span class="token punctuation" style="color: #999999;">.</span>mail<span class="token punctuation" style="color: #999999;">.</span>MessagingException<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> javax<span class="token punctuation" style="color: #999999;">.</span>mail<span class="token punctuation" style="color: #999999;">.</span>internet<span class="token punctuation" style="color: #999999;">.</span>MimeMessage<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>nio<span class="token punctuation" style="color: #999999;">.</span>charset<span class="token punctuation" style="color: #999999;">.</span>StandardCharsets<span class="token punctuation" style="color: #999999;">;</span>

<span class="token annotation punctuation" style="color: #999999;">@Component</span>
<span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">class</span> <span class="token class-name" style="">EmailJob</span> <span class="token keyword" style="color: #0077aa;">extends</span> <span class="token class-name" style="">QuartzJobBean</span> <span class="token punctuation" style="color: #999999;">{</span>
    <span class="token keyword" style="color: #0077aa;">private</span> <span class="token keyword" style="color: #0077aa;">static</span> <span class="token keyword" style="color: #0077aa;">final</span> Logger logger <span class="token operator" style="color: #a67f59;">=</span> LoggerFactory<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getLogger</span><span class="token punctuation" style="color: #999999;">(</span>EmailJob<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@Autowired</span>
    <span class="token keyword" style="color: #0077aa;">private</span> JavaMailSender mailSender<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@Autowired</span>
    <span class="token keyword" style="color: #0077aa;">private</span> MailProperties mailProperties<span class="token punctuation" style="color: #999999;">;</span>
    
    <span class="token annotation punctuation" style="color: #999999;">@Override</span>
    <span class="token keyword" style="color: #0077aa;">protected</span> <span class="token keyword" style="color: #0077aa;">void</span> <span class="token function" style="color: #dd4a68;">executeInternal</span><span class="token punctuation" style="color: #999999;">(</span>JobExecutionContext jobExecutionContext<span class="token punctuation" style="color: #999999;">)</span> <span class="token keyword" style="color: #0077aa;">throws</span> JobExecutionException <span class="token punctuation" style="color: #999999;">{</span>
        logger<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Executing Job with key {}"</span><span class="token punctuation" style="color: #999999;">,</span> jobExecutionContext<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getJobDetail</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getKey</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        JobDataMap jobDataMap <span class="token operator" style="color: #a67f59;">=</span> jobExecutionContext<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getMergedJobDataMap</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        String subject <span class="token operator" style="color: #a67f59;">=</span> jobDataMap<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"subject"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        String body <span class="token operator" style="color: #a67f59;">=</span> jobDataMap<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"body"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        String recipientEmail <span class="token operator" style="color: #a67f59;">=</span> jobDataMap<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"email"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token function" style="color: #dd4a68;">sendMail</span><span class="token punctuation" style="color: #999999;">(</span>mailProperties<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getUsername</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span> recipientEmail<span class="token punctuation" style="color: #999999;">,</span> subject<span class="token punctuation" style="color: #999999;">,</span> body<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token keyword" style="color: #0077aa;">private</span> <span class="token keyword" style="color: #0077aa;">void</span> <span class="token function" style="color: #dd4a68;">sendMail</span><span class="token punctuation" style="color: #999999;">(</span>String fromEmail<span class="token punctuation" style="color: #999999;">,</span> String toEmail<span class="token punctuation" style="color: #999999;">,</span> String subject<span class="token punctuation" style="color: #999999;">,</span> String body<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        <span class="token keyword" style="color: #0077aa;">try</span> <span class="token punctuation" style="color: #999999;">{</span>
            logger<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Sending Email to {}"</span><span class="token punctuation" style="color: #999999;">,</span> toEmail<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            MimeMessage message <span class="token operator" style="color: #a67f59;">=</span> mailSender<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">createMimeMessage</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

            MimeMessageHelper messageHelper <span class="token operator" style="color: #a67f59;">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">MimeMessageHelper</span><span class="token punctuation" style="color: #999999;">(</span>message<span class="token punctuation" style="color: #999999;">,</span> StandardCharsets<span class="token punctuation" style="color: #999999;">.</span>UTF_8<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            messageHelper<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setSubject</span><span class="token punctuation" style="color: #999999;">(</span>subject<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            messageHelper<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setText</span><span class="token punctuation" style="color: #999999;">(</span>body<span class="token punctuation" style="color: #999999;">,</span> <span class="token boolean" style="color: #990055;">true</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            messageHelper<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setFrom</span><span class="token punctuation" style="color: #999999;">(</span>fromEmail<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            messageHelper<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setTo</span><span class="token punctuation" style="color: #999999;">(</span>toEmail<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

            mailSender<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">send</span><span class="token punctuation" style="color: #999999;">(</span>message<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        <span class="token punctuation" style="color: #999999;">}</span> <span class="token keyword" style="color: #0077aa;">catch</span> <span class="token punctuation" style="color: #999999;">(</span><span class="token class-name" style="">MessagingException</span> ex<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
            logger<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">error</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Failed to send email to {}"</span><span class="token punctuation" style="color: #999999;">,</span> toEmail<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        <span class="token punctuation" style="color: #999999;">}</span>
    <span class="token punctuation" style="color: #999999;">}</span>
<span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <h2 id="running-the-application-and-testing-the-api" style="">Running the Application and Testing the API</h2> 
 <p style="">It’s time to run the application and watch the live action. Open your terminal, go to the root directory of the project and type the following command to run it -</p> 
 <pre class=" language-bash"><code class=" language-bash" style="font-family: monospace, monospace; font-size: 0.94em; background: 0px 0px; border: 0px; border-radius: 3px; padding: 1px 0px; line-height: 1.8;">mvn spring-boot:run -Dspring.mail.password<span class="token operator" style="color: #a67f59;">=</span><span class="token operator" style="color: #a67f59;">&lt;</span>YOUR_SMTP_PASSWORD<span class="token operator" style="color: #a67f59;">&gt;</span>
</code></pre> 
 <p style="">You don’t need to pass the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">spring.mail.password</code>&nbsp;command line argument if you have already set the password in the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">application.properties</code>&nbsp;file.</p> 
 <p style="">The application will start on port&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">8080</code>&nbsp;by default. Let’s now schedule an email using the&nbsp;<code style="font-family: monospace, monospace; font-size: 0.94em; background-color: #f6f8fa; border: 1px solid #f6f8fa; border-radius: 3px; padding: 1px 5px;">/scheduleEmail</code>API -</p> 
 <p>&lt;source media="(max-width: 520px)" srcset="https://www.callicoder.com/assets/images/post/medium/spring-boot-quartz-scheduler-email-scheduling-api.jpg" style="box-sizing: border-box;"&gt;&lt;/source&gt;<img style="border-style: none; max-width: 100%; vertical-align: middle; margin-bottom: 15px;" src="https://www.callicoder.com/assets/images/post/large/spring-boot-quartz-scheduler-email-scheduling-api.jpg" alt="Spring Boot Quartz Scheduler Email Job Scheduler API"></p> 
 <p style="">And, Here I get the email at the specified time :-)</p> 
 <p>&lt;source media="(max-width: 520px)" srcset="https://www.callicoder.com/assets/images/post/medium/spring-boot-quartz-scheduler-dyanmic-email-job-scheduling-example.jpg" style="box-sizing: border-box;"&gt;&lt;/source&gt;<img style="" src="https://www.callicoder.com/assets/images/post/large/spring-boot-quartz-scheduler-dyanmic-email-job-scheduling-example.jpg" alt="Spring Boot Quartz Scheduler Dynamic Email Job Scheduler API Example"></p> 
 <h2 id="conclusion" style="">Conclusion</h2> 
 <p style="">That’s all folks! I hope you enjoyed the article. You can find the complete source code of the project in the&nbsp;<a style="background-color: transparent; color: #419be8;" href="https://github.com/callicoder/spring-boot-quartz-scheduler-email-scheduling">Github Repository</a>. Consider giving the project a star on Github if you find it useful.</p> 
 <h3 id="references" style="">References</h3> 
 <ul style=""> 
  <li style=""> <p style="margin-bottom: 15px;"><a style="background-color: transparent; color: #419be8;" href="https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-quartz.html">Spring Boot Quartz Scheduler support</a></p> </li> 
  <li style=""> <p style="margin-bottom: 15px;"><a style="background-color: transparent; color: #419be8;" href="http://www.quartz-scheduler.org/documentation/quartz-2.2.x/tutorials/">Quartz Scheduler Official Tutorials</a></p> </li> 
 </ul> 
 <p style="">&nbsp;</p> 
 <p style="">&nbsp;</p> 
 <p style="">quartz 的数据库表结构：</p> 
 <p style="">地址：&nbsp;<a href="https://github.com/callicoder/spring-boot-quartz-scheduler-email-scheduling/blob/master/src/main/resources/quartz_tables.sql">https://github.com/callicoder/spring-boot-quartz-scheduler-email-scheduling/blob/master/src/main/resources/quartz_tables.sql</a></p> 
 <p style="">&nbsp;</p> 
 <table class="highlight tab-size js-file-line-container" style="">
  <tbody style=""> 
   <tr style=""> 
    <td id="LC1" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;">#</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L2" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC2" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">#</span> In your Quartz properties file, you'll need to set</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L3" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC3" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">#</span> org.quartz.jobStore.driverDelegateClass = org.quartz.impl.jdbcjobstore.StdJDBCDelegate</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L4" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC4" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;">#</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L5" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC5" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;">#</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L6" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC6" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">#</span> By: Ron Cordell - roncordell</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L7" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC7" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">#</span> I didn't see this anywhere, so I thought I'd post it here. This is the script from Quartz to create the tables in a MySQL database, modified to use INNODB instead of MYISAM.</span></td> 
   </tr> 
   <tr style=""> 
    <td id="L8" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC8" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L9" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC9" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_FIRED_TRIGGERS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L10" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC10" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_PAUSED_TRIGGER_GRPS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L11" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC11" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_SCHEDULER_STATE;</td> 
   </tr> 
   <tr style=""> 
    <td id="L12" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC12" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_LOCKS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L13" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC13" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_SIMPLE_TRIGGERS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L14" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC14" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_SIMPROP_TRIGGERS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L15" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC15" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_CRON_TRIGGERS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L16" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC16" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_BLOB_TRIGGERS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L17" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC17" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_TRIGGERS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L18" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC18" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_JOB_DETAILS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L19" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC19" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">DROP</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> IF EXISTS QRTZ_CALENDARS;</td> 
   </tr> 
   <tr style=""> 
    <td id="L20" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC20" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L21" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC21" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_JOB_DETAILS</span>(</td> 
   </tr> 
   <tr style=""> 
    <td id="L22" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC22" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L23" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC23" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L24" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC24" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L25" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC25" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">DESCRIPTION <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">250</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L26" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC26" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_CLASS_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">250</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L27" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC27" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">IS_DURABLE <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L28" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC28" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">IS_NONCONCURRENT <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L29" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC29" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">IS_UPDATE_DATA <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L30" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC30" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">REQUESTS_RECOVERY <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L31" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC31" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_DATA BLOB <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L32" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC32" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,JOB_NAME,JOB_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L33" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC33" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L34" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC34" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L35" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC35" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_TRIGGERS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L36" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC36" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L37" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC37" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L38" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC38" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L39" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC39" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L40" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC40" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L41" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC41" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">DESCRIPTION <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">250</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L42" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC42" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">NEXT_FIRE_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L43" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC43" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">PREV_FIRE_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L44" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC44" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">PRIORITY <span class="pl-k" style="color: #d73a49;">INTEGER</span> <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L45" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC45" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_STATE <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">16</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L46" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC46" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_TYPE <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">8</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L47" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC47" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">START_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L48" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC48" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">END_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L49" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC49" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">CALENDAR_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L50" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC50" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">MISFIRE_INSTR <span class="pl-k" style="color: #d73a49;">SMALLINT</span>(<span class="pl-c1" style="color: #005cc5;">2</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L51" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC51" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_DATA BLOB <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L52" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC52" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP),</td> 
   </tr> 
   <tr style=""> 
    <td id="L53" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC53" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">FOREIGN KEY</span> (SCHED_NAME,JOB_NAME,JOB_GROUP)</td> 
   </tr> 
   <tr style=""> 
    <td id="L54" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC54" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">REFERENCES</span> QRTZ_JOB_DETAILS(SCHED_NAME,JOB_NAME,JOB_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L55" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC55" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L56" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC56" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L57" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC57" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_SIMPLE_TRIGGERS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L58" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC58" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L59" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC59" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L60" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC60" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L61" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC61" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">REPEAT_COUNT <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">7</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L62" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC62" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">REPEAT_INTERVAL <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">12</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L63" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC63" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TIMES_TRIGGERED <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">10</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L64" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC64" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP),</td> 
   </tr> 
   <tr style=""> 
    <td id="L65" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC65" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">FOREIGN KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP)</td> 
   </tr> 
   <tr style=""> 
    <td id="L66" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC66" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">REFERENCES</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L67" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC67" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L68" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC68" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L69" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC69" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_CRON_TRIGGERS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L70" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC70" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L71" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC71" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L72" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC72" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L73" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC73" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">CRON_EXPRESSION <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L74" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC74" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TIME_ZONE_ID <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">80</span>),</td> 
   </tr> 
   <tr style=""> 
    <td id="L75" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC75" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP),</td> 
   </tr> 
   <tr style=""> 
    <td id="L76" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC76" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">FOREIGN KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP)</td> 
   </tr> 
   <tr style=""> 
    <td id="L77" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC77" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">REFERENCES</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L78" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC78" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L79" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC79" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L80" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC80" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_SIMPROP_TRIGGERS</span> </td> 
   </tr> 
   <tr style=""> 
    <td id="L81" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC81" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">(</td> 
   </tr> 
   <tr style=""> 
    <td id="L82" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC82" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L83" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC83" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L84" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC84" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L85" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC85" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">STR_PROP_1 <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">512</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L86" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC86" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">STR_PROP_2 <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">512</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L87" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC87" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">STR_PROP_3 <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">512</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L88" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC88" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">INT_PROP_1 <span class="pl-k" style="color: #d73a49;">INT</span> <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L89" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC89" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">INT_PROP_2 <span class="pl-k" style="color: #d73a49;">INT</span> <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L90" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC90" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">LONG_PROP_1 <span class="pl-k" style="color: #d73a49;">BIGINT</span> <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L91" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC91" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">LONG_PROP_2 <span class="pl-k" style="color: #d73a49;">BIGINT</span> <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L92" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC92" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">DEC_PROP_1 <span class="pl-k" style="color: #d73a49;">NUMERIC</span>(<span class="pl-c1" style="color: #005cc5;">13</span>,<span class="pl-c1" style="color: #005cc5;">4</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L93" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC93" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">DEC_PROP_2 <span class="pl-k" style="color: #d73a49;">NUMERIC</span>(<span class="pl-c1" style="color: #005cc5;">13</span>,<span class="pl-c1" style="color: #005cc5;">4</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L94" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC94" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">BOOL_PROP_1 <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L95" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC95" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">BOOL_PROP_2 <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L96" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC96" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP),</td> 
   </tr> 
   <tr style=""> 
    <td id="L97" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC97" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">FOREIGN KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP)</td> 
   </tr> 
   <tr style=""> 
    <td id="L98" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC98" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">REFERENCES</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L99" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC99" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L100" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC100" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L101" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC101" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_BLOB_TRIGGERS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L102" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC102" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L103" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC103" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L104" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC104" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L105" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC105" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">BLOB_DATA BLOB <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L106" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC106" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP),</td> 
   </tr> 
   <tr style=""> 
    <td id="L107" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC107" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">INDEX (SCHED_NAME,TRIGGER_NAME, TRIGGER_GROUP),</td> 
   </tr> 
   <tr style=""> 
    <td id="L108" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC108" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">FOREIGN KEY</span> (SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP)</td> 
   </tr> 
   <tr style=""> 
    <td id="L109" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC109" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">REFERENCES</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L110" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC110" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L111" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC111" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L112" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC112" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_CALENDARS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L113" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC113" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L114" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC114" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">CALENDAR_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L115" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC115" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">CALENDAR BLOB <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L116" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC116" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,CALENDAR_NAME))</td> 
   </tr> 
   <tr style=""> 
    <td id="L117" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC117" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L118" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC118" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L119" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC119" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_PAUSED_TRIGGER_GRPS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L120" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC120" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L121" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC121" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L122" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC122" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,TRIGGER_GROUP))</td> 
   </tr> 
   <tr style=""> 
    <td id="L123" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC123" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L124" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC124" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L125" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC125" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_FIRED_TRIGGERS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L126" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC126" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L127" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC127" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENTRY_ID <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">95</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L128" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC128" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L129" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC129" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">TRIGGER_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L130" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC130" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">INSTANCE_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L131" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC131" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">FIRED_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L132" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC132" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L133" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC133" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">PRIORITY <span class="pl-k" style="color: #d73a49;">INTEGER</span> <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L134" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC134" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">STATE <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">16</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L135" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC135" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L136" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC136" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">JOB_GROUP <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L137" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC137" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">IS_NONCONCURRENT <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L138" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC138" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">REQUESTS_RECOVERY <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">1</span>) <span class="pl-k" style="color: #d73a49;">NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L139" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC139" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,ENTRY_ID))</td> 
   </tr> 
   <tr style=""> 
    <td id="L140" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC140" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L141" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC141" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L142" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC142" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_SCHEDULER_STATE</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L143" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC143" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L144" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC144" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">INSTANCE_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">190</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L145" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC145" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">LAST_CHECKIN_TIME <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L146" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC146" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">CHECKIN_INTERVAL <span class="pl-k" style="color: #d73a49;">BIGINT</span>(<span class="pl-c1" style="color: #005cc5;">13</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L147" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC147" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,INSTANCE_NAME))</td> 
   </tr> 
   <tr style=""> 
    <td id="L148" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC148" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L149" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC149" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L150" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC150" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">TABLE</span> <span class="pl-en" style="color: #6f42c1;">QRTZ_LOCKS</span> (</td> 
   </tr> 
   <tr style=""> 
    <td id="L151" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC151" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">SCHED_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">120</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L152" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC152" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">LOCK_NAME <span class="pl-k" style="color: #d73a49;">VARCHAR</span>(<span class="pl-c1" style="color: #005cc5;">40</span>) <span class="pl-k" style="color: #d73a49;">NOT NULL</span>,</td> 
   </tr> 
   <tr style=""> 
    <td id="L153" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC153" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">PRIMARY KEY</span> (SCHED_NAME,LOCK_NAME))</td> 
   </tr> 
   <tr style=""> 
    <td id="L154" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC154" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">ENGINE<span class="pl-k" style="color: #d73a49;">=</span>InnoDB;</td> 
   </tr> 
   <tr style=""> 
    <td id="L155" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC155" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L156" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC156" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_J_REQ_RECOVERY</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_JOB_DETAILS(SCHED_NAME,REQUESTS_RECOVERY);</td> 
   </tr> 
   <tr style=""> 
    <td id="L157" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC157" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_J_GRP</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_JOB_DETAILS(SCHED_NAME,JOB_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L158" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC158" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L159" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC159" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_J</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,JOB_NAME,JOB_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L160" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC160" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_JG</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,JOB_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L161" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC161" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_C</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,CALENDAR_NAME);</td> 
   </tr> 
   <tr style=""> 
    <td id="L162" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC162" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_G</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L163" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC163" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_STATE</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_STATE);</td> 
   </tr> 
   <tr style=""> 
    <td id="L164" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC164" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_N_STATE</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP,TRIGGER_STATE);</td> 
   </tr> 
   <tr style=""> 
    <td id="L165" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC165" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_N_G_STATE</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_GROUP,TRIGGER_STATE);</td> 
   </tr> 
   <tr style=""> 
    <td id="L166" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC166" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_NEXT_FIRE_TIME</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,NEXT_FIRE_TIME);</td> 
   </tr> 
   <tr style=""> 
    <td id="L167" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC167" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_NFT_ST</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,TRIGGER_STATE,NEXT_FIRE_TIME);</td> 
   </tr> 
   <tr style=""> 
    <td id="L168" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC168" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_NFT_MISFIRE</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,MISFIRE_INSTR,NEXT_FIRE_TIME);</td> 
   </tr> 
   <tr style=""> 
    <td id="L169" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC169" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_NFT_ST_MISFIRE</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,MISFIRE_INSTR,NEXT_FIRE_TIME,TRIGGER_STATE);</td> 
   </tr> 
   <tr style=""> 
    <td id="L170" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC170" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_T_NFT_ST_MISFIRE_GRP</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_TRIGGERS(SCHED_NAME,MISFIRE_INSTR,NEXT_FIRE_TIME,TRIGGER_GROUP,TRIGGER_STATE);</td> 
   </tr> 
   <tr style=""> 
    <td id="L171" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC171" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L172" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC172" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_FT_TRIG_INST_NAME</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_FIRED_TRIGGERS(SCHED_NAME,INSTANCE_NAME);</td> 
   </tr> 
   <tr style=""> 
    <td id="L173" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC173" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_FT_INST_JOB_REQ_RCVRY</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_FIRED_TRIGGERS(SCHED_NAME,INSTANCE_NAME,REQUESTS_RECOVERY);</td> 
   </tr> 
   <tr style=""> 
    <td id="L174" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC174" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_FT_J_G</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_FIRED_TRIGGERS(SCHED_NAME,JOB_NAME,JOB_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L175" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC175" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_FT_JG</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_FIRED_TRIGGERS(SCHED_NAME,JOB_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L176" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC176" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_FT_T_G</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_FIRED_TRIGGERS(SCHED_NAME,TRIGGER_NAME,TRIGGER_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L177" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC177" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">CREATE</span> <span class="pl-k" style="color: #d73a49;">INDEX</span> <span class="pl-en" style="color: #6f42c1;">IDX_QRTZ_FT_TG</span> <span class="pl-k" style="color: #d73a49;">ON</span> QRTZ_FIRED_TRIGGERS(SCHED_NAME,TRIGGER_GROUP);</td> 
   </tr> 
   <tr style=""> 
    <td id="L178" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC178" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;">&nbsp;</td> 
   </tr> 
   <tr style=""> 
    <td id="L179" class="blob-num js-line-number" style="">&nbsp;</td> 
    <td id="LC179" class="blob-code blob-code-inner js-file-line" style="padding: 0px 10px; line-height: 20px; vertical-align: top; overflow: visible; font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; color: #24292e; white-space: pre;"> <span class="pl-k" style="color: #d73a49;">commit</span>;</td> 
   </tr> 
  </tbody>
 </table> 
</div>