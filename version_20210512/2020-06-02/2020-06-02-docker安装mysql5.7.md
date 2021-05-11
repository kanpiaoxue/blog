#docker安装mysql5.7
###发表时间：2020-06-02
###分类：docker,mac,经验,mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2514513" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2514513</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>（一）拉取镜像</p> 
 <p>docker pull mysql:5.7</p> 
 <p>（二）运行容器: 映射本地端口 3309 到容器的端口 3306</p> 
 <p>docker run -itd --name mysql-5.7 -p 3309:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7</p> 
 <p>（三）访问mysql5.7</p> 
 <p>mysql -h127.0.0.1 -P3309 -uroot -p123456</p> 
 <p>（四）创建数据库： hello</p> 
 <p>create database hello;</p> 
 <p>&nbsp;</p> 
</div>