#zeppelin的docker启动方式
###发表时间：2020-08-20
###分类：zeppelin,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2516385" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2516385</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">docker run --rm -ti -p 9080:8080 -e ZEPPELIN_ADDR=0.0.0.0 --name zeppelin apache/zeppelin:0.8.2</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">匿名登录的方式：</p> 
 <p>docker run -tid -p 9080:8080 -e ZEPPELIN_ADDR=0.0.0.0 --name zeppelin apache/zeppelin:0.8.2</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">访问地址：<a href="http://localhost:9080/#/">http://localhost:9080</a></p> 
</div>