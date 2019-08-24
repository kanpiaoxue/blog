#zookeeper常用命令
###发表时间：2018-01-10
###分类：zookeeper
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2407337" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2407337</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考一：<a href="https://blog.csdn.net/lihao21/article/details/51778255" target="_blank"><span style="font-family: 'microsoft yahei';"><span style="font-size: 18px;"><strong>ZooKeeper的安装与部署</strong></span></span>&nbsp;</a></p> 
 <p>参考二：<a href="http://www.cnblogs.com/zhaojiankai/p/7126181.html26181.html" target="_blank"><span style="font-size: 18px;">Zookeeper介绍及安装部署</span></a></p> 
 <p>&nbsp;</p> 
 <p>假设3个节点组成了zookeeper集群</p> 
 <p>1、连接zk集群：</p> 
 <div class="quote_div">
  bin/zkCli.sh -server localhost:2181,localhost:2182,localhost:2183
 </div> 
 <p>&nbsp;</p> 
 <p>2、查看zk集群中谁是leader 和当前zk的状态：</p> 
 <div class="quote_div">
  bin/zkServer.sh status
 </div> 
 <p>output：&nbsp;</p> 
 <p>&nbsp; &nbsp; Mode: leader</p> 
 <p>&nbsp; &nbsp; OR</p> 
 <p>&nbsp; &nbsp;&nbsp;Mode: follower</p> 
 <p>或者命令：</p> 
 <div class="quote_div">
  echo srvr | nc localhost 2181
 </div> 
 <p>&nbsp;&nbsp;</p> 
 <p>3、zk的服务器命令帮助信息：</p> 
 <div class="quote_div">
  bin/zkServer.sh help
 </div> 
 <p>&nbsp;output：</p> 
 <p>&nbsp; &nbsp; Usage: bin/zkServer.sh {start|start-foreground|stop|restart|status|upgrade|print-cmd}</p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  5节点集群，应用系统只配置了其中3个节点作为服务器列表的情况。 写道
 </div> 
 <div class="quote_div">
  比如，现在大家通用的zk配置是1、2、3共3台机器，我新增4、5两台机器，组成5节点的集群。现在机器1挂了，对应用系统是没有任何影响的，机器1、2都挂了，也没事，因为现在集群共5个节点有3个是活着的。如果机器1、2、3都挂了，那么5节点的zk就完蛋了，应用程序就挂了。
 </div> 
 <div class="quote_div">
  结论：只要zk集群存活正常，zk的客户端和任意的一台或者多台zk中的服务器连接都是可用正常工作的。
 </div> 
 <p>&nbsp;</p> 
</div>