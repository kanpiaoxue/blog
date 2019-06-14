#ubuntu上面apt-get安装mysql
###发表时间：2017-08-23
###分类：Linux,ubuntu,mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2390911" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2390911</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">mysql简单安装方式：</p> 
 <p style="font-size: 14px;">1. sudo apt-get install mysql-server</p> 
 <p style="font-size: 14px;">2. apt-get install mysql-client</p> 
 <p style="font-size: 14px;">3. &nbsp;sudo apt-get install libmysqlclient-dev</p> 
 <p style="font-size: 14px;">安装过程中会提示设置密码什么的，注意设置了不要忘了，安装完成之后可以使用如下命令来检查是否安装成功：</p> 
 <p style="font-size: 14px;">sudo netstat -tap | grep mysql</p> 
 <p style="font-size: 14px;">通过上述命令检查之后，如果看到有mysql 的socket处于 listen 状态则表示安装成功。</p> 
 <p style="font-size: 14px;">登陆mysql数据库可以通过如下命令：</p> 
 <p style="font-size: 14px;">mysql -u root -p</p> 
 <p style="font-size: 14px;">-u 表示选择登陆的用户名， -p 表示登陆的用户密码，上面命令输入之后会提示输入密码，此时输入密码就可以登录到mysql。</p> 
 <p style="font-size: 14px;">然后通过 show databases; 就可以查看当前的数据库。</p> 
 <p style="font-size: 14px;">我们选择 mysql数据库就行下一步操作，使用use mysql 命令，显示当前数据库的表单：show tables;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">如果运行命令行： # mysql -uroot -p 出现如下的错误信息：</p> 
 <div class="quote_div" style="font-size: 14px;">
  ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
 </div> 
 <p style="font-size: 14px;">&nbsp;你需要启动一下mysql，命令如下：</p> 
 <p># service mysql start</p> 
 <p>再次输入命令行：&nbsp;# mysql -uroot -p 出现如下的错误信息：</p> 
 <div class="quote_div">
  * Starting MySQL database server mysqld No directory, logging in with HOME=/
 </div> 
 <p>&nbsp;处理步骤如下：</p> 
 <p># service mysql stop</p> 
 <p># usermod -d /var/lib/mysql/ mysql</p> 
 <p># service mysql start</p> 
 <p>然后再次运行&nbsp;<span style="line-height: 1.5;">&nbsp;</span><span style="line-height: 1.5;"># mysql -uroot -p ，一切正常。</span></p> 
 <p><span style="line-height: 1.5;">查看mysql的版本：</span></p> 
 <pre name="code" class="sql">mysql&gt; select version();
+-------------------------+
| version()               |
+-------------------------+
| 5.7.19-0ubuntu0.16.04.1 |
+-------------------------+
1 row in set (0.00 sec)</pre> 
 <p><span style="line-height: 1.5;">&nbsp;</span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">参考：<a href="http://www.cnblogs.com/hmy-blog/p/6506412.html">http://www.cnblogs.com/hmy-blog/p/6506412.html</a></p> 
</div>