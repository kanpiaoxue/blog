#Mapped Diagnostic Context (MDC)
###发表时间：2020-12-14
###分类：log,slf4j,log4j
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2518080" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2518080</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">Mapped Diagnostic Context (MDC)</p> 
 <p style="font-size: 14px;">针对 MDC功能，目前只有logback 以及 log4j 支持。</p> 
 <p style="font-size: 14px;">相关文章：</p> 
 <ul style="font-size: 14px;"> 
  <li>https://www.baeldung.com/mdc-in-log4j-2-logback</li> 
  <li>http://logback.qos.ch/manual/mdc.html</li> 
  <li>https://www.jianshu.com/p/3fa7e7726fbb</li> 
  <li>https://ketao1989.github.io/2015/04/29/LogBack-Implemention-And-Slf4j-Mdc/</li> 
 </ul> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="margin-bottom: 10px; color: #333333; line-height: 1.334; font-family: raleway; font-size: 18px;">Let's now use the SLF4J's flavor of MDC. In this case, the syntax and semantics are the same as that in log4j:</p> 
 <pre><code class="language-java hljs" style="display: block; padding: 0px; color: #000000; font-family: 'source code pro', consolas, 'bitstream vera sans mono', 'courier new', Courier, monospace !important; font-size: 14px !important; line-height: 1.43 !important;"><span class="hljs-keyword" style="font-weight: 600; color: #267438;">import</span> org.slf4j.MDC;

<span class="hljs-keyword" style="font-weight: 600; color: #267438;">public</span> <span class="hljs-class"><span class="hljs-keyword" style="font-weight: 600; color: #267438;">class</span> <span class="hljs-title">Slf4jRunnable</span> <span class="hljs-keyword" style="font-weight: 600; color: #267438;">implements</span> <span class="hljs-title">Runnable</span> </span>{
    <span class="hljs-keyword" style="font-weight: 600; color: #267438;">private</span> <span class="hljs-keyword" style="font-weight: 600; color: #267438;">final</span> Transaction tx;
    
    <span class="hljs-function"><span class="hljs-keyword" style="font-weight: 600; color: #267438;">public</span> <span class="hljs-title">Slf4jRunnable</span><span class="hljs-params">(Transaction tx)</span> </span>{
        <span class="hljs-keyword" style="font-weight: 600; color: #267438;">this</span>.tx = tx;
    }
    
    <span class="hljs-function"><span class="hljs-keyword" style="font-weight: 600; color: #267438;">public</span> <span class="hljs-keyword" style="font-weight: 600; color: #267438;">void</span> <span class="hljs-title">run</span><span class="hljs-params">()</span> </span>{
        MDC.put(<span class="hljs-string" style="color: #267438; font-weight: bold;">"transaction.id"</span>, tx.getTransactionId());
        MDC.put(<span class="hljs-string" style="color: #267438; font-weight: bold;">"transaction.owner"</span>, tx.getOwner());
        <span class="hljs-keyword" style="font-weight: 600; color: #267438;">new</span> Slf4TransferService().transfer(tx.getAmount());
        MDC.clear();
    }
}
</code></pre> 
 <p style="margin-bottom: 10px; color: #333333; line-height: 1.334; font-family: raleway; font-size: 18px;">We have to provide the Logback configuration file,&nbsp;<em>logback.xml</em>:</p> 
 <div class="code-block code-block-5" style="color: #333333; font-family: raleway; font-size: 18px; margin: 8px 0px; clear: both;">
  &nbsp;
 </div> 
 <pre><code class="language-xml hljs" style="display: block; padding: 0px; color: #000000; font-family: 'source code pro', consolas, 'bitstream vera sans mono', 'courier new', Courier, monospace !important; font-size: 14px !important; line-height: 1.43 !important;"><span class="hljs-tag" style="color: #267438;">&lt;<span class="hljs-name" style="font-weight: bold;">configuration</span>&gt;</span>
    <span class="hljs-tag" style="color: #267438;">&lt;<span class="hljs-name" style="font-weight: bold;">appender</span> <span class="hljs-attr">name</span>=<span class="hljs-string" style="font-weight: bold;">"stdout"</span> <span class="hljs-attr">class</span>=<span class="hljs-string" style="font-weight: bold;">"ch.qos.logback.core.ConsoleAppender"</span>&gt;</span>
        <span class="hljs-tag" style="color: #267438;">&lt;<span class="hljs-name" style="font-weight: bold;">encoder</span> <span class="hljs-attr">class</span>=<span class="hljs-string" style="font-weight: bold;">"ch.qos.logback.classic.encoder.PatternLayoutEncoder"</span>&gt;</span>
            <span class="hljs-tag" style="color: #267438;">&lt;<span class="hljs-name" style="font-weight: bold;">pattern</span>&gt;</span>%-4r [%t] %5p %c{1} - %m - tx.id=%X{transaction.id} tx.owner=%X{transaction.owner}%n<span class="hljs-tag" style="color: #267438;">&lt;/<span class="hljs-name" style="font-weight: bold;">pattern</span>&gt;</span>
	<span class="hljs-tag" style="color: #267438;">&lt;/<span class="hljs-name" style="font-weight: bold;">encoder</span>&gt;</span>
    <span class="hljs-tag" style="color: #267438;">&lt;/<span class="hljs-name" style="font-weight: bold;">appender</span>&gt;</span>
    <span class="hljs-tag" style="color: #267438;">&lt;<span class="hljs-name" style="font-weight: bold;">root</span> <span class="hljs-attr">level</span>=<span class="hljs-string" style="font-weight: bold;">"TRACE"</span>&gt;</span>
        <span class="hljs-tag" style="color: #267438;">&lt;<span class="hljs-name" style="font-weight: bold;">appender-ref</span> <span class="hljs-attr">ref</span>=<span class="hljs-string" style="font-weight: bold;">"stdout"</span> /&gt;</span>
    <span class="hljs-tag" style="color: #267438;">&lt;/<span class="hljs-name" style="font-weight: bold;">root</span>&gt;</span>
<span class="hljs-tag" style="color: #267438;">&lt;/<span class="hljs-name" style="font-weight: bold;">configuration</span>&gt;</span>
</code></pre> 
 <p style="margin-bottom: 10px; color: #333333; line-height: 1.334; font-family: raleway; font-size: 18px;">Again, we'll see that the information in the MDC is properly added to the logged messages, even though this information is not explicitly provided in the&nbsp;<em>log.info()</em>&nbsp;method:</p> 
 <pre><code class="language-plaintext hljs" style="display: block; padding: 0px; color: #000000; font-family: 'source code pro', consolas, 'bitstream vera sans mono', 'courier new', Courier, monospace !important; font-size: 14px !important; line-height: 1.43 !important;">1020 [pool-1-thread-3]  INFO c.b.m.s.Slf4jBusinessService 
  - Has transfer of 1869$ completed successfully ? true. - tx.id=3 tx.owner=John
1021 [pool-1-thread-3]  INFO c.b.m.s.Slf4jBusinessService 
  - Preparing to transfer 1303$. - tx.id=6 tx.owner=Samantha
1221 [pool-1-thread-1]  INFO c.b.m.s.Slf4jBusinessService 
  - Has transfer of 1498$ completed successfully ? true. - tx.id=4 tx.owner=Marc
1221 [pool-1-thread-1]  INFO c.b.m.s.Slf4jBusinessService 
  - Preparing to transfer 1528$. - tx.id=7 tx.owner=Samantha
1492 [pool-1-thread-2]  INFO c.b.m.s.Slf4jBusinessService 
  - Has transfer of 1110$ completed successfully ? true. - tx.id=5 tx.owner=Samantha
1493 [pool-1-thread-2]  INFO c.b.m.s.Slf4jBusinessService 
  - Preparing to transfer 644$. - tx.id=8 tx.owner=John</code></pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <h1 style="font-size: 14px;">不合理使用MDC的危害</h1> 
 <p style="font-size: 14px;">MDC and Thread Pools</p> 
 <p style="font-size: 14px;">MDC implementations are usually using ThreadLocals to store the contextual information. That's an easy and reasonable way to achieve thread-safety. However, we should be careful using MDC with thread pools.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">Let's see how the combination of ThreadLocal-based MDCs and thread pools can be dangerous:</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <ol> 
  <li>We get a thread from the thread pool.</li> 
  <li>Then we store some contextual information in MDC using MDC.put() or ThreadContext.put().</li> 
  <li>We use this information in some logs and somehow we forgot to clear the MDC context.</li> 
  <li>The borrowed thread comes back to the thread pool.</li> 
  <li>After a while, the application gets the same thread from the pool.</li> 
  <li>Since we didn't clean up the MDC last time, this thread still owns some data from the previous execution.</li> 
 </ol> 
 <p style="font-size: 14px;">This may cause some unexpected inconsistencies between executions. One way to prevent this is to always remember to clean up the MDC context at the end of each execution. This approach usually needs rigorous human supervision and, therefore, is error-prone.</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>