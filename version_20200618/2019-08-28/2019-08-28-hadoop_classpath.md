#hadoop classpath
###发表时间：2019-08-28
###分类：java,经验,hadoop
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2443893" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2443893</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;<a href="https://mapr.com/docs/61/ReferenceGuide/hadoop-classpath.html">https://mapr.com/docs/61/ReferenceGuide/hadoop-classpath.html</a></p> 
 <p>&nbsp;</p> 
 <pre class="pre codeblock"><code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: inherit; color: inherit; background-color: #e7e7e7;">$hadoop classpath
/opt/mapr/hadoop/hadoop-2.7.0/etc/hadoop:/opt/mapr/hadoop/hadoop-2.7.0/share/hadoop/common/lib/
*:/opt/mapr/hadoop/hadoop-2.7.0/share/hadoop/common/*:/opt/mapr/hadoop/hadoop-2.7.0/share/hadoo
p/hdfs:/opt/mapr/hadoop/hadoop-2.7.0/share/hadoop/hdfs/lib/*:/opt/mapr/hadoop/hadoop-2.7.0/shar
e/hadoop/hdfs/*:/opt/mapr/hadoop/hadoop-2.7.0/share/hadoop/yarn/lib/*:/opt/mapr/hadoop/hadoop-2
.7.0/share/hadoop/yarn/*:/opt/mapr/hadoop/hadoop-2.7.0/share/hadoop/mapreduce/lib/*:/opt/mapr/h
adoop/hadoop-2.7.0/share/hadoop/mapreduce/*:/contrib/capacity-scheduler/*.jar:/opt/mapr/lib/kvs
tore*.jar:/opt/mapr/lib/libprotodefs*.jar:/opt/mapr/lib/baseutils*.jar:/opt/mapr/lib/maprutil*.
jar:/opt/mapr/lib/json-20080701.jar:/opt/mapr/lib/flexjson-2.1.jar</code></pre> 
 <p>&nbsp;</p> 
</div>