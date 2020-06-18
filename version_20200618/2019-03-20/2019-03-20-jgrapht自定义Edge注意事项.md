#jgrapht自定义Edge注意事项
###发表时间：2019-03-20
###分类：jgrapht,java,graph
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439129" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439129</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>我们在使用jgrapht的时候，可能会自定义Edge。一般来说按照文档我们应该继承&nbsp;</p> 
 <p class="p1">class : org.jgrapht.graph.DefaultEdge.java</p> 
 <p class="p1">这个时候需要注意，继承该类DefaultEdge的时候，不要去复写里面的 source 和&nbsp;<span>target 的属性，不要写这2个属性的赋值方法。edge的值是创建graph的时候赋予的，无法自己创建edge的实例。</span></p> 
</div>