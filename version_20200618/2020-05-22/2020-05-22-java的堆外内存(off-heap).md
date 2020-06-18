#java的堆外内存（off-heap）
###发表时间：2020-05-22
###分类：java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2514264" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2514264</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料：<a href="https://dzone.com/articles/heap-vs-heap-memory-usage">https://dzone.com/articles/heap-vs-heap-memory-usage</a></p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  Off heap memory provides;
  <br>
  <br>Scalability to large memory sizes e.g. over 1 TB and larger than main memory.
  <br>Notional impact on GC pause times.
  <br>Sharing between processes, reducing duplication between JVMs, and making it easier to split JVMs.
  <br>Persistence for faster restarts or replying of production data in test.
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>