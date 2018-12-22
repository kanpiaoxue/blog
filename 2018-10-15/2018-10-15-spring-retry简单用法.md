#spring-retry简单用法
###发表时间：2018-10-15
###分类：Spring,springboot,java,spring-retry
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2432203" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2432203</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>有些场景需要我们对一些异常情况下面的任务进行重试，比如：调用远程的RPC服务，可能由于网络抖动出现第一次调用失败，尝试几次就可以恢复正常。</p> 
 <p>&nbsp;</p> 
 <p>spring-retry是spring提供的一个基于spring的重试框架，非常好用。</p> 
 <p>官网地址：&nbsp;<a href="https://github.com/spring-projects/spring-retry">https://github.com/spring-projects/spring-retry</a></p> 
 <p>&nbsp;</p> 
 <p>下面是springboot调用spring-retry：</p> 
 <p>配置依赖Maven：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.retry&lt;/groupId&gt;
    &lt;artifactId&gt;spring-retry&lt;/artifactId&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>启动类：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@SpringBootApplication
@EnableTransactionManagement // 启注解事务管理
@EnableScheduling
@EnableRetry // 【注意这里】启用了重试功能
public class TestWebApplication {

	public static void main(String[] args) {
		SpringApplication.run(TestWebApplication.class, args);
	}
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>重试部分的代码：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Service
public class RetryServiceImpl implements RetryService {
    private static final Logger LOGGER = LoggerFactory.getLogger(RetryServiceImpl.class);

    private AtomicInteger count = new AtomicInteger(1);


    @Override
    @Retryable(value = { RemoteAccessException.class }, maxAttemptsExpression = "${retry.maxAttempts:10}",
            backoff = @Backoff(delayExpression = "${retry.backoff:1000}"))
    public void retry() {
        LOGGER.info("start to retry : " + count.getAndIncrement());

        throw new RemoteAccessException("here " + count.get());
    }

    @Recover
    public void recover(RemoteAccessException t) {
        LOGGER.info("SampleRetryService.recover:{}", t.getClass().getName());
    }        
}    </pre> 
 <p>【注意】<span style="background-color: #fafafa; font-family: monospace;">@Recover 的用法。它要求它注释的方法的返回值必须和</span><span style="background-color: #fafafa; font-family: monospace;">@Retryable的注释的方法返回值保持一致，否则</span><span style="background-color: #fafafa; font-family: monospace;">@Recover</span><span style="background-color: #fafafa; font-family: monospace;">&nbsp;注释的方法不会被调用。它还有关于自己参数的使用要求。</span></p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">更详细的</span><span style="background-color: #fafafa; font-family: monospace;">@Recover</span><span style="background-color: #fafafa; font-family: monospace;">&nbsp;的使用说明，参考它的官网Javadoc，如下：</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  原文 写道
 </div> 
 <p>&nbsp;</p> 
 <div class="quote_div">
  Recovery method can be supplied, in case you want to take an alternative code path when the retry is exhausted. Methods should be declared in the same class as the @Retryable and marked @Recover. The return type must match the @Retryable method. The arguments for the recovery method can optionally include the exception that was thrown, and also optionally the arguments passed to the orginal retryable method (or a partial list of them as long as none are omitted).
 </div> 
 <p><span style="background-color: #fafafa; font-family: monospace;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">org.springframework.retry.annotation.Recover

@Import(value={RetryConfiguration.class})
@Target(value={METHOD, TYPE})
@Retention(value=RUNTIME)
@Documented
Annotation for a method invocation that is a recovery handler. 
A suitable recovery handler has a first parameter of 
type Throwable (or a subtype of Throwable) 
and a return value of the same type as the @Retryable 
method to recover from. The Throwable first argument 
is optional (but a method without it will only 
be called if no others match). Subsequent arguments 
are populated from the argument list of the failed method in order.

Since:
2.0
Author:
Dave Syer</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">还可以自己写代码的方法定制化retry的使用，如下：</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    public static void main(String[] args) throws InterruptedException {
        RetryTemplate template = new RetryTemplate();

        TimeoutRetryPolicy policy = new TimeoutRetryPolicy();
        policy.setTimeout(2000L);

        
        SimpleRetryPolicy retryPolicy = new SimpleRetryPolicy();
        retryPolicy.setMaxAttempts(5);
        
        //template.setRetryPolicy(policy);
        template.setRetryPolicy(retryPolicy);

        String result = template.execute(context -&gt; {

            System.out.println("TestAll.main()1");
            TimeUnit.SECONDS.sleep(1L);
            throw new IllegalArgumentException();
        }, context -&gt; {
            System.out.println("TestAll.main()2");
            return "world";
        });
        System.out.println("result:" + result);

    }</pre> 
 <p>【注意】</p> 
 <p>&nbsp;</p> 
 <p><span class="s1" style="font-family: 'Courier New';"><strong>interface</strong></span><span style="font-family: 'Courier New';"> RetryPolicy</span><span style="background-color: #fafafa; font-family: monospace;">&nbsp;它有很多的实现类可以使用。</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><span style="background-color: #fafafa; font-family: monospace;">下面是官网的原始内容：</span></p> 
 <p>This project provides declarative retry support for Spring applications. It is used in Spring Batch, Spring Integration, Spring for Apache Hadoop (amongst others).</p> 
 <h2> <a id="user-content-quick-start" class="anchor" href="https://github.com/spring-projects/spring-retry#quick-start"></a>Quick Start</h2> 
 <p>Example:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">@Configuration</span>
<span class="pl-k" style="color: #d73a49;">@EnableRetry</span>
<span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">class</span> <span class="pl-en" style="color: #6f42c1;">Application</span> {

    <span class="pl-k" style="color: #d73a49;">@Bean</span>
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-smi" style="color: #24292e;">Service</span> <span class="pl-en" style="color: #6f42c1;">service</span>() {
        <span class="pl-k" style="color: #d73a49;">return</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">Service</span>();
    }

}

<span class="pl-k" style="color: #d73a49;">@Service</span>
<span class="pl-k" style="color: #d73a49;">class</span> <span class="pl-en" style="color: #6f42c1;">Service</span> {
    <span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-smi" style="color: #24292e;">RemoteAccessException</span><span class="pl-k" style="color: #d73a49;">.</span>class)
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">service</span>() {
        <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> ... do something</span>
    }
    <span class="pl-k" style="color: #d73a49;">@Recover</span>
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">recover</span>(<span class="pl-smi" style="color: #24292e;">RemoteAccessException</span> <span class="pl-v" style="color: #e36209;">e</span>) {
       <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> ... panic</span>
    }
}</pre> 
 </div> 
 <p>Call the "service" method and if it fails with a&nbsp;<code>RemoteAccessException</code>&nbsp;then it will retry (up to three times by default), and then execute the "recover" method if unsuccessful. There are various options in the&nbsp;<code>@Retryable</code>&nbsp;annotation attributes for including and excluding exception types, limiting the number of retries and the policy for backoff.</p> 
 <h2> <a id="user-content-building" class="anchor" href="https://github.com/spring-projects/spring-retry#building"></a>Building</h2> 
 <p>Requires Java 1.7 and Maven 3.0.5 (or greater)</p> 
 <pre><code style="font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0px; margin: 0px; border-radius: 3px; border: 0px; display: inline; overflow: visible; line-height: inherit;">$ mvn install
</code></pre> 
 <h2> <a id="user-content-features-and-api" class="anchor" href="https://github.com/spring-projects/spring-retry#features-and-api"></a>Features and API</h2> 
 <h3> <a id="user-content-retrytemplate" class="anchor" href="https://github.com/spring-projects/spring-retry#retrytemplate"></a>RetryTemplate</h3> 
 <p>To make processing more robust and less prone to failure, sometimes it helps to automatically retry a failed operation in case it might succeed on a subsequent attempt. Errors that are susceptible to this kind of treatment are transient in nature. For example a remote call to a web service or RMI service that fails because of a network glitch or a&nbsp;<code>DeadLockLoserException</code>in a database update may resolve themselves after a short wait. To automate the retry of such operations Spring Retry has the&nbsp;<code>RetryOperations</code>&nbsp;strategy. The&nbsp;<code>RetryOperations</code>&nbsp;interface looks like this:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">interface</span> <span class="pl-en" style="color: #6f42c1;">RetryOperations</span> {

    <span class="pl-k" style="color: #d73a49;">&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-smi" style="color: #24292e;">T</span> <span class="pl-en" style="color: #6f42c1;">execute</span>(<span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">retryCallback</span>) <span class="pl-k" style="color: #d73a49;">throws</span> <span class="pl-smi" style="color: #24292e;">Exception</span>;

    <span class="pl-k" style="color: #d73a49;">&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-smi" style="color: #24292e;">T</span> <span class="pl-en" style="color: #6f42c1;">execute</span>(<span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">retryCallback</span>, <span class="pl-k" style="color: #d73a49;">RecoveryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">recoveryCallback</span>)
        <span class="pl-k" style="color: #d73a49;">throws</span> <span class="pl-smi" style="color: #24292e;">Exception</span>;

    <span class="pl-k" style="color: #d73a49;">&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-smi" style="color: #24292e;">T</span> <span class="pl-en" style="color: #6f42c1;">execute</span>(<span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">retryCallback</span>, <span class="pl-smi" style="color: #24292e;">RetryState</span> <span class="pl-v" style="color: #e36209;">retryState</span>)
        <span class="pl-k" style="color: #d73a49;">throws</span> <span class="pl-smi" style="color: #24292e;">Exception</span>, <span class="pl-smi" style="color: #24292e;">ExhaustedRetryException</span>;

    <span class="pl-k" style="color: #d73a49;">&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-smi" style="color: #24292e;">T</span> <span class="pl-en" style="color: #6f42c1;">execute</span>(<span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">retryCallback</span>, <span class="pl-k" style="color: #d73a49;">RecoveryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">recoveryCallback</span>,
        <span class="pl-smi" style="color: #24292e;">RetryState</span> <span class="pl-v" style="color: #e36209;">retryState</span>) <span class="pl-k" style="color: #d73a49;">throws</span> <span class="pl-smi" style="color: #24292e;">Exception</span>;

}</pre> 
 </div> 
 <p>The basic callback is a simple interface that allows you to insert some business logic to be retried:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">interface</span> <span class="pl-en" style="color: #6f42c1;">RetryCallback</span>&lt;T&gt; {

    <span class="pl-smi" style="color: #24292e;">T</span> <span class="pl-en" style="color: #6f42c1;">doWithRetry</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>) <span class="pl-k" style="color: #d73a49;">throws</span> <span class="pl-smi" style="color: #24292e;">Throwable</span>;

}</pre> 
 </div> 
 <p>The callback is executed and if it fails (by throwing an&nbsp;<code>Exception</code>), it will be retried until either it is successful, or the implementation decides to abort. There are a number of overloaded execute methods in the&nbsp;<code>RetryOperations</code>&nbsp;interface dealing with various use cases for recovery when all retry attempts are exhausted, and also with retry state, which allows clients and implementations to store information between calls (more on this later).</p> 
 <p>The simplest general purpose implementation of&nbsp;<code>RetryOperations</code>&nbsp;is&nbsp;<code>RetryTemplate</code>. It could be used like this</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-smi" style="color: #24292e;">RetryTemplate</span> template <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">RetryTemplate</span>();

<span class="pl-smi" style="color: #24292e;">TimeoutRetryPolicy</span> policy <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">TimeoutRetryPolicy</span>();
policy<span class="pl-k" style="color: #d73a49;">.</span>setTimeout(<span class="pl-c1" style="color: #005cc5;">30000L</span>);

template<span class="pl-k" style="color: #d73a49;">.</span>setRetryPolicy(policy);

<span class="pl-smi" style="color: #24292e;">Foo</span> result <span class="pl-k" style="color: #d73a49;">=</span> template<span class="pl-k" style="color: #d73a49;">.</span>execute(<span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">Foo</span>&gt;</span>() {

    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-smi" style="color: #24292e;">Foo</span> <span class="pl-en" style="color: #6f42c1;">doWithRetry</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>) {
        <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> Do stuff that might fail, e.g. webservice operation</span>
        <span class="pl-k" style="color: #d73a49;">return</span> result;
    }

});</pre> 
 </div> 
 <p>In the example we execute a web service call and return the result to the user. If that call fails then it is retried until a timeout is reached.</p> 
 <h3> <a id="user-content-retrycontext" class="anchor" href="https://github.com/spring-projects/spring-retry#retrycontext"></a>RetryContext</h3> 
 <p>The method parameter for the&nbsp;<code>RetryCallback</code>&nbsp;is a&nbsp;<code>RetryContext</code>. Many callbacks will simply ignore the context, but if necessary it can be used as an attribute bag to store data for the duration of the iteration.</p> 
 <p>A&nbsp;<code>RetryContext</code>&nbsp;will have a parent context if there is a nested retry in progress in the same thread. The parent context is occasionally useful for storing data that need to be shared between calls to execute.</p> 
 <h3> <a id="user-content-recoverycallback" class="anchor" href="https://github.com/spring-projects/spring-retry#recoverycallback"></a>RecoveryCallback</h3> 
 <p>When a retry is exhausted the&nbsp;<code>RetryOperations</code>&nbsp;can pass control to a different callback, the&nbsp;<code>RecoveryCallback</code>. To use this feature clients just pass in the callbacks together to the same method, for example:</p> 
 <pre><code style="font-family: SFMono-Regular, Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 13.6px; padding: 0px; margin: 0px; border-radius: 3px; border: 0px; display: inline; overflow: visible; line-height: inherit;">Foo foo = template.execute(new RetryCallback&lt;Foo&gt;() {
    public Foo doWithRetry(RetryContext context) {
        // business logic here
    },
  new RecoveryCallback&lt;Foo&gt;() {
    Foo recover(RetryContext context) throws Exception {
          // recover logic here
    }
});
</code></pre> 
 <p>If the business logic does not succeed before the template decides to abort, then the client is given the chance to do some alternate processing through the recovery callback.</p> 
 <h2> <a id="user-content-stateless-retry" class="anchor" href="https://github.com/spring-projects/spring-retry#stateless-retry"></a>Stateless Retry</h2> 
 <p>In the simplest case, a retry is just a while loop: the&nbsp;<code>RetryTemplate</code>&nbsp;can just keep trying until it either succeeds or fails. The&nbsp;<code>RetryContext</code>&nbsp;contains some state to determine whether to retry or abort, but this state is on the stack and there is no need to store it anywhere globally, so we call this stateless retry. The distinction between stateless and stateful retry is contained in the implementation of the&nbsp;<code>RetryPolicy</code>&nbsp;(the&nbsp;<code>RetryTemplate</code>&nbsp;can handle both). In a stateless retry, the callback is always executed in the same thread on retry as when it failed.</p> 
 <h2> <a id="user-content-stateful-retry" class="anchor" href="https://github.com/spring-projects/spring-retry#stateful-retry"></a>Stateful Retry</h2> 
 <p>Where the failure has caused a transactional resource to become invalid, there are some special considerations. This does not apply to a simple remote call because there is no transactional resource (usually), but it does sometimes apply to a database update, especially when using Hibernate. In this case it only makes sense to rethrow the exception that called the failure immediately so that the transaction can roll back and we can start a new valid one.</p> 
 <p>In these cases a stateless retry is not good enough because the re-throw and roll back necessarily involve leaving the&nbsp;<code>RetryOperations.execute()</code>&nbsp;method and potentially losing the context that was on the stack. To avoid losing it we have to introduce a storage strategy to lift it off the stack and put it (at a minimum) in heap storage. For this purpose Spring Retry provides a storage strategy&nbsp;<code>RetryContextCache</code>&nbsp;which can be injected into the&nbsp;<code>RetryTemplate</code>. The default implementation of the&nbsp;<code>RetryContextCache</code>&nbsp;is in memory, using a simple&nbsp;<code>Map</code>. It has a strictly enforced maximum capacity, to avoid memory leaks, but it doesn't have any advanced cache features like time to live. You should consider injecting a&nbsp;<code>Map</code>&nbsp;that had those features if you need them. Advanced usage with multiple processes in a clustered environment might also consider implementing the&nbsp;<code>RetryContextCache</code>&nbsp;with a cluster cache of some sort (though, even in a clustered environment this might be overkill).</p> 
 <p>Part of the responsibility of the&nbsp;<code>RetryOperations</code>&nbsp;is to recognize the failed operations when they come back in a new execution (and usually wrapped in a new transaction). To facilitate this, Spring Retry provides the&nbsp;<code>RetryState</code>&nbsp;abstraction. This works in conjunction with a special execute methods in the&nbsp;<code>RetryOperations</code>.</p> 
 <p>The way the failed operations are recognized is by identifying the state across multiple invocations of the retry. To identify the state, the user can provide an&nbsp;<code>RetryState</code>&nbsp;object that is responsible for returning a unique key identifying the item. The identifier is used as a key in the&nbsp;<code>RetryContextCache</code>.</p> 
 <blockquote> 
  <p><em>Warning:</em>&nbsp;Be very careful with the implementation of&nbsp;<code>Object.equals()</code>&nbsp;and&nbsp;<code>Object.hashCode()</code>&nbsp;in the key returned by&nbsp;<code>RetryState</code>. The best advice is to use a business key to identify the items. In the case of a JMS message the message ID can be used.</p> 
 </blockquote> 
 <p>When the retry is exhausted there is also the option to handle the failed item in a different way, instead of calling the&nbsp;<code>RetryCallback</code>&nbsp;(which is presumed now to be likely to fail). Just like in the stateless case, this option is provided by the&nbsp;<code>RecoveryCallback</code>, which can be provided by passing it in to the execute method of&nbsp;<code>RetryOperations</code>.</p> 
 <p>The decision to retry or not is actually delegated to a regular&nbsp;<code>RetryPolicy</code>, so the usual concerns about limits and timeouts can be injected there (see below).</p> 
 <h2> <a id="user-content-retry-policies" class="anchor" href="https://github.com/spring-projects/spring-retry#retry-policies"></a>Retry Policies</h2> 
 <p>Inside a&nbsp;<code>RetryTemplate</code>&nbsp;the decision to retry or fail in the execute method is determined by a&nbsp;<code>RetryPolicy</code>&nbsp;which is also a factory for the&nbsp;<code>RetryContext</code>. The&nbsp;<code>RetryTemplate</code>&nbsp;has the responsibility to use the current policy to create a&nbsp;<code>RetryContext</code>and pass that in to the&nbsp;<code>RetryCallback</code>&nbsp;at every attempt. After a callback fails the&nbsp;<code>RetryTemplate</code>&nbsp;has to make a call to the&nbsp;<code>RetryPolicy</code>&nbsp;to ask it to update its state (which will be stored in the&nbsp;<code>RetryContext</code>), and then it asks the policy if another attempt can be made. If another attempt cannot be made (e.g. a limit is reached or a timeout is detected) then the policy is also responsible for identifying the exhausted state, but not for handling the exception. The&nbsp;<code>RetryTemplate</code>&nbsp;will throw the original exception, except in the stateful case, when no recover is available, in which case it throws&nbsp;<code>RetryExhaustedException</code>. You can also set a flag in the&nbsp;<code>RetryTemplate</code>&nbsp;to have it unconditionally throw the original exception from the callback (i.e. from user code) instead.</p> 
 <blockquote> 
  <p><em>Tip:</em>&nbsp;Failures are inherently either retryable or not - if the same exception is always going to be thrown from the business logic, it doesn't help to retry it. So don't retry on all exception types - try to focus on only those exceptions that you expect to be retryable. It's not usually harmful to the business logic to retry more aggressively, but it's wasteful because if a failure is deterministic there will be time spent retrying something that you know in advance is fatal.</p> 
 </blockquote> 
 <p>Spring Retry provides some simple general purpose implementations of stateless RetryPolicy, for example a&nbsp;<code>SimpleRetryPolicy</code>, and the&nbsp;<code>TimeoutRetryPolicy</code>&nbsp;used in the example above.</p> 
 <p>The&nbsp;<code>SimpleRetryPolicy</code>&nbsp;just allows a retry on any of a named list of exception types, up to a fixed number of times:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> Set the max attempts including the initial attempt before retrying</span>
<span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> and retry on all exceptions (this is the default):</span>
<span class="pl-smi" style="color: #24292e;">SimpleRetryPolicy</span> policy <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">SimpleRetryPolicy</span>(<span class="pl-c1" style="color: #005cc5;">5</span>, <span class="pl-smi" style="color: #24292e;">Collections</span><span class="pl-k" style="color: #d73a49;">.</span>singletonMap(<span class="pl-smi" style="color: #24292e;">Exception</span><span class="pl-k" style="color: #d73a49;">.</span>class, <span class="pl-c1" style="color: #005cc5;">true</span>));

<span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> Use the policy...</span>
<span class="pl-smi" style="color: #24292e;">RetryTemplate</span> template <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">RetryTemplate</span>();
template<span class="pl-k" style="color: #d73a49;">.</span>setRetryPolicy(policy);
template<span class="pl-k" style="color: #d73a49;">.</span>execute(<span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">Foo</span>&gt;</span>() {
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-smi" style="color: #24292e;">Foo</span> <span class="pl-en" style="color: #6f42c1;">doWithRetry</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>) {
        <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> business logic here</span>
    }
});</pre> 
 </div> 
 <p>There is also a more flexible implementation called&nbsp;<code>ExceptionClassifierRetryPolicy</code>, which allows the user to configure different retry behavior for an arbitrary set of exception types though the&nbsp;<code>ExceptionClassifier</code>&nbsp;abstraction. The policy works by calling on the classifier to convert an exception into a delegate RetryPolicy, so for example, one exception type can be retried more times before failure than another by mapping it to a different policy.</p> 
 <p>Users might need to implement their own retry policies for more customized decisions. For instance, if there is a well-known, solution-specific, classification of exceptions into retryable and not retryable.</p> 
 <h2> <a id="user-content-backoff-policies" class="anchor" href="https://github.com/spring-projects/spring-retry#backoff-policies"></a>Backoff Policies</h2> 
 <p>When retrying after a transient failure it often helps to wait a bit before trying again, because usually the failure is caused by some problem that will only be resolved by waiting. If a&nbsp;<code>RetryCallback</code>&nbsp;fails, the&nbsp;<code>RetryTemplate</code>&nbsp;can pause execution according to the&nbsp;<code>BackoffPolicy</code>&nbsp;in place.</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">interface</span> <span class="pl-en" style="color: #6f42c1;">BackoffPolicy</span> {

    <span class="pl-smi" style="color: #24292e;">BackOffContext</span> <span class="pl-en" style="color: #6f42c1;">start</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>);

    <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">backOff</span>(<span class="pl-smi" style="color: #24292e;">BackOffContext</span> <span class="pl-v" style="color: #e36209;">backOffContext</span>)
        <span class="pl-k" style="color: #d73a49;">throws</span> <span class="pl-smi" style="color: #24292e;">BackOffInterruptedException</span>;

}</pre> 
 </div> 
 <p>A&nbsp;<code>BackoffPolicy</code>&nbsp;is free to implement the backOff in any way it chooses. The policies provided by Spring Retry out of the box all use&nbsp;<code>Object.wait()</code>. A common use case is to backoff with an exponentially increasing wait period, to avoid two retries getting into lock step and both failing - this is a lesson learned from the ethernet. For this purpose Spring Retry provides the&nbsp;<code>ExponentialBackoffPolicy</code>. There are also randomized versions delay policies that are quite useful to avoid resonating between related failures in a complex system.</p> 
 <h2> <a id="user-content-listeners" class="anchor" href="https://github.com/spring-projects/spring-retry#listeners"></a>Listeners</h2> 
 <p>Often it is useful to be able to receive additional callbacks for cross cutting concerns across a number of different retries. For this purpose Spring Retry provides the&nbsp;<code>RetryListener</code>&nbsp;interface. The&nbsp;<code>RetryTemplate</code>&nbsp;allows users to register RetryListeners, and they will be given callbacks with the&nbsp;<code>RetryContext</code>&nbsp;and&nbsp;<code>Throwable</code>&nbsp;where available during the iteration.</p> 
 <p>The interface looks like this:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">interface</span> <span class="pl-en" style="color: #6f42c1;">RetryListener</span> {

    <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">open</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>, <span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">callback</span>);

    <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">onError</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>, <span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">callback</span>, <span class="pl-smi" style="color: #24292e;">Throwable</span> <span class="pl-v" style="color: #e36209;">e</span>);

    <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">close</span>(<span class="pl-smi" style="color: #24292e;">RetryContext</span> <span class="pl-v" style="color: #e36209;">context</span>, <span class="pl-k" style="color: #d73a49;">RetryCallback&lt;<span class="pl-smi" style="color: #24292e;">T</span>&gt;</span> <span class="pl-v" style="color: #e36209;">callback</span>, <span class="pl-smi" style="color: #24292e;">Throwable</span> <span class="pl-v" style="color: #e36209;">e</span>);
}</pre> 
 </div> 
 <p>The open and close callbacks come before and after the entire retry in the simplest case and&nbsp;<code>onError</code>&nbsp;applies to the individual&nbsp;<code>RetryCallback</code>&nbsp;calls. The close method might also receive a&nbsp;<code>Throwable</code>; if there has been an error it is the last one thrown by the&nbsp;<code>RetryCallback</code>.</p> 
 <p>Note that when there is more than one listener, they are in a list, so there is an order. In this case open will be called in the same order while onError and close will be called in reverse order.</p> 
 <h2> <a id="user-content-declarative-retry" class="anchor" href="https://github.com/spring-projects/spring-retry#declarative-retry"></a>Declarative Retry</h2> 
 <p>Sometimes there is some business processing that you know you want to retry every time it happens. The classic example of this is the remote service call. Spring Retry provides an AOP interceptor that wraps a method call in a&nbsp;<code>RetryOperations</code>for just this purpose. The&nbsp;<code>RetryOperationsInterceptor</code>&nbsp;executes the intercepted method and retries on failure according to the&nbsp;<code>RetryPolicy</code>&nbsp;in the provided&nbsp;<code>RepeatTemplate</code>.</p> 
 <h3> <a id="user-content-java-configuration-for-retry-proxies" class="anchor" href="https://github.com/spring-projects/spring-retry#java-configuration-for-retry-proxies"></a>Java Configuration for Retry Proxies</h3> 
 <p>Add the&nbsp;<code>@EnableRetry</code>&nbsp;annotation to one of your&nbsp;<code>@Configuration</code>&nbsp;classes and use&nbsp;<code>@Retryable</code>&nbsp;on the methods (or type level for all methods) that you want to retry. You can also specify any number of retry listeners. Example</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">@Configuration</span>
<span class="pl-k" style="color: #d73a49;">@EnableRetry</span>
<span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">class</span> <span class="pl-en" style="color: #6f42c1;">Application</span> {

    <span class="pl-k" style="color: #d73a49;">@Bean</span>
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-smi" style="color: #24292e;">Service</span> <span class="pl-en" style="color: #6f42c1;">service</span>() {
        <span class="pl-k" style="color: #d73a49;">return</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">Service</span>();
    }
    
    <span class="pl-k" style="color: #d73a49;">@Bean</span> <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-smi" style="color: #24292e;">RetryListener</span> <span class="pl-en" style="color: #6f42c1;">retryListener1</span>() {
        <span class="pl-k" style="color: #d73a49;">return</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">RetryListener</span>() {<span class="pl-c1" style="color: #005cc5;">...</span>}
    }
    
    <span class="pl-k" style="color: #d73a49;">@Bean</span> <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-smi" style="color: #24292e;">RetryListener</span> <span class="pl-en" style="color: #6f42c1;">retryListener2</span>() {
        <span class="pl-k" style="color: #d73a49;">return</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">RetryListener</span>() {<span class="pl-c1" style="color: #005cc5;">...</span>}
    }

}

<span class="pl-k" style="color: #d73a49;">@Service</span>
<span class="pl-k" style="color: #d73a49;">class</span> <span class="pl-en" style="color: #6f42c1;">Service</span> {
    <span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-smi" style="color: #24292e;">RemoteAccessException</span><span class="pl-k" style="color: #d73a49;">.</span>class)
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-en" style="color: #6f42c1;">service</span>() {
        <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> ... do something</span>
    }
}</pre> 
 </div> 
 <p>Attributes of&nbsp;<code>@Retryable</code>&nbsp;can be used to control the&nbsp;<code>RetryPolicy</code>&nbsp;and&nbsp;<code>BackoffPolicy</code>, e.g.</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">@Service</span>
<span class="pl-k" style="color: #d73a49;">class</span> <span class="pl-en" style="color: #6f42c1;">Service</span> {
    <span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-c1" style="color: #005cc5;">maxAttempts</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-c1" style="color: #005cc5;">12</span>, <span class="pl-c1" style="color: #005cc5;">backoff</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-k" style="color: #d73a49;">@Backoff</span>(<span class="pl-c1" style="color: #005cc5;">delay</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-c1" style="color: #005cc5;">100</span>, <span class="pl-c1" style="color: #005cc5;">maxDelay</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-c1" style="color: #005cc5;">500</span>))
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-en" style="color: #6f42c1;">service</span>() {
        <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> ... do something</span>
    }
}</pre> 
 </div> 
 <p>for a random backoff between 100 and 500 milliseconds and up to 12 attempts. There is also a&nbsp;<code>stateful</code>&nbsp;attribute (default false) to control whether the retry is stateful or not. To use stateful retry the intercepted method has to have arguments, since they are used to construct the cache key for the state.</p> 
 <p>The&nbsp;<code>@EnableRetry</code>&nbsp;annotation also looks for beans of type&nbsp;<code>Sleeper</code>&nbsp;and other strategies used in the&nbsp;<code>RetryTemplate</code>&nbsp;and interceptors to control the beviour of the retry at runtime.</p> 
 <p>The&nbsp;<code>@EnableRetry</code>&nbsp;annotation creates proxies for&nbsp;<code>@Retryable</code>&nbsp;beans, and the proxies (so the bean instances in the application) have the&nbsp;<code>Retryable</code>&nbsp;interface added to them. This is purely a marker interface, but might be useful for other tools looking to apply retry advice (they should usually not bother if the bean already implements&nbsp;<code>Retryable</code>).</p> 
 <p>Recovery method can be supplied, in case you want to take an alternative code path when the retry is exhausted. Methods should be declared in the same class as the&nbsp;<code>@Retryable</code>&nbsp;and marked&nbsp;<code>@Recover</code>. The return type must match the&nbsp;<code>@Retryable</code>&nbsp;method. The arguments for the recovery method can optionally include the exception that was thrown, and also optionally the arguments passed to the orginal retryable method (or a partial list of them as long as none are omitted). Example:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">@Service</span>
<span class="pl-k" style="color: #d73a49;">class</span> <span class="pl-en" style="color: #6f42c1;">Service</span> {
    <span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-smi" style="color: #24292e;">RemoteAccessException</span><span class="pl-k" style="color: #d73a49;">.</span>class)
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">service</span>(<span class="pl-smi" style="color: #24292e;">String</span> <span class="pl-v" style="color: #e36209;">str1</span>, <span class="pl-smi" style="color: #24292e;">String</span> <span class="pl-v" style="color: #e36209;">str2</span>) {
        <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> ... do something</span>
    }
    <span class="pl-k" style="color: #d73a49;">@Recover</span>
    <span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> <span class="pl-en" style="color: #6f42c1;">recover</span>(<span class="pl-smi" style="color: #24292e;">RemoteAccessException</span> <span class="pl-v" style="color: #e36209;">e</span>, <span class="pl-smi" style="color: #24292e;">String</span> <span class="pl-v" style="color: #e36209;">str1</span>, <span class="pl-smi" style="color: #24292e;">String</span> <span class="pl-v" style="color: #e36209;">str2</span>) {
       <span class="pl-c" style="color: #6a737d;"><span class="pl-c">//</span> ... error handling making use of original args if required</span>
    }
}</pre> 
 </div> 
 <p>Version 1.2 introduces the ability to use expressions for certain properties:</p> 
 <div class="highlight highlight-source-java"> 
  <pre><span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-c1" style="color: #005cc5;">exceptionExpression</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{message.contains('this can be retried')}<span class="pl-pds">"</span></span>)
<span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> service1() {
  <span class="pl-c1" style="color: #005cc5;">...</span>
}

<span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-c1" style="color: #005cc5;">exceptionExpression</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{message.contains('this can be retried')}<span class="pl-pds">"</span></span>)
<span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> service2() {
  <span class="pl-c1" style="color: #005cc5;">...</span>
}

<span class="pl-k" style="color: #d73a49;">@Retryable</span>(<span class="pl-c1" style="color: #005cc5;">exceptionExpression</span><span class="pl-k" style="color: #d73a49;">=</span><span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{@exceptionChecker.shouldRetry(#root)}<span class="pl-pds">"</span></span>,
    <span class="pl-c1" style="color: #005cc5;">maxAttemptsExpression</span> <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{@integerFiveBean}<span class="pl-pds">"</span></span>,
  <span class="pl-c1" style="color: #005cc5;">backoff</span> <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-k" style="color: #d73a49;">@Backoff</span>(<span class="pl-c1" style="color: #005cc5;">delayExpression</span> <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{1}<span class="pl-pds">"</span></span>, <span class="pl-c1" style="color: #005cc5;">maxDelayExpression</span> <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{5}<span class="pl-pds">"</span></span>, <span class="pl-c1" style="color: #005cc5;">multiplierExpression</span> <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>#{1.1}<span class="pl-pds">"</span></span>))
<span class="pl-k" style="color: #d73a49;">public</span> <span class="pl-k" style="color: #d73a49;">void</span> service3() {
  <span class="pl-c1" style="color: #005cc5;">...</span>
}</pre> 
 </div> 
 <p>These use the familier Spring SpEL expression syntax (<code>#{...}</code>).</p> 
 <p>Expressions can contain property placeholders such as&nbsp;<code>#{${max.delay}}</code>&nbsp;or&nbsp;<code>#{@exceptionChecker.${retry.method}(#root)}</code></p> 
 <ul> 
  <li> <code>exceptionExpression</code>&nbsp;is evaluated against the thrown exception as the&nbsp;<code>#root</code>&nbsp;object.</li> 
  <li style="margin-top: 0.25em;"> <code>maxAttemptsExpression</code>&nbsp;and the&nbsp;<code>@BackOff</code>&nbsp;expression attributes are evaluated once, during initialization; there is no root object for the evaluation but they can reference other beans in the context.</li> 
 </ul> 
 <h3> <a id="user-content-xml-configuration" class="anchor" href="https://github.com/spring-projects/spring-retry#xml-configuration"></a>XML Configuration</h3> 
 <p>Here is an example of declarative iteration using Spring AOP to repeat a service call to a method called&nbsp;<code>remoteCall</code>&nbsp;(for more detail on how to configure AOP interceptors see the Spring User Guide):</p> 
 <div class="highlight highlight-text-xml"> 
  <pre>&lt;<span class="pl-ent" style="color: #22863a;">aop</span><span class="pl-ent" style="color: #22863a;">:</span><span class="pl-ent" style="color: #22863a;">config</span>&gt;
    &lt;<span class="pl-ent" style="color: #22863a;">aop</span><span class="pl-ent" style="color: #22863a;">:</span><span class="pl-ent" style="color: #22863a;">pointcut</span> <span class="pl-e" style="color: #6f42c1;">id</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>transactional<span class="pl-pds">"</span></span>
        <span class="pl-e" style="color: #6f42c1;">expression</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>execution(* com..*Service.remoteCall(..))<span class="pl-pds">"</span></span> /&gt;
    &lt;<span class="pl-ent" style="color: #22863a;">aop</span><span class="pl-ent" style="color: #22863a;">:</span><span class="pl-ent" style="color: #22863a;">advisor</span> <span class="pl-e" style="color: #6f42c1;">pointcut-ref</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>transactional<span class="pl-pds">"</span></span>
        <span class="pl-e" style="color: #6f42c1;">advice-ref</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>retryAdvice<span class="pl-pds">"</span></span> <span class="pl-e" style="color: #6f42c1;">order</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>-1<span class="pl-pds">"</span></span>/&gt;
&lt;/<span class="pl-ent" style="color: #22863a;">aop</span><span class="pl-ent" style="color: #22863a;">:</span><span class="pl-ent" style="color: #22863a;">config</span>&gt;

&lt;<span class="pl-ent" style="color: #22863a;">bean</span> <span class="pl-e" style="color: #6f42c1;">id</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>retryAdvice<span class="pl-pds">"</span></span>
    <span class="pl-e" style="color: #6f42c1;">class</span>=<span class="pl-s" style="color: #032f62;"><span class="pl-pds">"</span>org.springframework.retry.interceptor.RetryOperationsInterceptor<span class="pl-pds">"</span></span>/&gt;</pre> 
 </div> 
 <p>The example above uses a default&nbsp;<code>RetryTemplate</code>&nbsp;inside the interceptor. To change the policies or listeners, you only need to inject an instance of&nbsp;<code>RetryTemplate</code>&nbsp;into the interceptor.</p> 
 <h2> <a id="user-content-contributing" class="anchor" href="https://github.com/spring-projects/spring-retry#contributing"></a>Contributing</h2> 
 <p>Spring Retry is released under the non-restrictive Apache 2.0 license, and follows a very standard Github development process, using Github tracker for issues and merging pull requests into master. If you want to contribute even something trivial please do not hesitate, but follow the guidelines below.</p> 
 <p>Before we accept a non-trivial patch or pull request we will need you to sign the&nbsp;<a style="background-color: initial; color: #0366d6;" href="https://cla.pivotal.io/%5Bcontributor's" rel="nofollow">https://cla.pivotal.io/[contributor's</a>agreement]. Signing the contributor's agreement does not grant anyone commit rights to the main repository, but it does mean that we can accept your contributions, and you will get an author credit if we do. Active contributors might be asked to join the core team, and given the ability to merge pull requests.</p> 
 <h2> <a id="user-content-code-of-conduct" class="anchor" href="https://github.com/spring-projects/spring-retry#code-of-conduct"></a>Code of Conduct</h2> 
 <p>This project adheres to the&nbsp;<a style="background-color: initial; color: #0366d6;" href="https://github.com/spring-projects/spring-retry/blob/master/CODE_OF_CONDUCT.adoc">Contributor Covenant</a>. By participating, you are expected to uphold this code. Please report unacceptable behavior to&nbsp;<a style="background-color: initial; color: #0366d6;" href="mailto:spring-code-of-conduct@pivotal.io">spring-code-of-conduct@pivotal.io</a>.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>