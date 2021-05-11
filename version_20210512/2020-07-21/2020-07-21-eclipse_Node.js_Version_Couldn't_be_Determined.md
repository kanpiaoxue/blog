#eclipse Node.js Version Couldn't be Determined
###发表时间：2020-07-21
###分类：eclipse,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2515796" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2515796</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>Mac系统，eclipse报错：&nbsp;Node.js Version Couldn't be Determined</p> 
 <p>已经安装了node，依然报错。</p> 
 <p>解决办法：在eclipse的配置文件eclipse.ini里面追加一个JVM参数指定node的位置，可以解决问题，如下：</p> 
 <div class="quote_div">
  -Dorg.eclipse.wildwebdeveloper.nodeJSLocation=/usr/local/bin/node
 </div> 
 <p>&nbsp;node的安装位置每个机器可能不同，需要自己定位一下。</p> 
 <p>参考资料：&nbsp;<a href="https://github.com/eclipse/wildwebdeveloper/issues/298">https://github.com/eclipse/wildwebdeveloper/issues/298</a></p> 
 <p>&nbsp;</p> 
</div>