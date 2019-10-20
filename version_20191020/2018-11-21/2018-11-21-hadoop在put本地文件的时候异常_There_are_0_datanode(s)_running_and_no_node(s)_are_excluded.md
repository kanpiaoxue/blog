#hadoop在put本地文件的时候异常：There are 0 datanode(s) running and no node(s) are excluded
###发表时间：2018-11-21
###分类：hadoop
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434137" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434137</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我在本地搭建了一个hadoop的伪分布式环境，在本地put文件到hdfs的时候发生异常。</p> 
 <pre name="code" class="java">hadoop fs -put hello.log /hello/201803201140/</pre> 
 <p>&nbsp;异常信息：</p> 
 <div class="quote_div">
  There are 0 datanode(s) running and no node(s) are excluded in this operation.
 </div> 
 <p>查看DataNode的日志文件，有如下的异常信息：</p> 
 <div class="quote_div">
  2018-11-21 14:49:15,524 WARN org.apache.hadoop.hdfs.server.common.Storage: Failed to add storage directory [DISK]file:/Users/kpx/Datas/hadoop/hdfs/tmp/dfs/data
  <br>java.io.IOException: Incompatible clusterIDs in /Users/kpx/Datas/hadoop/hdfs/tmp/dfs/data: namenode clusterID = CID-8d444e87-7d47-497d-b92a-83a15c2f025d; datanode clusterID = CID-206e5c4d-31bf-40e7-ad76-4ecf4bb2fa5c
 </div> 
 <p>&nbsp;&nbsp;表名DataNode有问题，然后使用 jps 命令查看java的检查，发现没有DataNode被启动：</p> 
 <div class="quote_title">
  进程情况： 写道
 </div> 
 <div class="quote_div">
  58400 ResourceManager
  <br>58499 NodeManager
  <br>58206 SecondaryNameNode
  <br>57967 NameNode
 </div> 
 <p>&nbsp;</p> 
 <p>突然意识到可能是之前我反反复复搭建hadoop的过程中几次中断过程、几次format namenode等乱七八糟的操作引起的DataNode的文件异常。</p> 
 <p>查看&nbsp;core-site.xml 配置文件里面的&nbsp;&lt;name&gt;hadoop.tmp.dir&lt;/name&gt; ，进入该目录下面的 dfs 目录，如下：</p> 
 <div class="quote_div">
  data
  <br>name
  <br>namesecondary
 </div> 
 <p>&nbsp;这3个目录下面的内容都删除，然后重新运行namenode的格式化：</p> 
 <pre name="code" class="java">hdfs namenode -format</pre> 
 <p>&nbsp;重新运行 put 命令上传文件，成功！</p> 
 <p>&nbsp;</p> 
</div>