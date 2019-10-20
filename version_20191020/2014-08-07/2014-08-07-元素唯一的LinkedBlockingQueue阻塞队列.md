#元素唯一的LinkedBlockingQueue阻塞队列
###发表时间：2014-08-07
###分类：java,并发
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2101309" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2101309</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>最近看见以前的一段代码，就粘了出来。这就是一个简单的阻塞队列，它继承了JDK原有的LinkedBlockingQueue，它也是线程安全的。与LinkedBlockingQueue不同的地方在于，UniqueLinkedBlockingQueue队列里面不允许出现重复性元素。该队列可以在很多场景中适用，比如：</p> 
 <p>多生产者的情形下，一起向队列中存放任务，这些任务不允许在队列里面出现重复，就可以使用这个队列。</p> 
 <p>代码如下：</p> 
 <pre name="code" class="java">import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.locks.ReentrantLock;

/**
 * &lt;pre&gt;
 * UniqueLinkedBlockingQueue.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月7日 下午1:32:31&lt;br&gt;
 * Description : 元素唯一的LinkedBlockingQueue阻塞队列
 * &lt;/pre&gt;
 */
public class UniqueLinkedBlockingQueue&lt;E&gt; extends LinkedBlockingQueue&lt;E&gt; {

    private static final long serialVersionUID = 6523405086129214113L;
    private final ReentrantLock putLock = new ReentrantLock();

    public void put(E e) throws InterruptedException {
        putLock.lock();
        try {
            if (!contains(e)) {
                super.put(e);
            }
        } finally {
            putLock.unlock();
        }
    }
}</pre> 
 <p>&nbsp;</p> 
</div>