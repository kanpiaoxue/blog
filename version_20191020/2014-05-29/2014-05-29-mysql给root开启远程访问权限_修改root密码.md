#mysql给root开启远程访问权限，修改root密码
###发表时间：2014-05-29
###分类：mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2073420" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2073420</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>引用自：<a href="http://www.cnblogs.com/easyzikai/archive/2012/06/17/2552357.html">&nbsp;http://www.cnblogs.com/easyzikai/archive/2012/06/17/2552357.html</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="sql">1.MySql-Server 出于安全方面考虑只允许本机(localhost, 127.0.0.1)来连接访问. 这对于 Web-Server 与 MySql-Server 都在同一台服务器上的网站架构来说是没有问题的. 但随着网站流量的增加, 后期服务器架构可能会将 Web-Server 与 MySql-Server 分别放在独立的服务器上, 以便得到更大性能的提升, 此时 MySql-Server 就要修改成允许 Web-Server 进行远程连接.

2.不用每次都登到服务器去添加修改表，只要用图形化界面即可远程管理。

我们可以按照下面的步骤修改:
1, 登录 Mysql-Server 连接本地 mysql (默认只允许本地连接)

 



 
2, 修改 Mysql-Server 用户配置

复制代码
mysql&gt; USE mysql; -- 切换到 mysql DB

Database changed

mysql&gt; SELECT User, Password, Host FROM user; -- 查看现有用户,密码及允许连接的主机

+------+----------+-----------+
| User | Password | Host      |
+------+----------+-----------+
| root |          | localhost |
+------+----------+-----------+
1 row in set (0.00 sec)

 

mysql&gt; -- 只有一个默认的 root 用户, 密码为空, 只允许 localhost 连接
12
mysql&gt; -- 下面我们另外添加一个新的 root 用户, 密码为空, 只允许 192.168.1.100 连接

mysql&gt; GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.1.100' IDENTIFIED BY '' WITH GRANT OPTION;

 

mysql&gt; -- @'192.168.1.100'可以替换为@‘%’就可任意ip访问，当然我们也可以直接用 UPDATE 更新 root 用户 Host, 但不推荐, SQL如下:

mysql&gt; -- UPDATE user SET Host='192.168.1.100' WHERE User='root' AND Host='localhost' LIMIT 1;

mysql&gt; flush privileges;

Query OK, 0 rows affected (0.00 sec)
复制代码
 

修改root密码
mysql&gt; use mysql
 
Database changed
 
mysql&gt; update user set password=PASSWORD('123456') where user='root';
 
Query OK, 0 rows affected (0.00 sec)
 
Rows matched: 1  Changed: 0  Warnings: 0
 
mysql&gt; flush privileges;
 
Query OK, 0 rows affected (0.00 sec)</pre> 
 <p>&nbsp;</p> 
</div>