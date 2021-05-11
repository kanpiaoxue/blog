#spring-retry简单包装工具类
###发表时间：2019-02-01
###分类：Spring,springboot,java,spring-retry
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2437337" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2437337</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>工具类：</p> 
 <pre name="code" class="java">import org.springframework.retry.RecoveryCallback;
import org.springframework.retry.RetryCallback;
import org.springframework.retry.RetryPolicy;
import org.springframework.retry.backoff.BackOffPolicy;
import org.springframework.retry.backoff.FixedBackOffPolicy;
import org.springframework.retry.policy.SimpleRetryPolicy;
import org.springframework.retry.support.RetryTemplate;

import com.google.common.base.Preconditions;

/**
 * @ClassName: RetryUtils
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/02/01 15:54:15
 * @Description: 重试工具类
 */
public class RetryUtils {

    /**
     * 创建重试模板
     *
     * @param retryPolicy
     *            重试策略
     * @param backOffPolicy
     *            延迟策略
     * @return 重试模板
     * @author kanpiaoxue
     * @CreateTime: 2019/02/01 16:23:00
     */
    public static RetryTemplate createRetryTemplate(RetryPolicy retryPolicy, BackOffPolicy backOffPolicy) {
        Preconditions.checkNotNull(retryPolicy, "retryPolicy is null");
        Preconditions.checkNotNull(backOffPolicy, "backOffPolicy is null");
        RetryTemplate template = new RetryTemplate();
        template.setRetryPolicy(retryPolicy);
        template.setBackOffPolicy(backOffPolicy);
        return template;
    }

    /**
     * 创建重试模板
     *
     * @param maxAttempts
     *            最大尝试次数
     * @param backOffPeriod
     *            延迟毫秒数
     * @return 重试模板
     * @author kanpiaoxue
     * @CreateTime: 2019/02/01 16:23:48
     */
    public static RetryTemplate createSimpleRetryTemplate(int maxAttempts, long backOffPeriod) {
        Preconditions.checkArgument(maxAttempts &gt;= 1, "maxAttempts must be greate than 1");
        Preconditions.checkArgument(backOffPeriod &gt;= 1, "backOffPeriod must be greate than 1");
        // 重试策略
        SimpleRetryPolicy retryPolicy = new SimpleRetryPolicy();
        retryPolicy.setMaxAttempts(maxAttempts);
        // 设置间隔策略
        FixedBackOffPolicy backOffPolicy = new FixedBackOffPolicy();
        backOffPolicy.setBackOffPeriod(backOffPeriod);
        // 初始化重试模板
        RetryTemplate template = createRetryTemplate(retryPolicy, backOffPolicy);
        return template;
    }

    /**
     * 使用重试策略执行方法
     *
     * @param maxAttempts
     *            最大尝试次数
     * @param backOffPeriod
     *            延迟毫秒数
     * @param retryCallback
     *            重试的方法回调函数
     * @return 正常执行方法的返回值
     * @throws E
     * @author kanpiaoxue
     * @CreateTime: 2019/02/01 16:24:25
     */
    public static &lt;T, E extends Throwable&gt; T execute(int maxAttempts, long backOffPeriod,
            RetryCallback&lt;T, E&gt; retryCallback) throws E {
        Preconditions.checkNotNull(retryCallback, "retryCallback is null");
        RetryTemplate template = createSimpleRetryTemplate(maxAttempts, backOffPeriod);
        return template.execute(retryCallback);
    }

    /**
     *
     * 使用重试策略执行方法
     *
     * @param maxAttempts
     *            最大尝试次数
     * @param backOffPeriod
     *            延迟毫秒数
     * @param retryCallback
     *            重试的方法回调函数
     * @param recoveryCallback
     *            重试失败之后覆盖回调函数
     * @return 正常执行方法的返回值
     * @throws E
     * @author kanpiaoxue
     * @CreateTime: 2019/02/01 16:25:41
     */
    public static &lt;T, E extends Throwable&gt; T execute(int maxAttempts, long backOffPeriod,
            RetryCallback&lt;T, E&gt; retryCallback, RecoveryCallback&lt;T&gt; recoveryCallback) throws E {
        Preconditions.checkNotNull(retryCallback, "retryCallback is null");
        Preconditions.checkNotNull(recoveryCallback, "recoveryCallback is null");
        RetryTemplate template = createSimpleRetryTemplate(maxAttempts, backOffPeriod);
        return template.execute(retryCallback, recoveryCallback);
    }

    /**
     * 私有化构造函数，防止被初始化
     */
    private RetryUtils() {
        super();
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>示例代码：</p> 
 <pre name="code" class="java">import org.kanpiaoxue.springExample.retry.utils.RetryUtils;
import org.springframework.retry.backoff.FixedBackOffPolicy;
import org.springframework.retry.policy.SimpleRetryPolicy;
import org.springframework.retry.support.RetryTemplate;

import java.util.concurrent.atomic.AtomicInteger;

/**
 * @ClassName: RetryExample
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/02/01 14:59:30
 */
public class RetryExample {

    /**
     *
     * @param args
     * @author kanpiaoxue
     * @throws Exception
     * @CreateTime: 2019/02/01 14:59:31
     */
    public static void main(String[] args) throws Exception {

        retry0();
        retry1();
        retry2();
        retry3();
    }

    public static void retry3() {

        AtomicInteger count = new AtomicInteger();
        String result = RetryUtils.execute(5, 3000L, context -&gt; {

            System.out.println("TestAll.main() " + count.incrementAndGet());
            throw new IllegalArgumentException();
        });
        System.out.println("result:" + result);
    }
    
    public static void retry2() {
        
        // 初始化重试模板
        RetryTemplate template = RetryUtils.createSimpleRetryTemplate(5, 3000L);
        
        AtomicInteger count = new AtomicInteger();
        String result = template.execute(context -&gt; {
            
            System.out.println("TestAll.main() " + count.incrementAndGet());
            throw new IllegalArgumentException();
        });
        
        System.out.println("result:" + result);
    }
    

    public static void retry1() {

        // 重试策略
        SimpleRetryPolicy retryPolicy = new SimpleRetryPolicy();
        retryPolicy.setMaxAttempts(5);

        // 设置间隔策略
        FixedBackOffPolicy backOffPolicy = new FixedBackOffPolicy();
        backOffPolicy.setBackOffPeriod(1000L);

        // 初始化重试模板
        RetryTemplate template = new RetryTemplate();
        template.setRetryPolicy(retryPolicy);
        template.setBackOffPolicy(backOffPolicy);

        AtomicInteger count = new AtomicInteger();

        String result = template.execute(context -&gt; {

            System.out.println("TestAll.main() " + count.incrementAndGet());
            throw new IllegalArgumentException();
        }, context -&gt; {
            System.out.println("TestAll.main() recover");
            return "world";
        });
        System.out.println("result:" + result);
    }
    
    public static void retry0() {
        
        AtomicInteger count = new AtomicInteger();
        String result = RetryUtils.execute(5, 3000L, context -&gt; {

            System.out.println("TestAll.main() " + count.incrementAndGet());
            throw new IllegalArgumentException();
        }, context -&gt; {
            System.out.println("TestAll.main() recover");
            return "world";
        });
        System.out.println("result:" + result);
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>