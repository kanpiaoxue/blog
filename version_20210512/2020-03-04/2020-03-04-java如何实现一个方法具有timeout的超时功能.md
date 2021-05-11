#java如何实现一个方法具有timeout的超时功能
###发表时间：2020-03-04
###分类：java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2512790" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2512790</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：<a href="https://stackoverflow.com/questions/17233038/how-to-implement-synchronous-method-timeouts-in-java">https://stackoverflow.com/questions/17233038/how-to-implement-synchronous-method-timeouts-in-java</a></p> 
 <p>&nbsp;</p> 
 <p>原文的问题描述：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  I have an synchronous execution path which needs to either complete or timeout within a given time frame. Let's say I have a class with main() method in which I invoke methods A() which in-turn calls B() and that in-turn calls C() of same or different classes.....all synchronous without using an external resource like database , webservice or file system (where each of them could be timed out independently using a TxManager or respective timeout api's). So it's more like a CPU or memory intensive computation. How do I code for it's timeout in Java ?
  <br>
  <br>I have looked at TimerTask but that more of making the flow async and for scheduling tasks. Any other suggestions ?
 </div> 
 <p>&nbsp;</p> 
 <p>最佳答案：<span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px;">You should use&nbsp;</span><a style="" href="http://docs.oracle.com/javase/6/docs/api/java/util/concurrent/ExecutorService.html">ExecutorService</a><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px;">&nbsp;to do that</span></p> 
 <pre name="code" class="java">ExecutorService executor = Executors.newSingleThreadExecutor();
Future&lt;String&gt; future = executor.submit(new Callable() {

    public String call() throws Exception {
        //do operations you want
        return "OK";
    }
});
try {
    System.out.println(future.get(2, TimeUnit.SECONDS)); //timeout is in 2 seconds
} catch (TimeoutException e) {
    System.err.println("Timeout");
}
executor.shutdownNow();</pre> 
 <p><span style="color: #242729; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
</div>