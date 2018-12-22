#java concurrent Queue
###发表时间：2011-12-15
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1312387" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1312387</a>

---

<p> </p>
<p>Queue： 基本上，一个队列就是一个先入先出（FIFO）的数据结构</p>
<p>&nbsp;</p>
<p>offer，add区别：</p>
<p>一些队列有大小限制，因此如果想在一个满的队列中加入一个新项，多出的项就会被拒绝。</p>
<p>这时新的 offer 方法就可以起作用了。它不是对调用 add() 方法抛出一个 unchecked 异常，而只是得到由 offer() 返回的 false。&nbsp;</p>
<p>&nbsp;</p>
<p>poll，remove区别：</p>
<p>remove() 和 poll() 方法都是从队列中删除第一个元素（head）。remove() 的行为与 Collection 接口的版本相似，</p>
<p>但是新的 poll() 方法在用空集合调用时不是抛出异常，只是返回 null。因此新的方法更适合容易出现异常条件的情况。</p>
<p>&nbsp;</p>
<p>peek，element区别：</p>
<p>element() 和 peek() 用于在队列的头部查询元素。与 remove() 方法类似，在队列为空时， element() 抛出一个异常，而 peek() 返回 null。</p>
<p>&nbsp;</p>
<p>-----------------------------------------------------------------------------------------</p>
<p>Tiger中有2组Queue的实现：实现了新的BlockingQueue接口的</p>
<p>和没有实现的</p>
<p>&nbsp;</p>
<p>-------------------------------------------------------------</p>
<p>没有实现的阻塞接口的：LinkedList： 实现了java.util.Queue接口</p>
<p>java.util.AbstractQueue</p>
<p>内置的不阻塞队列： PriorityQueue 和 ConcurrentLinkedQueue</p>
<p>&nbsp;</p>
<p>PriorityQueue 和 ConcurrentLinkedQueue 类在 Collection Framework 中加入两个具体集合实现。&nbsp;</p>
<p>&nbsp;</p>
<p>PriorityQueue 类实质上维护了一个有序列表。加入到 Queue 中的元素根据它们的天然排序（通过其 java.util.Comparable 实现）或者根据传递给构造函数的 java.util.Comparator 实现来定位。</p>
<p>&nbsp;</p>
<p>ConcurrentLinkedQueue 是基于链接节点的、线程安全的队列。并发访问不需要同步。因为它在队列的尾部添加元素并从头部删除它们，所以只要不需要知道队列的大小，ConcurrentLinkedQueue 对公共集合的共享访问就可以工作得很好。收集关于队列大小的信息会很慢，需要遍历队列。</p>
<p>&nbsp;</p>
<p>------------------------------------------------------------------</p>
<p>实现阻塞接口的：</p>
<p>&nbsp;</p>
<p>新的 java.util.concurrent 包在 Collection Framework 中可用的具体集合类中加入了 BlockingQueue 接口和五个阻塞队列类。</p>
<p>&nbsp;</p>
<p>它实质上就是一种带有一点扭曲的 FIFO 数据结构。不是立即从队列中添加或者删除元素，线程执行操作阻塞，直到有空间或者元素可用。</p>
<p>&nbsp;</p>
<p>五个队列所提供的各有不同：</p>
<p>&nbsp;</p>
<p>* ArrayBlockingQueue ：一个由数组支持的有界队列。</p>
<p>* LinkedBlockingQueue ：一个由链接节点支持的可选有界队列。</p>
<p>* PriorityBlockingQueue ：一个由优先级堆支持的无界优先级队列。</p>
<p>* DelayQueue ：一个由优先级堆支持的、基于时间的调度队列。</p>
<p>* SynchronousQueue ：一个利用 BlockingQueue 接口的简单聚集（rendezvous）机制。</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>前两个类 ArrayBlockingQueue 和 LinkedBlockingQueue 几乎相同，只是在后备存储器方面有所不同， LinkedBlockingQueue 并不总是有容量界限。无大小界限的 LinkedBlockingQueue 类在添加元素时永远不会有阻塞队列的等待（至少在其中有Integer.MAX_VALUE 元素之前不会）。</p>
<p>&nbsp;</p>
<p>PriorityBlockingQueue 是具有无界限容量的队列，它利用所包含元素的 Comparable 排序顺序来以逻辑顺序维护元素。可以将它看作 TreeSet 的可能替代物。不过对 PriorityBlockingQueue 有一个技巧。从 iterator() 返回的 Iterator 实例不需要以优先级顺序返回元素。如果必须以优先级顺序遍历所有元素，那么让它们都通过 toArray() 方法并自己对它们排序，像 Arrays.sort(pq.toArray())。</p>
<p>&nbsp;</p>
<p>新的 DelayQueue 实现可能是其中最有意思（也是最复杂）的一个。加入到队列中的元素必须实现新的 Delayed 接口（只有一个方法 —— long getDelay(java.util.concurrent.TimeUnit unit) ）。因为队列的大小没有界限，使得添加可以立即返回，但是在延迟时间过去之前不能从队列中取出元素。如果多个元素完成了延迟，那么最早失效/失效时间最长的元素将第一个取出。实际上没有听上去这样复杂。</p>
<p>&nbsp;</p>
<p>SynchronousQueue 类是最简单的。它没有内部容量。它就像线程之间的手递手机制。在队列中加入一个元素的生产者会等待另一个线程的消费者。当这个消费者出现时，这个元素就直接在消费者和生产者之间传递，永远不会加入到阻塞队列中。</p>
<p>&nbsp;</p>
<p>----------------------------------------------</p>
<p>实验结果：</p>
<p>&nbsp;</p>
<p>文档说BlockingQueue的队列： 不是立即从队列中添加或者删除元素，线程执行操作阻塞，直到有空间或者元素可用。</p>
<p>&nbsp;</p>
<p>实验了一下，使用put、take是这样子的,线程在等待</p>
<p>而使用offer是立刻返回false的</p>
<p>&nbsp;</p>
<p>---------// 引用自：&nbsp;<a href="http://zybing.itpub.net/post/170/376271">http://zybing.itpub.net/post/170/376271</a></p>