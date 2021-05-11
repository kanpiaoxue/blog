#was cached in the local repository, resolution will not be reattempted until the
###发表时间：2014-01-12
###分类：java,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2003088" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2003088</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">was cached in the local repository, resolution will not be reattempted until the update interval of nexus has elapsed or updates are forced</pre> 
 <p>&nbsp;<span style="color: #333333; font-family: Verdana, Arial, Helvetica, sans-serif; line-height: 26px; font-size: 12px;">去自己的.m2 文件夹下把 xxx.lastUpdated文件全部删掉，重新运行maven，ok！</span></p> 
 <p style="color: #333333; line-height: 26px; font-family: Verdana, Arial, Helvetica, sans-serif;">或者在用maven时加 -U参数，就可以忽略xxx.lastUpdated..</p> 
 <p style="color: #333333; line-height: 26px; font-family: Verdana, Arial, Helvetica, sans-serif;">参考：&nbsp;<a style="color: #000000; font-family: 'Microsoft YaHei'; font-size: 20px; line-height: 30px;" href="http://blog.csdn.net/happyteafriends/article/details/7451061">使用nexus搭建maven私服</a></p> 
 <p style="color: #333333; line-height: 26px; font-family: Verdana, Arial, Helvetica, sans-serif;">&nbsp;</p> 
 <p style="color: #333333; line-height: 26px; font-family: Verdana, Arial, Helvetica, sans-serif;"><a href="http://blog.csdn.net/happyteafriends/article/details/7451061">http://blog.csdn.net/happyteafriends/article/details/7451061</a></p> 
</div>