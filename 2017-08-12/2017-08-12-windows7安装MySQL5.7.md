#windows7安装MySQL5.7
###发表时间：2017-08-12
###分类：mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2389464" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2389464</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">参考地址： &nbsp;<a href="http://blog.csdn.net/qq_26525215/article/details/53424152">http://blog.csdn.net/qq_26525215/article/details/53424152</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">mysql 5.7 修改了之前的mysql数据库的user表，修改密码要进行如下操作：</p> 
 <p style="font-size: 14px;">&gt; update user set authentication_string=password('123abc') where user='root';</p> 
 <p style="font-size: 14px;">&gt; flush privileges</p> 
 <p style="font-size: 14px;">参考地址：http://www.cnblogs.com/jonsea/p/5510219.html</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">默认安装的mysql是不能通过远程访问的，需要开通：</p> 
 <p style="font-size: 14px;">&gt; GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;</p> 
 <p style="font-size: 14px;">&gt; flush privileges</p> 
</div>