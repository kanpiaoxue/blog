#springboot的Quartz使用
###发表时间：2018-10-08
###分类：springboot,Spring,java,经验,quartz
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431815" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431815</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="定义job接口">public interface Job {
    void setName(String name);
    void execute();
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import java.util.concurrent.TimeUnit;

@Component
public class SampleQuartzJob implements Job {
    private static final Logger LOGGER = LoggerFactory.getLogger(SampleQuartzJob.class);
    private String name;

    // Invoked if a Job data map entry with that name
    public void setName(String name) {
        this.name = name;
    }

    public void execute() {
        LOGGER.info(" --&gt; start to job work {}.", name);
        try {
            TimeUnit.SECONDS.sleep(5L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        LOGGER.info(" --&gt; finish job work {}.", name);
    }

}
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;
import java.util.concurrent.TimeUnit;

@Component
public class SampleQuartzJob2 implements Job {
    private static final Logger LOGGER = LoggerFactory.getLogger(SampleQuartzJob2.class);
    private String name;

    // Invoked if a Job data map entry with that name
    public void setName(String name) {
        this.name = name;
    }

    public void execute() {
        LOGGER.info(" --&gt; start to job doAction {}.", name);
        try {
            TimeUnit.SECONDS.sleep(5L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        LOGGER.info(" --&gt; finish job doAction {}.", name);
    }

}
</pre> 
 <p>&nbsp;&nbsp;</p> 
 <pre name="code" class="java">import org.quartz.JobDetail;
import org.quartz.Trigger;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.quartz.CronTriggerFactoryBean;
import org.springframework.scheduling.quartz.MethodInvokingJobDetailFactoryBean;
import org.springframework.scheduling.quartz.SchedulerFactoryBean;

@Configuration
public class QuartzManagement {

    private static final String JOB_NAME_SAMPLE_01 = "sampleJob-01";
    private static final String JOB_NAME_SAMPLE_02 = "sampleJob-02";

    public CronTriggerFactoryBean createCronTrigger(JobDetail jobDetail, String jobName,
            String cronExpression) {
        CronTriggerFactoryBean trigger = new CronTriggerFactoryBean();
        trigger.setName(getTriggerName(jobName));
        trigger.setCronExpression(cronExpression);
        trigger.setJobDetail(jobDetail);
        return trigger;
    }

    private MethodInvokingJobDetailFactoryBean createJobDetail(Job job) {
        MethodInvokingJobDetailFactoryBean jobDetailFactoryBean = new MethodInvokingJobDetailFactoryBean();
        // 是否设置并发执行
        jobDetailFactoryBean.setConcurrent(false);
        jobDetailFactoryBean.setTargetObject(job);
        jobDetailFactoryBean.setTargetMethod("execute");
        return jobDetailFactoryBean;
    }

    // 配置触发器
    @Bean(name = JOB_NAME_SAMPLE_01 + "trigger")
    public CronTriggerFactoryBean firstJobCornTriggerFacrotyBean(
            @Qualifier(JOB_NAME_SAMPLE_01) JobDetail jobDetail) {
        return createCronTrigger(jobDetail, JOB_NAME_SAMPLE_01, "*/2 * * * * ? *");
    }

    // 配置定时任务
    @Bean(name = JOB_NAME_SAMPLE_01)
    public MethodInvokingJobDetailFactoryBean firstJobDetail(SampleQuartzJob firstJob) {
        firstJob.setName(JOB_NAME_SAMPLE_01);
        return createJobDetail(firstJob);
    }

    private String getTriggerName(String jobName) {
        return String.format("%s-trigger", jobName);
    }

    // 配置触发器
    @Bean(name = JOB_NAME_SAMPLE_02 + "trigger")
    public CronTriggerFactoryBean secondJobCornTriggerFacrotyBean(
            @Qualifier(JOB_NAME_SAMPLE_02) JobDetail jobDetail) {
        return createCronTrigger(jobDetail, JOB_NAME_SAMPLE_02, "*/2 * * * * ? *");
    }

    // 配置定时任务
    @Bean(name = JOB_NAME_SAMPLE_02)
    public MethodInvokingJobDetailFactoryBean secondJobDetail(SampleQuartzJob2 firstJob) {
        firstJob.setName(JOB_NAME_SAMPLE_02);
        return createJobDetail(firstJob);
    }

    // 配置调度器
    @Bean
    public SchedulerFactoryBean schedulerFactoryBean(Trigger... cornTriggerFacrotyBean) {
        SchedulerFactoryBean bean = new SchedulerFactoryBean();
        bean.setSchedulerName("QUARTZ");
        bean.setTriggers(cornTriggerFacrotyBean);
        bean.setStartupDelay(5);
        return bean;
    }
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;或者更简洁的：</p> 
 <pre name="code" class="java">@SpringBootApplication
@EnableScheduling
public class BootApplication {
    private static final Logger LOGGER = LoggerFactory.getLogger(BootApplication.class);

    public static void main(String[] args) {
        LOGGER.info("start to run.");
        SpringApplication.run(BootApplication.class, args);
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public interface Job {

    void execute();

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Component
public class TestJob implements Job {
    private static final Logger LOGGER = LoggerFactory.getLogger(TestJob.class);
    private static final String JOB_NAME = TestJob.class.getSimpleName();

  
    @Override
    @Scheduled(cron = "${cronexpression:0 0 0/1 * * ?}")
    public void execute() {
        StopWatch sw = new StopWatch();
        sw.start();
        LOGGER.info("{} start to work. ", JOB_NAME);

        try {
            TimeUnit.SECONDS.sleep(5L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        LOGGER.info("{} finish working. it consumes {}", JOB_NAME, sw.toString());
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>