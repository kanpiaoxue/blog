#嵌入jetty的springMVC可运行jar的REST+
###发表时间：2014-05-20
###分类：Spring,REST,java,jetty
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2068591" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2068591</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp; &nbsp; 我想给一些可以运行jar的程序提供http REST的API，给客户提供服务，运行他们可以远程调用REST的API，和我的jar程序进行交互。</p> 
 <p>&nbsp; &nbsp; 问题：我喜欢用springMVC开发REST，可是springMVC是Web环境中运行的，需要运行在tomcat之类的服务器中。该如何脱离web容器呢？我想到了另一个web容器--jetty！它可以很容易的内置到java程序中，而且是nio的底层通信，性能非常好。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;于是我写了一个例子。具体内容请参看附件。</p> 
</div>