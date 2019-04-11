#解决elasticsearch client的maven中jar冲突的问题
###发表时间：2017-09-27
###分类：java,elasticsearch,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2394728" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2394728</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>今天尝试使用elasticsearch的 client 来访elasticsearch。它的客户端比自己写 REST 的调用提供了更多的功能，如下：</p> 
 <div class="quote_div">
  RestClient class线程安全，推荐进行多次服用提高性能。
  <br>失败重新连接服务器。
  <br>失败救援（HA）
  <br>负载均衡。
 </div> 
 <p>&nbsp;参考地址：&nbsp;<a href="https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-low.html">https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-low.html</a></p> 
 <p>它的文档里面有一段是专门用来说明它的 jar 和其他 jar 的冲突问题的。我觉得它说的方法效果不是很好，自己想了想，解决方法如下：</p> 
 <p>进入 elasticsearch 的自己本地 maven 仓库路径，如：</p> 
 <p>/maven/maven_repository/org/elasticsearch/client/elasticsearch-rest-client/5.6.2</p> 
 <p>查看它的项目原始的 maven 的依赖文件：&nbsp;elasticsearch-rest-client-5.6.2.pom</p> 
 <p>查看这个文件里面的依赖关系是如何配置的，将这些依赖黏贴到自己的 pom.xml 中，然后去掉自己和他冲突的 jar 的依赖（如果你之前的依赖不能更改，还是参考官网给出的依赖关系冲突的解决方案吧），这样就可以了。</p> 
 <p>&nbsp;</p> 
</div>