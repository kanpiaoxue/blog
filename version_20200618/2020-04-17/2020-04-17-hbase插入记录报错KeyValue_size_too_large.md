#hbase插入记录报错KeyValue size too large
###发表时间：2020-04-17
###分类：hbase,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2513690" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2513690</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>今天向hbase里面插入一条记录的时候报错：KeyValue size too large</p> 
 <p>查了网上的内容，hbase对kv的默认大小是&nbsp;<span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">10485760字节，也就是 10M。</span></p> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">我看了一下自己插入的value的大小是130M，远远大于这个默认值。</span></p> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">怎么解决呢？</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">org.apache.hadoop.conf.Configuration configuration = HBaseConfiguration.create();
// 设置keyvalue.maxsize的大小限制，这里设置500M = 500*1024*1024
configuration.set("hbase.client.keyvalue.maxsize", "524288000");
// --- 其他配置</pre> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">客户端里面配置即可，如上面的代码。</span></p> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">这个配置也可以在hbase服务器端配置，但是要重启hbase。</span></p> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">参考内容：</span></p> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">1、<a href="https://stackoverflow.com/questions/29819266/hbase-keyvalue-size-too-large">https://stackoverflow.com/questions/29819266/hbase-keyvalue-size-too-large</a></span></p> 
 <p><span style="color: #444444; font-family: Ubuntu, Helvetica, Arial, sans-serif;">2、<a href="https://blog.csdn.net/u010476994/article/details/78436858">https://blog.csdn.net/u010476994/article/details/78436858</a></span></p> 
</div>