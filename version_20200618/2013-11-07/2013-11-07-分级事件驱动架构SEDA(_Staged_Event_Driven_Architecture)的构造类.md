#分级事件驱动架构SEDA( Staged Event Driven Architecture)的构造类
###发表时间：2013-11-07
###分类：java,SEDA
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1972526" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1972526</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

import org.apache.log4j.Logger;

/**
 * &lt;pre&gt;
 * 分级事件驱动架构SEDA( Staged E ventDriven A rch itecture)的构造类
 * @author kanpiaoxue
 * @param &lt;Task&gt; SEDAThreadPoolUtils内置的 interface Task
 * 2013-11-07
 * &lt;/pre&gt;
 */
public final class SEDAThreadPool {
	private static final Logger LOGGER = Logger.getLogger(SEDAThreadPool.class);
	private final BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue;
	private final BlockingQueue&lt;SEDAThreadPool.Task&gt; outputQueue;
	private final ExecutorService exec;
	private final String threadName;
	private final int threadPoolSize;
	private final ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt; conflictMap;
	private volatile boolean hasOutput;
	private volatile boolean hasConflictMap;

	/**
	 * &lt;pre&gt;
	 * @param threadName 工作线程的名称
	 * @param inputQueue 输入任务的队列
	 * @param outputQueue 输出任务的队列。当不存在输出队列是，该项可以为 null
	 * @param exec 执行的线程池。如果该项为 null，则采用默认的 Executors.newCachedThreadPool()
	 * @param threadPoolSize 线程池的大小
	 * &lt;/pre&gt;
	 */
	public SEDAThreadPool(String threadName, BlockingQueue&lt;Task&gt; inputQueue,
			BlockingQueue&lt;Task&gt; outputQueue, ExecutorService exec,
			int threadPoolSize) {
		this(threadName, inputQueue, outputQueue, exec, threadPoolSize, null);
	}

	/**
	 * &lt;pre&gt;
	 * @param threadName 工作线程的名称
	 * @param inputQueue 输入任务的队列
	 * @param exec 执行的线程池。如果该项为 null，则采用默认的 Executors.newCachedThreadPool()
	 * @param threadPoolSize 线程池的大小
	 * &lt;/pre&gt;
	 */
	public SEDAThreadPool(String threadName, BlockingQueue&lt;Task&gt; inputQueue,
			ExecutorService exec, int threadPoolSize) {
		this(threadName, inputQueue, null, exec, threadPoolSize, null);
	}

	/**
	 * &lt;pre&gt;
	 * @param threadName 工作线程的名称
	 * @param inputQueue 输入任务的队列
	 * @param exec 执行的线程池。如果该项为 null，则采用默认的 Executors.newCachedThreadPool()
	 * @param threadPoolSize 线程池的大小
	 * @param conflictMap Task发生冲突Map ：和 conflictMap 中的key存在冲突的任务都不会被执行
	 * &lt;/pre&gt;
	 */
	public SEDAThreadPool(
			String threadName,
			BlockingQueue&lt;Task&gt; inputQueue,
			ExecutorService exec,
			int threadPoolSize,
			ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt; conflictMap) {
		this(threadName, inputQueue, null, exec, threadPoolSize, conflictMap);
	}

	/**
	 * &lt;pre&gt;
	 * @param threadName 工作线程的名称
	 * @param inputQueue 输入任务的队列
	 * @param outputQueue 输出任务的队列。当不存在输出队列是，该项可以为 null
	 * @param exec 执行的线程池。如果该项为 null，则采用默认的 Executors.newCachedThreadPool()
	 * @param threadPoolSize 线程池的大小
	 * @param conflictMap Task发生冲突Map ：和 conflictMap 中的key存在冲突的任务都不会被执行
	 * &lt;/pre&gt;
	 */
	public SEDAThreadPool(
			String threadName,
			BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue,
			BlockingQueue&lt;SEDAThreadPool.Task&gt; outputQueue,
			ExecutorService exec,
			int threadPoolSize,
			ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt; conflictMap) {
		super();
		this.threadName = threadName;
		this.inputQueue = inputQueue;
		this.outputQueue = outputQueue;
		this.exec = (null == exec) ? Executors.newCachedThreadPool() : exec;
		this.threadPoolSize = threadPoolSize;
		this.conflictMap = conflictMap;
		if (null != conflictMap) {
			hasConflictMap = true;
		}
		this.hasOutput = (null != outputQueue);

	}

	/**
	 * &lt;pre&gt;
	 * 创建SEDA线程池
	 * &lt;/pre&gt;
	 */
	public void createSEDAThreadPool() {
		for (int i = 0; i &lt; threadPoolSize; i++) {
			exec.execute(new InnerConsumer(threadName + i, inputQueue,
					outputQueue));
		}
	}

	private class InnerConsumer implements Runnable {
		private final String name;
		private final BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue;
		private final BlockingQueue&lt;SEDAThreadPool.Task&gt; outputQueue;

		public InnerConsumer(String name,
				BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue,
				BlockingQueue&lt;SEDAThreadPool.Task&gt; outputQueue) {
			super();
			this.name = name;
			this.inputQueue = inputQueue;
			this.outputQueue = outputQueue;
		}

		@Override
		public void run() {
			Thread.currentThread().setName(name);
			if (LOGGER.isInfoEnabled()) {
				LOGGER.info(name + " start to work.");
			}
			while (true) {
				try {
					SEDAThreadPool.Task inputTask = inputQueue.take();
					try {
						if (hasConflictMap) {
							if (null != conflictMap.putIfAbsent(inputTask,
									inputTask)) {
								if (LOGGER.isDebugEnabled()) {
									LOGGER.debug(inputTask
											+ " has found in conflictMap, it is abandoned.");
								}
								continue;
							} else {
								if (LOGGER.isDebugEnabled()) {
									LOGGER.debug(inputTask
											+ " is put into conflictMap.");
								}
							}
						}
						SEDAThreadPool.Task outputTask = consume(inputTask);
						if (hasOutput &amp;&amp; null != outputTask) {
							outputQueue.put(outputTask);
							if (LOGGER.isDebugEnabled()) {
								LOGGER.debug(outputTask
										+ " put into outputQueue.");
							}
						}
					} finally {
						if (hasConflictMap
								&amp;&amp; null != conflictMap.remove(inputTask)) {
							if (LOGGER.isDebugEnabled()) {
								LOGGER.debug(inputTask
										+ " is removed from conflictMap.");
							}
						}
					}
				} catch (Exception e) {
					LOGGER.error("Error:" + e.getMessage(), e);
				}
			}
		}

		private SEDAThreadPool.Task consume(SEDAThreadPool.Task task) {
			if (LOGGER.isDebugEnabled()) {
				LOGGER.debug(task + " takes from inputQueue.");
			}
			return task.execute() ? task : null;
		}
	}

	/**
	 * &lt;pre&gt;
	 * SEDA的Task接口
	 * @author kanpiaoxue
	 * &lt;/pre&gt;
	 * 
	 */
	public interface Task {
		public boolean execute();
	}

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.TimeUnit;

import com.wanmei.parallel.seda.SEDAThreadPool.Task;

public class Test {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue = new LinkedBlockingQueue&lt;SEDAThreadPool.Task&gt;();
		BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue2 = new LinkedBlockingQueue&lt;SEDAThreadPool.Task&gt;();
		BlockingQueue&lt;SEDAThreadPool.Task&gt; inputQueue3 = new LinkedBlockingQueue&lt;SEDAThreadPool.Task&gt;();

		ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt; conflictMap = test();
		int threadPoolSize = Runtime.getRuntime().availableProcessors() * 4;

		ExecutorService exec = Executors.newCachedThreadPool();

		SEDAThreadPool pool = new SEDAThreadPool("consumer-1-", inputQueue,
				inputQueue2, exec, threadPoolSize, conflictMap);
		pool.createSEDAThreadPool();

		SEDAThreadPool pool2 = new SEDAThreadPool("consumer-2-", inputQueue2,
				inputQueue3, exec, threadPoolSize, conflictMap);
		pool2.createSEDAThreadPool();

		SEDAThreadPool pool3 = new SEDAThreadPool("consumer-3-", inputQueue3,
				exec, threadPoolSize, conflictMap);
		pool3.createSEDAThreadPool();

		exec.execute(new Test().new Producer("producer", inputQueue));

		exec.shutdown();

	}

	private static ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt; test() {
		ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt; conflictMap = new ConcurrentHashMap&lt;SEDAThreadPool.Task, SEDAThreadPool.Task&gt;();
		for (int i = 0; i &lt; 10; i++) {
			Test.TaskImpl t = new Test().new TaskImpl("task-" + i);
			conflictMap.put(t, t);
		}
		return conflictMap;
	}

	private class Producer implements Runnable {
		private final String name;
		private final BlockingQueue&lt;SEDAThreadPool.Task&gt; outputQueue;

		public Producer(String name, BlockingQueue&lt;Task&gt; outputQueue) {
			super();
			this.name = name;
			this.outputQueue = outputQueue;
		}

		@Override
		public void run() {
			Thread.currentThread().setName(name);
			while (true) {
				try {
					for (SEDAThreadPool.Task t : getTasks()) {
						outputQueue.put(t);
					}
					TimeUnit.SECONDS.sleep(10);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		}

		private List&lt;SEDAThreadPool.Task&gt; getTasks() {
			List&lt;SEDAThreadPool.Task&gt; list = new ArrayList&lt;SEDAThreadPool.Task&gt;();
			for (int i = 0; i &lt; 10; i++) {
				list.add(new Test().new TaskImpl("task-" + i));
			}
			return list;
		}
	}

	private class TaskImpl implements SEDAThreadPool.Task {
		private String name;

		public TaskImpl(String name) {
			super();
			this.name = name;
		}

		@Override
		public int hashCode() {
			final int prime = 37;
			int result = 17;
			result = prime * result + getOuterType().hashCode();
			result = prime * result + ((name == null) ? 0 : name.hashCode());
			return result;
		}

		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			TaskImpl other = (TaskImpl) obj;
			if (!getOuterType().equals(other.getOuterType()))
				return false;
			if (name == null) {
				if (other.name != null)
					return false;
			} else if (!name.equals(other.name))
				return false;
			return true;
		}

		@Override
		public String toString() {
			return "Task [name=" + name + "]";
		}

		@Override
		public boolean execute() {
			try {

				TimeUnit.SECONDS.sleep(10);
			} catch (Exception e) {
				e.printStackTrace();
			}
			return true;
		}

		private Test getOuterType() {
			return Test.this;
		}

	}
}</pre> 
 <p>&nbsp;</p> 
 <p>参考：&nbsp;<a href="http://www.eecs.harvard.edu/~mdw/proj/seda/">http://www.eecs.harvard.edu/~mdw/proj/seda/</a></p> 
 <p>&nbsp;</p> 
 <p>下面添加的这些代码，只是个人记录一下。代码的正确性有待验证，日期：2017/05/12。</p> 
 <p>代码基于JDK1.8</p> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * Copyright baidu.com CDC [2000-2017]
 * &lt;/pre&gt;
 */
package org.kanpiaoxue.seda;

/**
 * &lt;pre&gt;
 * SEDAQueue.java
 * &amp;#64;author kanpiaoxue&lt;br&gt;
 * &amp;#64;version 1.0
 * Create Time 2017年5月12日 下午3:34:24&lt;br&gt;
 * Description : SEDAQueue接口
 * &lt;/pre&gt;
 */
public interface SEDAQueue&lt;E&gt; {
    /**
     * &lt;pre&gt;
     * 放入元素，如果元素已存在则抛弃该元素
     * &amp;#64;param e
     * &amp;#64;throws InterruptedException
     * &lt;/pre&gt;
     */
    void put(E e) throws InterruptedException;

    /**
     * &lt;pre&gt;
     * SEDAQueue 使用元素e开始工作
     * &amp;#64;param work SEDAWork实例
     * &amp;#64;throws InterruptedException
     * &lt;/pre&gt;
     */
    void work(SEDAWork&lt;E&gt; work) throws InterruptedException;
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * Copyright baidu.com CDC [2000-2017]
 * &lt;/pre&gt;
 */
package org.kanpiaoxue.seda;

/**
 * &lt;pre&gt;
 * SEDAStateMachineService.java
 * &amp;#64;author kanpiaoxue&lt;br&gt;
 * &amp;#64;version 1.0
 * Create Time 2017年5月12日 下午5:06:36&lt;br&gt;
 * Description : SEDA状态机服务
 * &lt;/pre&gt;
 */
public interface SEDAStateMachineService&lt;E&gt; {
    /**
     * &lt;pre&gt;
     * &amp;#64;param e 任务
     * &amp;#64;return 是否正确的状态
     * &lt;/pre&gt;
     */
    boolean isCorrectState(E e);
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * Copyright baidu.com CDC [2000-2017]
 * &lt;/pre&gt;
 */
package org.kanpiaoxue.seda;

/**
 * &lt;pre&gt;
 * Work.java
 * &amp;#64;author kanpiaoxue&lt;br&gt;
 * &amp;#64;version 1.0
 * Create Time 2017年5月12日 下午4:45:39&lt;br&gt;
 * Description : SEDA的work接口
 * &lt;/pre&gt;
 */
public interface SEDAWork&lt;E&gt; {
    /**
     * &lt;pre&gt;
     * 使用e开始工作
     * &amp;#64;param e 工作元素
     * &lt;/pre&gt;
     */
    void work(E e);
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * Copyright baidu.com CDC [2000-2017]
 * &lt;/pre&gt;
 */
package org.kanpiaoxue.seda;

import org.kanpiaoxue.seda.impl.SEDAQueueWithStateMachineImpl;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.common.collect.Lists;

import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

/**
 * &lt;pre&gt;
 * Test.java
 * &amp;#64;author kanpiaoxue&lt;br&gt;
 * &amp;#64;version 1.0
 * Create Time 2017年5月12日 下午3:54:39&lt;br&gt;
 * Description : 测试类
 * &lt;/pre&gt;
 */
public class Test {
    private static final Logger LOGGER = LoggerFactory.getLogger(Test.class);

    public static void main(String[] args) throws Exception {

        final SEDAQueue&lt;String&gt; queue = new SEDAQueueWithStateMachineImpl&lt;&gt;(e -&gt; {
            LOGGER.debug("{} was processed by stateMachine", e);
            return !e.contains("8");
        });
        ExecutorService e = Executors.newCachedThreadPool();
        e.execute(() -&gt; {
            Thread.currentThread().setName("Producer-0");
            while (true) {
                try {
                    List&lt;String&gt; list = Lists.newArrayList();
                    for (int i = 1; i &lt; 10; i++) {
                        String el = "hello" + i;
                        if (i % 7 == 0) {
                            el = "world";
                        }
                        list.add(el);
                    }

                    for (String el : list) {
                        queue.put(el);
                        LOGGER.info("{} was put into queue", el);
                    }

                    long sleepTime = 10L;
                    LOGGER.info("{} will sleep %s seconds", Thread.currentThread().getName(), sleepTime);
                    TimeUnit.SECONDS.sleep(sleepTime);
                } catch (Exception ex) {
                    ex.printStackTrace();
                }
            }
        });

        for (int i = 0, j = 4; i &lt; j; i++) {

            final int num = i;
            e.execute(() -&gt; {
                Thread.currentThread().setName("Consumer-" + num);
                while (true) {
                    try {
                        queue.work(w -&gt; {
                            LOGGER.info("[{}]{} was taken from queue", Thread.currentThread().getName(), w);

                            try {
                                TimeUnit.SECONDS.sleep(1L);
                            } catch (Exception e1) {
                                e1.printStackTrace();
                            }
                        });
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }
            });
        }

        e.shutdown();
        e.awaitTermination(2, TimeUnit.DAYS);
    }
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.seda.impl;

import org.kanpiaoxue.seda.SEDAQueue;
import org.kanpiaoxue.seda.SEDAStateMachineService;
import org.kanpiaoxue.seda.SEDAWork;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.Objects;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ConcurrentMap;
import java.util.concurrent.LinkedBlockingQueue;

/**
 * &lt;pre&gt;
 * SEDAQueue.java
 * &amp;#64;author kanpiaoxue&lt;br&gt;
 * &amp;#64;version 1.0
 * Create Time 2017年5月12日 下午2:55:24&lt;br&gt;
 * Description : SEDAQueue带有状态机服务的实现类
 * &lt;/pre&gt;
 */
public class SEDAQueueWithStateMachineImpl&lt;E&gt; implements SEDAQueue&lt;E&gt; {
    private static final Logger LOGGER = LoggerFactory.getLogger(SEDAQueueWithStateMachineImpl.class);
    private static final Object value = new Object();
    private final ConcurrentMap&lt;E, Object&gt; outerQueue = new ConcurrentHashMap&lt;&gt;();
    private final LinkedBlockingQueue&lt;E&gt; workingQueue = new LinkedBlockingQueue&lt;&gt;();
    private final SEDAStateMachineService&lt;E&gt; sedaStateMachineService;

    /**
     * &lt;pre&gt;
     * &amp;#64;param sedaStateMachineService
     * &lt;/pre&gt;
     */
    public SEDAQueueWithStateMachineImpl(SEDAStateMachineService&lt;E&gt; sedaStateMachineService) {
        super();
        Objects.requireNonNull(sedaStateMachineService, "sedaStateMachineService is null");
        this.sedaStateMachineService = sedaStateMachineService;
    }

    /*
     * (non-Javadoc)
     * @see org.kanpiaoxue.seda.SEDAQueue#put(java.lang.Object)
     */
    @Override
    public void put(E e) throws InterruptedException {
        Object returnValue = outerQueue.putIfAbsent(e, value);
        if (null != returnValue) {
            LOGGER.warn("{} was found in the queue. It was abandoned!", e);
            return;
        }

        boolean isCorrectState = sedaStateMachineService.isCorrectState(e);
        if (!isCorrectState) {
            LOGGER.warn("{}'s state is not correct. It was abandoned!", e);
            outerQueue.remove(e);
            return;
        }

        workingQueue.put(e);
    }

    /*
     * (non-Javadoc)
     * @see org.kanpiaoxue.seda.SEDAQueue#work(org.kanpiaoxue.seda.Work)
     */
    @Override
    public void work(SEDAWork&lt;E&gt; work) throws InterruptedException {
        E e = workingQueue.take();
        try {
            work.work(e);
        } finally {
            outerQueue.remove(e);
        }
    }
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>