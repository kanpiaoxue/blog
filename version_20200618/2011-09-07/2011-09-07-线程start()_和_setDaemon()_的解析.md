#线程start() 和 setDaemon() 的解析
###发表时间：2011-09-07
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1167936" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1167936</a>

---

<p>最近研究python。看了部分内容，开始尝试写Multiple-thread(多线程)的东西。中间遇到了问题：我书写了自己的线程类，在实例化之后，运行start()。程序会立即执行一次，而不像run()方面里面我定义的while True: 里面的代码那样运行。找了好久，才发现：原来我设置了setDaemon(True)，然后start()。因为线程是守护线程，主线程结束之后，它会立即结束。当我把setDaemon去掉之后，就没有问题了。</p>
<p>而且给线程命名self.name = name ，要生效必须用start()，而不能用run()。因为run()被调用的时候，self.name指向的是主线程MainThread</p>