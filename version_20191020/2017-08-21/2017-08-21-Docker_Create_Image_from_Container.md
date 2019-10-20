#Docker: Create Image from Container
###发表时间：2017-08-21
###分类：docker
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2390484" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2390484</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">转载地址：&nbsp;<a href="http://blog.csdn.net/wxqee/article/details/52081866">http://blog.csdn.net/wxqee/article/details/52081866</a></p> 
 <p style="font-size: 14px;">&nbsp;&nbsp;</p> 
 <p>Get a base Image</p> 
 <p>$ docker pull centos</p> 
 <p>&nbsp;</p> 
 <p>Run a base Container</p> 
 <p>$ docker run -it centos /bin/bash</p> 
 <p>&nbsp;</p> 
 <p>See Container status</p> 
 <p>$ docker ps -a</p> 
 <p>&nbsp;</p> 
 <p>Commit Container as Image</p> 
 <p>$ docker commit -m "echo container" -a "wang xiaoqiang" c71580983e83 echo:v1</p> 
 <p>&nbsp;&nbsp;</p> 
 <p>Save Image</p> 
 <p>$ docker save echo:v1 &gt;echo-v1.tar</p> 
 <p>&nbsp;</p> 
 <p>Load Image</p> 
 <p>$ docker load &lt; echo-v1.tar</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>