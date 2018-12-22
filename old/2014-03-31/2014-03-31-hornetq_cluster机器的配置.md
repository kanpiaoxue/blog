#hornetq cluster机器的配置
###发表时间：2014-03-31
###分类：HornetQ
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2038909" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2038909</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在这篇文章的附件中，我上传了一个&nbsp;<a style="font-size: 12px; line-height: 12px;" href="http://dl.iteye.com/topics/download/0ff07c97-1b1b-3fe0-8749-dcfb6cc4be1c" target="_blank">hornetq-2.4.0.Final.cluster.zip</a>&nbsp; 的附件。这个附件里面主要含有两个文件夹，分别是 bin 和 config 两个文件夹。如何配置hornetq的集群呢？去&nbsp;<a href="http://www.jboss.org/hornetq">http://www.jboss.org/hornetq</a>&nbsp;下载&nbsp;<a style="font-size: 12px; line-height: 12px;" href="http://dl.iteye.com/topics/download/0ff07c97-1b1b-3fe0-8749-dcfb6cc4be1c" target="_blank">hornetq-2.4.0.Final</a>&nbsp;版本的hornetq，解压之后将附件&nbsp;<a style="font-size: 12px; line-height: 12px;" href="http://dl.iteye.com/topics/download/0ff07c97-1b1b-3fe0-8749-dcfb6cc4be1c" target="_blank">hornetq-2.4.0.Final.cluster.zip</a>&nbsp;的bin 和 config 目录，覆盖掉 horneq的目录中。将这个覆盖之后的文件夹压缩，上传到需要部署机器节点的机器。</p> 
 <p>1、解压之后，修改bin目录下面run.sh，将</p> 
 <pre name="code" class="xml">export LOCALHOST=10.14.250.101</pre> 
 <p>&nbsp;修改为你本地机器的IP地址。</p> 
 <p>2、然后进入data目录，将这个目录里面所有的东西删除。</p> 
 <p>3、进入 bin 目录，运行 run.sh ，启动该节点。这个节点的hornetq就配置成功了。</p> 
 <p>4、将这个配置成功的hornetq打包，传输到需要添加节点的机器上面。解压之后，按照上面的步骤1，2，3进行操作。则第二个节点完成配置。</p> 
 <p>上面讲述了如果配置hornetQ 的集群。其他的节点的添加，也是如此操作。</p> 
 <p>&nbsp;</p> 
</div>