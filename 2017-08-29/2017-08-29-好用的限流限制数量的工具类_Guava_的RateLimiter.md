#好用的限流限制数量的工具类 Guava 的RateLimiter
###发表时间：2017-08-29
###分类：java,guava,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2391416" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2391416</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>今天在网上溜达着看 Guava 的相关的内容，发现 Guava 居然有一个非常有用的类：RateLimiter。</p> 
 <p>它的 javadoc：</p> 
 <div class="quote_title">
  javadoc 写道
 </div> 
 <div class="quote_div">
  Open Declarationcom.google.common.util.concurrent.RateLimiter
  <br>
  <br>@ThreadSafe
  <br>@Beta
  <br>@GwtIncompatible
  <br>A rate limiter. Conceptually, a rate limiter distributes permits at a configurable rate. Each acquire() blocks if necessary until a permit is available, and then takes it. Once acquired, permits need not be released.
  <br>
  <br>Rate limiters are often used to restrict the rate at which some physical or logical resource is accessed. This is in contrast to java.util.concurrent.Semaphore which restricts the number of concurrent accesses instead of the rate (note though that concurrency and rate are closely related, e.g. see Little's Law).
  <br>
  <br>A RateLimiter is defined primarily by the rate at which permits are issued. Absent additional configuration, permits will be distributed at a fixed rate, defined in terms of permits per second. Permits will be distributed smoothly, with the delay between individual permits being adjusted to ensure that the configured rate is maintained.
  <br>
  <br>It is possible to configure a RateLimiter to have a warmup period during which time the permits issued each second steadily increases until it hits the stable rate.
  <br>
  <br>As an example, imagine that we have a list of tasks to execute, but we don't want to submit more than 2 per second:
  <br>
  <br> final RateLimiter rateLimiter = RateLimiter.create(2.0); // rate is "2 permits per second"
  <br> void submitTasks(List&lt;Runnable&gt; tasks, Executor executor) {
  <br> for (Runnable task : tasks) {
  <br> rateLimiter.acquire(); // may wait
  <br> executor.execute(task);
  <br> }
  <br> }}
  <br>As another example, imagine that we produce a stream of data, and we want to cap it at 5kb per second. This could be accomplished by requiring a permit per byte, and specifying a rate of 5000 permits per second:
  <br>
  <br> final RateLimiter rateLimiter = RateLimiter.create(5000.0); // rate = 5000 permits per second
  <br> void submitPacket(byte[] packet) {
  <br> rateLimiter.acquire(packet.length);
  <br> networkService.send(packet);
  <br> }}
  <br>It is important to note that the number of permits requested never affects the throttling of the request itself (an invocation to acquire(1) and an invocation to acquire(1000) will result in exactly the same throttling, if any), but it affects the throttling of the next request. I.e., if an expensive task arrives at an idle RateLimiter, it will be granted immediately, but it is the next request that will experience extra throttling, thus paying for the cost of the expensive task.
  <br>
  <br>Note: RateLimiter does not provide fairness guarantees.
  <br>
  <br>Since:
  <br>13.0
  <br>Author:
  <br>Dimitris Andreou
 </div> 
 <p>&nbsp;</p> 
 <p>发现这个有趣工具类的地址：&nbsp;<a href="http://andreabergia.com/guava-tips-ratelimiter/">http://andreabergia.com/guava-tips-ratelimiter/</a></p> 
 <p>&nbsp;</p> 
 <p>这个工具类可以限制每秒的处理任务数量。举个列子：QPS, queries per second。可以用来限制每秒并发的任务数量，每秒的访问查询次数，每秒传输的数据流量。这些在并发访问的 API 和 WEB 系统中非常有用。对系统的流量进行控制，防止服务器的资源被瞬间耗尽。而且这个RateLimiter是线程安全的，可以在并发的环境中直接使用。</p> 
 <p>Guava 中很多很好用的工具类在它的用户手册和书籍中都没有提到，还是需要自己去深入看看每个 package，挖掘 guava 的潜力。</p> 
 <p>&nbsp;附带自己的一个小例子：</p> 
 <pre name="code" class="java">public class RateLimiterExample {

    public static void main(String[] args) {
        RateLimiterExample example = new RateLimiterExample();
        example.testOne();
    }

    void testOne() {
        // 一秒钟可以发布 50 个许可
        RateLimiter limit = RateLimiter.create(50);
        for (int i = 0; i &lt; 1000; i++) {
            // 获得一个许可就解除阻塞。当前的代码逻辑：一秒钟限流为 50次
            double t = limit.acquire();
            System.out.println(String.format("current number is:%s, consumes time:%s seconds.", i, t));
        }
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class RateLimiterExample {

    public static void main(String[] args) {
        RateLimiterExample example = new RateLimiterExample();
        example.testOne();
    }

    void testOne() {
        // 一秒钟可以发布 1 个许可
        RateLimiter limit = RateLimiter.create(1);
        for (int i = 0; i &lt; 1000; i++) {
            // 获得 10 个许可就解除阻塞。当前的代码逻辑：一秒钟可以发放一个执行许可，这里需要积累到 10 个许可之后才能解除阻塞，效果是：这里将会 sleep 10秒后解除阻塞。
            double t = limit.acquire(10);
            System.out.println(String.format("current number is:%s, consumes time:%s seconds.", i, t));
        }
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>这里有一个别人翻译过的文档：&nbsp;<a href="http://ifeve.com/guava-ratelimiter/">http://ifeve.com/guava-ratelimiter/</a></p> 
 <p>内容：</p> 
 <h3 class="title"><span style="display: block; margin: 0px 340px 0px 5px; border-top: 1px solid #cccccc;">Guava官方文档-RateLimiter类</span></h3> 
 <div class="post_content" style="margin: 0px 340px 0px 0px; color: #666666; font-family: Arial, Helvetica, sans-serif;"> 
  <p style="margin-bottom: 1em; line-height: 35px;"><a style="color: #00a19e;" title="原文链接" href="http://docs.guava-libraries.googlecode.com/git/javadoc/com/google/common/util/concurrent/RateLimiter.html" target="_blank">原文链接</a>&nbsp;作者：Dimitris Andreou &nbsp;译者：魏嘉鹏 校对：方腾飞<img class="alignright size-medium wp-image-19366" style="float: right; height: auto; max-width: 100%; width: auto; margin: 10px 0px 30px 30px; display: inline;" src="http://ifeve.com/wp-content/uploads/2015/05/token_bucket-300x172.jpg" alt="token_bucket" width="300" height="172"></p> 
  <p style="margin-bottom: 1em; line-height: 35px;">RateLimiter 从概念上来讲，速率限制器会在可配置的速率下分配许可证。如果必要的话，每个acquire()&nbsp;会阻塞当前线程直到许可证可用后获取该许可证。一旦获取到许可证，不需要再释放许可证。</p> 
  <p style="margin-bottom: 1em; line-height: 35px;"><em>校对注：RateLimiter使用的是一种叫令牌桶的流控算法，RateLimiter会按照一定的频率往桶里扔令牌，线程拿到令牌才能执行，比如你希望自己的应用程序QPS不要超过1000，那么RateLimiter设置1000的速率后，就会每秒往桶里扔1000个令牌。</em></p> 
  <div id="highlighter_69846" class="syntaxhighlighter  " style="width: 1155.55px; margin-top: 1em !important; margin-right: 0px !important; margin-left: 0px !important; padding: 1px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 1em !important; direction: ltr !important;"> 
   <div class="lines" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">1</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">com.google.common.util.concurrent.RateLimiter</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">2</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;">&nbsp;</td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">3</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="color1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #808080 !important;">@ThreadSafe</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">4</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="color1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #808080 !important;">@Betapublic</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">5</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">abstract</code>&nbsp;<code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">class</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">RateLimiter&nbsp;</code><code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">extends</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">Object</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
   </div> 
  </div> 
  <p style="margin-bottom: 1em; line-height: 35px;"><span id="more-19269"></span><br>RateLimiter经常用于限制对一些物理资源或者逻辑资源的访问速率。与Semaphore&nbsp;相比，Semaphore&nbsp;限制了并发访问的数量而不是使用速率。（注意尽管并发性和速率是紧密相关的，比如参考<a style="color: #00a19e;" title="Little定律" href="http://en.wikipedia.org/wiki/Little's_law" target="_blank">Little定律</a>）</p> 
  <p style="margin-bottom: 1em; line-height: 35px;">通过设置许可证的速率来定义RateLimiter。在默认配置下，许可证会在固定的速率下被分配，速率单位是每秒多少个许可证。为了确保维护配置的速率，许可会被平稳地分配，许可之间的延迟会做调整。<br>可能存在配置一个拥有预热期的RateLimiter&nbsp;的情况，在这段时间内，每秒分配的许可数会稳定地增长直到达到稳定的速率。</p> 
  <p style="margin-bottom: 1em; line-height: 35px;">举例来说明如何使用RateLimiter，想象下我们需要处理一个任务列表，但我们不希望每秒的任务提交超过两个：</p> 
  <div id="highlighter_135684" class="syntaxhighlighter  " style="width: 1155.55px; margin-top: 1em !important; margin-right: 0px !important; margin-left: 0px !important; padding: 1px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 1em !important; direction: ltr !important;"> 
   <div class="lines" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">1</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="comments" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #3f5fbf !important;">//速率是每秒两个许可</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">2</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">final</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">RateLimiter rateLimiter = RateLimiter.create(</code><code class="value" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #009900 !important;">2.0</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">);</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">3</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;">&nbsp;</td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">4</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">void</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">submitTasks(List tasks, Executor executor) {</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">5</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="spaces" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">for</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">(Runnable task : tasks) {</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">6</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="spaces" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">rateLimiter.acquire();&nbsp;</code><code class="comments" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #3f5fbf !important;">// 也许需要等待</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">7</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="spaces" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">executor.execute(task);</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">8</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="spaces" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">}</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">9</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">}</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
   </div> 
  </div> 
  <p style="margin-bottom: 1em; line-height: 35px;">再举另外一个例子，想象下我们制造了一个数据流，并希望以每秒5kb的速率处理它。可以通过要求每个字节代表一个许可，然后指定每秒5000个许可来完成：</p> 
  <div id="highlighter_63272" class="syntaxhighlighter  " style="width: 1155.55px; margin-top: 1em !important; margin-right: 0px !important; margin-left: 0px !important; padding: 1px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 1em !important; direction: ltr !important;"> 
   <div class="lines" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">1</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="comments" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #3f5fbf !important;">// 每秒5000个许可</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">2</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">final</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">RateLimiter rateLimiter = RateLimiter.create(</code><code class="value" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important; color: #009900 !important;">5000.0</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">);</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">3</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;">&nbsp;</td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">4</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">void</code>&nbsp;<code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">submitPacket(</code><code class="keyword" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-weight: bold !important; direction: ltr !important; display: inline !important; color: #7f0055 !important;">byte</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">[] packet) {</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">5</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="spaces" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">rateLimiter.acquire(packet.length);</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt2" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">6</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"> <code class="spaces" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">networkService.send(packet);</code> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div class="line alt1" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
     <table style="margin: 0px !important; padding: 0px !important; border-collapse: collapse !important; width: auto !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
      <tbody style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;">
       <tr style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 1em !important; direction: ltr !important;"> 
        <td class="number" style="border: 0px !important; padding: 0px !important; margin: 0px !important; background-image: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: 3em !important; line-height: 1.1em !important; direction: ltr !important; color: #787878 !important;"><code style="margin: 0px !important; padding: 0px 0.3em 0px 0px !important; border: 0px !important; background: none !important; text-align: right !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: 2.7em !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: block !important;">7</code></td> 
        <td class="content" style="border-width: 0px 0px 0px 1px !important; border-left-style: solid !important; border-top-color: initial !important; border-right-color: initial !important; border-bottom-color: initial !important; border-left-color: #d4d0c8 !important; padding: 0px 0px 0px 0.5em !important; margin: 0px !important; background: none !important; float: none !important; vertical-align: top !important; height: auto !important; width: auto !important; line-height: 1.1em !important; direction: ltr !important;"><code class="plain" style="margin: 0px !important; padding: 0px !important; border: 0px !important; background: none !important; float: none !important; vertical-align: baseline !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; direction: ltr !important; display: inline !important;">}</code></td> 
       </tr>
      </tbody>
     </table> 
    </div> 
   </div> 
  </div> 
  <p style="margin-bottom: 1em; line-height: 35px;">有一点很重要，那就是请求的许可数从来不会影响到请求本身的限制（调用acquire(1)&nbsp;和调用acquire(1000)&nbsp;将得到相同的限制效果，如果存在这样的调用的话），但会影响下一次请求的限制，也就是说，如果一个高开销的任务抵达一个空闲的RateLimiter，它会被马上许可，但是下一个请求会经历额外的限制，从而来偿付高开销任务。注意：RateLimiter&nbsp;并不提供公平性的保证。</p> 
  <p style="margin-bottom: 1em; line-height: 35px;"><strong>Since:</strong>13.0 &nbsp;<strong>作者: &nbsp;&nbsp;</strong>Dimitris Andreou</p> 
  <h2 style="line-height: 33.6px; margin-bottom: 10px;">方法摘要</h2> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr> 
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>修饰符和类型</strong></th> 
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>方法和描述</strong></th> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">double</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">acquire()<br>从RateLimiter获取一个许可，该方法会被阻塞直到获取到请求</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">double</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">acquire(int&nbsp;permits)<br>从RateLimiter获取指定许可数，该方法会被阻塞直到获取到请求</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">static&nbsp;RateLimiter</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">create(double&nbsp;permitsPerSecond)<br>根据指定的稳定吞吐率创建RateLimiter，这里的吞吐率是指每秒多少许可数（通常是指QPS，每秒多少查询）</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">static&nbsp;RateLimiter</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">create(double&nbsp;permitsPerSecond, long&nbsp;warmupPeriod,&nbsp;TimeUnit&nbsp;unit)<br>根据指定的稳定吞吐率和预热期来创建RateLimiter，这里的吞吐率是指每秒多少许可数（通常是指QPS，每秒多少个请求量），在这段预热时间内，RateLimiter每秒分配的许可数会平稳地增长直到预热期结束时达到其最大速率。（只要存在足够请求数来使其饱和）</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">double</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">getRate()<br>返回RateLimiter&nbsp;配置中的稳定速率，该速率单位是每秒多少许可数</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">void</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">setRate(double&nbsp;permitsPerSecond)<br>更新RateLimite的稳定速率，参数permitsPerSecond&nbsp;由构造RateLimiter的工厂方法提供。</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">String</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">toString()<br>返回对象的字符表现形式</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">boolean</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">tryAcquire()<br>从RateLimiter&nbsp;获取许可，如果该许可可以在无延迟下的情况下立即获取得到的话</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">boolean</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">tryAcquire(int&nbsp;permits)<br>从RateLimiter&nbsp;获取许可数，如果该许可数可以在无延迟下的情况下立即获取得到的话</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">boolean</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">tryAcquire(int&nbsp;permits, long&nbsp;timeout,&nbsp;TimeUnit&nbsp;unit)<br>从RateLimiter&nbsp;获取指定许可数如果该许可数可以在不超过timeout的时间内获取得到的话，或者如果无法在timeout 过期之前获取得到许可数的话，那么立即返回false&nbsp;（无需等待）</td> 
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">boolean</td> 
     <td style="border: 1px solid #cccccc; padding: 15px;">tryAcquire(long&nbsp;timeout,&nbsp;TimeUnit&nbsp;unit)<br>从RateLimiter&nbsp;获取许可如果该许可可以在不超过timeout的时间内获取得到的话，或者如果无法在timeout 过期之前获取得到许可的话，那么立即返回false（无需等待）</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;">从java.lang.Object 类继承的方法</th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">clone,&nbsp;equals,&nbsp;finalize,&nbsp;getClass,&nbsp;hashCode,&nbsp;notify,&nbsp;notifyAll,&nbsp;wait,&nbsp;wait,&nbsp;wait</td> 
    </tr> 
   </tbody>
  </table> 
  <h2 style="line-height: 33.6px; margin-bottom: 10px;">方法细节</h2> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>create</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public static&nbsp;RateLimiter&nbsp;create(double&nbsp;permitsPerSecond)<br>根据指定的稳定吞吐率创建RateLimiter，这里的吞吐率是指每秒多少许可数（通常是指QPS，每秒多少查询）。<br>The returned&nbsp;RateLimiter&nbsp;ensures that on average no more than&nbsp;permitsPerSecond&nbsp;are issued during any given second, with sustained requests being smoothly spread over each second. When the incoming request rate exceeds&nbsp;permitsPerSecond&nbsp;the rate limiter will release one permit every&nbsp;(1.0 / permitsPerSecond)&nbsp;seconds. When the rate limiter is unused, bursts of up to&nbsp;permitsPerSecond&nbsp;permits will be allowed, with subsequent requests being smoothly limited at the stable rate of&nbsp;permitsPerSecond.<br>返回的RateLimiter&nbsp;确保了在平均情况下，每秒发布的许可数不会超过permitsPerSecond，每秒钟会持续发送请求。当传入请求速率超过permitsPerSecond，速率限制器会每秒释放一个许可(1.0 / permitsPerSecond 这里是指设定了permitsPerSecond为1.0)&nbsp;。当速率限制器闲置时，允许许可数暴增到permitsPerSecond，随后的请求会被平滑地限制在稳定速率permitsPerSecond中。<br><strong>参数:</strong><br>permitsPerSecond&nbsp;– 返回的RateLimiter的速率，意味着每秒有多少个许可变成有效。<br><strong>抛出:</strong><br>IllegalArgumentException&nbsp;– 如果permitsPerSecond为负数或者为0</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>create</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public static&nbsp;RateLimiter&nbsp;create(double&nbsp;permitsPerSecond,long&nbsp;warmupPeriod,TimeUnit&nbsp;unit)<br>根据指定的稳定吞吐率和预热期来创建RateLimiter，这里的吞吐率是指每秒多少许可数（通常是指QPS，每秒多少查询），在这段预热时间内，RateLimiter每秒分配的许可数会平稳地增长直到预热期结束时达到其最大速率（只要存在足够请求数来使其饱和）。同样地，如果RateLimiter&nbsp;在warmupPeriod时间内闲置不用，它将会逐步地返回冷却状态。也就是说，它会像它第一次被创建般经历同样的预热期。返回的RateLimiter&nbsp;主要用于那些需要预热期的资源，这些资源实际上满足了请求（比如一个远程服务），而不是在稳定（最大）的速率下可以立即被访问的资源。返回的RateLimiter&nbsp;在冷却状态下启动（即预热期将会紧跟着发生），并且如果被长期闲置不用，它将回到冷却状态。<br><strong>参数:</strong> <p style="margin-bottom: 1em; line-height: 35px;">&nbsp;</p> 
      <ul style="margin-bottom: 1em; line-height: 0px;"> 
       <li style="margin-bottom: 0px; margin-left: 0px; padding-left: 9px; line-height: 28px;">permitsPerSecond&nbsp;– 返回的RateLimiter的速率，意味着每秒有多少个许可变成有效。</li> 
       <li style="margin-bottom: 0px; margin-left: 0px; padding-left: 9px; line-height: 28px;">warmupPeriod&nbsp;– 在这段时间内RateLimiter会增加它的速率，在抵达它的稳定速率或者最大速率之前</li> 
       <li style="margin-bottom: 0px; margin-left: 0px; padding-left: 9px; line-height: 28px;">unit&nbsp;– 参数warmupPeriod 的时间单位</li> 
      </ul> <p style="margin-bottom: 1em; line-height: 35px;"><strong>抛出:</strong></p> 
      <ul style="margin-bottom: 1em; line-height: 0px;"> 
       <li style="margin-bottom: 0px; margin-left: 0px; padding-left: 9px; line-height: 28px;">IllegalArgumentException –&nbsp;如果permitsPerSecond为负数或者为0</li> 
      </ul> </td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>setRate</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public final&nbsp;void&nbsp;setRate(double&nbsp;permitsPerSecond)<br>更新RateLimite的稳定速率，参数permitsPerSecond&nbsp;由构造RateLimiter的工厂方法提供。调用该方法后，当前限制线程不会被唤醒，因此他们不会注意到最新的速率；只有接下来的请求才会。需要注意的是，由于每次请求偿还了（通过等待，如果需要的话）上一次请求的开销，这意味着紧紧跟着的下一个请求不会被最新的速率影响到，在调用了setRate&nbsp;之后；它会偿还上一次请求的开销，这个开销依赖于之前的速率。RateLimiter的行为在任何方式下都不会被改变，比如如果&nbsp;RateLimiter&nbsp;有20秒的预热期配置，在此方法被调用后它还是会进行20秒的预热。<br><strong>参数:</strong><br>permitsPerSecond&nbsp;– RateLimiter的新的稳定速率<br><strong>抛出:</strong><br>IllegalArgumentException&nbsp;– 如果permitsPerSecond为负数或者为0</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>getRate</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public final&nbsp;double&nbsp;getRate()<br>返回RateLimiter&nbsp;配置中的稳定速率，该速率单位是每秒多少许可数。它的初始值相当于构造这个RateLimiter的工厂方法中的参数permitsPerSecond&nbsp;，并且只有在调用setRate(double)后才会被更新。</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>acquire</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;double&nbsp;acquire()<br>从RateLimiter获取一个许可，该方法会被阻塞直到获取到请求。如果存在等待的情况的话，告诉调用者获取到该请求所需要的睡眠时间。该方法等同于acquire(1)。<br><strong>返回:</strong><br>time spent sleeping to enforce rate, in seconds; 0.0 if not rate-limited<br>执行速率的所需要的睡眠时间，单位为妙；如果没有则返回0<br><strong>Since:</strong><br>16.0 (版本13.0没有返回值)</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>acquire</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;double&nbsp;acquire(int&nbsp;permits)<br>从RateLimiter获取指定许可数，该方法会被阻塞直到获取到请求数。如果存在等待的情况的话，告诉调用者获取到这些请求数所需要的睡眠时间。<br><strong>参数:</strong><br>permits&nbsp;– 需要获取的许可数<br><strong>返回:</strong><br>执行速率的所需要的睡眠时间，单位为妙；如果没有则返回0<br><strong>抛出:</strong><br>IllegalArgumentException&nbsp;– 如果请求的许可数为负数或者为0<br><strong>Since:</strong><br>16.0 (版本13.0没有返回值)</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>tryAcquire</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;boolean&nbsp;tryAcquire(long&nbsp;timeout,TimeUnit&nbsp;unit)<br>从RateLimiter获取许可如果该许可可以在不超过timeout的时间内获取得到的话，或者如果无法在timeout 过期之前获取得到许可的话，那么立即返回false（无需等待）。该方法等同于tryAcquire(1, timeout, unit)。<br><strong>参数:</strong> <p style="margin-bottom: 1em; line-height: 35px;">&nbsp;</p> 
      <ul style="margin-bottom: 1em; line-height: 0px;"> 
       <li style="margin-bottom: 0px; margin-left: 0px; padding-left: 9px; line-height: 28px;">timeout&nbsp;– 等待许可的最大时间，负数以0处理</li> 
       <li style="margin-bottom: 0px; margin-left: 0px; padding-left: 9px; line-height: 28px;">unit&nbsp;– 参数timeout 的时间单位</li> 
      </ul> <p style="margin-bottom: 1em; line-height: 35px;"><strong>返回:</strong><br>true表示获取到许可，反之则是false<br><strong>抛出:</strong><br>IllegalArgumentException&nbsp;– 如果请求的许可数为负数或者为0</p> </td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>tryAcquire</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;boolean&nbsp;tryAcquire(int&nbsp;permits)<br>从RateLimiter&nbsp;获取许可数，如果该许可数可以在无延迟下的情况下立即获取得到的话。该方法等同于tryAcquire(permits, 0, anyUnit)。<br><strong>参数:</strong><br>permits&nbsp;– 需要获取的许可数<br><strong>返回:</strong><br>true表示获取到许可，反之则是false<br><strong>抛出:</strong><br>IllegalArgumentException&nbsp;– 如果请求的许可数为负数或者为0<br><strong>Since:</strong><br>14.0</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>tryAcquire</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;boolean&nbsp;tryAcquire()<br>从RateLimiter&nbsp;获取许可，如果该许可可以在无延迟下的情况下立即获取得到的话。<br>该方法等同于tryAcquire(1)。<br><strong>返回:</strong><br>true表示获取到许可，反之则是false<br><strong>Since:</strong><br>14.0</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>tryAcquire</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;boolean&nbsp;tryAcquire(int&nbsp;permits,long&nbsp;timeout,TimeUnit&nbsp;unit)<br>从RateLimiter&nbsp;获取指定许可数如果该许可数可以在不超过timeout的时间内获取得到的话，或者如果无法在timeout 过期之前获取得到许可数的话，那么立即返回false&nbsp;（无需等待）。<br><strong>参数:</strong><br>permits&nbsp;– 需要获取的许可数<br>timeout&nbsp;– 等待许可数的最大时间，负数以0处理<br>unit&nbsp;– 参数timeout 的时间单位<br><strong>返回:</strong><br>true表示获取到许可，反之则是false<br><strong>抛出:</strong><br>IllegalArgumentException&nbsp;-如果请求的许可数为负数或者为0</td> 
    </tr> 
   </tbody>
  </table> 
  <table style="margin: 0px 0px 1em; padding: 0px; border-collapse: collapse; width: 1166px; border: 0px;">
   <tbody> 
    <tr>
     <th style="border: 1px solid #cccccc; padding: 15px; background: #eeeeee; font-weight: normal;"><strong>toString</strong></th>
    </tr> 
    <tr> 
     <td style="border: 1px solid #cccccc; padding: 15px;">public&nbsp;String&nbsp;toString()<br>以下描述复制于java.lang.Object类。<br>返回对象的字符表现形式。通常来讲，toString&nbsp;方法返回一个“文本化呈现”对象的字符串。<br>结果应该是一个简明但易于读懂的信息表达式。建议所有子类都重写该方法。<br>toString 方法返回一个由实例的类名，字符’@’和以无符号十六进制表示的对象的哈希值组成的字符串。换句话说，该方法返回的字符串等同于：<br>getClass().getName() + ‘@’ + Integer.toHexString(hashCode())<br><strong>重载:</strong><br>Object类的toString方法<br><strong>返回:</strong><br>对象的字符表现形式</td> 
    </tr> 
   </tbody>
  </table> 
 </div> 
 <p>&nbsp;</p> 
</div>