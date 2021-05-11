#指定java stream中并行处理的线程池大小
###发表时间：2021-03-04
###分类：经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519470" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519470</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <div class="quote_title">
  Java8实战：并行线程池 写道
 </div> 
 <div class="quote_div">
  并行流内部使用了默认的ForkJoinPool，它默认的 线程数量就是你的处理器数量，这个值是由Runtime.getRuntime().availableProcessors()得到的。
  <br>但是你可以通过系统属性 java.util.concurrent.ForkJoinPool.common.parallelism 来改变线程池大小，如下所示:
  <br>System.setProperty("java.util.concurrent.ForkJoinPool.common.parallelism","12");
  <br>这是一个全局设置，因此它将影响代码中所有的并行流。反过来说，目前还无法专为某个并行流指定这个值。
  <br>一般而言，让ForkJoinPool的大小等于处理器数量是个不错的默认值， 除非你有很好的理由，否则我们强烈建议你不要修改它。
 </div> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    static void test001() {
        System.setProperty("java.util.concurrent.ForkJoinPool.common.parallelism", "120");

        IntStream.range(0, 100).parallel().forEach(n -&gt; {
            System.out.println(String.format("%s --&gt; %s", Thread.currentThread().getName(), n));
        });
    }</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>